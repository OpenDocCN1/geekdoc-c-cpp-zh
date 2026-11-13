

## 算术表达式求值——设计

do an example by hand

Most of the program’s work will be carried out by a function that reads one line of input and evaluates that line as an arithmetic expression. To get a feel for the problem, let’s start by doing a simple example by hand.

Consider the following expression:

((6 + 9)/3)*(6 - 4))

If we evaluate this expression by hand, we might first evaluate the innermost expressions, (6 + 9) and (6 - 4), to produce the smaller expression:

((15/3)*2)

Next we would evaluate the expression (15/3) and replace this expression with its value of 5. That would leave us with the expression (5*2). Finally, we would evaluate this last operation to get the final answer of 10.

To convert this intuitive approach into a fully specified algorithm that can be implemented, we need to do things in a more systematic way: We need a specific way to find the expression to be evaluated next and a way to remember the results of our intermediate calculations.

First let us find a systematic way of choosing the next expression to be evaluated. (After that, we can worry about how we will keep track of the intermediate results.) We know that the expression to be evaluated first must be one of the innermost expressions—which is a subexpression that has just one operation. Let’s decide to evaluate the leftmost of these innermost expressions. For instance, in our example of

((6 + 9)/3)*(6 - 4))

the innermost expressions are (6 + 9) and (6 - 4), and the leftmost one of these is (6 + 9). If we evaluate this leftmost of the innermost expressions, we obtain

((15/3)*(6 - 4))

We could now go back and evaluate the other innermost expression (6 - 4), but why bother? There is a simpler approach that spares us the trouble of remembering any other expressions. After we evaluate the leftmost of the innermost expressions, we are left with another simpler arithmetic expression, namely ((15/3)*(6 - 4)), so we can simply repeat the process with this simpler expression. We again evaluate the leftmost of the innermost expressions of our new simpler expression. The entire process will look like the following:

- 1. 求值
  (((6 + 9)/3)*(6 - 4))
  中最内层表达式中最左边的一个，以产生更简单的表达式 ((15/3)*(6 - 4))。

- 2. 求值
  ((15/3) * (6 - 4))
  中最内层表达式中最左边的一个，以产生更简单的表达式 (5 * (6 - 4))。

- 3. 求值
  (5 * (6 - 4))
  中最内层表达式中最左边的一个，以产生更简单的表达式 (5 * 2)。

- 4. 求值
  (5 * 2)
  中最内层表达式中最左边的一个，以获得最终答案 10。

This method works fine with pencil and paper, but the function must read the input character at a time from left to right. How does the function find the leftmost of the innermost expressions? Look at the example on page 360. The end of the expression to be evaluated is always a right parenthesis, ')', and moreover, it is always the first right parenthesis. After evaluating one of these innermost expressions, there is no need to back up; to find the next right parenthesis we can just keep reading left to right from where we left off. The next right parenthesis will indicate the end of the next expression to be evaluated.

> 将手动方法转换为算法

Now we know how to find the expression to be evaluated next, but how do we keep track of our intermediate values? For this we use two stacks. One stack will contain numbers; there will be numbers from the input as well as numbers that were computed when subexpressions were evaluated. The other stack will hold symbols for the operations that still need to be evaluated. Because a stack processes data in a Last-In/First-Out manner, it will turn out that the correct two numbers are on the top of the numbers stack at the same time that the appropriate operation is at the top of the stack of operations. To better understand how the process works, let's evaluate our sample expression one more time, this time using the two stacks.

We begin by reading up to the first right parenthesis; the numbers we encounter along the way are pushed onto the numbers stack, and the operations we encounter along the way are pushed onto the operations stack. When we reach the first right parenthesis, our two stacks look like this:

![](img/7bf56f684fab50d5ff9e94ae2818f3ac_388_0.png)

Whenever we reach a right parenthesis, we combine the top two numbers (on the numbers stack) using the topmost operation (on the characters stack). In our example, we compute 6 + 9, yielding 15, and this number 15 is pushed back onto the numbers stack:

```
Characters read so far (shaded):
(( ( 6 + 9 ) / 3 ) * ( 6 - 4 )
```

![](img/7bf56f684fab50d5ff9e94ae2818f3ac_389_0.png)

Notice that the leftmost operand (6 in this example) is the second number popped off the stack, so the correct evaluation is 6 + 9, not 9 + 6. But the order of the operands does matter for subtraction and division.

