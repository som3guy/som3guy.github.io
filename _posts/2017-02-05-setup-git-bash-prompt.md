---
layout: post
section-type: post
title: Setup git bash prompt on Mac
category: devops
tags: [ 'git', 'mac' ]
---


Here is the git [repo](https://github.com/magicmonty/bash-git-prompt) and readme

Basically you can install it any number of ways however, I find simply using git easy.

{% highlight shell %}
cd ~
git clone https://github.com/magicmonty/bash-git-prompt.git .bash-git-prompt --depth=1
{% endhighlight %}
<br>

Add to the `~/.bashrc`:
{% highlight shell %}
  GIT_PROMPT_ONLY_IN_REPO=1
  source ~/.bash-git-prompt/gitprompt.sh
{% endhighlight %}

This will get you basically setup.

There are many more configs [here](https://github.com/magicmonty/bash-git-prompt#all-configs-for-bashrc).
