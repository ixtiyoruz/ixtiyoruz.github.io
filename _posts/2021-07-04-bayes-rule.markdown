---
layout: post
title:  "Bayes Rule"
date:   2021-08-04 11:55:28 +0900
author: ikhtiyor
---

<h1> Bayes Rule </h1>
<p>
Hello. In todays post we will go through one of the most important topic in machinle learning and mathematics which is Bayes rule. We will see its derivation mainly using some math so before reading make sure you have some knowledge about probability theorem. 
</p>

Initially lets assume that we have two kinds of data available ( we will learn the Bayes rule using  basic robot module):
1. z sensor information (observation)
2. u actions.

Firstly lets consider only the first input data which is z sensor observation. Basically, we have to find state estimation given sensor observation z P(x|z). We cannot measure this directly so lets try to simplify it so that we can calcualte it. From conditional probability we know that P(A and B) = P(A|B) * P(B) = P(B|A) * P(A). So Bayes rule can be directly obtained from conditional probability which then becomes:
