
debugging that make it easy to debug even where your code crosses the boundary between different languages—like your Java server and your client UI, which is really running in JavaScript or HTML5.

And that's the most valuable thing about GWT. You see, the biggest problem with cloud programming in general is that it's painful and difficult to test and debug. In a cloud application, you need to deal with the client program (HTML + JavaScript), plus whatever programming language the server is implemented in, plus XML and HTTP. That's a lot of complexity. But that's not the worst of it. You don't just need to deal with those languages: you also need to deal with the boundaries between them. You don't just need to write JavaScript code on the client; you need to write JavaScript code that knows how to generate HTTP requests and how to parse the XML response and generate JavaScript objects from them. Your server doesn't just need to have code to perform its basic operations: it needs to know how to parse HTTP requests to figure out what operation a client wants it to perform, and it needs to take the result of that operation and translate it into XML. And both the client and the server need to agree perfectly on what the requests, responses, and XML encodings are. Any problem with any piece of the code—particularly with code in the boundary regions between languages—can cause subtle, hard-to-find problems. I have no idea how many hours of my life I've wasted tracking down errors involving trivial mistakes in XML formats or HTTP message headers.

The most important thing about GWT isn't that it lets you write your UIs using widgets like a native UI toolkit. That's really nice and valuable. But far more important and valuable is the fact that GWT takes care of the boundaries: you write all of your code in Java, and GWT takes care of translating that Java into XML, HTTP, JSON, JavaScript, HTML, and CSS, and generates the code that bridges the boundaries between them. All of that stuff is still going on under the covers—but with GWT, you don't need to deal with it. You won't have problems with those boundaries, and the amount of time and effort that you'll save is astonishing.

### 11.2 Building GWT UIs with Widgets

It's time to build our own UI using GWT. We'll take our chat application and build the same basic UI that we built in Python, this time using GWT. To start, we'll concentrate on the real UI aspects—except where necessary, we'll ignore the application logic and focus on presentation. This is typical of how you'll build a GWT-based App Engine service: you start by figuring out what you want the service to do. As we did in the previous chapter, figure out the basic data you want to manipulate and what kinds of RPC calls you'll need. Then sit down with GWT and put together the UI.

Like most UI toolkits, in GWT, you work with *widgets*. A widget is a basic element of the user interface. There are widgets for all of the basic common user interface elements you're used to: text boxes, buttons, radio buttons, drop downs, menus, and so on. There are also *container widgets* for managing layout. This whole structure is, as I've said before, one of the great reasons for using GWT: you don't need to worry about how to do the CSS to make your UI layout work. You don't need to figure out how to set up all of the JavaScript to draw your UI. You build your UI out of widgets—including container widgets—and then you let GWT do the work. You can focus on the what, rather than the how.

In a traditional GUI toolkit, you start off with a window and place the widgets in it. With GWT, you're putting your application into a web page and putting widgets into that. So in GWT, the starting point is an HTML page. You can put whatever HTML you want into the basic page; in fact, if you want to, you can do almost all of the GUI layout using HTML. Back in Chapter 9, *Google App Engine and Java*, on page 123, we did use HTML to do the basic layout. But you don't have to do that: you can use an HTML page that is totally blank and just use GWT to do all of the layout. That's what we'll do in this chapter. We still need an HTML page—the only way of loading a cloud application is through a web page. So we will use a minimal skeleton page, shown below. All it does is set the links to load the GWT UI, using a `<link>` tag to load the CSS, and a `<script>` tag to load the UI code.

So we start with an HTML page. To tell App Engine exactly which page is the main frame of our application, we edit the `web.xml` file the same way we did in the previous chapter. We'd like the main page of our application to be called `Chat.html`, so we just edit the `welcome-file-list` entry:

```html
<welcome-file-list>
  <welcome-file>Chat.html</welcome-file>
</welcome-file-list>
```

Once the system knows what page provides our application frame, we can set that frame up by creating the Chat.html page:

Download: workspace/PersistChat/war/Chat.html

```html
<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN">

<html>
  <head>
    <meta http-equiv="content-type" content="text/html; charset=UTF-8">

    <link type="text/css" rel="stylesheet" href="Chat.css">

    <title>AppEngine Chat</title>

    <script type="text/javascript" language="javascript"
        src="persistchat/persistchat.nocache.js">
    </script>
  </head>

  <body>
  </body>
</html>
```

There's not much to it; it's a very minimal file. The body is completely empty: we're going to populate it completely using dynamic layout code in GWT. The important things are these:

- A link to the .css page for the application. You'll usually use the same name for the CSS and HTML files, so the CSS is Chat.css.
- A script tag, which loads the GWT-generated JavaScript code.

With the page in place as a frame for our application, we can start on the real work. What do we want in our Chat UI? Let's look at the mockup we put together previously in Figure 7.2, on page 104. We've got a title bar up at the top; under the title bar, there's a subheader with the current time and date; then there's a box containing a list of chats and a box containing the chat messages side by side. Underneath those boxes is the entry box where we can type new messages and a button to send them.

In GWT, we can set up exactly what we just described. The basic structure of the UI is a vertical layout: a top box with the title and subtitle, a middle box with the chat list and chat messages, and a bottom box with the text entry. We want to write GWT code that will set up those widgets and arrange them into our UI.

In GWT, the client application always starts by calling the onModuleLoad method of the application's main class. onModuleLoad is basically the main function of a GWT application, and since the first thing that a GWT application needs to do is to set up its user interface, put the UI construction code right there. In the rest of this section, we'll be building up the implementation of onModuleLoad.

We'll start by creating the basic frames of our UI:

Download workspace/PersistChat/src/com/progprog/aebook/persistchat/client/Chat.java

```java
final VerticalPanel mainVert = new VerticalPanel();
final VerticalPanel topPanel = new VerticalPanel();
final HorizontalPanel midPanel = new HorizontalPanel();
final HorizontalPanel bottomPanel = new HorizontalPanel();
mainVert.add(topPanel);
mainVert.add(midPanel);
mainVert.add(bottomPanel);
```

- 1. In order to set up a UI with a series of stacked UI elements, we must create a Panel widget and insert the other elements into it. First, we create a VerticalPanel, which is the main element of the UI.
- 2. Now, we want to create the vertical elements of the UI. We've got three things. At the top, we've got something that is going to vertically stack a title bar and a subtitle, so that's another VerticalPanel. In the middle, we'll have two things side by side (the chat list and the chat transcript), so that's going to be a HorizontalPanel. Finally, at the bottom, we're going to have the entry box and Send button—again, side by side—so that's another HorizontalPanel.

Now we want to put the title and subtitle into the top panel:

Download workspace/PersistChat/src/com/progprog/aebook/persistchat/client/Chat.java

```java
final Label title = new Label("AppEngine Chat");
final Label subtitle = new Label(new Date().toString());
title.addStyleName("title");
topPanel.add(title);
topPanel.add(subtitle);
```

- 1. In the top panel, we're going to want to put two widgets, both of which only display some text. The easiest way to put text into a GWT UI is to use the Label widget. We create label widgets for both the title and subtitle. Since they're passive and don't change, we can just put the text into them when we create them.
