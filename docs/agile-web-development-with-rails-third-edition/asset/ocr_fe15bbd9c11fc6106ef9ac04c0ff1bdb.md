First, we'll start a local WEBrick-based web server, supplied with Rails:

```
depot> ruby script/server
=> Booting WEBrick...
=> Rails application started on http://0.0.0.0:3000
=> Ctrl-C to shutdown server; call with --help for options
[2008-03-27 11:54:55] INFO  WEBrick 1.3.1
[2008-03-27 11:54:55] INFO  ruby 1.8.6 (2007-09-24) [i486-linux]
[2008-03-27 11:54:55] INFO  WEBrick::HTTPServer#start: pid=6200 port=3000
```

Just as it did with our demo application in Chapter 4, Instant Gratification, this command starts a web server on our local host, port 3000.9 Let's connect to it. Remember, the URL we give to our browser contains both the port number (3000) and the name of the controller in lowercase (products).

![](bbox=[0.18, 0.305, 0.515, 0.49])

That's pretty boring. It's showing us an empty list of products. Let's add some. Click the New product link, and a form should appear. Go ahead and fill it in:

![](bbox=[0.18, 0.555, 0.58, 0.83])

9. You might get an error saying Address already in use when you try to run WEBrick. That simply means that you already have a Rails WEBrick server running on your machine. If you've been following along with the examples in the book, that might well be the "Hello, World!" application from Chapter 4. Find its console, and kill the server using Ctrl-C.