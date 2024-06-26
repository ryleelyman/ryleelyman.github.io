---
title: "Nielsen Realization"
date: 2021-06-12T14:43:23-04:00
math: true
---

I'm giving a talk in [Nearly Carbon Neutral Geometric Topology][NCNGT]
about Nielsen realization for infinite-type surfaces.
The format for the conference is that everyone records and uploads their talks beforehand,
and then the conference format allows for discussion and comments via Discord.
The purpose of this post is to share and talk a little bit about my talk, which is below.

{{< youtube "https://www.youtube.com/embed/QwA3bSwkcW0" >}}

The Nielsen realization problem was posed by Nielsen in 1932.
The *mapping class group* of a surface {{< katex >}}$S${{< /katex >}},
call it {{< katex >}}$\operatorname{Map}(S)${{< /katex >}},
is the group of isotopy classes of homeomorphisms of {{< katex >}}$S${{< /katex >}}.
For a subgroup {{< katex >}}$G${{< /katex >}} of {{< katex >}}$\operatorname{Map}(S)${{< /katex >}},
it is not generally possible to realize {{< katex >}}$G${{< /katex >}}
as a group of honest homeomorphisms of {{< katex >}}$S${{< /katex >}}.
Nielsen's question was whether, in the special case that {{< katex >}}$G${{< /katex >}} is finite, such a realization is always possible.
Kerckhoff answered Nielsen's question in the affirmative in 1983 for finite-type surfaces.
In fact, Kerckhoff showed the stronger result that finite subgroups of {{< katex >}}$\operatorname{Map}(S)${{< /katex >}}
arise as groups of isometries of hyperbolic metrics on {{< katex >}}$S${{< /katex >}}
(when {{< katex >}}$S${{< /katex >}} supports a hyperbolic metric, of course).
The first and main theorem I discuss in my talk,
which is joint work with [Santana Afton][Santana], [Danny Calegari][Danny] and [Lvzhou Chen][Lvzhou],
is an extension of Kerckhoff's result to orientable, infinite-type surfaces.

Kerckhoff's proof is very cool;
I talk through the main ideas in my talk,
but briefly he defines a {{< katex >}}$G${{< /katex >}}-invariant, real-valued function on the *Teichmüller space of {{< katex >}}$S${{< /katex >}},*
which parametrizes (homotopy classes of) hyperbolic metrics on {{< katex >}}$S${{< /katex >}},
and shows that it attains a unique minimum, which is therefore fixed by {{< katex >}}$G${{< /katex >}}.
This fixed point yields a realization of {{< katex >}}$G${{< /katex >}} as a group of isometries of the corresponding hyperbolic metric.
Kerckhoff's proof does not work for infinite-type surfaces
basically because a certain finite sum in the definition of his function in the finite-type case
would need to become an infinite series,
and the obvious definition yields a divergent series.
As I mention in the talk,
I'd be very interested in talking with you
if you have ideas about how to weight this series to produce one that converges.
Instead the proof that we give involves cutting our surface up into finite-type pieces,
and applying Kerckhoff's result to each of the pieces.

I became interested in infinite-type surfaces and their mapping class groups
after reading a very cool (and short) [paper][TitsAlternative]
of [Marissa Kawehi Loving][Marissa] and [Justin Lanier][Justin]
finding interesting subgroups of big mapping class groups that cannot be found in finite-type mapping class groups.
It's a theorem that {{< katex >}}$\operatorname{Map}(S)${{< /katex >}} is a subgroup of the symmetric group on a countable set.
I wondered whether the symmetric group on a countable set is ever a subgroup of a big mapping class group.
The second result I discuss in the talk has the corollary that *no,*
the symmetric group on a countable set cannot continuously embed in any big mapping class group.

Finally, after reading a draft of our paper, [Mladen Bestvina][Mladen] suggested to me
that we should be able to use our techniques to prove that compact subgroups of mapping class groups are finite
and locally compact subgroups are discrete.
After a few days of thinking, I was able to find a proof!
It includes my new favorite way of proving that a group is finite:
show that it is *torsion,* that every element has finite order,
and that it is *virtually torsion free,* i.e. that it has a finite-index torsion-free subgroup.
Only the trivial subgroup of such a group is torsion free,
so this shows that the trivial subgroup has finite index in the whole group—so the group is finite.

[Mladen]: https://www.math.utah.edu/~bestvina/
[Justin]: https://justinlanier.org
[Marissa]: https://sites.google.com/view/lovingmath/home?authuser=0
[TitsAlternative]: https://arxiv.org/abs/1904.10060
[Santana]: https://sites.google.com/view/santanaafton/home
[Danny]: https://math.uchicago.edu/~dannyc/
[Lvzhou]: https://lvzhouchen.github.io
[NCNGT]: https://www.ncngt.org/home
