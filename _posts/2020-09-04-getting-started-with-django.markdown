---
layout: post
title:  Web Development with Django
date:   2020-09-04
categories: django python web development
---
# How do web applications work?
Here's a quick rundown of how web pages work. When you visit a website, your browser sends a
request to that site. The web server sees that request, processes it, and returns what the browser
requested. Pretty simple huh?

# What the heck is Django?
In layman terms, Django is a web framework written in python and it's actually pretty neato.
It allows a web developer to just focus on the meat of the project rather than worry about the
other hassles involved in web development (eg: cookies, security, etc.) There's a lot of good
documentation written around Django, so it's pretty rare to get completely stuck.

# How does a browser interact with Django?
Good question. Django is a web framework and NOT a web server. That basically means that a browser
won't be directly interacting with Django. You're going to need a web server, like NGINX, to handle
browser requests. Here's a simple flow of how things work:

`Browser -> Web Server -> WSGI -> Django`

So the browser sends a request to the web server. The web server takes that request and gives it to
WSGI (Web Server Gateway Interface) which then takes that request and hands it to Django. So, in
that case, why do we need WSGI? Why can't the web server just hand requests directly to Django? It's
because the web server doesn't know how. An example would be that the web server is like a
distribution center. It gets all types of packages from all over the world and sends it to a
local post office (WSGI). The post office then delivers that package to the end location (Django). 
It works in reverse too. Django will receive a request and then it will generate a response. It will
use WSGI to send that response to the web server which then sends it to the browser. Pretty neato
huh?

# How do we begin?
Go search for a tutorial. There's plenty of good resources that already exist and to write another
would be redundant. I'll mainly be explaining tips or problems I encountered and how I solved them.
