---
layout: post
section-type: post
title: Squashing git commits
category: devops
tags: [ 'git' ]
---

#### Check the log to see how many commit you want to squash
{% highlight shell %}
git log
or
git log --oneline --graph --decorate --all
{% endhighlight %}
<br>
#### Rebase the amount of commits you want to squash

{% highlight shell %}
git rebase -i HEAD~<number of commits to squash>
git rebase -i HEAD~5
{% endhighlight %}

This will prompt you to pick commits.  
You can use pick and squash or fixup for the rest.  
(Squash will open an editor where you can rename your commit.)  

#### Force push your squashed commit

{% highlight shell %}
git push -f <remote> <branch>
git push -f origin master
{% endhighlight %}
<br>
