# # CHAPTER 3 Scalars and Strings

and then try to compile, you are likely to face a long list of errors, and you deprive yourself of the positive feedback an interpreter (or compiler) can provide when you work in an incremental, iterative way.

![](bbox=[0.176, 0.185, 0.642, 0.334])

# ## Figure 3.3

Press F9 to compile; if you meet with success, add a few more lines.

To preserve space, in most of the code examples presented in this book, you do not see the bang and content-type lines. These lines remain in many of the programs that you download from the book’s Internet site.

# # Fundamental Programming Syntax

Among the most elementary items of syntax you use when programming with Perl are those you use to create comments, make statements, force new lines, and escape from regular program interpretation so that you can display special characters. This section reviews these items.

# ## Comments Using #

The pound sign (#) provides a way that you can tell the Perl interpreter to skip over notes you include in a program. Such notes are referred to as _comments_. Comments are not part of the code. Any line that begins with a pound sign is considered a comment.

The interpreter reads from left to right. For this reason, if you want to make it so that the interpreter does not read a line of text you have included in your program, you type the pound sign as the first character at which you want the interpreter to stop reading. From that point on, until the interpreter reaches the end-of-line character, it does not try to interpret anything you have typed as Perl code. Consider the following sample of code:

```
```
#Listing03_04
#Comments proceeded to the end-of-line character
#You press Enter to insert an EOL character
print "\nListing03_04.pl works."; #Comments can follow code
print "\nReady to add lines!";
```
```