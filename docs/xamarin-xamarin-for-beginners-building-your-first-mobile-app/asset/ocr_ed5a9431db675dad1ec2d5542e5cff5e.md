# # The concept of navigating between application pages

Navigating between application pages is very similar to the principle that Stack works. The stack is known as a data structure that supports the concept of LIFO (which finally comes out first). When you move from page A to page B, page B is pushed to the top of the stack, resulting in the user appearing. Similarly, when you move from page B to page C, page C is pushed to the stack to be shown to the user. When we want to return to the original page A, popped page C should be removed from the stack, page B will be at the top of the stack (i.e. it will appear to the user), and page B will be removed from the stack and page A will be at the top of the stack. See the following figure to illustrate this idea:

![](bbox=[0.05, 0.4, 0.95, 0.88])

Modal and Modeless Pages: