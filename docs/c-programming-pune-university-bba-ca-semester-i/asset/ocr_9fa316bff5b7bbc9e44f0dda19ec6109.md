When the program is executed, the function factorial will be accessed repeatedly, once in main and (n - 1) times within itself, though the person using the program will not be aware of this. Only the final answer will be displayed; for example,

n! = 3628800

When a recursive program is executed, the recursive function calls are not executed immediately. Rather, they are placed on a *stack* until the condition that terminates the recursion is encountered.* The function calls are then executed in reverse order, as they are "popped" off the stack. Thus, when evaluating a factorial recursively, the function calls will proceed in the following order.

n! = n x (n - 1)!
(n - 1)! = (n - 1) x (n - 2)!
(n - 2)! = (n - 2) x (n - 3)!
2! = 2 x 1!

The actual values will then be returned in the following reverse order.

1! = 1
2! = 2 x 1! = 2 x 1 = 2
3! = 3 x 2! = 3 x 2 = 6
4! = 4 x 3! = 4 x 6 = 24
n! = n x (n - 1)! = ...

This reversal in the order of execution is a characteristic of all functions that are executed recursively.

![](bbox=[0.3, 0.53, 0.7, 0.85])