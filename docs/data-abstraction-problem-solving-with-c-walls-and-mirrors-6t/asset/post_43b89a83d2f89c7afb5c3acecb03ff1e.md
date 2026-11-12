
Question 3 For each of the following strings, trace the execution of the balanced-braces algorithm and show the contents of the stack at each step.

- a. `x{{yz}}`
- b. `x{y{z}}`
- c. `{{{x}}}`

**Note:** The push operation can fail for implementation-dependent reasons. For example, push fails if the array in an array-based implementation is full. In the spirit of fail-safe programming, a function that implements this balanced-braces algorithm should check push's return value.

### Aside: A solution without stacks

It may have occurred to you that a simpler solution to this problem is possible. You need only keep a count of the current number of unmatched open braces. You need not actually store the open braces in a stack. However, the stack-based solution is conceptually useful as it presents more legitimate uses of stacks. For example, Exercise 7 at the end of this chapter asks you to extend the algorithm given here to check for balanced parentheses and square brackets in addition to braces.

### 6.2.2 Recognizing Strings in a Language

Consider the problem of recognizing whether a particular string is in the language

L = {ss' : s is a possibly empty string of characters other than $, s' = reverse(s)}

For example, the strings ASA, ABCSCBA, and $ are in L, but ABSAB and ABCSCB are not. (Exercise 14 in Chapter 5 introduced a similar language.) This language is like the language of palindromes that you saw in Chapter 5, but strings in this language have special middle character.

A stack is useful in determining whether a given string is in L. Suppose you traverse the first half of the string and push each character onto a stack. When you reach the $ you can undo the process. For each character in the second half of the string, you pop a character off the stack. However, you must match the popped character with the current character in the string to ensure that the second half of the string is the reverse of the first half. The stack must be empty when—and only when—you reach the end of the string; otherwise, one “half” of the string is longer than the other, and so the string is not in L.

The following algorithm uses this strategy. To avoid unnecessary complications, assume that aString contains exactly one $.

```
// Checks the string aString to verify that it is in language L.
// Returns true if aString is in L, false otherwise.
recognizeString(aString: string): boolean
```

```
aStack = a new empty stack
// Push the characters that are before the $ (that is, the characters in s) onto the stack
i = 0
ch = character at position i in aString
while (ch is not a '$')
{
    aStack.push(ch)
    i++
    ch = character at position i in aString
}
// Skip the $
i++

// Match the reverse of s
inLanguage = true // Assume string is in language
while (inLanguage and i < length of aString)
{
    if (!aStack.isEmpty())
    {
        stackTop = aStack.peek()
        aStack.pop()
        ch = character at position i in aString
        if (stackTop equals ch) // Characters match
            i++
        else
            inLanguage = false // Characters do not match (top of stack is not ch)
    }
    else
        inLanguage = false // Stack is empty (first half of string is shorter than second half)
}
if (inLanguage and aStack.isEmpty())
    aString is in language
else
    aString is not in language
```

> You can use an ADT's operations in an application without the distraction of implementation details

> **Note:** In both of the preceding examples, notice how you can focus on the task at hand without the distraction of implementation details such as arrays. With less to worry about, you are less likely to make an error in your logic when you use the ADT's operations in applications such as checkBraces and recognizeString. Likewise, when you finally implement the ADT's operations in C++, you will not be distracted by these applications. In addition, because checkBraces and recognizeString do not depend on any implementation decisions that you make, they are not altered by your decisions. These remarks assume that you do not change the specifications of the ADT's operations when you implement them. However, developing software is not a linear process. You may realize during implementation that you need to refine your specifications. Clearly, changes to the specification of any module affect any already-designed uses of that module.

To summarize, you can specify the behavior of an ADT independently of its implementation. Given such a specification, and without any knowledge of how the ADT will be implemented, you can design applications that use the ADT's operations to access its data.

Question 4 Trace the execution of the language-recognition algorithm described in the previous section for each of the following strings, and show the contents of the stack at each step.

- a. a$a
- b. ab$ab
- c. ab$ba
- d. ab$ba

