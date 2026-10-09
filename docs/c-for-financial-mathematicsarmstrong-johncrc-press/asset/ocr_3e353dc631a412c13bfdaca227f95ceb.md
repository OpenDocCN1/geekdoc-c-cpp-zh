# Chapter 11

# Arrays, Strings, and Pointers

One useful way to view C++ is as a collection of languages:

+   (i) the C language;

(ii) an object-oriented programming language;

(iii) a template programming language.

This chapter is about some of the C language aspects of C++. We have ignored them so far, because you should focus your efforts on the object-oriented features of C++. Similarly we will not discuss the template programming features until Chapter 17.

Pointers are a central feature of the C language. They are a tool for directly manipulating computer memory. You will not find them in a more modern pure object-oriented programming language like Java. The feature is omitted from other languages because pointer-based programs are typically harder to understand than object-oriented programs.

Most of what you learn in this chapter you should never use directly. The only thing you need to use is `shared_ptr`. We will discuss this towards the end of the chapter. Unfortunately, to understand `shared_ptr` you must first understand ordinary pointers.

There are three other motivations for studying the material in this chapter.

+   (i) The first is that C++ was originally designed for people with C programming experience. So some C++ code is designed to be intuitive to use if you have experience with C pointers. If you don't study pointers, you will find things like the C++ standard library very unintuitive.

(ii) The second is that job interviewers may assume that you know C and so may ask some trick questions about pointers, so it is good to be prepared!

(iii) The third is that to write maximally efficient C++ programs it can be helpful to manage memory consciously. Pointers are a tool for direct memory manipulation.

Because this chapter and the next are more about C programming than object-oriented programming, we've temporarily abandoned developing FM-Lib for this chapter. Instead the project `PointerExamples.zip` contains all code for this chapter.