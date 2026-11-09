But as you'll notice from the shopping application example, we can still express the necessary security policy in terms of the sets of data that are manipulated by the object and by the operations that can be performed on that data.

# ## 17.2 Basic Security

At its most basic, security consists of two parts: defining a security policy and using authentication and checks to implement code that enforces that policy. The policy defines exactly who is allowed to do what; authentication gives us a way of identifying users so we can grant them access to the things they're allowed to do, and checks allow us to refuse them access to the things they're not allowed to do.

In this section, we'll take a look at how to define a basic security policy and how to implement that policy using App Engine facilities by working through an example: we'll add an administration facility to our chat application and define a security policy controlling who is allowed to use it.

# ### Adding Administration to Chat

For a simple example of basic security, let's go back to our chat application. In our original chat application, the set of available chats was fixed. When the application ran for the first time, it automatically initialized a small list of chats, and that was all the chats that were ever allowed. In order to change that list, we would need to change the source code of the chat application.

Instead, we would like to be able to create new chats on the fly. But we don't want any user to be able to just create chats willy-nilly; we'd like some control over who can and who can't.

So what we'll do is define a policy, which describes the set of basic resources and operations that make sense for our application. Then we'll look at how to implement those policies in App Engine.

In our security policy, there are three kinds of objects: chat rooms, chat messages, and users. We'll define our security policy around just two of them: users and chat rooms. Individual chat messages will be controlled by the chat rooms they belong to. The actual security will be provided by controlling the rooms.