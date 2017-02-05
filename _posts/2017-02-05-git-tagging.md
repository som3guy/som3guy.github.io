---
layout: post
section-type: post
title: Tagging with git
category: devops
tags: [ 'git' ]
---

#### Create tags with git

Git checkout the commit you want to tag. 
{% highlight shell %} 
git checkout f2a019f
{% endhighlight %}  
<br>

#### Create the tag
{% highlight shell %}
git tag -a <environment>-<year>.<month>.<day>.<number of tags this day>
git tag -a prod-2017.02.05.1
{% endhighlight %}
<br>

#### Push these changes

{% highlight shell %}
git push origin prod-2017.02.05.1
{% endhighlight %}
<br>

#### Then you can push to a specific branch if desired:

{% highlight shell %}
git push origin HEAD:prod  (pushes latest tag to prod branch)
git push origin HEAD:nonprod (pushes latest tag to nonprod branch)
{% endhighlight %}
<br>
