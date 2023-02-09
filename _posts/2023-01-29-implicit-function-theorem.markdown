---
layout: post
title:  "The Implicit Function Theorem and the Implications Thereof"
date:   2023-01-29 08:39:57 -0800
categories: personal
---

\begin{enumerate}
\item $f(x) = Ax$ can be solved $\iff$ $\rank A = n.$
\item $f(x) = Ax  + b$ can be solved also if  $\rank A = n.$
\item Suppose differentiable $f :\reals^n \to \reals^n$, i.e., $\exists \bbD f_{x_0} \in L(\reals^n , \reals^n) \; \st f(x) - f(x_0) - \bbD f_{x_0} (x - x_0)$ is $o(\abs{x-x_0}),$ where $L(\reals^n , \reals^n) $ is the set of linear functions. In other words, 
\[
\lim_{x \to x_0} \frac{f(x)-f(x_0) - \bbD f_{x_0} (x-x_0)}{\abs{x-x_0} }= 0.
\]
Then, the purpose of the following discussion is so that we can solve for $x$ given $y=f(x),$ at least locally.
\end{enumerate}
\begin{definition}[Little ``oh'' notation]
A function $g(x-x_0)$ is ``little oh'' of a norm, say, $\abs{x-x_0}$ iff
\[
\lim_{x \to x_0} \frac{g(x-x_0)}{\abs{x-x_0}} = 0.
\]
\end{definition}
The derivative is defined using $o$ notation, that is, $\bbD f_x$ is called the derivative of $f$ at $x_0$ iff
\[
f(x) - f(x_0) - \bbD f_{x_0} (x - x_0) =o( \norm{x - x_0}).
\]
While we're on the subject,
\begin{definition}[Big``oh'' notation]
A function $f(x-x_0)$ is ``big oh'' of a norm, say, $\abs{x-x_0}$ iff
$ \frac{f(x-x_0)}{\abs{x-x_0}}$ is bounded in a neighborhood of $x_0.$
\end{definition}
We may want to solve $y=f(x)$ for $x$.
Typically, if $f$ is some nonlinear function, so first we hope that we can at least do so locally.
Moreover, we can only do so locally if the function is one-to-one in that local neighbordhood.
The IFT and various corollaries allow us to do that, and even get some additional local results with the derivative $\bbD f_{x_0}$ is not invertible (or nonsquare).

\begin{rem}[Infinite Dimensions]
Implicit in our discussion above is that for a bounded and invertible linear map $\bbD f_x,$ i.e., a square matrix, there exists a bounded inverse.
That is not always the case in infinite dimensional (linear) vector spaces, such as $\ccalC.$
\end{rem}
\begin{ex}
An example is, suppose we want to solve following equation in $\ccalC$,
\[
\left(
-\frac{\partial^2}{\partial x^2}
-\frac{\partial^2}{\partial y^2}
-\frac{\partial^2}{\partial z^2}
\right)u + u^3 = F,
\]
for $u$ given $F$.
In some sense, we have a function $G(u) = F$ that we wish to invert.
We can compute
\[
\bbD G_u (v) = \left(
-\frac{\partial^2}{\partial x^2}
-\frac{\partial^2}{\partial y^2}
-\frac{\partial^2}{\partial z^2}
\right)v + u^2 v,
\]
and we have reduced our nonlinear PDE to a linear PDE.
The question is, when is $\bbD G_u$ invertible?
If we can answer positively, then we can solve the linearized PDE.
\end{ex}

\subsection{Linear Algebra: A Review for Infinite Dimensions}
Let $\ccalX$ be a normed linear space.
This means that there is a function $\abs{\cdot}_\ccalX :\ccalX \to \reals_+$ s.t.
\begin{enumerate}
\item $\abs{0}_\ccalX = 0$
\item $\abs{\alpha x}_\ccalX = \alpha \abs{x}_\ccalX$
\item $\abs{x + y}_\ccalX \leq \abs{x}_\ccalX + \abs{y}_\ccalX.$
\end{enumerate}
For normed linear spaces, $\abs{\cdot}$ defines a distance metric.
\begin{ex}
For the $\ccalC([0,1], \reals),$ 
\[
\abs{f} = \sup_{x \in [0,1] }\abs{f(x)}.
\]
\end{ex}
For the remainder of this section, we assume $\ccalX,\ccalY$ are linear spaces unless otherwise stated.

