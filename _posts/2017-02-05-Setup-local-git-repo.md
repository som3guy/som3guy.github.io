---
layout: post
section-type: post
title: Setting up a local git repo
category: devops
tags: [ 'git' ]
---

#### Fork repo to your github repo 

{% highlight shell %}
git clone <local repo>
cd <cloned repo>
{% endhighlight %}
<br>

#### Add upsteam repo to pull updates from

{% highlight shell %}
git remote add upstream <original repo>
{% endhighlight %}
<br>

#### Pull down attached branches

{% highlight shell %}
git remote update -p
{% endhighlight %}
<br>

#### Create a new branch to work in.
Usually you will name this after a feature you are working on.
{% highlight shell %}
git checkout -b <new branch>
{% endhighlight %}
<br>

#### Commit your changes to your github repo
{% highlight shell %}
git add .
git commit -m ‘<message>'
git push origin < your branch>
{% endhighlight %}
<br>

#### Then you can login to github and create a pull request to the original repo
* Create a PR from fork/branch to original repo/master



