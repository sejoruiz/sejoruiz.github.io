---
layout: project
title:  "Personal Website"
date:   2014-09-28 16:54:46
author: Sergio Ruiz
categories:
- project
- network
- raspberrypi
tags:
- raspberry pi
- website
- network
- technology
- jekyll
- bootstrap
img: internet.jpg
thumb: internet.jpg
carousel:
- single01.jpg
- single02.jpg
- single03.jpg
images_root: website
website: http://sergioruiz.duckdns.org
---
## Table of Contents
{:.no_toc}
* TOC
{:toc}

<!--more-->

## 1. Introduction

One of the first projects I always wanted to accomplish was to build a personal website. Something where I could keep track of my projects, and also have my resume uploaded. One of the simplest ways of achieving this was simply registering at [Wordpress](http://www.wordpress.com), [Blogger](http://blogger.com) or other resources. These great tools provides a way of building a really professional looking website without even touching a single line of code. However, after thinking about what I really wanted, I decided to build my own page without using any [Content Management System](http://en.wikipedia.org/wiki/Content_management_system). 

[![Most popular Content Management Systems (CMS)]({{site.project_img}}{{page.images_root}}/cms.png)]({{site.project_img}}{{page.images_root}}/cms.png){:rel="prettyPhoto" title="Popular content management system"}

This way, I would be able to have full access to the server, and manage the website entirely by my own. Above all, I would be able to design some projects that could interact with the website. Here, I'll explain how I built the entire website. Or you can go directly to GitHub and [fork the code](#)

<br/>

## 2. Requirements.

For this little project we won't require much equipment. We will do fine as long as we have: 
- A computer with Linux (in my case, I'm going to use a Raspberry Pi): I recommend to use an old machine, or, as my case, a Raspberry Pi. Please keep in mind that if you choose a different platform, some of the commands might need to be changed. You'll do fine as long as you have Debian or derivates (Raspbian, Ubuntu, Mint etc.)
- Internet connection: We will have to download several packages through Internet. Plus, this is a web server, so I guess you already have this.
And that's it!


### 2.1. Introduction to the Raspberry Pi

As I have mentioned above, I wanted to host the website by myself. I needed a computer for that, and I bought the inexpensive, small and powerful Raspberry Pi B+. This little guy has an ARM processor that can run at 700MHz (without overclocking) and has 512 MB of RAM. 

[![Raspberry Pi Logo]({{site.project_img}}{{page.images_root}}/raspberry.png)]({{site.project_img}}{{page.images_root}}/raspberry.png){:rel="prettyPhoto" title="The Raspberry Pi logo"}

More than enough for a small website. The Raspberry Pi it's also a good starting point for new Linux users. There are tutorials for everything, and a lot of interesting projects out there. If you feel intrigued about this card-sized computer, you can go to [Raspberry Pi's website](http://www.raspberrypi.org) and read about it.

<br/>

## 3. Installing the software (I): Server software

First of all, I needed to set up the Raspberry. In my case, I had to install the operating system. In the Raspberry Pi, this was a piece of cake.  When the Raspberry is plugged for the first time, it will launch the installation of the system by itself. There is even a nice mouse driven menu that will guide you in the process. After initialy setting up the Raspberry Pi, I needed to turn it into a small web server. There are many software out there for web server. The most used one is [Apache](httpd://www.apache.org) but I needed something minimal. I decided to go with [Nginx](http://nginx.org).


[![A digital cloud]({{site.project_img}}{{page.images_root}}/cloud.jpg)]({{site.project_img}}{{page.images_root}}/cloud.jpg){:rel="prettyPhoto" title="A server will share your site with anybody who requests it"}


Nginx is a lightweight web server that has been proved to work amazingly well on Raspberry computers. You can install Nginx simply by typping in a terminal:

	sudo apt-get install nginx -y
	
After that you have to configure it. You need to edit the configuration file:

	sudo nano /etc/nginx/sites-available/default
	
You will find several settings, but you need to look where the line starting with root is. The path that follows is the folder where the website needs to be. In my case it says:

	root /var/www
	
That means that the website that will be served needs to be placed inside /var/www/. Finally, we can start Nginx:

	sudo service nginx restart
	
And if we go to [localhost](http://localhost) we will see something like this:

[![Nginx welcome page]({{site.project_img}}{{page.images_root}}/nginx.png)]({{site.project_img}}{{page.images_root}}/nginx.png){:rel="prettyPhoto" title="Nginx welcome page"}

I have to say, I also set up a database system (MySQL) and a couple of things more, but they are not really required for the website.
Finally, I set up a Dynamic DNS service. This allows the access of a website through a name (i.e. [http://sergioruiz.duckdns.org](http://sergioruiz.duckdns.org)) instead of through an IP address. I won't go into details, but basically the Dynamic DNS is a DNS for dynamic IP. It doesn't matter if your IP is assigned dynamically, you'll still be able to find your website using its address. I chose [DuckDNS](http://www.duckdns.org), but there are many other choices out there.

<br/>

## 4. Installing the software (II): The web framework

After installing all the server software, I started thinking about how to develop the website. After some research, I discovered [Jekyll](http://jekyllrb.com/). For those who don't know it, Jekyll is the framework that generates the [GitHub](http://www.github.com) pages. From their own website:

[![Jekyll logo]({{site.project_img}}{{page.images_root}}/jekyll.png)]({{site.project_img}}{{page.images_root}}/jekyll.png){:rel="prettyPhoto" title="Jekyll is a static site generator developed by Github"}

>Jekyll is a simple, blog-aware, static site generator. It takes a template directory containing raw text files in various formats, runs it through Markdown (or Textile) and Liquid converters, and spits out a complete, ready-to-publish static website suitable for serving with your favorite web server. Jekyll also happens to be the engine behind GitHub Pages, which means you can use Jekyll to host your project’s page, blog, or website from GitHub’s servers for free.

But then, what is the difference between Jekyll and a CMS like [Wordpress](http://www.wordpress.org) or [Joomla!](http://www.joomla.org)?. The main difference is that the website will be static. That means that it will be generated once, and then it will be served. With CMS, the website is generated when a user requests it. While for certain pages this can be a huge inconvenient, for a small website is an advantage. If the website is generated once, and then just served, the responsiness (how fast the page reacts to the user actions) is going to be highly increased . And if we have to put this website to work with a small computer like the Raspberry Pi... Well, I'll just say that with Wordpress, the page can be loading for more than 6 seconds. You don't want that.
Jekyll needs to install Ruby first:

	sudo apt-get install ruby -y
	
And then we can install Jekyll:

	gem update && gem install jekyll
	gem install rdiscount -s http://gemcutter.org
	
There we go, we have succesfully set up the Raspberry Pi as the web server, and we can start working with Jekyll. 

<br/>

## 5. The final product: The website

Finally, I had all the requirements for starting to develop the website. So it was time to start looking for templates and resources. There are millions of templates just a google search away. I've used [this one](https://github.com/st4ple/solid-jekyll) called Solid Jekyll. It's a gorgeous and colorful template created by [st4ple](https://github.com/st4ple) that uses [Bootstrap](https://www.getbootstrap.com).
