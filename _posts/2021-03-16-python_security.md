---
title: "Be cautious when installing external libraries"
categories:
  - Blog
tags:
  - Python
---
## TL;DR

PyPI does not guarantee package security. Make sure to check out its github for signs of activity and get the spelling right. 

## External libraries and security
Coders don’t like reinventing the wheel. We like to rely on great projects developed by our peers. However, working with external code poses a security risk because it may make your system vulnerable to malicious attacks intentionally or intentionally. This latter was rather the motive for creating those 4,000 packages that were subsequently published  to PyPI and later discovered that they contain malicious code. Read more on the [nakedsecruity](https://nakedsecurity.sophos.com/2021/03/07/poison-packages-supply-chain-risks-user-hits-python-community-with-4000-fake-modules/).

I need to admit that it took quite a while for me to actually to actually take this topic seriously.
Before that, I had just installed whatever package I found to be useful based on its documentation or
an interesting blogpost. Of course, later on, especially after starting my first tech job, I started
paying more attention to security and what packages I used in my Python projects. 

Still, my first encounter with strict company security policy on one of our projects caught me by surprise. Before deploying the software, it turned out that the No. 1 Python data analysis tool, Pandas, is not accepted by the customer's IT. Now let's not concentrate on why this only happened at a late stage (and the hustle I went through rewriting all the code in numpy) but rather on the fact that a major package could have not been deployed due to security concerns.*

## My checklist

I think the PyPI incident and my little anecdote clearly highlights why you should double check whether the package you about to install can be truly trusted. Here is my checklist:

1. Active development: go on the project's Github and check the history and the README whether the package is under development. It is a good sign if it is. 
1. Active maintenance: check the project’s bug tracking system to see how quickly the maintainers respond to bugs. It is a good sign if there are discussions on the submitted bugs.
1. Check package spelling: one of the tricks applied during these attacks is _typo-squatting_ which is naming malicious packages similar to popular packages like _beautifulsoup4_ and _beatufulsoup4_ or _dateutil_ and _python3-dateutil_. 

And don't forget to ask for your customer's list of approved packages and other security policies in advance. :)

*This does not mean that Pandas is not secure to use. Company IT departments may have other reasons to have a limited number of approved packages like not enough resources to run security screens.
