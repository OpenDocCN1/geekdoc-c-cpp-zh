# 17.3 Scaladoc Comments

You were introduced to Scala comments back in chapter 3. Through most of the book we have not been all that particular about putting comments into the code as descriptions of the code were part of the text. With the move to doing larger, object-oriented projects there is another reason for including comments. The comments you have been using previously, with // for a single line comment and /* followed by */ for a multiline comment, were passive. You would put them in the code to help remind yourself what a piece of code was doing. If you had been working on code with a group of people, those comments could have been useful for letting other people understand your code. Such comments can be very helpful, but they are also prone to certain risks. The risk is that if programmers are not extremely diligent, the comments can get out of sync with the code. This can lead to significant confusion and cause real problems. For this reason, there are many programmers who try not to rely too much on comments to explain their code and instead try to make the code "self-documenting". This is done by choosing variable and method names that reflect what is happening and breaking problems down in ways that make them more readable.

Now that you are writing full classes and objects, there is another factor to consider with comments, external documentation. The point of comments up to this point has just been for the benefit of programmers looking at that source code. Hopefully people who have access to the code in this way know how to read it and can figure out many things from the code. classes and objects can be part of libraries that will be called upon by people who do not have access to your code or who really should not be expected to go through your code to figure out what it does. This type of thing is so common that there is special formatting for comments that support documentation that is intended to be used without the code. This is not a completely new concept. The Application Programming Interface (API) documentation that you have been using for quite a while now works in exactly this way. You need to know what types are in the libraries and what members those types have as well as how you can use them. The API tells you that without you having to go through the code to find it. The API is created by putting comments in the code that have a specific format, then running a program called scaladoc to generate web pages.

You can insert your own scaladoc style comments in your code and generate web pages from them. While these comments are just as likely to get out of sync with the code as normal comments, these serve a more active purpose for outside documentation and, as such, warrant the effort that is required to maintain them.

A scaladoc comment is just like a multiline comment except that the opening has an extra asterisk. So you open the comment with /**. This still starts with /* so the compiler will ignore it like any other multiline comment. However, his opening tells the scaladoc tool that the contents are related to the thing that follows the comment. You should put scaladoc comments directly above the class/object/method/member that the comment modifies. This code shows an example.

```
/**
* This is an object where I am putting math functions.
*
* If I had more to say about this object I could put that here. You can
* use HTML tags if you want. To show code use triple curly braces.
* {{{ val a=5 }}}
*/
object MathFuncs {
/**
```