# ORGANIZING WITH MACROS

![](bbox=[0.068, 0.221, 0.26, 0.419])

**FIGURE 13.5** The Jump Bar pop-up organized using `#pragma mark`

Xcode includes CPP, the C preprocessor, through which your code is run just prior to compilation. The preprocessor transforms your code wherever macros are encountered. For example, when it encounters an `#import` directive, the preprocessor replaces it with the referenced file (nearly always a header file) so its contents are available to the compiler.

A less obvious use of preprocessor macros is for organization within a graphical editor. Using the `#pragma mark` directive, you can define areas within your source file. When you have this file open in the Source Editor, the last segment of the Jump Bar (which, as you’ll recall, lists class members for easy navigation) will reflect your marks by grouping them in its pop-up menu. For example, **Figure 13.5** shows one possible organization of the TestAppAppDelegate.m file.

To use the directive, just place it (along with a name for the section) on a blank line by itself as follows:

```
```objc
#pragma mark Constructors / Destructors
```
```

You can go a step further and place a separating line in the menu by using a dash as the mark as follows:

```
```objc
#pragma mark –
```
```

There is no defined standard dictating how you should use this directive, nor does it have any effect on your compiled code (it is not part of the compiled code). Although it’s easy to get carried away and pepper your code with marks, most take a minimalist approach and group methods by their primary function.

As an example, you might create a section for UI actions in a controller class, another section for model manipulation methods, another for initialization and deallocation, and another still for accessors. Figure 13.5 roughly follows this general approach. Your style may vary.