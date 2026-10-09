
case <possible value>:
    <statements>
case <possible value>:
    <statements>
...
case <possible value>:
    <statements>
default:
    <statements>
}

The body of the switch statement is the code between the curly brackets. This consists of a list of possible cases and some code to execute. When executing this switch statement, the computer will first evaluate **expression**. It then looks for the first matching case statement and executes all the code from there up to either the first break statement or up to the end of the switch statement.

If there is no match, the computer looks for a **default** statement and evaluates all the code from there to the end of the switch statement.

After executing the required statements from the body of the switch statement, the program moves on to the next statement after the switch statement. In our example this means it will wish you good luck in your career.

Notice that you have to be careful to insert **break** or **return** statements into your *switch* statements to make sure the code doesn’t execute more statements than you want it to.

For example, if you remove all the **break** statements from our example, then a score of 0 would be greeted with the response

```
You have failed.
You have passed.
Merit.
Distinction.
Invalid score.
Good luck in your future career.
```

If you dislike the syntax of *switch* statements, you are not alone. Fortunately, they aren’t very useful in modern C++ code. In modern C++ one should use the object-oriented programming technique of *polymorphism* instead. We will cover this subject in depth in Chapter 10. If you find yourself tempted to write a *switch* statement, it’s a sign that you aren’t using object-oriented programming to full advantage.

## **Tip: Always include a default case**

If you must write a *switch* statement, always be sure to include a **default** case. Usually your default case will generate an error by using a **throw** statement. Simply printing an error (as happens in our example) is a bad idea.

## 4.7 Scope

The flow of control statements above make use of curly brackets. If you define a variable within curly brackets, it can only be used within those brackets. Once the execution of the program leaves the brackets, the variable is deleted. The part of the code in which you can refer to a variable is called the *scope* of the variable.

Here is an example code snippet that computes the sum of the squares of the first 10 integers (starting from 0, of course).

```cpp
int n=0;
int total;
for (int i=0; i<10; i++) {
    int squareValue = i*i;
    total += squareValue;
}
std::cout << n;
// std::cout << squareValue;
// std::cout << i;
```

The variable `squareValue` is only valid within the curly brackets. The variable `i` is only valid within the for statement itself and within the curly brackets. If you were to try to remove the comment characters `//` on the last two lines, the code would not compile.

The scope of variables is used to control the use of memory in C++. When variables go out of scope, the memory can be safely reused. Often you won't need to think about the memory management in C++. However, there are times when you will want to take control of memory management yourself. We will discuss this in Chapter 11.

## 4.8 Flow of control in operators

A technical point is that certain operators in C++ actually control the flow of the program in subtle ways.

### 4.8.1 **Short circuit evaluation**

The expression lhs && rhs evaluates to true if both lhs and rhs evaluate to true. To improve efficiency, C++ doesn't even bother evaluating the expression rhs if lhs isn't true. This is usually just what you want to happen. However, if evaluating the expression rhs actually calls another function, you may be surprised that this function isn't always called.

Similarly lhs || rhs doesn't evaluate rhs if it is already known that lhs is true.

As an example, try the following code:

```cpp
bool test1() {
    cout << "In test1\n";
    return false;
}
bool test2() {
    cout << "In test2\n";
    return true;
}
int main() {
    bool value = test1() && test2();
    cout << "Value " << value << "\n";
    return 0;
}
```

You will see that the function test2 is never called.

### 4.8.2 **The ternary operator**

The operator * as in the expression a*b is called a binary operator because it takes two arguments. The operator ++ on the other hand is called a unary operator.

C++ also contains one operator which takes three arguments and which so is known as the ternary operator.

The ternary operator is, in essence, a short cut for writing if statements. The syntax is:

`<test expression> ? <value if true> : <value if false>`

As an example, here is a program that uses the ternary operator to compute the maximum of two numbers:

```cpp
int max(int a, int b) {
    return a>b ? a : b;
}
```

Here is some equivalent code that uses an if statement.

```cpp
int max(int a, int b) {
  if (a > b) {
    return a;
  } else {
    return b;
  }
}
```

People who are too lazy to type like the ternary operator, but it results in code which is very hard to understand. Don't use it.

### 4.8.3 The comma operator

Between the round brackets of a for statement one always has three expressions separated by semi-colons. Here is an example:

```cpp
for (int i = 0; i < 100; i++) {
  cout << i << "\n";
}
```

You can if you like perform multiple calculations at the end of each loop and multiple initialisations by using the so-called "comma operator". Here's an example that prints out the first 10 powers of 2:

```cpp
for (int count = 0, power = 1;
     count < 10;
     count++, power *= 2) {
  cout << power << "\n";
}
```

In this code we maintain two loop variables, count and power, each of which is updated every iteration.

The formal definition of the comma operator is that the expression lhs, rhs evaluates lhs and discards the result and then evaluates rhs. Thus you can, if you wish, string expressions together using the comma operator as an alternative to using semi-colons in the conventional way.

Don't use the comma operator yourself. It leads to code that is hard to read (as our example demonstrates). We wrote a program earlier (page 56) that printed out the powers of 2 using a while loop that was much easier to follow.

## Exercises

- 4.8.1. Use a `while` loop, a `for` loop, and a `do-while` loop to provide different implementations for the `factorial` function.
- 4.8.2. Given a function $f : \mathbb{R} \rightarrow \mathbb{R}$, we can approximate the integral

$$ \int_{a}^{b} f(x) \, dx $$

using the *rectangle rule*. Given an integer $n$, the rectangle rule approximation for this integral is:

$$ \frac{1}{n} \sum_{i=0}^{n-1} f \left( a + i h + \frac{1}{2} h \right) $$

where $h = \frac{b-a}{n}$. Write a function that computes the rectangle rule approximation to:

$$ \int_{a}^{b} \sin(x) \, dx $$

for given $a$, $b$ and $n$.

- 4.8.3. We would like to compute the integral

$$ \int_{-\infty}^{x} \exp(-t^{2}/2) \, dt. $$

By making the substitution $t = x + 1 - \frac{1}{s}$ we can see that this is equal to the integral

$$ \int_{0}^{1} \frac{1}{s^{2}} \exp \left( -\frac{(x+1-\frac{1}{s})^{2}}{2} \right) \, ds. $$

This integral can then be estimated using the rectangle rule. Write a function that uses a `for` loop to compute this second integral using the rectangle rule.

- 4.8.4. Use the looping construct of your choice to compute the $n$-th Fibonacci number. Explain why this is more efficient than the method using recursion considered in Exercise 3.9.3.

- 4.8.5. Improve the `norminv` function so that it throws an error if asked to evaluate a number outside the range $[0, 1]$.

- 4.8.6. Improve the `norminv` function so that it takes an extra boolean parameter that indicates whether or not to throw an exception when given an input outside the range 0 and 1. What would be a good default value for this parameter?
