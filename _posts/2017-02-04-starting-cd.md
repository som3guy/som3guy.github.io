---
layout: post
section-type: post
title: Getting Started with Continuous Deployment
category: devops
tags: [ 'continuous delivery' ]
---

### Deciding on a pipeline

I chose to go with using Jenkins for code testing and Rundeck for deployment. There are a number of plugins for Jenkins to get you started quickly in setting up a quick continuous delivery platform.

Jenkins was an easy choice as it is open-source and I wanted to keep this project as cheap as possibly.

Here are the things I needed in my Continuous Delivery pipeline:

<ul style="text-align:left;">
<li>Automatically be able to test code once pushed to Github</li>
<li>Upload passing cookbook to my chef server</li>
<li>Send a notification to Rundeck to deploy my cookbooks.</li>
<li>Rundeck should be able to run chef-client on specific nodes based on what code was changed.</li>
</ul>

The did this using the pipeline plugins available in Jenkins. I setup all steps in freestyle projects in folders for each cookbook. I have 4 projects for each cookbook.

I will use my zabbix_agent cookbook as an example:

<ol style="text-align:left;">
<li>zabbix_agent_code_review</li>
<li>zabbix_agent_test</li>
<li>zabbix_agent_release</li>
<li>zabbix_agent_deploy</li>
</ol>

### zabbix_agent_code_review

This project specifies which GitHub URL to pull the cookbook from, the delivery pipeline configuration, will build when a new change is pushed to GitHub, polls GitHub at a specified interval, and executes shell commands `rubocop` and `foodcritic`

### zabbix_agent_test

This project specifies which GitHub URL to pull the cookbook from, the delivery pipeline configuration, builds when `zabbix_agent_code_review` has completed successfully, and executes shell commands `kitchen test`.

### zabbix_agent_release

This project specifies which GitHub URL to pull the cookbook from, the delivery pipeline configuration, builds when `zabbix_agent_test` has completed successfully, and executes shell commands:

{% highlight shell %}
cd /chef_jenkins/
rm -rf cookbooks/zabbix_agent
git clone https://github.com/som3guy/zabbix_agent.git cookbooks/zabbix_agent
knife cookbook upload zabbix_agent --force
rm -rf cookbooks/zabbix_agent
{% endhighlight %}

I had to create the directory `/chef_jenkins/` and give the `jenkins` user permissions to it.

### zabbix_agent_deploy

This project specifies the delivery pipeline configuration, builds when `zabbix_agent_release` has completed successfully, and notifies a post-build action Rundeck job which specifies the UUID from a job that is setup to run `chef-client -o 'recipe[zabbix_agent]'` on all nodes that have or should have `zabbix_agent` in their run list.

Finally, I have setup a view using the “Delivery Pipeline View” which begins with `zabbix_agent_code_review` and ends with `zabbix_agent_deploy`.

Here is a screen shot of the Delivery Pipeline View:

![zabbix pipeline]({{ site.url }}/assets/blogs/zabbix_agent_pipeline.png)
