---
layout: post
title: The Normal Distribution
categories: []
tags: [concept, mathematics, probability]
description: The normal distribution, also known as the Gaussian or standard normal distribution, is the probability distribution that plots all of its values in a symmetrical fashion, and most of the results are situated around the probability's mean.
cover: "/assets/images/normal-distribution.jpg"
cover_source: "https://pbs.twimg.com/media/DBQttG0XYAAK8_M.jpg"
comments: true
mathjax: true
---

### Introduction
The concept of normal distribution as explained using the game of darts is easier to understand and explain. Consider a game of dart with aim of throwing the dart at the origin of a cartesian plane. The errors in throwing the dart at the origin will have random errors and produce varying results in different trials. Some of the assumptions one can make in this game are: 

* The errors do not depend on the orientation of the cartesian plane.
* Errors in perpendicular directions are independent i.e. dart hitting too high does not alter the probability of it being off to the right.
* Large errors are less likely to occur than the small errors.

### Determining the Shape of the Distribution

The probability of dart falling in a region that lies in the vertical strip from \\(x\\) to \\(x + \Delta x\\) can be given by,

$$p(x) \Delta x$$

Similarly, the probability of dart landing in horizontal strip from \\(y\\) to \\(y + \Delta y\\) can be given by,

$$p(y) \Delta y$$

![The Dart Game](/assets/2017-07-31-normal-distribution/fig-1-dart-game-visualization.png?raw=true)

Because the two events are assumed to be independent, the probability of dart falling in the shaded region is given by

$$p(x) \Delta x \cdot p(y) \Delta y$$

Also, since orientation does not alter probability of an error, any region r units from the origin and with area \\(\Delta x \cdot \Delta y\\) has the same probability and hence can be expressed as, 

$$p(x) \Delta x \cdot p(y) \Delta y = g(r) \Delta x \Delta y$$

This results in the inference

$$g(r) = p(x) \cdot p(y)$$

Differentiating on both the sides, 

$$0 = p(x) \frac {dp(y)} {d \theta} + p(y) \frac {dp(x)} {d \theta} \tag{1}$$

From the figure above, 

$$x = r cos(\theta) \tag{2}$$

$$y = r sin(\theta) \tag{3}$$

So the derivative in (1) can be expressed as,

$$0 = p(x) p'(y) r\,cos(\theta) + p(y) p'(x)(- r\,sin(\theta)) \tag{4}$$

Using (2) and (3), (4) can be rewritten as,

$$0 = p(x) p'(y) x - p(y) p'(x) y \tag{5}$$

Differential equation can be solved by seperating the variables, so (5) becomes,

$$\frac {p'(x)} {x\,p(x)} = \frac {p'(y)} {y\,p(y)} \tag{6}$$

Differential equation (6) is true for any x and y, and x and y are independent. This leads to the result that the ratio must be a constant, i.e.,

$$\frac {p'(x)} {x\,p(x)} = \frac {p'(y)} {y\,p(y)} = C$$

So, 

