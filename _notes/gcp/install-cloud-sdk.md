---
layout: page
title: Install Clould SDK
permalink: /notes/gcp/install-cloud-sdk.html
---
{% highlight bash %}
$ cd directory-where-you-want-Cloud-SDK-installed
$ curl https://sdk.cloud.google.com | bash
{% endhighlight %}
This downloads the Cloud SDK archive, unpacks it, and runs an interactive
installation routine. Alternatively you can download the Clould SDK archive
manually and run the installation routine `./google-cloud-sdk/install.sh`

* Close and reopen `bash` shell so that newly set environmental variables are
available to you. Test the installation by running `gcloud -h`

* Authenticating Cloud SDK to access cloud services
{% highlight bash %}
$ gcloud auth login #opens browser for Google authentication
$ gcloud auth list #you can sign into multiple accounts
$ gcloud config set account your.email@gmail.com #switching between accounts
$ gcloud auth revoke
{% endhighlight %}

* Cloud SDK Components
{% highlight bash %}
$ gcloud components list
$ gcloud components update
{% endhighlight %}

* Install App Engine SDK
{% highlight bash %}
$ gcloud components install app-engine-python
dev_appserver.py --help #check appengine
{% endhighlight %}
