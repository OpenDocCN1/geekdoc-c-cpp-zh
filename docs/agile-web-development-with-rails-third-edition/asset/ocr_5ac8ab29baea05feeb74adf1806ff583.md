+   - Using the logger to log events
+   - Removing duplication from controllers

We've also generated our fair share of errors and seen how to get around them.

But, just as we think we've wrapped this functionality up, our customer wanders over with a copy of *Information Technology and Golf Weekly*. Apparently, there's an article about a new style of browser interface, where stuff gets updated on the fly. "Ajax," she says, proudly. Hmmm...let's look at that tomorrow.

# Playtime

Here's some stuff to try on your own:

+   - Add a new variable to the session to record how many times the user has accessed the store controller's index action. The first time through, your count won't be in the session. You can test for this with code like this:
+   
+     `if session[:counter].nil?`
+     `...`
+   
+     If the session variable isn't there, you'll need to initialize it. Then you'll be able to increment it.

```
if session[:counter].nil?
...
```

+   - Pass this counter to your template, and display it at the top of the catalog page. Hint: the pluralize helper (described on page 517) might be useful when forming the message you display.

+   - Reset the counter to zero whenever the user adds something to the cart.

+   - Change the template to display the counter only if it is greater than five.

(You'll find hints at http://pragprog.wiki dot com/rails-play-time.)