can apply various methods to them, like the css method you saw earlier. You also need to know a little about jQuery events that enable you to attach behavior to the events that your HTML elements might fire, like click, mouseover, and so on. In the next couple of sections, you see all of these main jQuery topics at work.

# jQuery Core

Most of the jQuery code you write will be executed when the browser is done loading the page. It's important to wait with executing your code until the page is done loading the DOM. The DOM— the document object model—is a hierarchical representation of your web page and contains a tree-like structure of all your HTML elements, script files, CSS, images, and so on. The DOM is always in sync with the page you see in the browser, so if you make a programmatic change to the DOM (for example, with jQuery code), the change is reflected in the page in the browser. If you execute your jQuery code too early (for example, at the very top of the page), the DOM may not have loaded the elements you're referring to in your script, and you may get errors. Fortunately, it's easy to postpone the execution of your code until the DOM is ready using the ready function in jQuery. You've already seen the ready function at work in the previous Try It Out, but it's shown here again now that you better understand what it's used for:

```
```javascript
$(document).ready(function() {
  // Code added here is executed when the DOM is ready.
});
```
```

Any code you add between the opening and closing curly braces is executed when the page is ready for DOM manipulation. jQuery also comes with a shortcut for the ready function to make it easier to write code that fires when the DOM is ready. The following snippet is equivalent to the preceding example:

```
```javascript
$(function() {
  // Code added here is executed when the DOM is ready.
});
```
```

> > NOTE It's important that any code referencing the jQuery library is not run before the jQuery library itself is loaded. Because the link to the jQuery library is added after the <body> tag by the ScriptManager, you need to find a location later in the page. A good place for this is near the closing </body> tag defined in the master page.

Because jQuery code is often specific to a page, it makes sense to add the code to the end of just the pages that require it. To make this a little easier, you can add a ContentPlaceHolder in your master page especially for this purpose. The pages that use this master page then have an easy location to write jQuery code. You see how to do this in the next exercise.

In the previous jQuery example you saw some code that selected the MainContent <section> element and the button in your page. However, jQuery comes with a lot more options to select specific elements in your pages. These options are discussed next.