Cross-Reference Use of endline comments to mark ends of blocks is described further in “Commenting Control Structures,” later in this section.

Use endline comments to mark ends of blocks An endline comment is useful for marking the end of a long block of code—the end of a while loop or an if statement, for example. This is described in more detail later in this chapter.

Aside from a couple of special cases, endline comments have conceptual problems and tend to be used for code that’s too complicated. They are also difficult to format and maintain. Overall, they’re best avoided.

# Commenting Paragraphs of Code

Most comments in a well-documented program are one-sentence or two-sentence comments that describe paragraphs of code:

```
Java Example of a Good Comment for a Paragraph of Code
// swap the roots
oldRoot = root[0];
root[0] = root[1];
root[1] = oldRoot;
```

The comment doesn’t repeat the code—it describes the code’s intent. Such comments are relatively easy to maintain. Even if you find an error in the way the roots are swapped, for example, the comment won’t need to be changed. Comments that aren’t written at the level of intent are harder to maintain.

Write comments at the level of the code’s intent Describe the purpose of the block of code that follows the comment. Here’s an example of a comment that’s ineffective because it doesn’t operate at the level of intent:

Cross-Reference This code that performs a simple string search is used only for purposes of illustration. For real code, you’d use Java’s built-in string library functions instead. For more on the importance of understanding your language’s capabilities, see “Read!” in Section 33.3.

```
Java Example of an Ineffective Comment
/* check each character in "inputString" until a dollar sign is found or all characters have been checked */
done = false;
maxLen = inputString.length();
i = 0;
while ( !done && ( i < maxLen ) ) {
    if ( inputString[ i ] == '$' ) {
        done = true;
    }
    else {
        i++;
    }
}
```

You can figure out that the loop looks for a $ by reading the code, and it’s somewhat helpful to have that summarized in the comment. The problem with this comment is