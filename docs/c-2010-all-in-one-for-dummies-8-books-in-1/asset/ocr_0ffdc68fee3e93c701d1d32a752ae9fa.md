# 362 A Real-World Example

In that setup, the sequence of events:

+   1. UseTheDel() takes two arguments, a MyDelType delegate, and a string that it calls arg. So, when Main() calls UseTheDel, it passes my delegate instance to be used inside the method. When I created the delegate instance, del, in Main(), I passed the name of the CallbackMethod() as the method to be called. Because CallbackMethod() is static, I had to prefix the method with the class name, Program. I tell you more about it in this chapter.
2. UseTheDel(), the method ensures that the delegate isn't null and starts a WriteLine() call. When that, before it finishes, the method invokes the delegate by calling del(arg). arg is something you can pass to the delegate, which causes the CallbackMethod() to be called.
3. CallbackMethod(), the method writes its own message, including the string that was passed when UseTheDel() invoked the delegate. Then CallbackMethod() returns the length of the string it was passed, and that length is written out as the last part of the WriteLine() in UseTheDel().

The output looks like this:

```
CallbackMethod writes: hello
UseTheDel writes 5
Press Enter to terminate...
```

UseTheDel() phones home and CallbackMethod() answers the call.

# A Real-World Example

For a more realistic example than SimpleDelegateExample, I show you how to write a little app that puts up a progress bar and updates it every time a lengthy method invokes delegate.