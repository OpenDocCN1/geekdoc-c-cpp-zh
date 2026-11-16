# # COMMENTING LINES...

As we'll see, the C# compiler understands several different types of comments. The simplest are line and block comments, which are simply ignored by the compiler.

The most basic type of comment, a LINE COMMENT, begins with two slashes and ends at the end of the line:

```
//This is a comment
Int32 MyInteger; //This is also a comment
```

As you can see, the slashes can come anywhere on a line. The only rule is that everything after the comment will be ignored. You can type anything you like after the slashes; C# doesn't care. But you can't continue the comment onto the next line:

![](bbox=[0.12, 0.55, 0.22, 0.64])

```
//This will
cause an error.
```

```
//This will
//NOT cause an error.
```

How do you know what to comment? This is what experience has taught the programming community: First, comment everything you think you might not remember in six months. Then go back and comment everything you think you will.