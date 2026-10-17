You can write a conditional block of code as follows:

```
#ifdef SOMEMACRO
    NSLog(@"This code will only be included if SOMEMACRO is
    → defined...");
#endif
```

The NSLog() statement will not be included in the compiled code unless SOMEMACRO is defined. The #ifdef directive doesn’t care what SOMEMACRO represents, only that it is defined. Recall that you can define SOMEMACRO like this:

```
#define SOMEMACRO 1
```

# DEFINING MACROS IN THE BUILD ENVIRONMENT

Defining a macro and then checking if it’s defined is easy enough. Whether a macro is defined can also be based on the current build settings, as the BETABUILD flag is.

To try this scenario out for yourself, start by adding the following code to the end of the TestApp delegate class’s -applicationDidFinishLaunching: method:

```
#ifdef BETABUILD
    [[NSAlert alertWithMessageText:@"Beta Version"
        defaultButton:@"Ok"
        alternateButton:nil
        otherButton:nil
        informativeTextWithFormat:@"Warning: you are using a beta
        → version of this application. Bad stuff might happen."]
        → runModal];
#endif
```