$$\frac {p'(x)} {p(x)} = Cx \tag{7}$$

Integrating (7), 

$$ln(p(x)) = \frac {Cx^2} {2} + c$$

So, 

$$p(x) = Ae^{ {C \over 2} x^2 }$$

Since, large errors are less likely than smaller errors, C must be negative, so,

$$p(x) = Ae^{ - {k \over 2} x^2 }$$

where k is positive.


### Determining the Coefficient A

If p is the probability density function of a random variable following normal distribution, then the total area under the curve must be 1. So value of A should be such that this property is satisfied. The equation to ve evaluated is,

$$ \int_{-\infty}^\infty A e^{ - {k \over 2} x^2 } dx = 1$$

Dividing both sides by A, 

$$ \int_{-\infty}^\infty e^{ - {k \over 2} x^2 } dx = {1 \over A}$$

Since the distribution is symmetric, changing the limits of distribution,

$$ \int_0^\infty e^{ - {k \over 2} x^2 } dx = {1 \over 2A}$$

Then, 

$$ \int_0^\infty e^{ - {k \over 2} x^2 } dx \cdot \int_0^\infty e^{ - {k \over 2} y^2 } dy = {1 \over 4A^2} \tag{8}$$

Since x and y are independent, (8) can be rewritten as double integral,

$$ \int_0^\infty \int_0^\infty e^{ - {k \over 2} (x^2 + y^2) } dx = {1 \over 4A^2} \tag{9}$$

The double integral in (9) can be evaluated as polar coordinates,

$$ \int_0^\infty \int_0^\infty e^{ - {k \over 2} (x^2 + y^2) } dx = \int_0^{\pi/2} \int_0^\infty e^{ - {k \over 2} r^2 } r\,dr\,d \theta \tag{10}$$

Applying u-substitution to (9),

$$u = - {k \over 2} r^2 \tag{11}$$

differentiating w.r.t. r, 

$${du \over dr} = -{k \over 2} \cdot 2$$

So,

$$r\,dr = {du \over -k} \tag{12}$$

Substituting (11) and (12) in (10),

$$ \int_0^{\pi/2} \int_0^\infty e^{ - {k \over 2} r^2 } r\,dr\,d \theta = \int_0^{\pi/2} {-1 \over k} [\int_0^{-\infty} e^u du]\,d \theta = \int_0^{\pi/2} {d\theta \over k} = {\pi \over 2k}$$

Using (9), 

$${1 \over 4A^2} = {\pi \over 2k}$$

So finally, 

$$A = \sqrt{ \frac {k} {2 \pi} } \tag{13}$$

Substituting A in the \\(p(x)\\) for normal distribution, 

$$p(x) = \sqrt{ \frac {k} {2 \pi} } e^{ - {k \over 2} x^2 }$$


### Determining the value of k

Probably k can be calculated using the formulae for mean or variance. 

The mean, \\(\mu\\), is defined as the following integral,

$$\int_{-\infty}^\infty x\, p(x) dx$$

Since function \\(x\,p(x)\\) is an odd function, \\(\mu\\) is zero.

The variance, \\(\sigma^2\\), is given by following integral,

$$\int_{-\infty}^\infty (x-\mu)^2\, p(x) dx$$

Since mean is zero, above equation becomes,

$$\int_{-\infty}^\infty x^2\, p(x) dx = \sigma^2$$

Changing the limits of integral,

$$2 \sqrt{ \frac {k} {2 \pi} } \int_0^\infty x^2 \, e^{ - {k \over 2} x^2} dx = \sigma^2 \tag{14}$$

Evaluating the integral on left by parts where u and v are given by,

$$u = x$$

$$ dv = x\, e^{ {-k \over 2} x^2} $$

$$v = \int x\, e^{ {-k \over 2} x^2} dx \tag{15}$$

Then v can be evaluated by substitution, 

$$ y = {-k \over 2} x^2 \tag{16}$$

So, 

$$x\,dx = {dy \over -k} \tag{17}$$

Substituting (16) and (17) in (15),

$$v = -{1 \over k} \int e^y\, dy = {e^y \over -k} = \frac {e^{ {-k \over 2} x^2 } } {-k}$$

Applying the parts to (14) , 

$$2 \sqrt{ \frac {k} {2 \pi} } \left( \lim_{M \to \infty} \left[ {-x \over k} e^{ {-k \over 2} x^2 } \right]_0^M + {1 \over k} \int_0^\infty e^{ {-k \over 2} x^2 } dx \right) = \sigma^2 \tag{18}$$

Simplifying it further, 

$$\lim_{M \to \infty} \left[ {-x \over k} e^{ {-k \over 2} x^2 } \right]_0^M = 0 \tag{19}$$

Now consider the second part of the integral in (18),

Let \\(k_1 = {k \over 2}\\), and \\(u = x \sqrt{k}\\) which means \\(du = dx \sqrt{k} \\), and using gaussian integral.

$$ \int_0^\infty e^{ -k_1 x^2 } dx = {1 \over 2\sqrt{k_1}} \int_{-\infty}^\infty e^{-u^2} du =  { \sqrt{\pi} \over 2\sqrt{k_1} } = { \sqrt{2 \pi} \over 2\sqrt{k} } \tag{20}$$ 

Substituting (19) and (20) in (18),

$$ 2 \sqrt{ \frac {k} {2 \pi} } \cdot {1 \over k} \cdot  { \sqrt{2 \pi} \over 2\sqrt{k} } = {1 \over k} = \sigma^2 $$

So, 

$$ k = {1 \over \sigma^2} \tag{21}$$


Substituting A and k from (13) and (21) in the basic equation,

$$p(x) = {1 \over {\sigma \sqrt{2 \pi } } } e^{- {1 \over 2} \left( {x \over \sigma} \right)^2 }$$

The general equation for the normal distribution with mean \\(\mu\\) and standard deviation \\(\sigma\\) is a simple horizontal shift of this basic distribution,


$$p(x) = {1 \over {\sigma \sqrt{2 \pi } } } e^{- {1 \over 2} \left( {x - \mu \over \sigma} \right)^2 }$$


## REFERENCES:

<small>[The Normal Distribution: A derivation from basic principles](http://courses.ncssm.edu/math/Talks/PDFS/normal.pdf){:target="_blank"}</small><br>
<small>[Derivation of univariate normal distribution](http://www.planetmathematics.com/DerNorm.pdf){:target="_blank"}</small>

