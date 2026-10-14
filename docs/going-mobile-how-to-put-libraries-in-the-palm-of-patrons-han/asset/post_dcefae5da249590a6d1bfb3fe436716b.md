
## 7 BEYOND THE BASICS

The point of this book is to make building an app as simple as possible. You can add JavaScript to your app to make it flashier, but talking in detail about JavaScript would take away from the point of this book—keeping it simple.

JavaScript is a pretty powerful language that can do a lot of things, but learning it isn’t essential to building a great-looking app. If you know JavaScript, then use it; if you don’t, then there’s another option: widgets. If you blog or read blogs, then you likely know all about widgets, even if you don’t know them by name. Widgets are the small little boxes that sit on the sidebars of blogs and offer links to things like Twitter, Facebook, and Google News streams. Widgets appear on the surface to be quite simple, but there are pages of code built into each one. The good news is that you don’t have to know the code to build them.

A simple Web search for “widgets” turns up thousands of pages that offer customizable widgets; some are free, and others have small fees attached. You’ll need to watch out for widgets that use Flash (which many phones do not currently support—most notably, the iPhone).

Many websites also offer widgets. Twitter is the perfect example. On the widget web page for Twitter (https://twitter.com/widgets/) you can build a custom widget in just a couple of short steps.

First, on the widget page, select My Website (figure 7.1).

![](img/1c33fb3bae0a705f04846bc77d279fd7_48_0.png)

On the following page you will see several options; choose Profile Widget, which will display your library’s most recent tweets.

Next, you can customize your widget (figure 7.2). Under the user name, you ideally would put the name of your library, but you can also put authors, magazines, or the name of anyone else with a public Twitter account. This would give your app content if you don’t have time to do it yourself.

![](img/1c33fb3bae0a705f04846bc77d279fd7_49_0.png)

**Figure 7.2**

Under Preferences, you can select how many tweets you display. Although the limit on Twitter is thirty tweets, it is advisable to consider the screen size of the mobile device you are developing for. You don’t want users to have to scroll too much—ideally, you don’t want them to scroll at all. Because of that, you might keep the number of tweets displayed to four.

Under Appearance, make sure the colors you select match the colors of your app. Under dimensions, you can adjust them to the dimensions of the phone or choose auto width if you want it to resize the widget itself.

Finally, go to the bottom of the page and select Finish & Grab Code (figure 7.3). Now just copy the code and paste it into your app’s code.

![](img/1c33fb3bae0a705f04846bc77d279fd7_49_1.png)

**Figure 7.3**

If you are thinking about providing a chat-based reference service (if you are not, you should be—by not doing so, you’ll miss an entire generation of users), then consider LibraryH3lp (http://libraryh3lp.com). There is a small annual fee for the site’s service (which varies depending on the size of the city you’re in), but it is much cheaper than many similar services. Meebo and Google Talk offer free chat services, but their widgets use Flash, so they aren’t supported on the iPhone app. In contrast, LibraryH3lp uses Java, so it’s app friendly. Box 4 displays the source code of LibraryH3lp’s widget.

In a mobile browser, the code from Box 4 would look similar to figure 7.4.

Widgetbox (www.widgetbox.com) is one of the most popular widget builders; it’s free but advertisement supported. A pro version (without the ads) is also available, starting at $29.99 a year. The site offers both Flash- and Java-based widgets.

Facebook also provides steps for embedding profiles into websites (http://developers.facebook.com/docs/guides/web/). Widgetbox, however, makes a much more user-friendly version, and if you are new to development, it is the better choice. Just make sure you copy the Java-based version of the widget and not the Flash-based one.

### BOX 4 ■ Source Code for LibraryH3lp’s Widget

```html
<html xmlns="http://www.w3.org/1999/xhtml" xml:lang="en" lang="en">
<head>
<meta http-equiv=content-type content="text/html; charset=UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0 user-scalable=yes" />
<title></title>
<link type="text/css" rel="stylesheet" href="/css/mobile.css" />

<style id="dynamic" type="text/css">
</style>
<script type="text/javascript" src="http://ajax.googleapis.com/ajax/libs/jquery/1.3.2/jquery.min.js"></script>
<script type="text/javascript" src="http://d1aaqh87bn7fin.cloudfront.net/mobile_2010011801.min.js"></script>
<!--
<script type="text/javascript" src="/js/lib/strophe.js"></script>
<script type="text/javascript" src="/emoticons/emoticons.js"></script>
<script type="text/javascript" src="/js/mobile.js"></script>
-->
</head>
<body>
<div id="header">
<img id="presence" src="/presence/image/simpletext/unavailable" />
<h1 id="title"></h1>
</div>

<div id="to" jid="my-queue@chat.libraryh3lp.com" lang="en"></div>
<div id="recv"></div>
<div id="send">
<form action="#" method="post" onSubmit="return false;">
<textarea id="msg">chat requires javascript...</textarea>
</form>
<div id="buttons"><a href="#" onclick="libraryh3lp.sendLine(); return false;"><img height="42" width="30" src="/images/mobilesend.png" /></a></div>
</div>
<div id="status"><a id="mail" href="#" onclick="libraryh3lp.mailTranscript(); return false;">Email transcript</a></div>
</body>
</html>
```

![](img/1c33fb3bae0a705f04846bc77d279fd7_51_0.png)

**Figure 7.4**

Widgetbox also makes it easy to develop a mobile app (www.widgetbox.com/mobile/). If you want a basic mobile web app (not a native app) that shows Twitter, Facebook, or Flickr updates, then Widgetbox might work well for the library; it does not, however, allow for users to edit the source code, and you might quickly find it to be too restrictive for your library.

Widgipedia (www.widgipedia.com) is another great resource for finding widgets; however, they are user submitted and customizable.

PhoneGap offers several codes that developers can copy for use in their own app; you can find these in the Community section of the website (www.phonegap.com/community/). It’s frequently updated, so check back often. A useful code is for including a map, based on the phone’s GPS (http://phonegap.pbworks.com/PhoneGap-Geolocation-Sample-Application).

I have tested all of the widgets and tools in this chapter to ensure that they will work with an iPhone app. As I have said before, however, JavaScript is tricky on mobile web apps and native apps, so always test before implementing. For every JavaScript that I have tested successfully on a native iPhone app, a dozen more come back with errors.

## OTHER WAYS TO GO MOBILE

The point of this book is to show librarians how simple it can be to develop mobile applications. For the most part, mobile apps run on smartphones. However, librarians can also proactively investigate other mobile application programming interfaces (APIs).

Foursquare (for documentation information, see http://groups.google.com/group/foursquare-api/web/api-documentation/), which some bill as the next Twitter, is a location-based social media app that allows people to tell their friends exactly where they are and become “mayors” of locations they visit frequently. Gowalla (http://gowalla.com) is another social website like Foursquare that’s growing in popularity; unlike Foursquare, though, Gowalla offers a little more in terms of customization.

When thinking about mobile apps, libraries should think of as many free technologies as possible for promotion—Foursquare and Yelp already have apps that you can easily link to. If your library has not staked its claim on Foursquare, why not? It’s a perfect avenue for promotion—people can check into the library with the library app and get something for free—free videos, reduced fines, small prizes, and so on.

Some of the best social media sites that work on mobile phones are the same ones that are most popular on the Web: Facebook, Twitter, YouTube, and Flickr. If your library doesn’t have a Facebook fan page, it’s time. This is true too, though to a lesser extent, with the other three. What better way to showcase your library programming than with videos and photos? What’s great about all the social media sites is that they are integrated together—you can feed Twitter updates into Facebook and share YouTube videos and Flickr slide shows instantly on Twitter and Facebook. The best thing about these sites, however, is that you don’t have to do anything to go mobile. If you have a page on Twitter or Facebook, it’s already mobile compatible—no extra steps are required.

Librarians don’t give you answers—they merely point you in the right direction. Your app should work the same way. Save yourself time and trouble by finding code that’s already finished. I hope you decide to develop a mobile app, but at the very least, I hope you make sure that your library is actively involved in the mobile technologies mentioned here.
