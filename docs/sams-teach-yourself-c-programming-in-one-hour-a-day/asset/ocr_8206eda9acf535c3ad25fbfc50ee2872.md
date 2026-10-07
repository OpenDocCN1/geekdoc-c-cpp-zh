itself a pointer (to a string), the argument is, therefore, a pointer to a pointer. Within the
function itself, you dereference the pointers so that the return value of comp() depends
on the values of the strings pointed to.

The fact that the arguments passed to comp() are pointers creates another
problem. You store the search key in buf(), and you also know that the value of an array
(buf in this case) is a pointer to the array. However, you need to not buf itself but
p pointer to buf. The problem is that buf is a constant, not a variable. buf
elf has no address in memory; it's a symbol that evaluates to the address of the array.
Because of this, you can't create a pointer that points to buf by using the address-of
operator in front of buf, as &buf.

What to do? First, create a pointer variable and assign the value of buf to it. In the
program, this pointer variable has the name key. Because key is a pointer variable, it
an address, and you can create a pointer that contains that—in this case, key1.
When you call bsearch(), the first argument is key1, a pointer to a pointer to the
key string. The function bsearch() passes that argument to comp(), and everything
works properly.

| DO | DON'T |
|---|---n| DO check your compiler's ANSI documentation to see the other standard functions you can use. | DON'T forget to put your search array into ascending order before using bsearch(). |

# # Summary

In this lesson, you explored some of the more useful functions supplied in the C function
library. There are functions that perform mathematical calculations, deal with time, and
assist your program with error-handling. The functions for sorting and searching data are
particularly useful; they can save you considerable time when you write your programs.

# # Q&A

+   Why do nearly all the math functions return double?

The answer to this question is to achieve precision, not consistency. A double is
more precise than the other variable types; yours are more accu-
rate. In Lesson 21, "Working with Memory," you learn the specifics of casting
variables and variable promotion. These topics are also applicable to precision.