# JQUERY SYNTAX

To understand and use jQuery, you need to know a few important basics. First, you need to know more about jQuery's core functionality, including the s function you have seen before, and its ready method that enables you to execute code when the page is loading in the browser. Next, you need to learn about jQuery's selector and filter syntax, which enable you to find elements in a page by criteria that you specify. When you have a reference to one or more elements in a page, you can apply various methods to them, like the css method you saw earlier. You also need to know little about jQuery events that enable you to attach your behavior to the events that your HTML elements might fire, like click, mouseover, and so on. In the next sections, you will see all of these main jQuery's topics at work.

# jQuery Core

Most of your jQuery code will be executed when the browser is done loading the page. It is important to wait without executing your code until the page is loading the DOM. The DOM — the document object model — is a hierarchical representation of your web page and contains a tree-like structure of all HTML elements, script files, CSS, images, and so on. The DOM is always in sync with the page in the browser, so if you make a programmatic change to the DOM (for example, with jQuery code), the change is reflected in the page in the browser. If you execute your jQuery code too early (referring to your script, for example, at the very top of the page), the DOM may not have loaded the elements you're referring to in your script, and you may get errors. It's easy to postpone the execution of code until the DOM is ready using the ready function in jQuery. You've already seen the ready function at work in the previous Try It Out, but it's shown again now that you better understand what it's used for:

```
$(document).ready(function() {
  // Code added here is executed when the DOM is ready.
});
```

Any code you add between the opening and closing curly braces is executed when the page is ready for DOM manipulation. jQuery also calls for the ready function to make it easier to write code that fires when the DOM is ready. The following snippet is equivalent to the preceding example:

```
$(function() {
  // Code added here is executed when the DOM is ready.
});
```

> NOTE It's important that any code referencing the jQuery library is not run before the jQuery library is loaded. The link to the jQuery library is added after the <body> tag by the ScriptManager, you need to find a location later in the page. A good place for this is the closing </body> tag defined in the master page.