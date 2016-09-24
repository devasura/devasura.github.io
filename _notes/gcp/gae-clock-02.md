---
layout: page
title: Jinja2 template engine
permalink: /notes/gcp/gae-clock-02.html
---
* `jinja2` takes a HTML template and populates dynamic data to render the result
* `time.html` a simple HTML template
{% highlight html %}
{% raw %}
<html>
  <head>
    <title>
      Time
    </title>
  </head>
  <body>
    <p> The current time in UTC is: {{ current_time }}</p>
  </body>
</html>
{% endraw %}
{% endhighlight %}

* to use the templating system:
{% highlight python %}
import jinja2
import os
jinja2_env = jinja2.Environment(
              loader=jinja2.FileSystemLoader(os.getcwd()) )
jinja2_template = jinja2_env.get_template('home.html')
context = {
        'current_time':current_time
}
self.response.out.write(jinja2_template.render(context))
{% endhighlight %}

* Jinja2 Environment object can be stored as a global variable because we only
need to create this object once in the lifetime of the application instance,
and the object stays resident in memory.
* As we have set `threadsafe: true` in `app.yaml` the App Engine uses one
instance to process multiple requests simultaneously. So these requests will
share global variables. So if you want to use global variable they better be
read-only.
