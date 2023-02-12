---
layout: post
title:  "The Implicit Function Theorem"
date:   2023-01-29 08:39:57 -0800
categories: personal
comments: true

---



Trying to solve $$y=f(x)$$ for $$x$$ is a fundamental objective that applies to all branches of mathematics.
For example, [here is an answer on stack exchange](https://math.stackexchange.com/questions/4496360/how-do-we-know-that-some-system-of-equations-doesnt-have-an-analytical-solutio/4498479#4498479) I gave to this effect in machine learning.

When can we find $$x$$ given $$y$$, even if $$f^{-1}$$ does not exist?  

The Implicit Function Theorem gives us the basic tools needed to break down this problem into manageable chunks.
It gives us the basic tools needed to do differential geometry.

The following are my notes from Mark Stern's Basic Analysis lectures at Duke University.
I have added my comments and explanations to the notes to hopefully motivate them in a new style.
Please, let me know if you have questions via my email at the bottom of the page.

# Linear Systems

Let us begin by remembering when linear systems have solutions:
- $$f(x) = Ax$$ can be solved if $$\text{rank} A = n.$$
- $$f(x) = Ax  + b$$ can be solved also if  $$\text{rank} A = n.$$

<!-- 
Now consider some arbitrary function $$f :\mathbb{R}^n \to \mathbb{R}^n$$. 

If there exists -->

<!-- $$\mathbf{D} f_{x_0} \in L(\mathbb{R}^n , \mathbb{R}^n) \; \text{ such that } f(x) - f(x_0) - \mathbf{D} f_{x_0} (x - x_0)$$ is $$o(\|x-x_0\|),$$ where $$L(\mathbb{R}^n , \mathbb{R}^n) $$ is the set of linear functions, in other words, 

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


Returning to our goal of solving equations, we want to invert functions.
Usually, we can only do so locally, and we can only do that if the function is one-to-one in that local neighbordhood.
The Implicit Function Theorem and various corollaries, like the Inverse Function Theorem, allow us to do that.
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
The question is, when is $$\mathbf{D} G_u$$ invertible, and what do we do if it isn't square?
<!-- If we can answer positively, then we can solve the linearized PDE. -->


# Linear Algebra: A Review for Infinite Dimensions
Let $$X$$ be a normed linear space.
Recall that this means that there is a function $$\|\cdot\|_X :X \to \mathbb{R}_+$$ s.t.
1. $$\|0\|_X = 0$$, 
1. $$\|\alpha x\|_X = \alpha \|x\|_X$$, and
1. $$\|x + y\|_X \leq \|x\|_X + \|y\|_X$$.

For normed linear spaces, $$\|\cdot\|$$ defines a distance metric.

Here's an example. For the $$C([0,1], \mathbb{R}),$$ 

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




# Another brief example
Let

$$\ell_1 (\mathbb{R}) = \Big\{ \{a_k\}_{k \in \mathbb{N}} \mid \sum_{k\in \mathbb{N}} \|a_k\| < \infty \Big\}.$$

Define $$A \in \mathcal{B} (\ell_1(\mathbb{R}), \ell_1(\mathbb{R}))$$ by 

$$A (v_1, v_2, \dots) = (0, v_1, v_2,\dots)$$

to be the shift.
Note that $$A$$ is injective but not surjective.
Let also 

$$B  (v_1, v_2, \dots) = (v_2,v_3, \dots).$$

It is not injective, but it is surjective.
The composition does not commute, i.e.,

$$B \circ A = I, \text{ but } A \circ B \neq I.$$


# Invertibility of Linear Operators
In what follows, $$\mathcal{M}$$ is a metric space, $$\mathcal{B}$$ is the set of bounded linear functions, and $$\mathcal{X}$$ and $$\mathcal{Y}$$ are linear vector spaces.

# Lemma
Let $$A \in C(\mathcal{M}, \mathcal{B}(\mathcal{X},\mathcal{Y})).$$
Let $$p \in \mathcal{M} \; \text{ s.t. } A(p)$$ is invertible. Then there is a neighborhood $$U$$ of $$p$$ such that $$\forall q \in U,$$ $$q \mapsto A^{-1}(q)$$ is continuous.

## Proof

Let $$W(q) = A(p)^{-1} A(q)$$ so that $$W : \mathcal{M} \to \mathcal{B}(\mathcal{X}, \mathcal{X}).$$

Pictorially,

$$\mathcal{M}  \xrightarrow{A} \mathcal{B}(\mathcal{X}, \mathcal{Y})  \xrightarrow{A(p)^{-1}} \mathcal{B}(\mathcal{Y}, \mathcal{X}).$$

So $$W(p) = I$$, i.e., $$4\|I-W(p)\| = 0.$$

Also note that $$W(q)$$ is continuous because $$A(q)$$ is continuous, and all $$W$$ is doing is premultiplying by a constant.
Thus, $$\|I-W(q)\|$$ is a continuous function as a composition of continuous maps, and there is a neighborhood $$U$$ of $$p$$ such that $$\|I-W(q)\| \leq \frac{1}{2}$$ for $$q \in U.$$
 Note

 $$ W(q) = I- (I - W(q)).$$

 Let's try to invert $$I - W(q).$$
 The geometric series 

 $$ \frac{1}{1-r} = 1 + r + r^2 + \cdots$$
 
 suggests that we consider
 
 $$\sum_{k=0}^\infty (I - W(q))^k \triangleq PW(q)^{-1}$$

 the putative inverse of $$W(q).$$
 Note that the series converges if it converges absolutely and $$\|(I - W(q))^k\| \leq \|I - W(q)\|^k \leq (1/2)^k, $$ which converges.
By the M-test, the series $$PW(q)^{-1}$$ converges.
We have that

$$\begin{aligned}
W(q) PW(q)^{-1} &= W(q) \sum_{k=0}^\infty (I - W(q))^k 
\\
&= \lim_{n \to \infty} W(q) \sum_{k=0}^n (I - W(q))^k 
\\
&= \lim_{n \to \infty} \sum_{k=0}^n ( W(q)+I-I) (I - W(q))^k 
\\
&= \lim_{n \to \infty} - \sum_{k=0}^n (I - W(q))^{k+1} +  \sum_{k=0}^n (I - W(q))^k 
\\
&= \lim_{n \to \infty}  \sum_{k=0}^n (I - W(q))^k - \sum_{k=1}^{n+1} (I - W(q))^{k} 
\\
&= \lim_{n \to \infty} I - (I - W(q))^{n+1} 
\\
&=I
\end{aligned}
$$

Similarly, $$PW(q)^{-1}$$ is the left inverse of $$W(q).$$
This proves that $$PW(q)^{-1}$$ is the actual inverse of $$W(q).$$ 
From now on we just call it $$W(q)^{-1}$$.
Then,

$$A(q)^{-1} = W(q)^{-1} \circ A(p)^{-1},$$

which is continuous because $$W(q)^{-1}$$ is a continuous and $$A(p)^{-1}$$ is a constant, as desired.


# The Inverse Function Theorem
Let $$A \subset \mathbb{R}^n$$ be open, $$f:A \to \mathbb{R}^n$$ a $$C^1$$ function.
Let $$x_0 \in A.$$
Suppose $$\mathbf{D} f_{x_0}$$ is invertible.
Then we can find an open neighborhood $$U$$ of $$x_0$$ and an open neighborhood $$W$$ of $$f(x_0)$$ such that for each $$x \in U$$, $$f(x) \in W$$ and there is a $$C^1$$ function $$\phi: W\to U$$ such that $$\phi$$ is both a left and right inverse to $$f$$, that is

$$f\circ \phi (y) = y \; \text{and } \phi \circ f (x) = x$$

i.e, $$\phi = f|_U^{-1}$$.
Moreover, $$\mathbf{D} f_x^{-1} = \mathbf{D} \phi_{f(x)}$$ and if $$f$$ is $$C^k,$$ then so is $$\phi.$$


The Inverse Function Theorem holds for infinite dimensional linear spaces.
Just replace the finite dimensional spaces $$\mathbb{R}^n$$ with a Banach space and everything still holds.
In the following proof, however, we restrict ourselves to finite dimensions because we will not assume the chain rule works for infinite dimensions (even though it does).
We'll make a note in the proof where we have to assume finite dimensional Banach space.

## Proof of the Inverse Function Theorem
The first step of the proof is book keeping.
Essentially, we'll want to show that if the theorem holds for a function $$f$$ such that $$f(0) = 0$$ and $$\mathbf{D} f_0 = I,$$ then it holds for an arbitrary $$f$$ that also meets the conditions of the theorem.
Define

$$\tilde{f} (x) =  [\mathbf{D} f_{x_0}]^{-1} ( f(x_0 + x) - f(x_0)).$$

We have that $$\tilde{f}(0) = 0,$$ and

$$\begin{align}
\mathbf{D} \tilde{f}_0 &=\mathbf{D}  ( [\mathbf{D} f_{x_0}]^{-1}\mathbf{D} f(x_0) )\\
&= [\mathbf{D} f_{x_0}]^{-1}\mathbf{D} f(x_0)\\
&=I.\end{align}$$

Now suppose $$g$$ inverts $$\tilde{f}$$.  Then,

$$\begin{align}
\tilde{f} \circ g (y) &= y \\
\mathbf{D} f^{-1}_{x_0} \circ ( f(x_0 + g(y)) - f(x_0)) &= y \\
f(x_0 + g(y)) - f(x_0) &=\mathbf{D} f_{x_0}   y \\
f(x_0 + g(y)) &=\mathbf{D} f_{x_0}   y  +  f(x_0)
\end{align}$$

then, since $$y$$ was arbitrary, 

$$\begin{align}
f(x_0 + g(\mathbf{D} f^{-1}_{x_0} y)) &=\mathbf{D} f_{x_0}   \mathbf{D} f^{-1}_{x_0} y  +  f(x_0)\\
f(x_0 + g(\mathbf{D} f^{-1}_{x_0} y)) &=  y  +  f(x_0)
\end{align}$$

Again, since $$y$$ was arbitrary, 

$$f(x_0 + g(\mathbf{D} f^{-1}_{x_0} (y - f(x_0)))) =  y.$$

Set $$G(y) = x_0 + g(\mathbf{D} f^{-1}_{x_0} (y - f(x_0))).$$

Thus, $$f \circ G (y) = y \text{ and } G \circ f (x) = x.$$
Therefore, to prove the theorem, we only need to consider functions such that $$f(0) = 0$$ and $$\mathbf{D} f_0 = I.$$


We proceed proving the theorem assuming that $$f(0) = 0$$ and $$\mathbf{D} f (0) = I.$$
Essentially, what we are setting out to do in this theorem is, given $$y$$ in a neighborhood of 0, find $$x$$ also in a neighborhood of 0 such that $$f(x)= y.$$

Define $$\psi_y (x) = y + x - f(x).$$
We have that

$$\psi_y (x) = x \iff y = f(x).$$

First we'll show that $$\psi_y$$ is a contraction map.
For this, let 

$$\alpha (t) = \psi_y( (1-t)z + tx)$$

so that

$$\psi_y(x) - \psi_y (z) = \alpha (1) - \alpha (0) = \int_0^1 \alpha' (t) dt.$$
Note that

$$\|\psi_y(x) - \psi_y (z) | = \| \alpha (1) - \alpha (0)\| \leq \int_0^1 \|\alpha' (t) \|dt.$$
Applying the chain rule (for infinite dimensions, if you like),

$$\alpha' (t) = (\mathbf{D} \psi_y)_{(1-t)z + tx} (x-z).$$

Taking the norm and applying the triangle inequality and taking the sup,

$$\begin{align}
\|\alpha' (t) | &\leq \|(\mathbf{D} \psi_y)_{(1-t)z + tx} \| \|(x-z)\| 
\leq \sup_{0 \leq t \leq 1}  \|(\mathbf{D} \psi_y)_{(1-t)z + tx} \| \|(x-z)\|
\end{align}$$

Now, we know that $$ \|(\mathbf{D} \psi_y)_{x }\| = I - \mathbf{D} f_0 = I-I = 0,$$ and we also assumed that the derivative is continuous in the hypothesis.
Thus, we can find a $$\delta>0$$ such that

$$\|(\mathbf{D} \psi_y)_{x} \| < \frac{1}{2} \quad \forall x \in \bar{B}_\delta (0).$$

where $$\bar{B}_\delta (0)$$ denotes the closed $$\delta$$-ball centered at zero.
Note that $$\bar{B}_\delta (0)$$ is convex, so if $$z,x \in \bar{B}_\delta (0)$$, then so is $$(1-t)z + tx$$ for $$0\leq t \leq 1.$$
Thus, 

$$\|\psi_y (x) - \psi_y(z)\| < \frac{1}{2},$$

so $$\psi_y$$ is a contraction map as long as it maps $$\bar{B}_\delta (0)$$ onto $$\bar{B}_\delta (0)$$.
To verify this directly

$$\begin{align}
\psi_y(x) &= y + x - f(x) \\
&\leq \|y\| + \|x  -f(x)\|\\
&=\|y\| + \| \psi_y(x)   -\psi_y(0) \|\\
&\leq \|y\| + \frac{1}{2} \|x \|\\
&\leq \|y\| + \frac{1}{2}\delta,
\end{align}$$

so $$\psi_y$$ is a contraction map as long as $$\|y\| < \delta,$$ which is fine because we only claimed the theorem held locally.

Recall the contraction mapping theorem, and apply it to the current state of things.
In particular, it tells us that

$$\exists_! x_y \in \bar{B}_{\frac{\delta}{2}} (0) \; \text{ s.t. } \psi_y(x_y) = x_y, \text{ i.e., }f(x_y) = y.$$

Let $$g(y) = x_y.$$
Thus far, we only showed that

$$\exists g : \bar{B}_{\frac{\delta}{2}} (0) \to \bar{B}_{\delta} (0) \; \text{ s.t. } f(g(y)) = y.$$

We need to show that $$g$$ is continuous before we can prove anything about the differentiability of it.
Let $$y_1,y_2 \in  \bar{B}_{\frac{\delta}{2}} (0).$$
For $$i=1,2,$$

$$\psi_y (g(y_i)) = g(y_i) $$

and we can write an identity based on the fact that $$f$$ inverts $$g$$, 

$$y_i + g(y_i) - f(g(y_i)) = g(y_i)$$

Then

$$\begin{align}
\|g(y_1) - g(y_2)\| &=\|y_1+ g(y_1) - f(g(y_1))  - y_2 + g(y_2) - f(g(y_2)) \| \\
&\leq \|y_1- y_2\| + \| g(y_1) - f(g(y_1)) + g(y_2) - f(g(y_2)) \| \\
&= \|y_1- y_2\| + \| \psi_0 ( g(y_1) ) - \psi_0 ( g(y_2) ) \| 
\\
&\leq \|y_1- y_2\| + \frac{1}{2}  \| g(y_1) -g(y_2)  \| 
\end{align}$$

which implies that $$\frac{1}{2}  \| g(y_1) -g(y_2)  \|  \leq \|y_1- y_2\|.$$
Thus $$g$$ is Lipschitz, which is in fact stronger than continuity.
Now we need to show $$g$$ is differentiable and show that its derivative is equal to the inverse of the derivative of $$f$$.
We do this by showing that $$\mathbf{D} f_x^{-1}$$ meets the requirements of the derivative of $$g$$.
In particular,

$$\begin{align}
\|g(y) - g(w) - \mathbf{D} f_x^{-1} (y-x)\| &= \|-  \mathbf{D}f_x^{-1} ( \mathbf{D} f_x (g(y) - g(w)  )+ y-w)\|
\\
&\leq \|  \mathbf{D} f_x^{-1} \| \| \mathbf{D} f_x (g(y) - g(w)  )+ y-w\|
\\
&= \|  \mathbf{D} f_x^{-1}\|\| \mathbf{D} f_x (x - g(w))  + f(x) -f(g(w))\|
\\
&=  \|  \mathbf{D} f_x^{-1} \| o(\|x - g(w)\|),
\end{align}$$

as desired.

Now that the Inverse Function Theorem is proven, note that
$$g$$ is $$C^1$$ in a neighborhood of 0.
Because $$\mathbf{D} f_x$$ is continuous in $$x$$ and $$\mathbf{D} f_0$$ is invertible, so is $$\mathbf{D} f^{-1}_x$$ near $$0.$$


Now we want to show that, if $$f$$ is $$C^k$$, then $$g$$ is $$C^k.$$
To do it, consider the following lemma.



# Lemma
Let $$\mathcal{W}$$ be a normed linear space.
Let 

$$A : U \subset \mathcal{X} \xrightarrow{C^k} \mathcal{B} (\mathcal{W}, \mathcal{W}).$$


Assume that for all $$p \in \mathcal{X}, A(p)$$ is invertible.
Then
$$x \mapsto A^{-1} (p)$$ is $$C^k.$$

## Proof

$$\begin{align}
A^{-1}(x) - A^{-1}(y) &= A^{-1} (x) ( I - A(x) A^{-1}(y)) \\
&=  A^{-1} (x) \big( A(y)- A(x)  \big)A^{-1}(y) \\
&=  -A^{-1} (x) \big(  A(x) - A(y) \big)A^{-1}(y) \\
&=-  A^{-1} (x)  \big( A(x) - A(y) - \mathbf{D} A_y (x-y)   \big)A^{-1}(y)  -  A^{-1} (x)\mathbf{D} A_y (x-y)  A^{-1}(y) 
\end{align}$$

Stop for a second and consider what the maps are doing: 
- $$A^{-1}(y)   : \mathcal{W} \to \mathcal{W}$$,  
- $$\mathbf{D} A_y   : \mathcal{X} \to \mathcal{B}(\mathcal{W},\mathcal{W})$$, 
- $$\mathbf{D} A_y(x-y)   : \mathcal{W} \to \mathcal{W}$$. 

Now, note that

$$\underbrace{A^{-1} (x) }_\text{bounded} \underbrace{ \big( A(x) - A(y) - \mathbf{D} A_y (x-y)   \big) }_{o(\|{x-y}\|)} \underbrace{A^{-1}(y) }_\text{bounded}.$$

Thus, 

$$
A^{-1}(x) - A^{-1}(y) =-  A^{-1} (x)\mathbf{D} A_y (x-y)  A^{-1}(y) + o(\|x-y\|)
$$

By the definition of continuity, 
$$
\|A^{-1} (x) - A^{-1} (y)| = o(1),
$$
so that

$$\begin{align}
\|
(A^{-1}(x) - A^{-1}(y)) \mathbf{D} A_y (x-y)A^{-1} (y)\
\|&\leq 
\|
(A^{-1}(x) - A^{-1}(y))
\|\|
(A^{-1}(x) - A^{-1}(y))\mathbf{D} A_y
\|\|
A^{-1}(y)
\|\|x-y\| \\
&= o(\|x-y\|)
\|
\end{align}$$

Therefore,

$$\begin{align}
A^{-1}(x) - A^{-1}(y) - (-)A^{-1} (x) \mathbf{D} A_y (x-y) A^{-1} (y) = o(\|x-y\|),
\end{align}$$

and we identify the derivative we are looking for as 

$$(\mathbf{D} A^{-1})_y = -A^{-1} (x) \mathbf{D} A_y (x-y) A^{-1} (y) $$

To prove that $$A^{-1}$$ is $$C^k,$$ repeat this process $$k-1$$ more times.




