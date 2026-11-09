# # Creating Protocols for Delegation

Notifications are great when more than one object might need to be told about a change or when you might not know ahead of time which object(s) might be interested in being notified. For example, the application we wrote in the previous chapter is listening for notifications that the NSWorkspace sends out. That’s a great use of notifications in our application.

On the other hand, the communication between our model and our controller is not a very good use of notifications.¹ The CurrentApp object’s applicationDidLaunch: and applicationDidTerminate: methods each do little more than call methods of essentially the same name in the ApplicationController object. This is being accomplished in a roundabout way right now. The CurrentApp methods are posting notifications that the ApplicationController has registered to observe. We’d be better off using a delegate instead of notifications.

You’ve used protocols and delegates before. In this chapter, we will create our own protocol and add it to the controller’s header file. We’ll make the controller the delegate for our model. Then comes the tricky part. The model will turn around and call the delegate methods if they exist.

1. If it’s not a good use of notifications, then why did I show it to you? I used notifications in this way so that I could show you how to generate your own notifications. My goal is to use this example to show you a range of useful techniques.