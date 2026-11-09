# Chapter 11

# Posting and Listening
for Notifications

There are so many things that you need to keep track of in your life. It wouldn’t be practical for you to stop and check on the progress of all of them every few minutes or even once a day. For most of them, you just want to know when something has changed.

Maybe you want an alert when a stock hits a certain price. Maybe the alert should go to a broker instead with a specific set of instructions. How might you set this up?

You would have to arrange with the notification center that you are interested in knowing about a specific event. In our case, it is something like “Tell me when XXX drops to yyy.” You have to tell the notification center who it should notify. Should it send the notification to you or to some agent?

Now whether the message comes to me or to someone else, we need to figure out what to do about it quickly. We get lots of notifications in a day. It’s easier to parse them and figure out what to do next if the context is clear to us. In code this happens by telling the notification center what message to send us. The message might be buy or sell. In other words, we are telling the notification center the action it will be sending for the target we’ve already set.

The notification center will then send our target a notification as part of the message. In code, this means that a notification object is the parameter of the message. The notification will contain information that the recipient might need. You’ll always find the name of the notification