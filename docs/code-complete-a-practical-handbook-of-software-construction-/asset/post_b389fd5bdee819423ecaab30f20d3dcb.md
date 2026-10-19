
If this comment documents the whole block of code following the if test, it serves as a summary-level comment and it’s appropriate to retain it as a section heading for the paragraph of code it references.

## Use comments to prepare the reader for what is to follow

Good comments tell the person reading the code what to expect. A reader should be able to scan only the comments and get a good idea of what the code does and where to look for a specific activity. A corollary to this rule is that a comment should always precede the code it describes. This idea isn’t always taught in programming classes, but it’s a well-established convention in commercial practice.

## Make every comment count

There’s no virtue in excessive commenting—too many comments obscure the code they’re meant to clarify. Rather than writing more comments, put the extra effort into making the code itself more readable.

## Document surprises

If you find anything that isn’t obvious from the code itself, put it into a comment. If you have used a tricky technique instead of a straightforward one to improve performance, use comments to point out what the straightforward technique would be and quantify the performance gain achieved by using the tricky technique. Here’s an example:

### C++ Example of Documenting a Surprise

```cpp
for ( element = 0; element < elementCount; element++ ) {
    // Use right shift to divide by two. Substituting the
    // right-shift operation cuts the loop time by 75%.
    elementList[ element ] = elementList[ element ] >> 1;
}
```

The selection of the right shift in this example is intentional. Among experienced programmers, it’s common knowledge that for integers, right shift is functionally equivalent to divide-by-two.

If it’s common knowledge, why document it? Because the purpose of the operation is not to perform a right shift; it is to perform a divide-by-two. The fact that the code doesn’t use the technique most suited to its purpose is significant. Moreover, most compilers optimize integer division-by-two to be a right shift anyway, meaning that the reduced clarity is usually unnecessary. In this particular case, the compiler evidently doesn’t optimize the divide-by-two, and the time saved will be significant. With the documentation, a programmer reading the code would see the motivation for using the nonobvious technique. Without the comment, the same programmer would be inclined to grumble that the code is unnecessarily “clever” without any meaningful gain in performance. Usually such grumbling is justified, so it’s important to document the exceptions.

## Avoid abbreviations

Comments should be unambiguous, readable without the work of figuring out abbreviations. Avoid all but the most common abbreviations in comments. Unless you’re using endline comments, using abbreviations isn’t usually a temptation. If you are, and it is, realize that abbreviations are another strike against a technique that struck out several pitches ago.

## Differentiate between major and minor comments

In a few cases, you might want to differentiate between different levels of comments, indicating that a detailed comment is part of a previous, broader comment. You can handle this in a couple of ways. You can try underlining the major comment and not underlining the minor comment:

### C++ Example of Differentiating Between Major and Minor Comments with Underlines—Not Recommended

```cpp
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

### C++ Example of Differentiating Between Major and Minor Comments with Ellipses

```cpp
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

Another approach that’s often best is to put the major-comment operation into its own routine. Routines should be logically “flat,” with all their activities on about the same logical level. If your code differentiates between major and minor activities within a routine, the routine isn’t flat. Putting the complicated group of activities into its own routine makes for two logically flat routines instead of one logically lumpy one.

This discussion of major and minor comments doesn’t apply to indented code within loops and conditionals. In such cases, you’ll often have a broad comment at the top of the loop and more detailed comments about the operations within the indented code. In those cases, the indentation provides the clue to the logical organization of the comments. This discussion applies only to sequential paragraphs of code in which several paragraphs make up a complete operation and some paragraphs are subordinate to others.

## Comment anything that gets around an error or an undocumented feature in a language or an environment

If it’s an error, it probably isn’t documented. Even if it’s documented somewhere, it doesn’t hurt to document it again in your code. If it’s an undocumented feature, by definition it isn’t documented elsewhere and it should be documented in your code.

Suppose you find that the library routine `WriteData( data, numItems, blockSize )` works properly except when `blockSize` equals 500. It works fine for 499, 501, and every other value you’ve ever tried, but you’ve found that the routine has a defect that appears only when `blockSize` equals 500. In code that uses `WriteData()`, document why you’re making a special case when `blockSize` is 500. Here’s an example of how it could look:

### Java Example of Documenting the Workaround for an Error

```java
blockSize = optimalBlockSize( numItems, sizePerItem );

/* The following code is necessary to work around an error in
WriteData() that appears only when the third parameter
equals 500. *500* has been replaced with a named constant
for clarity.
*/
if ( blockSize == WRITEDATA_BROKEN_SIZE ) {
    blockSize = WRITEDATA_WORKAROUND_SIZE;
}
WriteData( file, data, blockSize );
```

## Justify violations of good programming style

If you’ve had to violate good programming style, explain why. That will prevent a well-intentioned programmer from changing the code to a better style, possibly breaking your code. The explanation will make it clear that you knew what you were doing and weren’t just sloppy—give yourself credit where credit is due!

## Don’t comment tricky code; rewrite it

Here’s a comment from a project I worked on:

![](img/649c8eee28c38ca1e062691e45dc9883_837_0.png)

### C++ Example of Commenting Clever Code

```cpp
// VERY IMPORTANT NOTE:
// The constructor for this class takes a reference to a UiPublication.
// The UiPublication object MUST NOT BE DESTROYED before the DatabasePublication
// object. If it is, the DatabasePublication object will cause the program to
// die a horrible death.
```

This is a good example of one of the most prevalent and hazardous bits of programming folklore: that comments should be used to document especially “tricky” or “sensitive” sections of code. The reasoning is that people should know they need to be careful when they’re working in certain areas.

This is a scary idea.

Commenting tricky code is exactly the wrong approach to take. Comments can’t rescue difficult code. As Kernighan and Plauger emphasize, “Don’t document bad code—rewrite it” (1978).

![](img/649c8eee28c38ca1e062691e45dc9883_837_1.png)

One study found that areas of source code with large numbers of comments also tended to have the most defects and to consume the most development effort (Lind and Vairavan 1989). The authors hypothesized that programmers tended to comment difficult code heavily.

![](img/649c8eee28c38ca1e062691e45dc9883_837_2.png)

When someone says, “This is really *tricky* code,” I hear them say, “This is really bad code.” If something seems tricky to you, it will be incomprehensible to someone else. Even something that doesn’t seem all that tricky to you can seem impossibly convoluted to another person who hasn’t seen the trick before. If you have to ask yourself “Is this tricky?” it is. You can always find a rewrite that’s not tricky, so rewrite the code. Make your code so good that you don’t need comments, and then comment it to make it even better.

This advice applies mainly to code you’re writing for the first time. If you’re maintaining a program and don’t have the latitude to rewrite bad code, commenting the tricky parts is a good practice.
