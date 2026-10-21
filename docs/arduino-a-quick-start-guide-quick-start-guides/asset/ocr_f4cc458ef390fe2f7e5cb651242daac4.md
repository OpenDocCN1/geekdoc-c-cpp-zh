# Web Services for Publishing Sensor Data

With the advent of cheap open source hardware and sensors, web services for publishing sensor data have become popular over the past few years. Such services allow you to publish, read, and analyze sensor data. People from all over the world publish data from their weather stations, environmental sensors, and so on, and make it available for free on the Internet.

The most popular services are Pachube* and Sensorpedia.† In principle, they all work the same: you register an account, and you get back an API key. Then you can use this key to authenticate against the service and upload sensor data.

*. http://pachube.com
†. http://sensorpedia.com/

# 8.3 Registering an Application with Twitter

Before we start coding, we have to register our application at the Twitter website to get an OAuth access token.² OAuth is an authentication scheme that allows applications to use other applications’ resources. In our case, we’ll grant our very own application the right to update our Twitter feed without using our Twitter username and password.

For a long time, Twitter supported HTTP Basic Authentication.³ Automatic services only needed a username and password to request or update Twitter feeds. But as of August 2010, Twitter has removed support for Basic Authentication and now uses OAuth.

To get the OAuth access token, register your new application in the developer section of the Twitter website.⁴ After you’ve logged in, click the “Register an app” link, and fill out the form you see in Figure 8.3, on the next page. Make sure you set the application type to Client and the default access type to Read & Write. You can set the application name to an arbitrary string, and it will appear on your Twitter channel whenever you use the application to tweet messages. If you set it to RescueMeFromWork, for example, your tweets will be published via RescueMeFromWork.

2. http://en.wikipedia.org/wiki/Oauth
3. http://en.wikipedia.org/wiki/Basic_authentication
4. http://dev.twitter.com