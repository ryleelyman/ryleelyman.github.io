---
layout: post
math: true
---
Gromov's original definition of Gromov hyperbolicity makes sense for arbitrary metric spaces.
However, it is only a quasi-isometry invariant for geodesic metric spaces.
I learned this from a
[paper of Väisälä](https://www.sciencedirect.com/science/article/pii/S0723086905000113?via%3Dihub).
The purpose of this post is to understand the counterexample he gives.
I also define Gromov hyperbolicity and quasi-isometry in this post,
which might make it useful for future reference.
The reader already familiar with Gromov hyperbolicity and quasi-isometries
might wish to skip ahead to the heading below.

Let $$(X,d)$$ be a metric space.
We say that $$X$$ is a *length space* if the distance between any two points $$x$$ and $$y$$ in $$X$$
is equal to the infimum of the length of a path joining them.
A *geodesic* in $$X$$ is a path $$\gamma\colon [a,b] \to X$$ from a closed interval $$[a,b] \subset \mathbb{R}$$
such that $$d(\gamma(s),\gamma(t)) = |s-t|$$ for all $$s$$ and $$t$$ in the interval $$[a,b]$$.
We say that $$X$$ is a *geodesic* metric space if any two points can be joined by a geodesic.
Geodesic metric spaces are length spaces but not necessarily conversely.

Gromov's original definition of hyperbolicity of $$X$$ is the following.
Given points $$x$$, $$y$$ and $$z$$ in $$X$$, define the *Gromov product*
of $$x$$ and $$y$$ with respect to $$z$$ to be the quantity

$$(x,y)_z = \frac{1}{2}\left(d(x,z) + d(y,z) - d(x,y)\right).$$

Then we say that $$X$$ is *$$\delta$$-hyperbolic* if there exists some $$\delta \ge 0$$
with the property that for any four points $$x$$, $$y$$, $$z$$ and $$w$$ in $$X$$,
we have

$$(x,z)_w \ge \min\{(x,y)_w,(y,z)_w\} - \delta.$$

Let's try and make sense of this.
The intuition for the Gromov product is the following.
A *tripod* is a metric tree with four vertices, three of which are leaves and one of which has valence three.
Given any triple of points $$x$$, $$y$$ and $$z$$ in a metric space,
you should convince yourself that we can always construct a tripod
with leaves $$\hat x$$, $$\hat y$$ and $$\hat z$$ such that we have

$$d(x,y) = d(\hat x,\hat y),\quad d(x,z) = d(\hat x,\hat z),\quad\text{and}\quad d(y,z) = d(\hat y,\hat z).$$

In this situation, the Gromov product $$(x,y)_z$$
is equal to the distance from $$\hat z$$ to the center vertex of the tripod.
To make sense of the hyperbolicity condition,
let's continue to think about trees,
only in this case assume that $$X$$ itself is a metric tree.
Then in this case it's not too hard to argue that the hyperbolicity condition holds with $$\delta = 0$$;
a picture illustrating the general case is below.
Thus one way to think of $$\delta$$-hyperbolicity is to think that from the point of view of any point $$w \in X$$,
triangles in $$X$$ look like triangles in trees, up to an error of $$\delta$$.

![Trees are $$0$$-hyperbolic](/assets/img/GromovProduct.jpeg)

If $$X$$ is a geodesic metric space, there are other conditions equivalent to this one
that are more directly about the geometry of, e.g. triangles in $$X$$.
I've been collecting as many of these conditions as the community will give me
in a [MathOverflow post](https://mathoverflow.net/q/396359/135175).
Eventually I expect to make a blog post or several about the various definitions.

Given metric spaces $$(X,d_X)$$ and $$(Y,d_Y)$$ and constants $$K \ge 1$$ and $$C \ge 0$$,
a *$$(K,C)$$-quasi-isometric embedding* is a function $$f\colon X \to Y$$
(it need not be continuous)
such that for all points $$x$$ and $$y$$ in $$X$$, the following inequality holds

$$ \frac 1Kd_X(x,y) - C \le d_Y(f(x),f(y)) \le Kd_X(x,y) + C. $$

So we see that $$f$$ is allowed to distort distances by a bounded multiplicative and additive amount.
A *$$(K,C)$$-quasi-isometry* is a $$(K,C)$$-quasi-isometric embedding with the additional property that
for every point $$y \in Y$$ there is a point $$x \in X$$ such that $$d_Y(y,f(x)) \le C$$.

## The theorem and the counterexample

Väisälä proves the following theorem.
> **Theorem** Let $$X$$ and $$Y$$ be length spaces and $$f\colon X \to Y$$ a quasi-isometric embedding.
> If $$Y$$ is $$\delta$$-hyperbolic, then $$X$$ is $$\delta'$$-hyperbolic
> for some $$\delta'$$ depending only on $$\delta$$ and the quasi-isometry constants for $$f$$.

He then observes that the theorem is not true if one does not assume that $$X$$ is a length space.
Here is the counterexample.
The hyperbolic space $$Y$$ is the real line $$\mathbb{R}$$ with the standard metric.
(Recall that $$\mathbb{R}$$ is a real tree, and thus $$0$$-hyperbolic.)
The space $$X$$ is the graph of the absolute value function $$\{(x,y) \in \mathbb{R}^2 : y = |x| \}$$
with the Euclidean metric.
The claim is that the map $$f\colon X \to Y$$ defined as $$f(x,y) = x$$ is a quasi-isometric embedding,
but that $$X$$ is not hyperbolic.

First we show that $$f$$ is a quasi-isometric embedding.
Indeed, it is clear that given $$\vec x$$ and $$\vec y$$ in $$X$$,
we have $$d_Y(f(\vec x),f(\vec y)) \le d_X(\vec x,\vec y)$$.
On the other hand, note that $$d_X(\vec x,\vec y)$$ is furthest from $$d_Y(f(\vec x),f(\vec y))$$
when $$\vec x$$ and $$\vec y$$ are in the same quadrant, where we have
$$d_X(\vec x,\vec y) = \sqrt{2}d_Y(f(\vec x),f(\vec y))$$.
Thus the map $$f$$ is a $$(\sqrt 2,0)$$-quasi-isometric embedding, in fact a $$(\sqrt 2,0)$$-quasi-isometry.

Finally we show that $$X$$ is not hyperbolic.
Consider the four points $$x = (0,0)$$, $$y = (-2t,2t)$$, $$z = (2t,2t)$$ and $$w = (t,t)$$.
Then we have

$$ (x,z)_w = \frac 12\left(\sqrt 2t + \sqrt 2t - 2\sqrt 2t\right) = 0,$$

$$ (x,y)_w = \frac 12\left(\sqrt 2t + 2\sqrt 5t - 2\sqrt 2t\right) \approx 1.53t$$

$$ (y,z)_w = \frac 12\left(2\sqrt 5 + \sqrt 2t - 4t\right) \approx 0.94t$$

But observe that as $$t \to \infty$$, we have that $$(x,y)_w$$ and $$(y,z)_w$$ tend to $$\infty$$,
so no uniform choice of $$\delta$$ makes the inequality
$$(x,z)_w \ge \min\{(x,y)_w,(y,z)_w\} - \delta$$ hold.