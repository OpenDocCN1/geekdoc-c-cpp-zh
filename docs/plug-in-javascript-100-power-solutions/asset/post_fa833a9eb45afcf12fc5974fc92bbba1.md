
# Chapter 1: Making the Best Use of These plug-ins

main browsers. I know, it's a pain, but it has to be done. Luckily, there's a trick to make this easier than it might otherwise be.

## Emulating Internet Explorers 6 and 7

To developers who have designed websites to work specifically with older versions, the developers of Internet Explorer created a meta tag that you can add to the head of a web page IE thinks is an earlier version of itself. Here are the two main meta tags you will use:

```html
<meta http-equiv="UA-Compatible" content="IE7" />
<meta http-equiv="UA-Compatible" content="IE5" />
```

This is an example of how to incorporate the IE tag:

```html
<html>
<head>
<meta http-equiv="UA-Compatible" content="IE7" />
<title>My Website</title>
</head>
<body>
Website Contents
</body>
</html>
```

There is no IE=6 (presumably the rendering engines of IE5 and IE6 are so similar), using the IE=5 option makes Internet Explorer enter what is known as "quirks" mode, in which it behaves like both IE5 and IE6.

Incidentally, if you force Internet Explorer into full standards (to be as compatible with other browsers) you can use the option IE=8. Without the meta tag, Internet Explorer will use its proprietary and optimal settings, known as "edge mode", which you can also select with the option IE=edge. Of course, once you have finished testing, you should remove or comment out these meta tags unless you wish to use one for a particular reason.

In addition to the meta tags, always ensure that you have a suitable HTML doctype declaration at the start of each document. The most commonly found doctype is the following, which has been fully tested and works with all of this book's plug-ins.

```html
<!DOCTYPE HTML PUBLIC "-//W3TD HTML 4.0 Transitional//EN"
http://www.w3.org/TR/html4/loose.dtd">
```

> Caution: If you use a different doctype from the one listed, you may find you to slightly modify them. I often use both the preceding "loose" doctype and the IE meta tag to get the most compatible results with other browsers. Remember, if IE behaves strangely when all other browsers appear to work well with your code, the solution could be to change the doctype or IE5/IE meta tags. If you are interested in the subject of browser compatibility and its various nuances, I recommend visiting website at quirksmode.org.

## 8 Plug-In JavaScript: 100 Solutions

## The Companion Website

To save the effort of typing all plug-ins in this book, you can download them from this book's companion website at pluginjavascript.com (see Figure 1-4).

Click the "Download Plug-ins" link to download the file plug-ins.zip, which is an archive file (easily extractable on all operating systems) containing all the plug-ins. Once extracted, in the root of the plug-ins.zip you will find files P1.js and P1.js, which contain the plug-ins in a ready-to-use form. Also in the root is a file ReadMe.txt, which contains the latest details about the plug-ins, including any improvements or updates that have been made since this book was published.

There are also examples from 3 to 13, corresponding to chapters in this book. Within each folder you will find example HTML and JavaScript files showing the use of each function that you can load into a browser to try out for. Some plug-ins also make use of Ajax techniques and may include other associated files (such as those with .php extensions), in case they will be documented in the associated chapter.

![](img/95e4c43b430487125c342550cc090977_28_0.png)

# CONTENTS

JavaScript is the free language built into all modern browsers including Internet Explorer, Firefox, Safari, and Chrome. It is the power behind dynamic web applications, the technology used for Web 2.0 websites such as Facebook, Flickr, Gmail and many others. Plug-In JavaScript is aimed at people who have learned basic HTML, and provides a Little Ajax that they may wish to create dynamic menu systems, provide mouse hover effects, support Ajax functionality and more. They will be shown how to do all these things and make more using simple JavaScript.

- 1. Building a Development Server
- 2. The DOM
- 3. Plug-ins
- 4. Location
- 5. Visibility
- 6. Movement & Animation
- 7. Changing & Interaction
- 8. Menus & Navigation
- 9. Text Effects
- 10. Audio & Visual Effects
- 11. Cookies, Ajax & Security
- 12. Forms & Validation
- 13. Solutions to Common Problems

FIGURE 1-4 The companion website at pluginjavascript.com

## Chapter 1: Making the Best Use of These Plug-ins

## Including All the Plug-ins

The easiest (and recommended) way for to use these plug-ins is to load them all into a web page as a complete set, which you can do with the following command, assuming you saved the file PJ.js into the current folder:

```html
<script type="text/javascript" src="PJ.js"></script>
```

In fact, by all modern browsers assume that script will be JavaScript, so you can use the following short form, which omits the type= parameter:

```html
<script src="PJ.js"></script>
```

Or, if you have PJ.js located elsewhere, such as in the root folder, you change the command to include the path, like this:

```html
<script src="PJ.js"></script>
```

Alternatively, if you use a specific folder for your JavaScript files, such as scripts, you use this command:

```html
<script src="scripts/PJ.js"></script>
```

And the compressed version of the file, PJsmall.js, can be included instead, like this:

```html
<script src="scripts/PJsmall.js"></script>
```

Immediately the line that includes the plug-ins, you need to add a second line as follows, which will initialize the plug-ins, ready for:

```html
<script>Initialize()</script>
```

The benefits of using is that you only need to add a couple of lines to your web pages to have access to all the plug-ins, and there is only one change when you want to modify any plug-ins. Also, at around 60KB for the raw JavaScript file, it doesn't take very long to load or consume bandwidth.

What's more, already mentioned, you can choose to use the compressed version of the file, PJsmall.js, which is half the size. The only difference between the two files is that the larger one has all the functions shown in.

## Including Single Plug-ins

All the plug-ins included in this book are fully integrated with each other, and as you progress through the book you will see plug-ins rely more and more until you reach the point where would normally require dozens of lines of code.

## Plug-In JavaScript: 100 Solutions

Therefore, because you have the option of using the compressed file, which takes up less space than even images, I don’t recommend to copy and paste individual plug-ins into your web pages unless essential.

## Where to Include the JavaScript

The best place to insert the plug-ins is in the head section of your web pages so the whole page will have access to them. The following example (which assumes that PJsmall.js is in the document root) the recommended way to insert the file (shown in bold):

```html
<html>
<head>
  <script src="PJsmall.js"></script>
  <script>Initialize()</script>
  <title>My Website</title>
</head>
<body>
  Website Contents
</body>
</html>
```

Placing the code in the head section means the file of plug-ins will be loaded first, and therefore, your JavaScript code can be placed anywhere you like within the rest of the page (including the head) and when it calls one of the plug-in functions it's guaranteed to be available.

## Cherry Picking Code Sections

Although the primary objective of this book is to provide you with a comprehensive toolkit of plug-in functions to save you from reinventing the wheel, I also hope that the documentation of the plug-ins will make them easy for you to adapt to your own purposes. In fact, I encourage you to take what you can from this book and extend and improve it.

If that means you to cherry pick a routine from here and code a snippet from there and build your own new plug-ins, then this book succeeded in its secondary goal of helping you to take your JavaScript programming skills to the next level.

## Bug Fixing and Reporting

The raw JavaScript plug-ins comprise over 2500 lines of code, which has been tested over and again in many different conditions possible. But you should realize that this book represents a major amount of programming and it is inevitable that unforeseen bugs will show up.

Hopefully there are not many of them, and that there will be of minimal consequence. Even so, this means to ensure you have the latest versions, which you grab the plug-ins from the companion website at pluginjavascript.com. Speaking of which, if you come up with any fixes or improvements please send them to me via the website and I'll use them to update the source files and improve their capabilities for all readers—you will be
