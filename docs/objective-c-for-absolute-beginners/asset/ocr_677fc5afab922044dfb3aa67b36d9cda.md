# Chapter 7

# # Objective-C Classes, Objects, and Methods

If you haven't already read Chapter 6, please do so before reading this one, because it provides a great introduction to some of the basics of Objective-C. This chapter builds on that foundation a bit more. By the end of this chapter, you can expect to have a greater understanding of the Objective-C language and how to use the basics to write simple programs. For Mitch, the best way to learn is to take small programs and write (or rewrite) them in Objective-C just to see how the language works.

This chapter will cover what an Objective-C class is and how to interact with Objective-C objects via methods. We will use a simple radio station class as an example of how an Objective-C class is written. This will hopefully impart an understanding of how an Objective-C class can be used. This chapter will teach you how to formulate a design for objects that are needed to solve a problem. We'll touch on how to create custom objects, as well as how to use existing objects provided in the Foundation classes.

If you're coming from a C-like language, you'll find that Objective-C shares several similarities. As described in Chapter 6, Objective-C's roots are firmly planted in the C language. This chapter will expand on Chapter 6's topics and incorporate some of the concepts described in Chapter 8.

# # Creating an Objective-C Class

Chapter 6 introduced some of the common elements of the Objective-C language, so let's quickly review them.

+   - Objective-C class is divided into two parts: a class interface and class implementation.

+   - @interface: This keyword is used to define an interface to a new Objective-C class. This is written in an .h or header file.