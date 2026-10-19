# Avoid abbreviations

Comments should be unambiguous, readable without the work of figuring out abbreviations. Avoid all but the most common abbreviations in comments. Unless you’re using endline comments, using abbreviations isn’t usually a temptation. If you are and it is, realize that abbreviations are another strike against a technique that struck out several pitches ago.

# Differentiate between major and minor comments

In a few cases, you might want to differentiate between different levels of comments, indicating that a detailed comment is part of a previous, broader comment. You can handle this in a couple of ways. You can try underlining the major comment and not underlining the minor comment:

# C++ Example of Differentiating Between Major and Minor Comments with Underlines—Not Recommended

```
// copy the string portion of the table, along the way omitting
// strings that are to be deleted
//---------------------------------------------------------------
// determine number of strings in the table
...
// mark the strings to be deleted
...
```

The major comment is underlined.

A minor comment that’s part of the action described by the major comment isn’t underlined here...

...or here.

The weakness of this approach is that it forces you to underline more comments than you’d really like to. If you underline a comment, it’s assumed that all the nonunderlined comments that follow it are subordinate to it. Consequently, when you write the first comment that isn’t subordinate to the underlined comment, it too must be underlined and the cycle starts all over. The result is too much underlining or inconsistent underlining in some places and no underlining in others.

This theme has several variations that all have the same problem. If you put the major comment in all caps and the minor comments in lowercase, you substitute the problem of too many all-caps comments for too many underlined comments. Some programmers use an initial cap on major statements and no initial cap on minor ones, but that’s a subtle visual cue too easily overlooked.

A better approach is to use ellipses in front of the minor comments:

# C++ Example of Differentiating Between Major and Minor Comments with Ellipses

```
// copy the string portion of the table, along the way omitting
// strings that are to be deleted
// ... determine number of strings in the table
...
// ... mark the strings to be deleted
...
```

The major comment is formatted normally.

A minor comment that’s part of the action described by the major comment is preceded by an ellipsis here...

...and here.