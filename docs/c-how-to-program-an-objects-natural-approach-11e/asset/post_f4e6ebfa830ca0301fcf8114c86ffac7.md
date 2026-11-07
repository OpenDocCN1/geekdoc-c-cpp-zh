
| C++ Keywords (Cont.) | | | | |
|---|---|---|---|---|
| continue | decltype | default | delete | do |
| double | dynamic_cast | else | enum | explicit |
| export | extern | false | final | float |
| for | friend | goto | if | import |
| inline | int | long | module | mutable |
| namespace | new | noexcept | not | not_eq |
| nullptr | operator | or | or_eq | override |
| private | protected | public | register | reinterpret_cast |
| return | short | signed | sizeof | static |
| static_assert | static_cast | struct | switch | template |
| this | thread_local | throw | true | try |
| typedef | typeid | typename | union | unsigned |
| using | void | volatile | virtual | wchar_t |
| while | xor | xor_eq | | |
| **Keywords new in C++20** | | | | |
| char8_t | concept | consteval | constinit | co_await |
| co_return | co_yield | requires | | |

### 3.4.4 Summary of Control Statements

C++ has only three kinds of control structures, which from this point forward, we refer to as control statements:

- sequence,
- selection (`if`, `if…else` and `switch`) and
- iteration (`while`, `do…while`, `for` and range-based `for`).

You form every program by combining these statements as appropriate for the algorithm you’re implementing. We can model each control statement as an activity diagram. Each diagram contains initial and final states representing a control statement’s entry and exit points. Single-entry/single-exit control statements make it easy to build readable programs—we simply connect the exit point of one to the entry point of the next using control-statement stacking. There’s only one other way in which you may connect control statements—control-statement nesting, in which one control statement appears inside another. Thus, algorithms in C++ programs are constructed from only three kinds of control statements combined in only two ways. This is the essence of simplicity.

![](img/7b5e2088e71c7f78681d4ddbcf104c06_157_0.png)

### Checkpoint

- **1. (Fill-in)** Böhm and Jacopini’s work demonstrated that all programs could be written in terms of only three control structures—______, ______ and ______ structure.  
  **Answer:** sequence, selection, iteration.
- **2. (True/False)** The while, for and do...while statements perform their action (or group of actions) zero or more times.  
  **Answer:** False. The while and for statements perform their action (or group of actions) zero or more times. The do...while statement performs its action (or group of actions) one or more times.
- **3. (Fill-in)** ________ control statements make it easy to build readable programs by connecting the exit point of one to the entry point of the next using control-statement stacking.  
  **Answer:** Single-entry/single-exit.

## 3.5 *if* Single-Selection Statement

We introduced the `if` single-selection statement briefly in Section 2.7. Programs use selection statements to choose among alternative courses of action. For example, suppose that the passing grade on an exam is 60. The following pseudocode represents an `if` statement that tests the condition “student's grade is greater than or equal to 60”:

```text
if student's grade is greater than or equal to 60
    print "Passed"
```

If this condition is true, the statement prints “Passed”—otherwise, the `print` statement is ignored. Indenting the second line of this selection statement is optional but recommended for clarity—it emphasizes that the `print` statement is in the `if` statement's body.

The preceding pseudocode may be written in C++ as

```cpp
if (studentGrade >= 60) {
    cout << "Passed";
}
```

The C++ code corresponds closely to the pseudocode.

### bool Data Type

In Chapter 2, you created conditions using the relational or equality operators. Actually, any expression that evaluates to zero or nonzero can be used as a condition. Zero is treated as `false`, and nonzero is treated as `true`. C++ also provides the data type `bool` for Boolean variables that can hold only the values `true` and `false`—each is a C++ keyword. The compiler can implicitly convert `true` to `1` and `false` to `0`.

### UML Activity Diagram for an if Statement

The following UML activity diagram illustrates the single-selection `if` statement.

![](img/7b5e2088e71c7f78681d4ddbcf104c06_158_0.png)

This figure contains the most important symbol in an activity diagram—the diamond, or decision symbol, which indicates that a decision is to be made. The workflow continues along a path determined by the symbol’s associated guard conditions, which can be true or false. Each transition arrow emerging from a UML decision symbol has a guard condition (specified in square brackets next to the arrow). If a guard condition is true, the workflow enters the action state to which the transition arrow points. The diagram shows that if the grade is greater than or equal to 60 (i.e., the condition is true), the program prints “Passed” then transitions to the activity’s final state. If the grade is less than 60 (i.e., the condition is false), the program immediately transitions to the final state without displaying a message. The if statement is a single-entry/single-exit control statement.

### Checkpoint

- **(Pseudocode)** Write a pseudocode *if* statement that determines whether a count is greater than 10 and, if so, prints “Count is greater than 10.”
  
  **Answer:**
  
  ```text
  if count is greater than 10
      print "Count is greater than 10."
  ```
- **(Code)** Write an if statement that implements the preceding exercise’s pseudocode. Assume the int variable count already exists.
  
  **Answer:**
  
  ```cpp
  if (count > 10) {
      cout << "Count is greater than 10.";
  }
  ```
- **(Fill-in)** A diamond, or decision symbol, in an activity diagram indicates that a decision is to be made. The workflow continues along a path determined by the symbol’s associated ______.
  
  **Answer:** guard conditions.

## 3.6 if…else Double-Selection Statement

The if-then selection statement performs an indicated action only when the condition is true. The if…else double-selection statement allows you to specify an action to perform when the condition is true and another action when the condition is false. For example, the following pseudocode represents an if…else statement that prints “Passed” if the student’s grade is greater than or equal to 60 but prints “Failed” if it’s less than 60:

```text
if student’s grade is greater than or equal to 60
    print “Passed”
else
    print “Failed”
```

In either case, after printing occurs, the next statement in sequence is “performed.” The preceding if…else pseudocode statement can be written in C++ as

```cpp
if (studentGrade >= 60) {
    cout << "Passed";
}
else {
    cout << "Failed";
}
```

The if and else bodies are both indented equally. Whatever indentation convention you choose should be applied consistently throughout your programs. If there are several indentation levels, each should be indented the same additional amount of space. We prefer three-space indents. IDEs often auto-indent the code for you.

### UML Activity Diagram for an if...else Statement

The following diagram illustrates the flow of control in the preceding if...else statement:

![](img/7b5e2088e71c7f78681d4ddbcf104c06_160_0.png)

### 3.6.1 Nested if...else Statements

A program can test multiple cases by placing if...else statements inside other if...else statements to create nested if...else statements. For example, the following pseudocode represents a nested if...else statement that prints "A" for exam grades greater than or equal to 90, "B" for grades 80 to 89, "C" for grades 70 to 79, "D" for grades 60 to 69 and "F" for all other grades. We use shading to highlight the nesting:

```text
if student’s grade is greater than or equal to 90
   print “A”
else
   if student’s grade is greater than or equal to 80
      print “B”
   else
      if student’s grade is greater than or equal to 70
         print “C”
      else
         if student’s grade is greater than or equal to 60
            print “D”
         else
            print “F”
```
