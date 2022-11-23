---
layout: post
title: Bayes Rule
date: 2021-07-04 07:05:20 +0900
description: You’ll find this post in your `_posts` directory. Go ahead and edit it and re-build the site to see your changes. # Add post description (optional)
# img: back_1.jpg # Add image post (optional)
tags: [Blog, Math]
author: # Add name author (optional)
usemathjax: true
---

<p>
Hello. In todays post we will go through one of the most important topic in machinle learning and mathematics which is Bayes 
rule. We will see its derivation mainly using some math so before reading make sure you have some knowledge about probability 
theorem. 
</p>

Initially lets assume that we have two kinds of data available ( we will learn the Bayes rule using  basic robot module):
1. z sensor information (observation)
2. u actions.
<p>
Firstly lets consider only the first input data which is z sensor observation. Basically, we have to find state estimation 
given sensor observation z P(x|z). We cannot measure this directly so lets try to simplify it so that we can calcualte it. 
From conditional probability we know that P(A and B) = P(A|B) * P(B) = P(B|A) * P(A). So Bayes rule can be directly obtained 
from conditional probability which then becomes:
</p>
<p>
$$ P(A|B)= \frac{P(B|A)P(A)}{P(B)} $$
</p>

<mark>
This is too easy right  ?
</mark>

<p>
If we apply this rule to our case where we have to find likelihood of state x given sensor information z 
we will get this : 
</p>
<p>
$$ P(x|z)= \frac{P(z|x)P(x)}{P(z)} $$
</p>

Lets imagine that we have a sensor and we have to find the probability of it producing some z output. 
Yes, it is almost impossible. So, usually find it with some workaround using law of total probability:

<p>
  $$ P(A)=\sum_{n} P(A \land B_n) $$
  $$ P(A)=\sum_{n} P(A|B_n) P(B_n) $$
</p>

Now, lets apply this to our equation:
<p>
  $$ P(x|z)= \frac{P(z|x)P(x)}{\sum_{n} P(z|x_n) P(x_n)} $$
</p>


If we have some backround knowledge y we can incorporte that into Bayes formula (assuming y and x is not independent from each other):
<p>
  $$P(x,y|z) =P((x|z)\land (y|z)) = P(x|y,z)p(y|z)$$
  $$P(x,y|z) =P((x|z)\land (y|z))= P(y|x,z)p(x|z)$$

  $$ P(x|y, z)= \frac{P(y|x,z)P(x|z)}{P(y|z)} $$
</p>


<h2> Bayes rule for multiple prior observations </h2>
If we need to estimate the likelyhood of the current estimate given multiple prior observations, 
the basic view of the bayes formula becomes like this:
<p>
$$ P(x|z_1, z_2 ... z_n)= \frac{P(z_n|x,z_1,z_2 .. z_{n-1})P(x|z_1,z_2 ... z_{n-1})}{P(z_n|z_1, z_2 .. z_{n-1})} $$
</p>

Now lets simplify the equation as it is now very obstruse. To do that we will adopt Markov assumption which indicates : 
1. Current state only depends on previous estimate and current action.
2. Current observation only depends on current estimate.

Based on 1st part of Markov assumption we can simplify the above equation to this:
<p>
$$ P(x|z_1, z_2 ... z_n)= \frac{P(z_n|x)P(x|z_1,z_2 ... z_{n-1})}{P(z_n|z_1, z_2 .. z_{n-1})} $$
</p>

Now lets replace the denominator with some $$\eta$$ variable so that we will compute it later assuming that all the
probabilities of the state x given sensor observations $$z_1 .. z_n$$ should sum up to 1.

<p>
  $$ P(x|z_1, z_2 ... z_n)= \eta P(z_n|x)P(x|z_1,z_2 ... z_{n-1}) $$
</p>

Now pay attention to the last term of the equation above it is the same equation we have to find but without last sensor observation. Lets apply the bayes filter again:


<p>
  $$ P(x|z_1, z_2 ... z_n)= \eta _{1:2}  P(z_n|x)P(z_{n-1}|x)P(x|z_1,z_2 ... z_{n-2})$$
</p>


As you can see it has recursive characteristic,that is why it is called <b> recursive Bayesian estimation. </b>

We can now write it with more general term by using product term:

<p>
  $$ P(x|z_1, z_2 ... z_n)= \eta _{1:n} (\prod_{i=1,...,n} P(z_n|x)) P(x)$$
</p>