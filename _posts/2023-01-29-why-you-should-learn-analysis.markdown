---
layout: post
title:  "Why you should learn analysis"
date:   2023-01-29 08:39:57 -0800
toc: true
---

Visualization, and often geometry, for me, and this has been true since I was a kid, has been a first resort when trying to figure out the world.
It holds today as an adult with a career in machine learning, software engineering, and computer vision.
It highlights assumptions and reveals patterns.
I like to think it was a first resort for Einstein as well on his journey toward general relativity, given that he turned toward differential geometry to create the theory.
In fact, when you zoom in (or out, for that matter), you'll find more and more geometric complexity and curvature.
Mandlebrot showed us that nature exhibits irregularity much more regularly than regularity.
This even gets called out in one of my all time favorite movies, Prometheus:
> God does not build in straight lines

Which is why so many students (including me once upon a time) feel suffocated by the frictionless vacuums and spherical cows of academia.
I could not stand college math, so I turned to physics, which I then dropped for control theory, which I later cast aside for software engineering, arguably the least pure possible format for engineering.

In my journey, a pattern emerged: Interesting problems are often constrained, and there was a mathematical itch that constantly needed scratching.

For example, imagine trying to control a walking robot.
Let's say the lower body has twenty degrees of freedom.
I argue that baking twenty degrees of freedom into a smooth cost function ignores a lot of *a priori* information.
It wastes precious memory and computation (and thus time) in the form of Lagrange multipliers.
Humans don't waste compute on wondering if we should bend our knee in the reverse direction.
Instead, humans, and I argue intelligent control systems, should focus their resources on the constrained space of their reality.
By planning our motion within the bounds of the physical body, we waste less, just like nature.
This is the concept of holonomy (youtube math nerd video alert: one of my professors, Robert Bryant, gave [this fantastic keynote on the topic](https://www.youtube.com/watch?v=QORRJEkhw6s) several years ago to the American Math Society).
I think Einstein would agree with Dr. Bryant's claim; it is probably why the most fundamental thing that we have found -- spacetime -- is nothing more than a curved space in which matter and energy are constrained to exist.

If you are now sufficiently motivated to learn geometry, take a look at [my notes from Mark Stern's Basic Analysis lectures at Duke University](../assets/diff-forms.pdf).
This class (and the others I took from Professors Stern and Bryant) is when my mind really opened up.
I started to appreciate nature in a more deep, and, I think more profound, way.
It also helped the algorithms of machine learning, optimization, and computer vision click for me.
Finally it opened the door to understanding the general theory of relativity to me, which is cool for anyone that wants to understand why are all here in the first place.

