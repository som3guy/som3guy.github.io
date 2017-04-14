---
layout: post
section-type: post
title: Installing motionEyeOS on Raspberry Pi Zero W
category: linux
tags: [ 'linux', 'raspberry pi', 'motioneyeos' ]
---


### What you need:  


<ul style="text-align:left;">
<li>Raspberry Pi Zero W</li>
<li>Power cord</li>
<li>owered USB hub (Might be able to use non-powered)</li>
<li>USB to micro USB for Keyboard</li>
<li>USB to Ethernet</li>
<li>MicroSD Card</li>
</ul>

### What to do:

#### Load the right image

Go to the release page and get an image from at least [20170326](https://github.com/ccrisan/motioneyeos/releases/tag/20170326) or later.  
Download the image for the `Rasberry Pi`  
Load that image on to your MicroSD Card.  [More Info](https://github.com/ccrisan/motioneyeos/wiki/Installation)

#### Plug in all the things.

Hook up your ethernet to you USB hub  
Hook up your keyboard to your USB hub  
Plug in your USB hub to your RPiZW using the USB to micro USB  
Insert your MicroSD Card in to the Pi.  
Plug in your power cord and let it initialize.  

#### Make some changes to enable wifi

Log in as root with no password    
Run these commands:  
{% highlight shell %}
mount -o remount,rw /
mount -o remount,rw /boot
{% endhighlight %}
<br>
Edit this file:
{% highlight shell %}
vi /data/etc/wpa_supplicant.conf
{% endhighlight %}
<br>
With this data:
{% highlight shell %}
update_config=1
ctrl_interface=/var/run/wpa_supplicant

network={
    scan_ssid=1
    psk="<WiFi Password>"
    ssid="<WiFi SSID>"
}{% endhighlight %}
<br>
Now edit this file:
{% highlight shell %}
vi /data/etc/static_ip.conf
{% endhighlight %}
<br>
With this data:
{% highlight shell %}
static_ip="192.168.0.3/24"
static_gw="192.168.0.1"
static_dns="8.8.8.8"
{% endhighlight %}
<br>

#### Finish up

You can now reboot by typing `reboot` or unpluging your Pi and plugging it back in.  
As it is rebooting you can unplug the ethernet cable from you hub.  
You should see it start up and connect to your WiFi connection.

You can then go to the IP address in your web browser that you set in yor `static_ip.conf` file.  
The default login should be `admin` with no password.

For further configuration please visit the motionEyeOS [Wiki](https://github.com/ccrisan/motioneyeos/wiki)
<br>
