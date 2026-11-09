
and set up a domain using Google Apps and then have your App Engine programs run at that domain. At the moment, if you own a domain that isn’t run by Google Apps, you can’t use it for your App Engine services.

The Permissions view allows you to give administration privileges to other users. If you give administration privileges to another user, then they will be able to access the full control panel for your application, including the ability to change any settings, to modify the code, and to disable or even delete the application.

The Versions view shows you a list of the versions of your application that have been deployed and gives you the ability to choose any of them as the current, active version. The main use of this is in case of errors. If you deploy a new version of your application and it contains an error, you can instantly revert to any prior version by going to the Versions view and selecting the error-free prior version.

Finally, Admin Logs let you see what administrative actions have been performed on your application. This is mainly useful for letting you monitor the actions of other administrators: any action taken by any administrator will generate an entry in the admin logs.

### 18.5 Paying for What You Use

As I said at the beginning of this book, the basic point of cloud computing is to let you buy exactly the resources that you want to use. You don’t buy an entire computer and then let its CPU sit idle for most of the time in order to ensure that you’ll have enough CPU if you get slashdotted: you just buy what you need. The billing panel is where App Engine lets you tell Google how much you want to pay.

There’s a Billing Settings link on your control panel. If you follow it, it gives you the option of enabling billing. By default, you’re working with free resources—Google gives you your first hit for free—but if you want more than the minimum resources, you’ll need to pay for it.

With the billing controls, you can set up a daily budget. You can set a daily maximum—the most money you’re willing to pay for additional resources in a given day. You can also set per-resource maximums to say things like, “I’m willing to spend up to $4 per day on CPU but only $1.50 for bandwidth.”

Once you've set up your budget, you can set up a payment on your credit card using Google Checkout.

You can see exactly what resources you've been using and how much you've paid every day by looking in the billing history. There's a daily entry in the billing history in the same format as the log entries that tells you exactly how much of each resource you've consumed every day.

In this chapter, we've taken a quick look at the administration controls provided by the App Engine control panel for your application. Nothing here should be at all surprising: it's all very straightforward and easy to use.

## Wrapping Up

We've covered a lot of ground in the last 300 pages. At this point, you've become familiar with the basics of programming for Google App Engine. Of course, there's no way that we could cover everything in this amount of space, but now you are ready to build your first applications and work with the Google App Engine online documentation. In this chapter, we'll recap the basic concepts we've covered and give a quick overview of what else you might want to look at and where to go from here.

### 19.1 Cloud Concepts

As we've seen, cloud programming is very different from programming in more traditional environments. The key characteristics that make the cloud so interesting and powerful include these concepts:

- You don’t know—or care—where your program is running. This is one of the most fundamental facts of the cloud. You don't run your program on a computer: your cloud service provider gives you a platform—that is, a basic software system that can run programs written in a specific way—and all of the low-level details are their problem, not yours. In general, you don’t know what kind of computer it's running on or how many computers it's running on, where those computers are, or what operating systems they're running. None of that matters.
- Software is a service. In a traditional programming world, you implement applications that are executed on your customers' computers. In the cloud, you still write an application, but from the viewpoint of your customers, it’s not quite the same thing as a program because they don’t run it. In the cloud, your software is a service—an application that is running somewhere else, which they access through their web browser when they want to use it. The key difference is that the users don’t run the program: the program is always running. The users connect to it when they want to use it, and they don’t need to worry about how to run it, whether it needs to be upgraded, whether it works on their computer, or anything like that. The service is always there, ready to be accessed by any computer from anywhere.
- There are no limits. You don’t need to worry about limits and questions like, “How many page views can my computer handle?” In the cloud, everything is elastic. If you suddenly get more users, it’s not a problem: your cloud platform just grabs more resources as it needs them and continues to provide services to your customers.
- You pay for what you use. In the cloud, you literally pay for what you use. You don’t need to buy a big, powerful, expensive computer in case you eventually need it. If today you only need a single, rinky-dink processor and tomorrow you need something a thousand times more powerful, that’s no problem. Today you’ll pay a few cents for a single processor; tomorrow, you might pay a few dollars for some serious computing horsepower. Whatever you need, you pay for it as you need it, and when you’re done using it, you’re not stuck with a useless brick of overpowered hardware.

### 19.2 Google App Engine Concepts

As we’ve seen in this book, Google App Engine is built around a collection of basic concepts. To review, the fundamental concepts of programming for the cloud using Google App Engine include the following:

- Programming is HTTP request handling. In Google App Engine, your program’s job is to handle HTTP requests. Through the magic of webhooks, every interaction that your program has with users or with other applications, is implemented as an HTTP request handler.
- You can bootstrap from standards. In Google App Engine, everything tries to build on existing standard technologies when possible. So, for example, in Python, templates are built using the widely used Django template framework. In Java, the interface to the datastore is built in terms of the standard Java Data Objects framework. Throughout Google App Engine, we've seen that wherever possible, GAE uses existing standard technologies as their basis, rather than inventing new stuff.
- Everything is a service. All of the bits and pieces of GAE that you interact with in your program are services. Things that would be libraries to link against in a conventional program are services that you talk to through RPC requests in GAE cloud applications. And there's a wealth of services available to you, providing everything from security to data storage to instant messaging.
- The browser is the UI. Every bit of user interface, everything that your customers see, everything that your customers do, all happens inside of a web browser.
- There is no state. In a traditional program, you can count on variables to hold state—that is, if you put something into a variable, when you come back to look at it later, it will still be there. In a cloud environment, that’s not necessarily true. You have to program under the assumption that the only way to preserve state is through external storage in datastore.
- Always think about security. In a cloud application, security is much trickier than in a conventional application. Since your code is running as a service that can be accessed online by malicious people, and your customers’ data is all accessible by that online service, you must be extra careful that your system is built to be secure. From the very first step of designing your system, plan your security policy and make sure you enforce it in every facet of the design. All it takes is one mistake to compromise your users’ data!

These basic ideas make up the heart of Google App Engine. There's not that much to it. But that’s sort of the point. What makes App Engine such a beautiful, powerful system to work with is its basic simplicity. There’s just this modest set of concepts and libraries built around them—and that’s it. But this simple framework turns out to be a remarkable and elegant tool for building your own cloud applications.
