---
layout: page
title: User Authentication
permalink: /notes/gcp/gae-clock-03.html
---
* [User Authentication Options](https://cloud.google.com/appengine/docs/python/oauth/):
  * *Firebase Authentication*: Provides multiple user authentication options
    including with Google, Facebook, Twitter etc
  * *OAuth 2.0 and OpenID Connect*: If you want to build things from ground up
  * *App Engine's built-in Users API*: to authenticate Google accouts only.

{% highlight python %}
from google.appengine.api import users

user = users.get_current_user()

login_url = users.create_login_url(self.request.path)
logout_url = users.create_logout_url(self.request.path)

context = {
        'current_time':current_time,
        'user':user,
        'login_url':login_url,
        'logout_url':logout_url
}
{% endhighlight %}

* HTML template to use user infomation
{% highlight html %}
{% raw %}
{% if user %}
<p>
  Welcome, {{ user.email() }}!
  You can <a href="{{ logout_url }}"> sign out </a>
</p>
{% else %}
<p>
  Welcome!
  <a href="{{ login_url }}"> sign in or register </a> to customize
</p>
{% endif %}
{% endraw %}
{% endhighlight %}
