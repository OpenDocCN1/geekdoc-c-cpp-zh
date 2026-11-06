# Chapter 2: Creating Data Structures

# In This Chapter

+   - Discovering all the different data types
+   - Casting and converting
+   - Using structures with your data
+   - Comparing and manipulating structures

C++, being a computer language and all, provides you with a lot of ways to manipulate data — numbers, letters, strings, arrays — anything you can store inside the computer memory. To get the most out of C++, you should know as much as you can about the fundamental data types. This chapter covers them and how to use them.

In this chapter, we refer to the *ANSI standard* of C++. ANSI is the American National Standards Institute. The information we provide in this chapter deals with the ANSI standard (singular) of C++. Fortunately, the GNU gcc compiler that comes with Code::Blocks is ANSI-standard-compliant. (Little nuances show up, but not often.)

# Working with Data

In the sections that follow, we tell you how you can manipulate your data, discuss the types of data available to you, and point out how you can change them.

# The great variable roundup

The ANSI C++ standard dictates these fundamental C++ types:

+   - `char`: This is a single character. On most computers, it takes 1 byte.
+   - `int`: This is an integer. On most computers from the late 1990s until now, a single integer takes 4 bytes — which gives you a range from −2147483648 to 2147483647.
+   - `short int`: This is a half-size integer. Just a little 2-byte fellow, which leaves just enough room for −32768 to 32767.