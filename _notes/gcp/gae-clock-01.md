---
layout: page
title: Simple Clock Application
permalink: /notes/gcp/gae-clock-01.html
---
* This Clock Application will display the current time of the day.
* The simplest python application has just 2 files:
  * A configuration file name app.yaml
  * A file with python code for request handlers
* app.yaml
{% highlight yaml %}
application: devasura-clock
version: 1
runtime: python27
api_version: 1
threadsafe: yes
handlers:
- url: .*
  script: main.application
libraries:
- name: webapp2
  version: latest
{% endhighlight %}

* main.py which contains the python handler
{% highlight python %}
import datetime
import webapp2

class MainPage(webapp2.RequestHandler):
    def get(self):
        message = '<p>The time is: %s</p>' % datetime.datetime.now()
        self.response.out.write(message)

application = webapp2.WSGIApplication([('/', MainPage)],
                                      debug=True)
{% endhighlight %}

* GAE (in app.yaml) can be configured to route differnet URLs to different WSGI complaint objects
{% highlight yaml %}
handlers:
- url: /
  script: main.application
- url: /time
    script: main.time
- url: .*
    script: main.notFound
{% endhighlight %}

* WSGIApplication object can also be configured to route variouls URLs to different `RequestHandler` objects
{% highlight python %}
application = webapp2.WSGIApplication([('/', MainPage),
                                      ('/time', Time),
                                      ('.*', notFound)],
                                      debug=True)
{% endhighlight %}
