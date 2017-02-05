---
layout: post
section-type: post
title: Unlock accounts in pam or faillock
category: linux
tags: [ 'linux', 'security' ]
---

### Using PAM  

#### Check the account for failed login attempts
{% highlight shell %}
pam_tally2 --user=<user>
{% endhighlight %}

#### Reset the account to 0 failed attempts
{% highlight shell %}
pam_tally2 --user=<user> --reset
{% endhighlight %}

#### Verify there are no failed attempts

{% highlight shell %}
pam_tally2 --user=<user>
{% endhighlight %}
<br>
### Using faillock

#### Check the account for failed login attempts
{% highlight shell %}
faillock --user <user name>
{% endhighlight %}

#### Reset the account to 0 failed attempts
{% highlight shell %}
faillock --user <user name> --reset
{% endhighlight %}

#### Verify there are no failed attempts

{% highlight shell %}
faillock --user <user name>
{% endhighlight %}
<br>
