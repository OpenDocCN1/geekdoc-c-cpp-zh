# Chapter 18

# # Administering Your App Engine Deployment

So far, we've focused almost exclusively on how to write Google App Engine applications. That's because the hardest part of working with App Engine is actually implementing the applications. Once you've got your application working, it's really easy to administer it.

But you *do* need to administer your App Engine services and applications. It's easy, but it is a job that needs doing on an ongoing basis. In this chapter, we'll take a quick look at the tools that are available to you via the App Engine control panel. We'll see how you can do things like monitor the amount of resources you're using, how you can scan the data being stored by your application to identify problems, and how to see who is using your application from where.

# ## 18.1 Monitoring

Monitoring your application just means seeing how it's being used and what kinds of resources it's using. App Engine makes it really easy for you to see exactly what's happening with your application. If you go to [http://appengine.google.com](http://appengine.google.com) and sign in, you'll get a list of the applications that you've deployed. You can look at any of your applications by clicking on their names.

When you click on one of the applications, you'll be brought to the main App Engine control panel for that application, with a view showing you the *dashboard* for your application. The *dashboard* give you a concise overview of the data you probably care about. You can see an example