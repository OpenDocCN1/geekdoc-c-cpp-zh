# Chapter 17

# # Unusual Control Structures

# ## Contents

+   - 17.1 Multiple Returns from a Routine: page 391
+   - 17.2 Recursion: page 393
+   - 17.3 `goto`: page 398
+   - 17.4 Perspective on Unusual Control Structures: page 408

# ## Related Topics

+   - General control issues: Chapter 19
+   - Straight-line code: Chapter 14
+   - Code with conditionals: Chapter 15
+   - Code with loops: Chapter 16
+   - Exception handling: Section 8.4

Several control constructs exist in a hazy twilight zone somewhere between being leading-edge and being discredited and disproved—often in both places at the same time! These constructs aren’t available in all languages but can be useful when used with care in those languages that do offer them.

# ## 17.1 Multiple Returns from a Routine

Most languages support some means of exiting from a routine partway through the routine. The *return* and *exit* statements are control constructs that enable a program to exit from a routine at will. They cause the routine to terminate through the normal exit channel, returning control to the calling routine. The word *return* is used here as a generic term for *return* in C++ and Java, *Exit Sub* and *Exit Function* in Microsoft Visual Basic, and similar constructs. Here are guidelines for using the *return* statement:

![](bbox=[0.166, 0.791, 0.235, 0.849])

**Use a return when it enhances readability**  In certain routines, once you know the answer, you want to return it to the calling routine immediately. If the routine is defined in such a way that it doesn’t require any further cleanup once it detects an error, not returning immediately means that you have to write more code.