If you’re struggling with that answer, take a look back at our diagram:

![](bbox=[0.1, 0.09, 0.9, 0.54])

From this, we can see that we need to consult with the Account Manager to see if the userName exist. And once we validate that the user’s credentials are valid, we’ll need to inform the Session Manager that we have a logged on user.

This means that we cannot continue with the API code until we first develop both the Account Manager and Session Manager.

But, before the Account Manager can be coded, we’re going to need to have the Account Handler done otherwise we’ll have no Accounts.

# 28.6. Coding the Account Handler

The Account Handler’s job is to load Accounts from our file and to write a single Account to the file when we create a new User. That should be enough for what we’ll need in this application. We don’t really support deletion since this is just a learning application.

There is one thing else that we’ll need to do and that’s create the file with a Bootstrap Account. The first time we run our server, they will be NO Accounts. In that case, we’ll first need to create a file with a Bootstrap Account and then load that.