---
layout: post
title: Bayes Rule
date: 2017-08-20 13:32:20 +0300
description: You’ll find this post in your `_posts` directory. Go ahead and edit it and re-build the site to see your changes. # Add post description (optional)
# img: post-6.jpg # Add image post (optional)
tags: [Blog, Meditation]
author: # Add name author (optional)
---

<p>
Hello. In todays post we will go through one of the most important topic in machinle learning and mathematics which is Bayes rule. We will see its derivation mainly using some math so before reading make sure you have some knowledge about probability theorem. 
</p>

Initially lets assume that we have two kinds of data available ( we will learn the Bayes rule using  basic robot module):
1. z sensor information (observation)
2. u actions.
<p>
Firstly lets consider only the first input data which is z sensor observation. Basically, we have to find state estimation given sensor observation z P(x|z). We cannot measure this directly so lets try to simplify it so that we can calcualte it. From conditional probability we know that P(A and B) = P(A|B) * P(B) = P(B|A) * P(A). So Bayes rule can be directly obtained from conditional probability which then becomes:
</p>


{% highlight ruby %}
def print_hi(name)
  puts "Hi, #{name}"
end
print_hi('Tom')
#=> prints 'Hi, Tom' to STDOUT.
{% endhighlight %}
