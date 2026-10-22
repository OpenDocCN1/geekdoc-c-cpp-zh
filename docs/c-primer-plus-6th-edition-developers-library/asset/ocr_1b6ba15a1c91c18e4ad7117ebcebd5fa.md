standard form, and you won’t run into problems if you move a program from one compiler to another.

# Comments

```
/* a simple program */
```

The parts of the program enclosed in the /* */ symbols are comments. Using comments makes it easier for someone (including yourself) to understand your program. One nice feature of C comments is that they can be placed anywhere, even on the same line as the material they explain. A longer comment can be placed on its own line or even spread over more than one line. Everything between the opening /* and the closing */ is ignored by the compiler. The following are some valid and invalid comment forms:

```
/* This is a C comment. */
/* This comment, being somewhat wordy, is spread over
two lines. */
/*
    You can do this, too.
*/
/* But this is invalid because there is no end marker.
```

C99 added a second style of comments, one popularized by C++ and Java. The new style uses the symbols // to create comments that are confined to a single line:

```
// Here is a comment confined to one line.
int rigue;      // Such comments can go here, too.
```

Because the end of the line marks the end of the comment, this style needs comment markers just at the beginning of the comment.

The newer form is a response to a potential problem with the old form. Suppose you have the following code:

```
/*
I hope this works.
*/
x = 100;
y = 200;
/* Now for something else. */
```

Next, suppose you decide to remove the fourth line and accidentally delete the third line (the */), too. The code then becomes

```
/*
I hope this works.
y = 200;
/* Now for something else. */
```