Next we simply continue the process: reading up to the next right parenthesis, pushing the numbers we encounter onto the numbers stack and pushing the operations we encounter onto the operations stack. When we reach the next right parenthesis, we combine the top two numbers using the topmost operation. Here's what happens in our example when we reach the second right parenthesis:

```
Characters read so far (shaded):
(( ( 6 + 9 ) / 3 ) * ( 6 - 4 )
```

![](img/7bf56f684fab50d5ff9e94ae2818f3ac_389_1.png)

Again, the leftmost operand (15) is the second number popped off the stack, so the correct evaluation is 15/3, not 3/15. Continuing the process, we obtain:

```
Characters read so far (shaded):
(( ( 6 + 9 ) / 3 ) * ( 6 - 4 )
```

![](img/7bf56f684fab50d5ff9e94ae2818f3ac_389_2.png)

Finally, continuing the process one more time does not add anything to the stacks, but it does read the last right parenthesis and does combine two numbers from the numbers stack with an operation from the operations stack:

```
Characters read so far (shaded):
(((6 + 9) / 3) * (6 - 4))
```

![](img/7bf56f684fab50d5ff9e94ae2818f3ac_390_0.png)

At this point there is no more input, and there is exactly one number in the numbers stack, namely 10. That number is the answer. Notice that when we used the two stacks we performed the exact same evaluations as we did when we first evaluated this expression in a simple pencil-and-paper fashion.

### 求值算术表达式的情况

To evaluate our expression we only need to repeatedly handle each input item according to the following cases:

- **数字。** 当输入中遇到一个数字时，读取该数字并将其压入数字栈。

- **运算字符。** 当输入中遇到四个运算字符之一时，读取它并将其压入运算栈。

- **右括号。** 当从输入中读取一个右括号时，会发生一个“求值步骤”。该步骤从数字栈中取出最顶层的两个数字，从运算栈中取出最顶层的运算。这些项目从其栈中移除，并使用该运算组合这两个数字（第二个弹出的数字作为左操作数）。运算的结果被重新压入数字栈。

- **左括号或空格。** 输入中出现的其他字符只有左括号和空格。这些字符被读取后丢弃，不影响计算。一个更完整的算法需要以某种方式处理左括号，以确保每个左括号都有右括号与之匹配，但目前我们假设输入以正确的方式完全加了括号。

The processing of input items halts when the end of the input line occurs, indicated by ‘\n’ in the input. At this point, the answer is the single number that remains in the numbers stack.

We now have our algorithm, which we plan to implement as a function meeting this specification:

```
double read_and_evaluate(istream& ins);
// Precondition: The next line of characters in the stream ins is a fully
// parenthesized arithmetic expression formed from non-negative
// numbers and the four operations +, -, *, and /.
// Postcondition: A line has been read from the stream ins, and this line
// has been evaluated as an arithmetic expression. The value of the
// expression has been returned by the function.
```

The implementation of this function appears as part of a complete program in Figure 7.5.

## 图 7.5 基本计算器程序

### 一个程序

```
// FILE: calc.cxx
// Basic calculator program to evaluate a fully parenthesized arithmetic expression.
// The purpose is to illustrate a fundamental use of stacks.

#include <cctype> // Provides isdigit
#include <cstdlib> // Provides EXIT_SUCCESS
#include <cstring> // Provides strchr
#include <iostream> // Provides cout, cin, peek, ignore
#include <stack> // Provides the stack template class
using namespace std;

// PROTOTYPES for functions used by this demonstration program:
double read_and_evaluate(istream& ins);
// Precondition: The next line of characters in the stream ins is a fully parenthesized
// expression formed from non-negative numbers and the four operations +, -, *, and /.
// Postcondition: A line has been read from the stream ins, and this line has been evaluated
// as an arithmetic expression. The value of the expression has been returned by the function.

void evaluate_stack_tops(stack<double>& numbers, stack<char>& operations);
// Precondition: The top of the operations stack contains +, -, *, or /, and the numbers stack
// contains at least two numbers.
// Postcondition: The top two numbers have been popped from the numbers stack, and the top
// operation has been popped from the operations stack. The two numbers have been
// combined using the operation (with the second number popped as the left operand). The
// result of the operation has then been pushed back onto the numbers stack.
(continued)
```

