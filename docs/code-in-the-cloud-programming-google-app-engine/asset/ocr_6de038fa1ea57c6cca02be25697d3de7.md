![](bbox=[0.12, 0.045, 0.895, 0.315])

Figure 3.2: The Chatroom app in action

You can see the result in Figure 3.2. It looks exactly like it did running on the local development server. I sent a few messages using two different usernames and got a beautiful chat transcript.

But then I needed to take a break to give my son a bath and put him in bed. When I got back, I sent another message. You can see the result in Figure 3.3, on the next page.

When I sent the new message, all of the older messages were gone! The transcript doesn't have anything except the new message I just added. We didn't write any code to delete old messages, in fact, our code has absolutely no concept of getting rid of messages; we just continually add messages to the chat room. So what happened to the transcript that we had before? Where did the old messages go?

They didn't go anywhere. We got bitten by one of the basic and important differences between cloud code and regular code. When you write code for your own server, you know that every request is going to be handled by your server. If you start a Python interpreter and send requests to it for processing, you know that the Python interpreter will stay around for as long as you want it to.

When you send a request to a cloud server, it gets routed to some server in some cloud data center. There's no guarantee that any two requests will be routed to the same server or even to servers on the