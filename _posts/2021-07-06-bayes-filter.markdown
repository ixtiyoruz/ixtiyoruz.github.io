---
layout: post
title: Bayes Filter
date: 2021-07-06 07:07:20 +0900
description: This post explains Bayes Filter. # Add post description (optional)
# img: back_1.jpg
tags: [Blog, Math]
author: # Add name author (optional)
usemathjax: true
---


Hello. Today, we will see , another very basic and profound integral part of machine learning and statistics, Bayes filter. It is mainly derived from bayes rule and its' basic objective is to find out the likelihood/estimation of current state given all the actions and observations up to now. 
$$ p(x_t|z_{1:t}, u_{1:t}) $$
Usually, state estimation is called belief, so we introduce new term :
$$bel(x_t) = p(x_t|z_{1:t}, u_{1:t}) $$

We will apply Bayes rule to simplify this term as it is almost impossible to directly obtain current state from actions and observations up to now.
1. Initially, i will separate $$z_t$$ from $$z_{1:t}$$ so that we can condition on it later.
    <p>
    $$bel(x_t) = p(x_t|z_t, z_{1:t-1}, u_{1:t}) $$
    </p>

2. Then, we will find probability of xt given all the actions up to now and all the observations exept the current observation given current observation using bayes rule. (I know it is little hard to stomach)

    <p>
    $$bel(x_t) = p((x_t| z_{1:t-1}, u_{1:t}) | z_t) $$
    </p>

3. __After applying the Bayes theorem we will get the equation below. Here η denotes p(z). In Bayes theorem, as you may remember, we changed it so that  remaining part should sum up to one after multiplying with this η value.__
   
    <p>
    $$bel(x_t) = \eta p(z_t | x_t, z_{1:t-1}, u_{1:t})p(x_t | z_{1:t-1}, u_{1:t}) $$
    </p>
Now it is time to use Markov assumption which indicates current observation only depends on current state. So the first part of the equation above becomes shorter and simpler :
<p>
$$bel(x_t) = \eta p(z_t | x_t) p(x_t | z_{1:t-1}, u_{1:t}) $$
</p>

The equation is still very hard to obtain directly so we will introduce new variable $$xt-1$$ using law of total probability. 
<p>

$$ P(A)=\int P(A \land B_n) d(B_n) = \int P(A | B_n)P(B_N) d(B_n)$$
$$ p(x_t | z_{1:t-1}, u_{1:t}) = \int P(x_t \land x_{t-1}|z_{1:t-1}, u_{1:t}) d(x_{t-1}) = \int P(x_t | x_{t-1}, z_{1:t-1}, u_{1:t}) P(x_{t-1}|z_{1:t-1}, u_{1:t}) d(x_{t-1})$$
</p>

Then our equation for belief changes to
<p>
$$bel(x_t) = \eta p(z_t | x_t) \int P(x_t | x_{t-1}, z_{1:t-1}, u_{1:t}) P(x_{t-1}|z_{1:t-1}, u_{1:t}) d(x_{t-1})$$
</p>
We again apply Markov assumption to the first part of the integral. (Current state only depends on current action and previous estimate so we can get rid of $$z_{1:t-1}$$ and $$u_{1:t-1}$$.)

<p>
$$bel(x_t) = \eta p(z_t | x_t) \int P(x_t | x_{t-1}, u_t) P(x_{t-1}|z_{1:t-1}, u_{1:t}) d(x_{t-1})$$
</p>

If you look at the second term of the integral above, you may notice that it is the same as previous estimate/ belief $$bel(x_{t-1})$$ but with one extra condition which is current action $$u_t$$. According to the Markov assumption , again, current state does not depend on future action so we can get rid of it.

So, final Bayes filter equation then becomes like this. 

<p>
$$bel(x_t) = \eta p(z_t | x_t) \int P(x_t | x_{t-1}, u_t) bel(x_{t-1}) d(x_{t-1})$$
</p>


This is also called Bayes Filter framework.All the other filters derived from it --- Kalman filter, Extended Kalman filter ,  Particle filter and so on.


