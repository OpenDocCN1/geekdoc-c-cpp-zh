background color of the MainContent <section> element to red, and changes the height and the width of it using a fluid animation:

```
$('#Button1').click(function() {
  $('#MainContent').css('background-color', 'red')
    .animate({ width: '100px', height: '800px' })
});
```

Again, you learn more about how jQuery is able to find the button and the <section> element and how the css and animate methods work later in this chapter, so don't worry too much if none of this is making a lot of sense right now.

When you click the button in the browser, the MainContent's background color is changed to red, and then its width and height are changed to 100 and 800 pixels, respectively.

When you typed the jQuery code you may have noticed you got help from IntelliSense. As soon as you typed $() you got a tooltip explaining the information you can pass to this function. Likewise, IntelliSense helps you find and complete the css method and the various arguments you need to pass to it, as shown in Figure 11-4.

![](bbox=[0.15, 0.57, 0.78, 0.7])

FIGURE 11-4

IntelliSense for jQuery works through the extra file—jquery-1.7.2.intellisense.js—you added to the site with NuGet. VS scans the library's folder for files ending in intellisense.js, parses them, and then uses the documentation it finds in them to build up the IntelliSense list.

The reason for the separate documentation file is to keep the size of the original jQuery library down. Without the documentation, the library is only 93 KB; with the documentation the file size would be much bigger.

You should never include a link to the IntelliSense version of the library in your pages because it doesn't add any value in the browser.

Now that you've seen some jQuery at work, it's time to get a better understanding of its possibilities and syntax.

# JQUERY SYNTAX

To understand and use jQuery, you need to know a few important basics. First, you need to know more about jQuery's core functionality, including the $ function you've seen before, and its ready method that enables you to execute code when the page is done loading in the browser. Next, you need to learn more about jQuery's selector and filter syntax, which enable you to find elements in a page by criteria that you specify. Once you have a reference to one or more elements in a page, you