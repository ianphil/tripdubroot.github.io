---
layout: post
title: Getting Started with the Azure Python SDK
date: 2016-05-10 13:00:00 -0500
published: true
tags: Azure, Python
---

Python is something that interests me. Mostly it’s the allure of the data science libraries that are available. There are a lot of research institutions doing really sweet work and a lot of its completed using python. This should be interesting to you… it should make you question why that might be?

I’ve played with this language off and on over the years. I’ve never devoted serious brain cycles to understanding it better. Turns out this is exactly why Python is so popular… it’s easy to use, easy to read, and easy to learn.

With that in mind, playing with the various APIs in Azure is a good way to pass the time, so let us ask… What’s the state of Python in Azure? What can and can’t we do with it? …OK then let’s dig in and rock out on the cloud with Python.

 We’ll start out at the [Python Developers Center](https://azure.microsoft.com/en-us/develop/python/). Here you’ll find links to different tools, SDKs, and how-to guides. It’s a great place to get an introduction to Python and Azure, but for us… we want to go a bit deeper and explore the SDK. The Python SDK uses standard python practices and is provided as a pip package.

Since this does use pip and follows convention, we’ll head over to [readthedocs.io](http://azure-sdk-for-python.readthedocs.io/en/latest/) and start there. Here you’ll find the latest documentation for working with the Azure SDK for Python.

Let’s start with getting things setup. I’m going to assume you have Python installed… maybe I shouldn’t but I’m going to. If you don’t, check out the [Beginner’s Guide](https://wiki.python.org/moin/BeginnersGuide/Download). Getting the SDK down to your machine and ready for consumption is pretty simple, just run this command:

{% highlight bash %}
pip install --pre azure
{% endhighlight %}

Let’s talk about what you just did here. First “install” reads from PyPI index and looks for the package you specify. In this case the package in question is “azure”.  We’ve also stipulated we’d like the development version (pip by default only looks for stable packages), by throwing in the “—pre” flag.

We’re starting to rock out… 

Now that we have the Azure SDK for Python, let’s start using it. So, what would be the “hello world” be? I don’t know exactly, but for me… it was getting some basic info about a specific Azure subscription. Here’s the code:

{% highlight python %}

'''
    Python script that grabs Azure subscription information
    using username/password.
    
    @tripdubroot is to blame!
'''
import json

# Import Azure Credentials
from azure.common.credentials import UserPassCredentials

# Import Azure Subscription
from azure.mgmt.resource.subscriptions import SubscriptionClient, SubscriptionClientConfiguration
from azure.mgmt.resource.subscriptions.models import SubscriptionPaged, LocationPaged

# Read json file that contains SubID/Username/Password
with open("az_config.json") as data_file:
    data = json.load(data_file)

# Get auth token using OAuth
def get_credentials(config_data):
    return UserPassCredentials(
        config_data["username"],
        config_data["password"],
    )

credentials = get_credentials(data)
print "Creds have been delivered from:", credentials.cred_store

# Setup Subscription client
subscription_client = SubscriptionClient(
    SubscriptionClientConfiguration(
        credentials
    )
)

# Get subscription info using subscription id
subscription_info = subscription_client.subscriptions.get(data["subscription_id"])
print "The name of the current subscription is:", subscription_info.display_name

{% endhighlight %}

There is a bit of code here, but this is what matters. First, we have three from/import statements. Second, a function that returns user credentials. Lastly, a get call using the subscription client passing the subscription id as an argument. The output looks like this:

{% highlight bash %}

Creds have been delivered from: AzureAAD
The name of the current subscription is: BizSpark

{% endhighlight %}

That’s it! Till next time…
