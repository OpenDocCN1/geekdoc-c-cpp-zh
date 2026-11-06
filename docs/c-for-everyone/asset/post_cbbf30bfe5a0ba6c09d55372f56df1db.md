
## Program Run

```
Enter the side length: 4
Area: 10
```

![](img/5e58fb4c840712efd6ed6fa82bb97f57_512_0.png)

## SELF CHECK

- 1. Why is the statement `if (side_length == 1) { return 1; }` in the `triangle_area` function unnecessarily?
- 2. How would you modify the triangle program to recursively compute the area of a square?
- 3. In some cultures, numbers containing the digit 8 are lucky numbers. What is wrong with the following function that tries to test whether a number is lucky?
  ```cpp
  bool is_lucky(int number)
  {
      int last_digit = number % 10;
      if (last_digit == 8) { return true; }
      else
      {
          return is_lucky(number / 10); // Test the number without the last digit
      }
  }
  ```
- 4. In order to compute a power of two, you can take the next-lower power and double it. For example, if you want to compute 2¹¹ and you know that 2¹⁰ = 1024, then 2¹¹ = 2 × 1024 = 2048. Write a recursive function `int pow2(int n)` that is based on this observation.
- 5. Consider the following recursive function:
  ```cpp
  int mystery(int n)
  {
      if (n <= 0) { return 0; }
      int smaller_n = n - 1;
      int result = mystery(smaller_n);
      return result + n * n;
  }
  ```
  What is `mystery(4)`?

**Practice It** Now you can try these exercises at the end of the chapter: R11.2, P11.2, P11.6.

![](img/5e58fb4c840712efd6ed6fa82bb97f57_512_1.png)

## Common Error 11.1 — Infinite Recursion

A common programming error is an infinite recursion: a function calling itself over and over with no end in sight. The computer needs some amount of memory for bookkeeping for each call. After some number of calls, all memory that is available for this purpose is exhausted. Your program shuts down and reports a “stack fault”.

Infinite recursion happens either because the arguments don’t get simpler or because a terminating case is missing. For example, suppose the `triangle_area` function computes the area of a triangle with side length 0. If you do not include a test for this situation, the function calls itself with side length −1, −2, −3, and so on.

![](img/5e58fb4c840712efd6ed6fa82bb97f57_514_0.png)

**Figure 2** Three Calls to `triangle_area` Are Pending

You can debug recursive functions with the debugger. You just need to be particularly careful, and watch the call stack to understand which nested call you currently are in.

## 11.2 Thinking Recursively

How To 5.2 in Chapter 5 tells you how to solve a problem recursively by pretending that “someone else” will solve the problem for simpler inputs and by focusing on how to turn the simpler solutions into a solution for the whole problem.

In this section, we walk through these steps with a more complex problem: testing whether a sentence is a *palindrome*—a string that is equal to itself when you reverse all characters. Typical examples of palindromes are:

- rotor
- A man, a plan, a canal—Panama!
- Go hang a salami, I’m a lasagna hog

and, of course, the oldest palindrome of all:

- Madam, I’m Adam

Our goal is to implement the function

```
bool is_palindrome(string s)
```

For simplicity, assume for now that the string has only lowercase letters and no punctuation marks or spaces. Exercise P11.14 asks you to generalize the function to arbitrary strings.

### Step 1 Break the input into parts that can themselves be inputs to the problem.

When you consider simpler inputs, you may want to remove just a little bit from the original input—maybe remove one or two characters from a string, or remove a small portion of a geometric shape. But sometimes it is more useful to cut the input in half and then see what it means to solve the problem for both halves.

In the palindrome test problem, the input is the string that we need to test. How can you simplify the input? Here are several possibilities:

- Remove the first character.
- Remove the last character.
- Remove both the first and the last character.
- Remove a character from the middle.
- Cut the string into two halves.

These simpler inputs are all potential inputs for the palindrome test.

### Step 2 Combine solutions with simpler inputs to a solution of the original problem.

You should simply assume that the solutions for the simpler problem are available, without worrying how they were obtained. In this step, ask yourself how you can turn the solution for the simpler inputs into a solution for the input that you are currently thinking about. Maybe you need to add a small quantity, related to the quantity that you lopped off to arrive at the simpler input. Maybe you cut the original input in two halves and have solutions for both halves. Then you may need to add both solutions to arrive at a solution for the whole.

Consider the methods for simplifying the inputs for the palindrome test. Cutting the string in half doesn’t seem a good idea. If you cut "rotor" in half, you get two strings: "rot" and "or". Neither of them is a palindrome. Cutting the input in half and testing whether the halves are palindromes seems a dead end.

> The key step in finding a recursive solution is reducing the input to a simpler input for the same problem.
>
> When designing a recursive solution, do not worry about multiple nested calls. Simply focus on reducing a problem to a slightly simpler one.

The most promising simplification is to remove the first *and* last characters, provided they match. Removing the r at the front and back of "rotor" yields

```
"oto"
```

Assume you can verify that the shorter string is a palindrome. Then *of course* the original string is a palindrome—we put the same letter in the front and the back. That’s extremely promising. A word is a palindrome if

- The first and last letters match, and
- The word obtained by removing the first and last letters is a palindrome.

Again, don’t worry how the test works for the shorter string. It just works.

### Step 3 Find solutions to the simplest inputs.

A recursive function keeps calling itself with simpler inputs. Eventually, the function must stop calling itself. You must deal with the simplest inputs separately. Usually, it is an easy matter to come up with solutions for the simplest inputs.

However, sometimes you get into philosophical questions dealing with *degenerate* inputs: empty strings, shapes with no area, and so on. Then you may want to investigate a slightly larger input that gets reduced to such a trivial input and see what value you should attach to the degenerate inputs so that the simpler value, when used according to the rules you discovered in Step 2, yields the correct answer.

Look at the simplest strings for the palindrome test:

- Strings with two characters
- Strings with a single character
- The empty string

You don’t have to come up with a special solution for strings with two characters. Step 2 still applies to those strings—either or both of the characters are removed. But you do need to worry about strings of length 0 and 1. In those cases, Step 2 can’t apply. There aren’t two characters to remove.

A string with a single character, such as "I", is a palindrome.

The empty string is a palindrome—it’s the same string when you read it backwards. If you find that too artificial, consider a string "oo". According to the rule discovered in Step 2, this string is a palindrome if the first and last character of that string match and the remainder—that is, the empty string—is also a palindrome. Therefore, it makes sense to consider the empty string a palindrome.

Thus, all strings of length 0 or 1 are palindromes.

### Step 4 Implement the solution by combining the simple cases and the reduction step.

Usually, you want to get the simplest cases out of the way. In the case of the palindrome test, those are the strings with length 0 or 1. If the input isn’t one of the simplest cases, then make one or more recursive calls with simpler inputs and use the results of those calls to complete your solution.

The following program shows the complete `is_palindrome` function:
