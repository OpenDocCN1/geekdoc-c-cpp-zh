# Questioning the Client 657

to get the client it wanted and waited then. And wait for some more.

Even if the server wants an acknowledgement from the client, it might never get one. The server user might have closed the browser.

Communication from the client to the server is sporadic. Secure trans-actions are nearly impossible because the server cannot be sure that the client will communicate any information back. Because of the loosely coupled nature of the Internet, you can't make any assumptions about communication time.

+   **Dist input:** Browser documents are sent as a package of text and images (and sounds and fonts Flash movies, if needed) to the client from the server. The requests are sent back to the server in a similar way — text.

With all this text, you would think that someone would find a way to fake a request. Oh, they have. Lots of them. And it is free, and.

Take a look at Fiddler (www.fiddlurtle.com), a free tool that lets you alter the requests from a browser (see Figure 1-4). Fiddler gives you the capability to view a request — including the results from a form (a login form) — after the text directly, and then sends it on its merry way.

![](bbox=[0.134, 0.525, 0.866, 0.845])

![](bbox=[0.875, 0.305, 0.966, 0.435])