## 6.3 Using Stacks with Algebraic Expressions

This section contains two more problems that you can solve neatly by using the ADT stack. Keep in mind throughout that you are using the ADT stack to solve the problems. You can use the stack operations only, but you may not assume any particular implementation. You choose a specific implementation only as a last step.

### Your use of an ADT's operations should not depend on its implementation

Chapter 5 presented recursive grammars that specified the syntax of algebraic expressions. Recall that prefix and postfix expressions avoid the ambiguity inherent in the evaluation of infix expressions. We will now consider stack-based solutions to the problems of evaluating infix and postfix expressions. To avoid distracting programming issues, we will allow only the binary operators *, /, +, -, and ^, and we will disallow exponentiation and unary operators.

The strategy we shall adopt here is first to develop an algorithm for evaluating postfix expressions and then to develop an algorithm for transforming an infix expression into an equivalent postfix expression. Taken together, these two algorithms provide a way to evaluate infix expressions. This strategy eliminates the need for an algorithm that directly evaluates infix expressions, which is a somewhat more difficult problem that Programming Problem 8 considers.

### To evaluate an infix expression, first convert it to postfix form and then evaluate the postfix expression

### 6.3.1 Evaluating Postfix Expressions

As we mentioned in Chapter 5, some calculators require you to enter postfix expressions. For example, to compute the value of

```
2 * (3 + 4)
```

by using a postfix calculator, you would enter the sequence 2, 3, 4, +, and *, which corresponds to the postfix expression

```
2 3 4 + *
```

Recall that an operator in a postfix expression applies to the two operands that immediately precede it. Thus, the calculator must be able to retrieve the operands entered most recently. The ADT stack provides this capability. In fact, each time you enter an operand, the calculator pushes it onto a stack. When you enter an operator, the calculator applies it to the top two operands on the stack, pops the operands from the stack, and pushes the result of the operation onto the stack. Figure 6-4 shows the action of the calculator for the previous sequence of operands and operators. The final result, 14, is on the top of the stack.

You can formalize the action of the calculator to obtain an algorithm that evaluates a postfix expression, which is entered as a string of characters. To avoid issues that cloud the algorithm with programming details, assume that

### Simplifying assumptions

- The string is a syntactically correct postfix expression
- No unary operators are present
- No exponentiation operators are present
- Operands are single lowercase letters that represent integer values

### FIGURE 6-4 The effect of a postfix calculator on a stack when evaluating the expression 2 * (3 + 4)

| Key entered | Calculator action | Stack (bottom to top): |
|---|---|---|
| 2 | push 2 | 2 |
| 3 | push 3 | 2 3 |
| 4 | push 4 | 2 3 4 |
| + | operand2 = peek (4)<br>pop<br>operand1 = peek (3)<br>pop<br>result = operand1 + operand2 (7)<br>push result | 2 3 4<br>2 3<br>2<br>2 7 |
| * | operand2 = peek (7)<br>pop<br>operand1 = peek (2)<br>pop<br>result = operand1 * operand2 (14)<br>push result | 2 7<br>2<br>2<br>14 |

### A pseudocode algorithm that evaluates postfix expressions

The pseudocode algorithm is then

```
for (each character ch in the string)
{
  if (ch is an operand)
    Push the value of the operand ch onto the stack
  else // ch is an operator named op
  {
    // Evaluate and push the result
    operand2 = top of stack
    Pop the stack
    operand1 = top of stack
    Pop the stack
    result = operand1 op operand2
    Push result onto the stack
  }
}
```

Upon termination of the algorithm, the value of the expression will be on the top of the stack. Programming Problem 5 at the end of this chapter asks you to implement this algorithm.

Question 5 Evaluate the postfix expression a b - c +. Assume the following values for the identifiers: a = 7, b = 3, and c = -2. Show the status of the stack after each step.

### 6.3.2 Converting Infix Expressions to Equivalent Postfix Expressions

Now that you know how to evaluate a postfix expression, you will be able to evaluate an infix expression if you first can convert it into an equivalent postfix expression. The infix expressions here are the
