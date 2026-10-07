# Q&A

# 555

compiler enables you to do almost anything, even things you shouldn’t! You can
overwrite one string with a bigger string as long as the new string’s length is equal
to or smaller than the original allocated space. However, if the new string
is bigger, you can also overwrite whatever came after the string in memory. This
could be nothing, or it could be vital. If you need a bigger allocated section of
memory, call `realloc()`.

+   What’s the advantage of the `memset()`, `memcpy()` and `memmove()` functions?
Why can’t I use a loop with an assignment statement to initialize or copy
memory?

+   You can use a loop with an assignment statement to initialize memory in some
cases. In fact, this is the only way to do it—for example, setting all
elements of a type `float` array to the value `1.23`. In other situations, however, the
memory will not have been assigned to an array list, and the `mem...()` functions
are your only choice. There are also times when a loop and assignment statement
work, but the `mem...()` functions are simpler and faster.

+   When will I use the shift operators and the bitwise operators?

+   A common use for these operators is when a program is interacting directly
with the computer hardware—a task that often requires specific bit patterns to be
generated and interpreted. This topic is beyond the scope of this book. Even if you
need to manipulate hardware directly, you can use the shift operators, in cer-
tstances, to divide or multiply integer values by powers of two.

+   Do I really gain that by using bit fields?

+   Yes, you can gain a bit with bit fields. (Pun intended!) Consider a circum-
stance similar to the example in this chapter in a file contains information
of a survey. People are asked to answer `TRUE` or `FALSE` to the questions. If
y ask 100 questions of 10,000 people and store each answer as a type `char` as T
or `F`, you will need 10,000 × 100 bytes of storage (because a character is 1 byte).
This is 1 million bytes. If you use bit fields instead and allocate 1 bit for
each answer, you need 10,000 × 100 bits. Because 1 byte holds 8 bits, this amounts
to 130,000 bytes of data, which is significantly less than 1 million bytes.

![](bbox=[0.923, 0.823, 0.954, 0.843])