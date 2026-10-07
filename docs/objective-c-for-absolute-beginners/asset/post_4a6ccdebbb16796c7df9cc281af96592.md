
# Chapter 6

## Learning Objective-C and Xcode

For the most part, all computer languages perform the typical tasks any computer needs to do—store information, compare information, make decisions about that information, and perform some action based on those decisions. Objective-C is a language that makes these tasks easier to understand and accomplish. The real trick with Objective-C (actually, the trick with any C language) is to understand the symbols and keywords used to accomplish those tasks. This chapter continues our examination of Objective-C and Xcode so you can become even familiar with them.

## A Brief History of Objective-C

Objective-C is a real combination of two languages, C language and a lesser-known language called Smalltalk. Back in the 1970s, very bright engineers from Bell Labs created a language named C that made it easy to port their pet project, the Unix operating system, from one machine to another. Prior to C, people had to write programs in assembly. The problem with assembly languages is that each is specific to its machine, moving software from one machine to another was nearly impossible. The C language, created by Brian Kernighan and Dennis Ritchie, solved this problem by providing a language that wrote out the assembly language for whatever it supported, a kind of Rosetta Stone for early computer languages. Because of its portability, C quickly became the *de facto* language for many types of computers, especially early PCs.

Fast forward to the early 1980s and the C language is on its way to becoming one of the most popular languages of the decade. Around this time, an engineer from a company called Stephenson was mixing the C language with another called Smalltalk. The C Language is typically referred to as a *procedural language*, a language that uses procedures to divide up processing steps. Smalltalk, on the other hand, was something entirely different. An *object-oriented programming language*. Instead of processing things procedurally, it used programming objects to get its work done. This new superset of the C language became known as "C with Objects" or more commonly, Objective-C.

In 1985, Brad Cox sold the Objective-C language and trademark to NeXT Computer, Inc. NeXT was the brainchild of Steve Jobs, who had been fired from his own company, Apple Computer, that very year. NeXT used the Objective-C language to build the NEXTSTEP operating system and its suite of development tools. In fact, the Objective-C language gave NeXT a competitive advantage with all of its software. Programmers using NEXTSTEP and Objective-C could write programs faster than writing in the traditional C language. While the hardware part of Next computers never took off, the operating system and tools did. Interestingly, NeXT was purchased by Apple Computer in late 1996 with the intention of replacing its aging operating system, had in existence since the first Macintosh was developed in 1984. Four years after acquisition, what had had been NEXTSTEP reemerged as Mac OS X—with Objective-C at the heart of the system.

## Understanding the Language Symbols

Even though Objective-C integrates a great deal of object-oriented language, at the heart of Objective-C is C. Here are some of the symbols and language constructs used in Objective-C, some of which are part of the C language and most of which we've already encountered in one way or another. It's not important to know which are pure C or which are not; just know that the old and the newer symbols/constructs together make the Objective-C language.

- { This is the begin brace. It's used to begin what is commonly referred to a block of code. Blocks are used to define and surround a section of code and define its scope.
- } This is the end brace. It's used to end a block of code. Wherever there is a begin { }, there must always be an accompanying end { }.
- - (void)methodName This is how Objective-C method is defined. The word methodName of course can represent any name. The word (void) can also change. It represents what type of information the method represents. In this example, (void) indicates there is no data type associated with this method (data types were introduced in Chapter 3 and will be covered in more depth in later chapters). (void) could be replaced with something like (NSString*). This will be discussed further later on.
- * The asterisk (referred to as 'star' or 'splat') is used to represent what is called a pointer (see Chapter 13). All that's really important to know for now is that when you see something like NSString*, consider part of the name. NSString and NSString* are completely different.
- ; The semicolon character is used to end a line of code. The thing to remember about a semicolon is that they aren't used at the end of statements that control the flow of the program, that is, if, for, while, etc. You'll eventually understand the rules of where they go and don't go.
- [ These are called brackets and are used when sending a message to an Objective-C object. Chapter 7 covers more on this topic.
- @ While many people associate this with an e-mail address, the @ sign is used in Objective-C to identify an Objective-C directive. A directive is a special Objective-C command, such as @interface, @implementation or @property.
- # The pound sign (or octothorpe if you like trivia) is similar to the @ sign and is used to identify a C language directive, such as #import or #define. While originally part of the C language, the use of # is still found in nearly all Objective-C programs.

So, let's see an example of Objective-C code:

Line #1 represents an Objective-C method. The (void) indicates this method is not associated with a data type, and if invoked, would not send a value back to a caller.

Lines #2 and #5 are the braces that define block of code. This block is what defines the method. Every method has at least one block.

Line #3 defines an NSString* object and assigns it the value of @"Hello World". Remember, that @ is an Objective-C directive and is a quick way of defining a constant string object (recall that we first saw strings in Chapter 3).

Line #4 is a call to the NSLog method; it is not an object, so we can't send it to a message. Instead, we're passing the method to print the hello NSString* object.

While it does look a little cryptic to someone who is learning Objective-C, the simple and terse syntax doesn't take too much time to learn.

## Putting the “Objective” into Objective-C

The majority of what makes Objective-C, well, objective, is its basis in Smalltalk. Smalltalk is 100 percent object-oriented language and Objective-C borrows heavily from Smalltalk concepts. Here are a few of the high-level concepts borrowed from Smalltalk. Don't worry if some of these terms seem unfamiliar; they will be discussed in later chapters (Chapters 7 and 8).

- Pretty much everything is an object.
- Objects receive messages. In this context, the object is sometimes known as the receiver since it is receiving the message.
- Objects contain instance variables.
- Objects and instance variables have a defined scope.
- Classes hide an object's implementation.

> NOTE: As we saw in Chapter 5, the term class is used to represent, generically, the definition or type of an object. An object is what is created from the class. For example, an SUV is a class of vehicle. A class is a blueprint of sorts. A factory builds SUVs. The results are SUV objects that people drive. 

Well, for starters, in Objective-C is defined using two different sections, @interface and @implementation. The @interface section defines what messages the object can respond to and any instance variables the object will use. The @implementation section contains the actual code of the various messages from the @interface section.

Why is there a split between the interface and implementation? Well, Objective-C object is defined only once within a program. However, it might be used in many different areas of that program. Where the object is used, the program simply reads in, or imports, the interface; it would be inefficient if the code for that object needed to be replicated every time it was used.

> NOTE: It is a common convention to have an object's interface stored in an .h file and the implementation stored in an .m file. Both files are named after the object. So, if a Library object is to be defined, its interface would be Library.h and its implementation would be Library.m (remember that names are case-sensitive).

Let's look at a simple example of the complete definition of an Objective-C object called HelloWorld. Following is the interface file (HelloWorld.h).
