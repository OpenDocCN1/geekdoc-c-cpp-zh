# # Chapter 7: Referring to Your Data Through Pointers

# ### In This Chapter

+   - Using two types of memory: the stack and the heap
+   - Accessing variable addresses through pointers
+   - Creating variables on the heap by using the `new` keyword
+   - Taking pointers as parameters and returning pointers
+   - Modifying variables the easy way

Where do you live? Don't say it out loud, because thousands of people are reading this book and you don't want them all to know. So just think about your address. Most places have some sort of address so that the mail service knows where to deliver your packages and the cable guy can show up sometime between now and 5:00 next Thursday. (So make sure that you're there.)

Other things have addresses, too. For example, a big corporation in an office building likely has all its cubes numbered. And offices in buildings usually have numbers; and apartments normally have numbers, too.

Now suppose that someone named Sam works in office number 180. Last week, however, Sam got booted out the door for spending too much time surfing the web. Now Sally gets first dibs on office number 180, even though she's not taking over Sam's position. Sam moved out; Sally moved in. Same office — different person staying there.

The computer's memory works similarly. Every little part of the computer's memory is associated with a number that represents its location, or *address*. In this chapter, we show you that after you determine the address of a variable stored in memory, you can do powerful things with it, which gives you the tools to create powerful applications.

![](bbox=[0.113, 0.873, 0.168, 0.921])

If any single topic in C++ programming is most important, it is the notion of pointers. Therefore, if you want to become a millionaire, read this chapter. Okay, so it may not make you a millionaire, but suggesting it *could* give you the incentive to master this chapter. Then you can become an ace programmer and make lots of money.