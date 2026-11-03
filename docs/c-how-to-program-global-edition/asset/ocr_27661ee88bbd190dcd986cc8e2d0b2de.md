| Recursion examples and exercises |  |
|---|---|
| *Chapter 5* | *Chapter 7* |
| Factorial function | Maze traversal |
| Fibonacci function | *Chapter 8* |
| Greatest common divisor | Printing a string input at the keyboard backward |
| Multiply two integers | *Chapter 12* |
| Raising an integer to an integer power | Search a linked list |
| Towers of Hanoi | Print a linked list backward |
| Recursive main | Binary tree insert |
| Visualizing recursion | Preorder traversal of a binary tree |
| *Chapter 6* | Inorder traversal of a binary tree |
| Sum of the elements of an array | Postorder traversal of a binary tree |
| Print an array | Printing trees |
| Print an array backward | *Appendix D* |
| Print a string backward | Selection sort |
| Check whether a string is a palindrome | Quicksort |
| Minimum value in an array | *Appendix E* |
| Linear search | Fibonacci function |
| Binary search |  |
| Eight Queens |  |

Fig. 5.21 | Recursion examples and exercises in the text.

# Performance Tip 5.2

Dividing a large program into functions promotes good software engineering. But it has a price. A heavily functionalized program—as compared to a monolithic (i.e., one-piece) program without functions—makes potentially large numbers of function calls, and these consume execution time on a computer’s processor(s). Although monolithic programs may perform better, they’re more difficult to program, test, debug, maintain, and evolve.

# Performance Tip 5.3

Today’s hardware architectures are tuned to make function calls efficient, C compilers help optimize your code and today’s hardware processors are incredibly fast. For the vast majority of applications and software systems you’ll build, concentrating on good software engineering will be more important than programming for high performance. Nevertheless, in many C applications and systems, such as game programming, real-time systems, operating systems and embedded systems, performance is crucial, so we include performance tips throughout the book.

# 5.17 Secure C Programming

# Secure Random Numbers

In Section 5.10, we introduced the rand function for generating pseudorandom numbers. The C standard library does not provide a secure random-number generator. According to the C standard document’s description of function rand, “There are no guarantees as to the