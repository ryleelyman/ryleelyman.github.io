---
layout: post
math: true
---
I've spent the past couple years on and off understanding how to think of graphs of groups
and orbifolds as (being represented by) étale groupoids.
In view of [Lerman's critique], to which his answer is the category of geometric stacks over manifolds,
I thought it might be relevant to try and understand what a stack is.
This is the first in what will likely be several posts towards understanding the definition of a stack;
this one is focused on the concept of a *category fibered in groupoids.*

## Categories fibered in groupoids

Let $$\mathbf{Top}$$ denote the category of compactly generated topological spaces and continuous maps.
(All spaces I tend to think about are compactly generated, being either manifolds or CW complexes,
so this is not a serious restriction for me.
That being said, I don't immediately understand the desire to restrict to compactly generated spaces,
because my algebraic topology is not strong in that direction.)

A functor $$\pi \colon \mathsf{C} \to \mathbf{Top}$$ 
is a *category fibered in groupoids over $$\mathbf{Top}$$*
if the following conditions hold.

- Given a continuous map $$f\colon X \to Y$$ and an object $$\xi \in \mathsf{C}$$
    with $$\pi(\xi) = Y$$,
    there is an arrow $$\tilde f \colon \zeta \to \xi$$ in $$\mathsf{C}$$ such that
    $$\pi(\tilde f) = f$$.
    Apparently we are supposed to think of $$\zeta$$ as a *pullback* of $$\xi$$ along $$f$$.
- Given a diagram of the following form

$$\require{AMScd}\begin{CD}
        \xi'' @>f>> \xi \\
        @. @| \\
        \xi' @>h>> \xi
\end{CD}$$

in $$\mathsf{C}$$ such that there exists a continuous map $$g\colon \pi(\xi'') \to \pi(\xi')$$
making the following diagram commute

$$\begin{CD}
    \pi(\xi'') @>\pi(f)>> \pi(\xi) \\
    @VgVV @| \\
    \pi(\xi') @>\pi(h)>> \pi(\xi),
\end{CD}$$

There exists a unique arrow $$\tilde g\colon \xi'' \to \xi'$$
such that $$h\tilde g = f$$ and $$\pi(\tilde g) = g$$.
In other words, there is a unique way to lift the map $$g$$ to make the diagram commute in $$\mathsf{C}$$.

In understanding stacks, I'm trying to follow [Lerman's paper] 
and also [Fantechi's survey paper], so there are two main examples:
Lerman gives the example of the category $$\mathsf{B}\mathcal{G}$$ of principal $$\mathcal{G}$$-bundles
with arrows $$\mathcal{G}$$-equivariant maps.
Fantechi gives the example of vector bundles of rank $$r$$ and bundle isomorphisms.
I'll give Fantechi's example.

## Example: Vector bundles of constant rank

Recall that a *vector bundle of rank $$r$$* over a topological space $$X$$
is a space $$E$$ equipped with a continuous surjection $$\pi\colon E \to X$$
such that for each point $$x \in X$$, the space $$\pi^{-1}(x)$$ is a real vector space of dimension $$r$$
and such that for each $$x \in X$$, there exists an open neighborhood $$U$$ of $$x$$
and a homeomorphism $$\varphi\cong U\times \mathbb{R}^r \to \pi^{-1}(U)$$
with the property that $$\pi\varphi(y,\vec v) = y$$
and the property that the map $$\vec v \mapsto \varphi(y,\vec v)$$ is a linear isomorphism
from $$\mathbb{R}^r$$ to $$\pi^{-1}(y)$$
for all $$y \in U$$.

There is a category $$\mathsf{Vect}_r$$ of rank-$$r$$ vector bundles
where the arrows are *vector bundle maps of rank $$r$$:* commutative diagrams of the form

$$\begin{CD}
E_1 @>\tilde f>> E_2 \\
@VV\pi_1V @VV\pi_2V \\
X_1 @>f>> X_2
\end{CD}$$

with the property that each map $$\pi_1^{-1}(x) \to \pi_2^{-1}(f(x))$$ is a linear isomorphism of vector spaces.
We will abuse notation, writing $$\tilde f\colon E_1 \to E_2$$ to mean the bundle map above.

The claim is that the functor (also called $$\pi$$) 
sending a rank-$$r$$ vector bundle $$\pi\colon E \to X$$ to its base $$X$$
defines a category fibered in groupoids over $$\mathbf{Top}$$.

To see this, suppose that $$\pi\colon E \to X$$ is a vector bundle and $$f\colon Y \to X$$ is a continuous map.
We need a pullback $$\tilde f \colon \xi \to E$$ for some vector bundle $$\xi$$ over $$Y$$.
Let us take the literal pullback, that is,

$$ \xi = \{ (y,e) \in Y \times E : f(y) = \pi(e) \}$$

There is an obvious projection $$\pi\colon \xi \to Y$$ given by projection to the first factor.
Given $$x \in X$$, let $$U$$ be the neighborhood of $$x$$ 
with the homeomorphism $$\varphi \colon U \times \mathbb{R}^r \to \pi^{-1}(U)$$.
Write $$V = f^{-1}(U)$$ and define
$$\psi\colon V \times \mathbb{R}^r \to \pi^{-1}(V)$$ by the rule

$$\psi(y,\vec v) = (y,(\varphi(f(y),\vec v)).$$

It is clear that $$\pi\psi(y,\vec v) = y$$ for all $$y \in V$$.
Conversely, given $$(y,e) \in \pi^{-1}(V)$$, note that $$\varphi^{-1}(e) = (f(y),\vec v)$$ 
for some $$\vec v \in \mathbb{R}^r$$;
put another way, the map $$(y,e) \mapsto (y,\vec v)$$, where $$\vec v$$ is the $$\mathbb{R}^r$$ component
of $$\varphi^{-1}(e)$$, is an inverse homeomorphism for $$\psi$$.
The map $$\vec v \mapsto \psi(y,\vec v)$$ is a linear isomorphism because $$\vec v \mapsto \varphi(f(y),\vec v)$$
is a linear isomorphism.
Therefore $$\xi$$ is a rank-$$r$$ vector bundle over $$Y$$.

There is a map $$\tilde f \colon \xi \to E$$ given by projection to the second factor.
The map $$\pi^{-1}(y) \to \pi^{-1}(f(y))$$ given by $$(y, e) \mapsto e$$ is a linear isomorphism.
To see this, note that we have the following commutative diagram

$$\begin{CD}
\pi^{-1}(y) @>f>> \pi^{-1}(f(y)) \\
@A\psi AA @A\varphi AA \\
\mathbb{R}^r @= \mathbb{R}^r
\end{CD}
\qquad
\begin{CD}
\psi(y,\vec v) @>>> \varphi(f(y),\vec v) \\
@AAA @AAA \\
\vec v @= \vec v
\end{CD}$$

and the vertical maps are isomorphisms.
Therefore the map $$\tilde f\colon \xi \to E$$ is an arrow of $$\mathsf{Vect}_r$$.

Given maps of vector bundles $$\tilde f\colon \xi'' \to \xi$$ and $$\tilde h\colon \xi' \to \xi$$
such that there exists a continuous map $$g \colon \pi(\xi'') \to \pi(x')$$ making the following diagram commute

$$\begin{CD}
\pi(\xi'') @>f>> \pi(\xi) \\
@VVgV @| \\
\pi(\xi') @>h>> \pi(\xi),
\end{CD}$$

we claim that there is a unique bundle map $$\tilde g\colon \xi'' \to \xi'$$ making the appropriate diagram commute.
Given $$x \in \pi(\xi'')$$, note that $$\tilde f$$ and $$\tilde g$$
induce linear isomorphisms $$\pi^{-1}(x) \to \pi^{-1}(f(x))$$ and 
$$\pi^{-1}(g(x)) \to \pi^{-1}(hg(x)) = \pi^{-1}(f(x))$$.
Call these isomorphisms $$f_x$$ and $$h_{g(x)}$$.
Therefore define $$\tilde g$$ as

$$\tilde g(\tilde x) = h_{g(\pi(\tilde x))}^{-1}f_{\pi(\tilde x)}(\tilde x)$$.

It is clear that $$\tilde g$$ is a bundle map making the relevant diagram commute
and that conversely $$\tilde g$$ is the only definition we could have made.
Therefore $$\mathsf{Vect}_r$$ defines a category fibered in groupoids over $$\mathbf{Top}$$.

[Lerman's critique]: {% link _posts/2022-05-15-More-Maps:-Lerman's-Critique.md %}
[Lerman's paper]: https://ems.press/content/serial-article-files/6839
[Fantechi's survey paper]: https://www.math.uni-bielefeld.de/~rehmann/ECM/cdrom/3ecm/pdfs/pant3/fantechi.pdf