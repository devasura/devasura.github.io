---
layout: page
title: Web Form
permalink: /notes/gcp/gae-clock-04.html
---
* HTML template to Set Preferences `prefs.html` using `FORM` element with `get`
method.
{% highlight html %}
{% raw %}
<html>
<head>
  <title>
    Preferences
  </title>
</head>
<body>
  <p>
    <a href="/">Home</a>
  </p>
  <p>
    Preferences of {{ user.email() }}:
  </p>
  <p>
  <form action="prefs" method="get">
    Timezone Offset:
    <input type="text" name="tz_offset" value="{{ tz_offset }}">
    <input type="submit" value="Submit">
  </form>
  </p>
</body>
</html>
{% endraw %}
{% endhighlight %}

* RequestHandler to handle  `prefs` request:
{% highlight python %}
class PrefsHandler(webapp2.RequestHandler):
        def get(self):
            tz_offset = self.request.get('tz_offset')
            if not tz_offset:
                tz_offset = 0
            user = users.get_current_user()
            if not user:
                self.redirect('/')
                return
            else:
                jinja2_template = jinja2_env.get_template('prefs.html')
                context = {
                        'user':user,
                        'tz_offset':tz_offset
                }
                self.response.out.write(jinja2_template.render(context))


application = webapp2.WSGIApplication([('/', MainPage),
                                        ('/prefs', PrefsHandler)],
                                        debug=True)
{% endhighlight %}
