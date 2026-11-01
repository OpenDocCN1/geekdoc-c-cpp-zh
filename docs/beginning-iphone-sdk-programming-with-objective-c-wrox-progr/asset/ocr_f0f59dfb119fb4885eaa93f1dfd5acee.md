# DEBUGGING YOUR APPLICATIONS

Debugging your iPhone applications is an essential part of your development journey. Xcode includes debugger utilities that help you trace and examine your code as you execute your application. The following sections show some of the tips and tricks that you can employ when developing your iPhone applications.

# Error

When you try to run your application, Xcode first tries to build the project before it can deploy the application onto the real device or Simulator. Any syntax errors that Xcode detects are immediately highlighted in red. Figure B-10 shows Xcode highlighting a syntax error. The error with the code block is the missing brace symbol (() for the {[UIAlertView alloc] statement:

```
UIAlertView *alert = [UIAlertView alloc]
    initWithTitle:@"Hello World!"
    message:@"Hello, my World"
    delegate:self
    cancelButtonTitle:@"OK"
    otherButtonTitles:nil];
```

![](bbox=[0.17, 0.58, 0.65, 0.8])

FIGURE B-10