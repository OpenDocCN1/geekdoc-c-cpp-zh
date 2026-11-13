
## 3.6 The Stack ADT

A stack is a list with the restriction that insertions and deletions can be performed in only one position, namely, the end of the list, called the top.

### 3.6.1 Stack Model

The fundamental operations on a stack are push, which is equivalent to an insert, and pop, which deletes the most recently inserted element. The most recently inserted element can be examined prior to performing a pop by use of the top routine. A pop or top on an empty stack is generally considered an error in the stack ADT. On the other hand, running out of space when performing a push is an implementation limit but not an ADT error.

Stacks are sometimes known as LIFO (last in, first out) lists. The model depicted in Figure 3.23 signifies only that pushes are input operations and pops and tops are output. The usual operations to make empty stacks and test for emptiness are part of the repertoire, but essentially all that you can do to a stack is push and pop.

Figure 3.24 shows an abstract stack after several operations. The general model is that there is some element that is at the top of the stack, and it is the only element that is visible.

![](img/e449061a0cac9cafaefd979fab665b33_121_0.png)

Figure 3.23 Stack model: Input to a stack is by push; output is by pop and top

![](img/e449061a0cac9cafaefd979fab665b33_121_1.png)

Figure 3.24 Stack model: Only the top element is accessible

### 3.6.2 Implementation of Stacks

Since a stack is a list, any list implementation will do. Clearly `list` and `vector` support stack operations; 99% of the time they are the most reasonable choice. Occasionally it can be faster to design a special-purpose implementation. Because stack operations are constant-time operations, this is unlikely to yield any discernible improvement except under very unique circumstances.

For these special times, we will give two popular stack implementations. One uses a linked structure, and the other uses an array, and both simplify the logic in `vector` and `list`, so we do not provide code.

### Linked List Implementation of Stacks

The first implementation of a stack uses a singly linked list. We perform a push by inserting at the front of the list. We perform a pop by deleting the element at the front of the list. A top operation merely examines the element at the front of the list, returning its value. Sometimes the pop and top operations are combined into one.

### Array Implementation of Stacks

An alternative implementation avoids links and is probably the more popular solution. It uses the `back`, `push_back`, and `pop_back` implementation from `vector`, so the implementation is trivial. Associated with each stack is `theArray` and `topOfStack`, which is -1 for an empty stack (this is how an empty stack is initialized). To push some element `x` onto the stack, we increment `topOfStack` and then set `theArray[topOfStack] = x`. To pop, we set the return value to `theArray[topOfStack]` and then decrement `topOfStack`.

Notice that these operations are performed in not only constant time but very fast constant time. On some machines, `pushes` and `pops` (of integers) can be written in one machine instruction, operating on a register with auto-increment and auto-decrement addressing. The fact that most modern machines have stack operations as part of the instruction set enforces the idea that the stack is probably the most fundamental data structure in computer science, after the array.

### 3.6.3 Applications

It should come as no surprise that if we restrict the operations allowed on a list, those operations can be performed very quickly. The big surprise, however, is that the small number of operations left are so powerful and important. We give three of the many applications of stacks. The third application gives a deep insight into how programs are organized.

### Balancing Symbols

Compilers check your programs for syntax errors, but frequently a lack of one symbol (such as a missing brace or comment starter) can cause the compiler to spill out a hundred lines of diagnostics without identifying the real error.

A useful tool in this situation is a program that checks whether everything is balanced. Thus, every right brace, bracket, and parenthesis must correspond to its left counterpart.

The sequence [()] is legal, but [(] is wrong. Obviously, it is not worthwhile writing a huge program for this, but it turns out that it is easy to check these things. For simplicity, we will just check for balancing of parentheses, brackets, and braces and ignore any other character that appears.

The simple algorithm uses a stack and is as follows:

Make an empty stack. Read characters until end of file. If the character is an opening symbol, push it onto the stack. If it is a closing symbol and the stack is empty, report an error. Otherwise, pop the stack. If the symbol popped is not the corresponding opening symbol, then report an error. At end of file, if the stack is not empty, report an error.

You should be able to convince yourself that this algorithm works. It is clearly linear and actually makes only one pass through the input. It is thus online and quite fast. Extra work can be done to attempt to decide what to do when an error is reported—such as identifying the likely cause.

### Postfix Expressions

Suppose we have a pocket calculator and would like to compute the cost of a shopping trip. To do so, we add a list of numbers and multiply the result by 1.06; this computes the purchase price of some items with local sales tax added. If the items are 4.99, 5.99, and 6.99, then a natural way to enter this would be the sequence

4.99 + 5.99 + 6.99 * 1.06 =

Depending on the calculator, this produces either the intended answer, 19.05, or the scientific answer, 18.39. Most simple four-function calculators will give the first answer, but many advanced calculators know that multiplication has higher precedence than addition.

On the other hand, some items are taxable and some are not, so if only the first and last items were actually taxable, then the sequence

4.99 * 1.06 + 5.99 + 6.99 * 1.06 =

would give the correct answer (18.69) on a scientific calculator and the wrong answer (19.37) on a simple calculator. A scientific calculator generally comes with parentheses, so we can always get the right answer by parenthesizing, but with a simple calculator we need to remember intermediate results.

A typical evaluation sequence for this example might be to multiply 4.99 and 1.06, saving this answer as A1. We then add 5.99 and A1, saving the result in A1. We multiply 6.99 and 1.06, saving the answer in A2, and finish by adding A1 and A2, leaving the final answer in A1. We can write this sequence of operations as follows:

4.99 1.06 * 5.99 + 6.99 1.06 * +

This notation is known as postfix, or reverse Polish notation, and is evaluated exactly as we have described above. The easiest way to do this is to use a stack. When a number is seen, it is pushed onto the stack; when an operator is seen, the operator is applied to the two numbers (symbols) that are popped from the stack, and the result is pushed onto the stack. For instance, the postfix expression

```
6 5 2 3 + 8 + 3 + *
```

is evaluated as follows:

The first four symbols are placed on the stack. The resulting stack is

![](img/e449061a0cac9cafaefd979fab665b33_124_0.png)

Next, a ‘+’ is read, so 3 and 2 are popped from the stack, and their sum, 5, is pushed.

![](img/e449061a0cac9cafaefd979fab665b33_124_1.png)

Next, 8 is pushed.

![](img/e449061a0cac9cafaefd979fab665b33_124_2.png)

Now a ‘*’ is seen, so 8 and 5 are popped, and 5 * 8 = 40 is pushed.

![](img/e449061a0cac9cafaefd979fab665b33_124_3.png)

Next, a ‘+’ is seen, so 40 and 5 are popped, and 5 + 40 = 45 is pushed.

| topOfStack -> | 45 |
|---|---|
| | 6 |

Now, 3 is pushed.

| topOfStack -> | 3 |
|---|---|
| | 45 |
| | 6 |

Next, ‘+’ pops 3 and 45 and pushes 45 + 3 = 48.

| topOfStack -> | 48 |
|---|---|
| | 6 |

Finally, a ‘*’ is seen and 48 and 6 are popped; the result, 6 * 48 = 288, is pushed.

| topOfStack -> | 288 |
|---|---|

The time to evaluate a postfix expression is O(N), because processing each element in the input consists of stack operations and therefore takes constant time. The algorithm to do so is very simple. Notice that when an expression is given in postfix notation, there is no need to know any precedence rules; this is an obvious advantage.
