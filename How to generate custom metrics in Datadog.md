# How to generate custom metrics in Datadog

## Introduction

Hi all,

Datadog is a monitoring service for cloud applications, which provides monitoring of servers, databases, tools and services, through a data analysis platform based on "Software as a Service".

## Prerequisites

Being on the team project, prior knowledge of DD

## Directions

Currently, all Fury instances have a container with the Datadog agent integrated, dedicated to collecting instance metrics (including those of the application container) and sending packets using the UDP protocol.

Thanks to this, it is possible to send custom metrics using the agent from the application container, using the agent libraries integrated in all the toolkits of the technologies supported in Fury: https://github.com/mercadolibre/fury_meli-toolkits

An example of this in python would be (Reference: https://docs.datadoghq.com/guides/metrics):
Remember to install the lib first: pip install datadog
With this in your code, you can do as follows:

```python
from datadog import statsd
 
def render_page():
    """ Render a web page. """
    statsd.increment('web.page_views')
    return 'Hello World!'
    
```
Once the metrics are being sent, from Datadog, we go to New Monitor :
![1](https://user-images.githubusercontent.com/81833300/161585432-1fcce757-00ce-4b74-b917-3e4491bd85c3.png)

And our metric should appear in the following list:
![2](https://user-images.githubusercontent.com/81833300/161585505-354dc785-54c3-4d77-9902-ac89b5e0b3e6.png)

Then, we can save the monitor and integrate it into our dashboard, it is also possible to configure alerts from the “Alerts” section in Fury, setting our custom monitor id that we have created!

For more information, we can consult the official DataDog documentation: 
[here](https://docs.datadoghq.com/metrics/custom_metrics/)

   