\begin{definition}[Banach Space]
A Banach space is a normed linear space that is complete.
\end{definition}

%Let $\ccalX,\ccalY$ be normed linear spaces.
Let $\ccalB(\ccalX,\ccalY)$ be the set of bounded linear functions from $\ccalX$ to $\ccalY$.
Let  $\ccalL(\ccalX,\ccalY)$ be the set of any linear function from $\ccalX$ to $\ccalY$.
We have that $\ccalB(\ccalX,\ccalY) \subset \ccalL(\ccalX,\ccalY),$ with equality if $\ccalX$ is finite dimensional.

\begin{ex}
Let 
\[
\ccalX = \set{a_1, a_2, \dots \mid \text{ only finitely many }a_j >0}
\]
Note that $\ccalX$ is a linear vector space.
It has the $\ell_1$ norm, i.e., for a vector $a\in \ccalX,$ $\abs{a}_\ccalX = \sum_j \abs{a_j}_\reals.$
Now define a linear function on $\ccalX$ by 
\[
La = (a_1, 2a_2, 3a_3, \dots).
\]
Clearly, $La \in \ccalX$ for any $a \in \ccalX.$
However, it is an unbounded operator.
To verify this fact, let 
\[
a = (0, \dots, 0 ,\underbrace{ 1}_\text{ the $n$-th spot}, 0, \dots).
\]
so that 
\[
La = (0, \dots, 0 ,n, 0, \dots).
\]
Note that $L$ is thus unbounded.
%thus
Note that $L^{-1}$ is given by 
\[
Sa = (a_1, \frac{1}{2}a_2, \frac{1}{3}a_3, \dots).
\]
Then, $SL = LS = I.$
We say that $S$ is invertible if {\bf we can find a bounded inverse}, i.e., not just any inverse will do.
But $L$ is the inverse of $S$, and we just showed that $L$ is unbounded.
Thus, $S \not  \in \ccalB(\ccalX,\ccalY)$.
\end{ex}
In summary, we have the following definition.
\begin{definition}[Invertible Linear Function]
A linear function is invertible iff its inverse is a bounded linear function.
\end{definition}

\begin{definition}
A function $f :\ccalX \to \ccalY$ is $\ccalC^1$ if $f$ is differentiable for all $x \in \ccalX,$ and $\bbD f : \ccalX \to \ccalB(\ccalX,\ccalY)$ is continuous.
\end{definition}

For $\bbD f : \ccalX \to \ccalB(\ccalX,\ccalY)$ to be a continuous function, obviously we need that $\ccalB(\ccalX,\ccalY)$ to a be a metric space (otherwise what would continuity even mean?).
Then, we need a norm for $\ccalB(\ccalX,\ccalY).$
\[
\abs{A} = \sup_{v \neq 0} \frac{\abs{Av}_\ccalY}{\abs{v}_\ccalX} = \sup_{\abs{v}_\ccalX = 1} \abs{Av}_\ccalY.
\]

\begin{lem}
If $B \in \ccalB(\ccalX,\ccalY)$ and $A \in B(\ccalY,\ccalZ),$ then $AB \in B(\ccalX,\ccalZ)$ and $\abs{AB} \leq \abs{A}\abs{B}.$
\end{lem}
\begin{proof}
Suppose $Bv \neq 0$ (if it does equal zero then proof is trivial).
Then
\[
\frac{\abs{AB v}}{\abs{v}} = \frac{\abs{AB v}}{\abs{Bv}} \frac{\abs{Bv}}{\abs{v}} \leq \abs{A}{\abs{B}}
\]
\end{proof}




