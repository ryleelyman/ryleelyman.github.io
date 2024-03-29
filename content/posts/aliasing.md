---
title: "Aliasing"
date: 2022-10-13T16:40:32-04:00
math: true
---
Perhaps my main non-mathematical joy is music.
I took piano lessons from when I was eight through the end of college,
and this year I wrote and recorded an album of pop songs,
about which more certainly sometime soon.
Anyway, I lost most of my weekend to a musical math problem.
The purpose of this post is to explain the problem and the solution,
partly so that I will have fewer steps to retrace,
should I need to in the future.

## Aliasing

Many analog synthesizers,
like the Moog Wendy Carlos's "Switched-on Bach" was recorded on,
make their sound by shaping tones made from
simple-looking waveshapes:
square waves, triangle waves, sawtooth waves and so on.
These waveshapes are musically useful because they contain
a lot of *harmonic content,*
which unlike a pure sine wave,
mimics the fact that sounds produced by physical objects
have many overtones hidden in them.

Anyway, when I came to computer music
partly through taking a class in college where we learned [Max/MSP](https://cycling74.com),
I was excited to find `phasor~`, which generates a sawtooth wave,
and then very disappointed to find that it sounds awful when you listen to it.
The problem is called *aliasing.*

Imagine you're a computer recording a bit of audio.
Since computers are digital, 
what this means is that at regular intervals,
you'll be measuring the amplitude of a waveform—how far from rest it is.
Let's say you're sampling at {{< katex >}}$2X${{< /katex >}} Hertz—{{< katex >}}$2X${{< /katex >}} times per second,
and that what you're sampling is a perfect sine wave
that is running at {{< katex >}}$X${{< /katex >}} Hertz,
lined up so that we, the computer,
see the peak and then the trough,
the peak and then the trough of the sine wave over and over.
Now, when we look at our samples that we've recorded,
we can attempt to draw sine waves that match with the recorded data.
Certainly a sine wave running at {{< katex >}}$X${{< /katex >}} Hertza will do,
but you can try and draw a *faster* wave that will hit the same points as well.
Try it! I think when I did, I drew a wave that was about three times as fast as the original one.

Anyway, the point here, sort of, is that our ears are lazy.
When you listen to a speaker reproducing that sampled waveform,
what you hear is the lowest frequency that makes sense with the data given:
so, we'll here a wave with frequency {{< katex >}}$X${{< /katex >}} Hertz and not {{< katex >}}$3X${{< /katex >}}, {{< katex >}}$5X${{< /katex >}} or so on.
That's the content of what's known as the Nyquist–Shannon sampling theorem:
if we record something that's faster than {{< katex >}}$X${{< /katex >}} Hertz (i.e. one half of the sampling rate),
our ears will find a lower-frequency resonance to hear.
This becomes a problem when the waveform we're recording has frequency content
above {{< katex >}}$X${{< /katex >}} Hertz!
Our square waves, our triangle waves, our sawtooth waves,
because they have either discontinuities or sharp turns,
*do* have frequency content higher than whatever sample rate we could possibly record at.

This also means that if you try to *synthesize* a waveform in a computer,
say a triangle wave,
if you try to do the obvious thing, that is, have the computer draw the waveform you imagine,
what you actually hear will not sound correct, because of this aliasing phenomenon.

## Anti-aliasing in Bitters

This comes home for me in particular,
because I wanted to make my own synthesizer—I'd wanted to ever since I learned Max/MSP.
One thing I wanted to do was have a waveshape that started as a triangle,
so sloping up and down evenly over time,
but could be morphed until it became a sawtooth wave
by changing the relative slopes of the "rise" and "fall" sections.
It became clear that I would have to roll my own oscillator code to do this.
When I opened up a Max4Live synthesizer that I thought was inspiring
(I believe it is/was called "Poli")
I discovered that Peter McCulloch had implemented
a pulse wave (so a square wave, but with a varying length to the "high" and "low" sections)
using an algorithm called "Polynomial Transition Region", or PTR for short.

The Polynomial Transition Region algorithm, I believe, was developed by
Jari Kleimola and Vesa Välimäki.
It's based on a couple of very interesting mathematical observations
which I'd like to explain.

### Integration is filtering

The first observation is that if you have a function, say {{< katex >}}$f(x)${{< /katex >}},
which produces a waveform,
*integrating* that function—in the sense of Calculus!—does two things.
First, it applies a "lowpass filter" to the signal,
smoothing it out and thus reducing the high-frequency content.
Thus if we do it to our naîve or ideal waveform,
the integrated signal will have less high-frequency content that could cause aliasing
when we synthesize it.
The second thing that integrating does,
which you can observe by looking at what happens to {{< katex >}}$f(x) = \cos x${{< /katex >}},
is that it shifts the phase of the waveform, moving it in time.
Most filtering schemes do this, as it happens,
and it's something we'll need to keep in mind.

### Discrete differentiation doesn't alias

Okay, so we have our integrated waveform.
Since we filtered it, however,
if we listen back to the integrated signal,
it won't sound like how we expect it to;
likely it will be much darker in tone than the original.
As we learn in the Fundamental Theorem of Calculus,
we can undo this by differentiating our signal.
If we do that analytically, however,
we'll just end up with the naïve waveform,
losing all the anti-aliasing benefits we just gained.

The solution, which I think is very clever,
is to differentiate *discretely.*
Remember, the derivative of {{< katex >}}$f(x)${{< /katex >}} is defined to be the limit

{{< katex >}}$f'(x) = \lim_{h\to 0} \frac{f(x) - f(x-h)}{h}.${{< /katex >}}

To do things discretely is to work with the samples that we have,
not letting {{< katex >}}$h${{< /katex >}} go to zero, but instead letting it be the length of one sample period.
Here's why this is useful:
doing that differentiation is a *linear combination* of the anti-aliased signal with itself.
If you know a little linear algebra or a little Fourier analysis,
this will point up to you a useful fact:
if the anti-aliased signal has little-to-no frequency content at a certain frequency,
a linear combination of it with itself will 
*also* have relatively little frequency content at that frequency!

### Polynomials like to be differentiated discretely

The final thing to notice is that if our signal {{< katex >}}$f(x)${{< /katex >}} happens to be a *polynomial,*
then this discrete-time differentiation actually will give us the true derivative of the signal,
just with a shift in phase.
So if our function {{< katex >}}$f(x)${{< /katex >}} is actually a piecewise function;
being one polynomial some of the time and another the rest,
when *the current and previous samples are drawn from the piece of the waveform,*
we can actually just use a phase-shifted version of the naïve (and cheap-to-calculate) waveform!

## An asymmetric triangle wave

Anyway, I did all this back in probably 2018, 2019
but discovered recently that I had made a mistake with my triangle wave calculations
and so set out to fix it.
Here's how to go about it:
suppose we have a counter {{< katex >}}$t${{< /katex >}} that ticks up from {{< katex >}}$0${{< /katex >}} to {{< katex >}}$1${{< /katex >}} at the frequency of our waveform,
and we want to use this counter to generate a waveshape
that rises linearly from {{< katex >}}$-1${{< /katex >}} to {{< katex >}}$1${{< /katex >}} over a fraction {{< katex >}}$w${{< /katex >}} of the period,
and hten falls from {{< katex >}}$1${{< /katex >}} back to {{< katex >}}$-1${{< /katex >}} over the remaining {{< katex >}}$1-w${{< /katex >}} of our period.
The naïve waveform then is given by the function

{{< katex >}}$ f(t) = \begin{cases} \frac{2t}{w} - 1 & t \le w \\ \frac{2t}{w-1} + 1 & t \ge w. \end{cases}${{< /katex >}}

If you remember your Calculus, integrating these functions is not hard;
for example integrating the "first half" once yields {{< katex >}}$\frac{t^2}{w} - t + C${{< /katex >}}.
The "{{< katex >}}$+C${{< /katex >}}" term is the challenge.
I wanted to do a higher-order approximation,
which involves integrating a couple times (I think three in my case),
which yields a polynomial with three unknown coefficients.
So what to do about them?
The key is to get them to agree at the overlaps.
So if {{< katex >}}$f_4(t)${{< /katex >}} and {{< katex >}}$g_4(t)${{< /katex >}} are the two polynomials making up the integrated signal,
what we want is the following:

{{< katex >}}$$\begin{align*}
f_4(0) &= g_4(1) \\
f_4(w) &= g_4(w) \\
f'_4(0) &= g'_4(1) \\
f'_4(w) &= g'_4(w) \\
f''_4(0) &= g''_4(1) \\
f''_4(w) &= g''_4(w).
\end{align*}$${{< /katex >}}

This, together with maybe arbitrarily choosing {{< katex >}}$f_4(0) = 0${{< /katex >}},
gives us enough constraints to determine the coefficients of our polynomials!

From there, computing the actual terms of the algorithm amounts to computing the values of

{{< katex >}}$f_4(x) - 3g_4(x+1-h) + 3g_4(x+1-2h) - g_4(x+1-3h)${{< /katex >}}

for the first sample,

{{< katex >}}$f_4(x) - 3f_4(x-h) + 3g_4(x+1-2h) - g_4(x+1-3h)${{< /katex >}}

for the second, and so on.

Anyway, if you're a [SuperCollider](https://supercollider.github.io) user,
you can try out my implementation of this algorithm as a UGen [here](https://github.com/ryleelyman/triangleptr/releases/tag/v0.2).

