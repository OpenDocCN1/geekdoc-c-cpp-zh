One obvious disadvantage of NSOperation is its inflexibility. If your application needs to queue many different tasks, it can take a lot of time to create a custom subclass for each.

NSOperation has been extended to allow task code to be defined with blocks, which allow the use of inline code or predefined code blocks that are used more fluidly.

# Getting Started with Blocks

Blocks are a new feature in Objective-C, borrowed from similar idioms in other languages, such as Ruby. A block is an object, but is used like a function. Block code can be created inline, or it can be defined in a separate declaration and called via a *block pointer*, which is similar to an object pointer, with modified syntax.

A block is an alternative design pattern that can replace delegation and selectors. Both delegates and selectors can be difficult to follow, because related code may be scattered among many objects. Block code is inline, which makes it easy to read and maintain. For example, in the block operation example later in this chapter, code that runs in a separate thread is immediately visible and can be edited in-place. It isn't buried in a method inside a separate object.

Technically a block encapsulates a block of code, *including the state of all relevant variables at the time it is created*. This complicates variable and parameter assignment. By default, variable values are fixed when the block is defined. To make them mutable, you must prefix them with a `__block` directive, defined with a double underscore.

Block support was added to some of Cocoa’s key classes in OS X 10.6 and will be developed further in future versions. For some applications, blocks offer a viable alternative to delegation, because they allow inline code that is easier to write and easier to understand.

Although blocks are often associated with multithreading, blocks are a separate technology. They’re not inherently multithreaded, and can be used as standard single-threaded Objective-C code. But some of the new Cocoa extensions make it possible to define a task with block code and launch it, in much the same way that NSTask calls a selector to define a method and then launches the method in a separate thread.

# Understanding block syntax

Blocks have two sections: an optional header and a body that contains the block code. Classes that support blocks allow body-only blocks to be used as inline code. Depending on the context, this may disable certain features, such as parameter passing or support for return values.

Blocks are marked with the ^ (caret) character and delimited with curly brackets, followed by an apostrophe.

```
aBlock = ^{ some code goes here};
```

If no parameters or return values are defined, void is assumed. You can call the block with

```
aBlock();
```