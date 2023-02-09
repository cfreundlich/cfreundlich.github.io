---
layout: post
title:  "The Implicit Function Theorem"
date:   2023-01-29 08:39:57 -0800
categories: personal

---



Trying to solve $$y=f(x)$$ for $$x$$ is a fundamental objective that applies to all branches of mathematics.
For example, [here is an answer on stack exchange](https://math.stackexchange.com/questions/4496360/how-do-we-know-that-some-system-of-equations-doesnt-have-an-analytical-solutio/4498479#4498479) I gave to this effect in machine learning.

When can we find $$x$$ given $$y$$, even if $$f^{-1}$$ does not exist?  

The Implicit Function Theorem gives us the basic tools needed to break down this problem into manageable chunks.
It lets us "linearize" very hard problems, and it gives us the basic tools needed to do differential geometry.

The following are my notes from Mark Stern's Basic Analysis lectures at Duke University.
I have added my comments and explanations to the notes to hopefully motivate them in a new style.
Please, let me know if you have questions via my email at the bottom of the page.

# Linear Systems

Let us begin by remembering when linear systems have solutions:
- $$f(x) = Ax$$ can be solved if $$\text{rank} A = n.$$
- $$f(x) = Ax  + b$$ can be solved also if  $$\text{rank} A = n.$$

<!-- 
Now consider some arbitrary function $$f :\mathbf{R}^n \to \mathbf{R}^n$$. 

If there exists -->

<!-- $$\mathbf{D} f_{x_0} \in L(\mathbf{R}^n , \mathbf{R}^n) \; \text{ such that } f(x) - f(x_0) - \mathbf{D} f_{x_0} (x - x_0)$$ is $$o(\|x-x_0\|),$$ where $$L(\mathbf{R}^n , \mathbf{R}^n) $$ is the set of linear functions, in other words, 

$$
\lim_{x \to x_0} \frac{f(x)-f(x_0) - \mathbf{D} f_{x_0} (x-x_0)}{\|x-x_0\| }= 0.
$$

Then we can say  symbol, $$\mathbf{D} f_{x}$$, is the "derivative of $$f$$ at $$x$$." -->

Before I get into nonlinear systems, a brief note on notation:

# Little "oh" notation
A function $$g(x-x_0)$$ is "little oh" of a norm, say, $$\|x-x_0\|$$ if and only if
$$
\lim_{x \to x_0} \frac{g(x-x_0)}{\|x-x_0\|} = 0.
$$

The derivative is defined using $$o$$ notation, that is, $$\mathbf{D} f_x$$ is called the derivative of $$f$$ at $$x_0$$ iff
$$
f(x) - f(x_0) - \mathbf{D} f_{x_0} (x - x_0) =o( \|x-x_0\|).
$$
While we're on the subject,
# Big "oh" notation
A function $$f(x-x_0)$$ is "big oh" of a norm, say, $$\|x-x_0\|$$ iff
$$ \frac{f(x-x_0)}{\|x-x_0\|}$$ is bounded in a neighborhood of $$x_0.$$

We'll need that later.


Returning to the Implicit Function Theorem, if $$f$$ is some nonlinear function, we might be interested in inverting all or part of it.
Usually, we can only do so locally, and we can only do that if the function is one-to-one in that local neighbordhood.
The Implicit Function Theorem and various corollaries allow us to do that.
It givus us some additional local results even when the derivative $$\mathbf{D} f_{x_0}$$ is not invertible (or nonsquare).

# Infinite dimensions
Implicit in our discussion above is that for a bounded and invertible linear map $$\mathbf{D} f_x,$$ i.e., a square matrix, there exists a bounded inverse.
That is not always the case in infinite dimensional (linear) vector spaces.

An example is, suppose we want to solve following equation in the space of continuous functions $$C$$,

$$
\left(
-\frac{\partial^2}{\partial x^2}
-\frac{\partial^2}{\partial y^2}
-\frac{\partial^2}{\partial z^2}
\right)u + u^3 = F,
$$

for $$u$$ given $$F$$.

In some sense, we have a function $$G(u) = F$$ that we wish to invert.
We can compute
$$
\mathbf{D} G_u (v) = \left(
-\frac{\partial^2}{\partial x^2}
-\frac{\partial^2}{\partial y^2}
-\frac{\partial^2}{\partial z^2}
\right)v + u^2 v,
$$
and we have reduced our nonlinear PDE to a linear PDE.
The question is, when is $$\mathbf{D} G_u$$ invertible?
If we can answer positively, then we can solve the linearized PDE.


# Linear Algebra: A Review for Infinite Dimensions
Let $$X$$ be a normed linear space.
Recall that this means that there is a function $$\|\cdot\|_X :X \to \mathbf{R}_+$$ s.t.
1. $$\|0\|_X = 0$$, 
1. $$\|\alpha x\|_X = \alpha \|x\|_X$$, and
1. $$\|x + y\|_X \leq \|x\|_X + \|y\|_X$$.

For normed linear spaces, $$\|\cdot\|$$ defines a distance metric.

Here's an example. For the $$C([0,1], \mathbf{R}),$$ 

$$
\|f\| = \sup_{x \in [0,1] }\|f(x)\|.
$$

For the remainder of this section, we assume $$X,Y$$ are linear spaces unless otherwise stated.


A Banach space is a normed linear space that is complete.

<!-- Let $$X,Y$$ be normed linear spaces. -->
Let $$B(X,Y)$$ be the set of bounded linear functions from $$X$$ to $$Y$$.
Let $$L(X,Y)$$ be the set of any linear function from $$X$$ to $$Y$$.
We have that $$B(X,Y) \subset L(X,Y),$$ with equality if $$X$$ is finite dimensional.

Let 
$$
X = \{a_1, a_2, \dots \mid \text{ only finitely many }a_j >0\}
$$

Note that $$X$$ is a linear vector space.
It has the $$\ell_1$$ norm, i.e., for a vector $$a\in X,$$ 

$$\|a\|_X = \sum_j \|a_j\|.$$

Now define a linear function on $$X$$ by 
$$
La = (a_1, 2a_2, 3a_3, \dots).
$$
Clearly, $$La \in X$$ for any $$a \in X.$$
However, it is an unbounded operator.
To verify this fact, let 

$$a = (0, \dots, 0 ,\underbrace{ 1}_\text{ the n-th spot}, 0, \dots).$$

so that 
$$
La = (0, \dots, 0 ,n, 0, \dots).
$$
Note that $$L$$ is thus unbounded.

Note that $$L^{-1}$$ is given by 
$$
Sa = (a_1, \frac{1}{2}a_2, \frac{1}{3}a_3, \dots).
$$
Then, $$SL = LS = I.$$
We say that $$S$$ is invertible if we can find a bounded inverse, i.e., not just any inverse will do.
But $$L$$ is the inverse of $$S$$, and we just showed that $$L$$ is unbounded.
Thus, $$S \not  \in B(X,Y)$$.


In summary, we have the following definition.
# Invertible Linear Functions
A linear function is invertible iff its inverse is a bounded linear function.

# Differetiable Functions
A function $$f :X \to Y$$ is $$C^1$$ if $$f$$ is differentiable for all $$x \in X,$$ and $$\mathbf{D} f : X \to B(X,Y)$$ is continuous.


For $$\mathbf{D} f : X \to B(X,Y)$$ to be a continuous function, obviously we need that $$B(X,Y)$$ to a be a metric space (otherwise what would continuity even mean?).
Then, we need a norm for $$B(X,Y).$$

$$\|A\| = \sup_{v \neq 0} \frac{\|Av\|_Y}{\|v\|_X} = \sup_{\|v\|_X = 1} \|Av\|_Y.$$


If $$B \in B(X,Y)$$ and $$A \in B(Y,Z),$$ then $$AB \in B(X,Z)$$ and $$\|AB\| \leq \|A\|\|B\|.$$

Proof:

Suppose $$Bv \neq 0$$ (if it does equal zero then proof is trivial).
Then

$$\frac{\|AB v\|}{\|v\|} = \frac{\|AB v\|}{\|Bv\|} \frac{\|Bv\|}{\|v\|} \leq \|A\|{\|B\|}.$$





