The functions you need are those in the ajStrAppend* family. You’ll see that some of the functions accept other string objects, character strings or just single characters.

This search method is of course limited by the vocabulary used in the function descriptions. For instance, the term “append” is used rather than “catenate”. You can see this for yourself by repeating the above search using catenate & string.

To show the advantage of limiting the search:

+   Change the Description field back to AllText and repeat the string & append query.

You’ll see that there is a significant amount of noise in the results list.

Of course you can use SRS if you know the name of a function and need to examine the source code.

+   1. Return to the EFUNC page and change AllText to ID.

+   2. Now use ajstrappend as the search term. Perform the search and then click on EFUNC: ajStrAppends.

You should see the source code for ajStrAppendS on screen. Again, the output is in several sections. The name of the function indicates the source library file in which it is to be found; the str of ajStrAppendS indicates the ajstr library. The description field gives the text you search with a Description search.

The most useful information for a user of the library are the Input, Returns and Prototype fields.

The Input field shows that this function takes the address of a string object pointer as its first parameter and a string object pointer as its second parameter. The Returns field shows the return value of the function (AjBool, a boolean value). All this information is given at a glance in the Prototype field for the function.

Below the prototype is the body of the function. This patently contains the source code of the function. C language reserved words are highlighted in red. The source code is marked up with any calls to other EMBOSS functions. Unhighlighted function calls are standard C library calls. You could click on, for example, ajFatal and see the code for that function.

Clicking on the red arrow on the prototype line will show all the EMBOSS functions that use this particular function. Clicking on the blue arrow will show all the EMBOSS functions that are called by this particular function.

# 1.3.5 Demonstration applications

EMBOSS includes, for certain AJAX and NUCLEUS library files, an application which illustrates the correct usage of the common functions. Currently, these ‘demonstration applications’ are kept in the myembossdemo package and have the prefix “demo”. For example the following files illustrates the use of the string library:

```
/home/auser/emboss/emboss/embassy/myembossdemo/emboss src/demostring.c
/home/auser/emboss/emboss/embassy/myembossdemo/emboss_acd/demostring.acd
```

For information on compiling and using these applications see Section 3.1, ‘EMBOSS programming’.