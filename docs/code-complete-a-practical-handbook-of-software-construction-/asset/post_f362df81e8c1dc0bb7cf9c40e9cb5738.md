
This is close, but still no cigar. If you use Cube() in an expression that has operators with higher precedence than multiplication, the (a)*(a)*(a) will be torn apart. To prevent that, enclose the whole expression in parentheses:

## C++ Example of a Macro That Works

```
#define Cube( a ) ((a)*(a)*(a))
```

## Surround multiple-statement macros with curly braces

A macro can have multiple statements, which is a problem if you treat it as if it were a single statement. Here’s an example of a macro that’s headed for trouble:

![](img/649c8eee28c38ca1e062691e45dc9883_219_0.png)

### C++ Example of a Nonworking Macro with Multiple Statements

```
#define LookupEntry( key, index ) \
    index = (key - 10) / 5; \
    index = min( index, MAX_INDEX ); \
    index = max( index, MIN_INDEX );
...

for ( entryCount = 0; entryCount < numEntries; entryCount++ )
    LookupEntry( entryCount, tableIndex[ entryCount ] );
```

This macro is headed for trouble because it doesn’t work as a regular function would. As it’s shown, the only part of the macro that’s executed in the for loop is the first line of the macro:

```
index = (key - 10) / 5;
```

To avoid this problem, surround the macro with curly braces:

### C++ Example of a Macro with Multiple Statements That Works

```
#define LookupEntry( key, index ) { \
    index = (key - 10) / 5; \
    index = min( index, MAX_INDEX ); \
    index = max( index, MIN_INDEX ); \
}
```

The practice of using macros as substitutes for function calls is generally considered risky and hard to understand—bad programming practice—so use this technique only if your specific circumstances require it.

## Name macros that expand to code like routines so that they can be replaced by routines if necessary

The convention in C++ for naming macros is to use all capital letters. If the macro can be replaced by a routine, however, name it using the naming convention for routines instead. That way you can replace macros with routines and vice versa without changing anything but the routine involved.

Following this recommendation entails some risk. If you commonly use ++ and -- as side effects (as part of other statements), you’ll get burned when you use macros that you think are routines. Considering the other problems with side effects, this is yet another reason to avoid using side effects.

## Limitations on the Use of Macro Routines

Modern languages like C++ provide numerous alternatives to the use of macros:

- *const* for declaring constant values
- *inline* for defining functions that will be compiled as inline code
- *template* for defining standard operations like *min*, *max*, and so on in a type-safe way
- *enum* for defining enumerated types
- *typedef* for defining simple type substitutions

![](img/649c8eee28c38ca1e062691e45dc9883_220_0.png)

> As Bjarne Stroustrup, designer of C++ points out, “Almost every macro demonstrates a flaw in the programming language, in the program, or in the programmer.... When you use macros, you should expect inferior service from tools such as debuggers, cross-reference tools, and profilers” (Stroustrup 1997). Macros are useful for supporting conditional compilation—see Section 8.6, “Debugging Aids”—but careful programmers generally use a macro as an alternative to a routine only as a last resort.

## Inline Routines

C++ supports an *inline* keyword. An inline routine allows the programmer to treat the code as a routine at code-writing time, but the compiler will generally convert each instance of the routine into inline code at compile time. The theory is that *inline* can help produce highly efficient code that avoids routine-call overhead.

***Use inline routines sparingly***  Inline routines violate encapsulation because C++ requires the programmer to put the code for the implementation of the inline routine in the header file, which exposes it to every programmer who uses the header file.

Inline routines require a routine’s full code to be generated every time the routine is invoked, which for an inline routine of any size will increase code size. That can create problems of its own.

The bottom line on inlining for performance reasons is the same as the bottom line on any other coding technique that’s motivated by performance: profile the code and measure the improvement. If the anticipated performance gain doesn’t justify the bother of profiling the code to verify the improvement, it doesn’t justify the erosion in code quality either.

cc2e.com/0792

Cross-Reference This is a checklist of considerations about the quality of the routine. For a list of the steps used to build a routine, see the checklist "The Pseudocode Programming Process" in Chapter 9, page 215.

## CHECKLIST: High-Quality Routines

## Big-Picture Issues

- Is the reason for creating the routine sufficient?
- Have all parts of the routine that would benefit from being put into routines of their own been put into routines of their own?
- Is the routine’s name a strong, clear verb-plus-object name for a procedure or a description of the return value for a function?
- Does the routine’s name describe everything the routine does?
- Have you established naming conventions for common operations?
- Does the routine have strong, functional cohesion—doing one and only one thing and doing it well?
- Do the routines have loose coupling—are the routine’s connections to other routines small, intimate, visible, and flexible?
- Is the length of the routine determined naturally by its function and logic, rather than by an artificial coding standard?

## Parameter-Passing Issues

- Does the routine’s parameter list, taken as a whole, present a consistent interface abstraction?
- Are the routine’s parameters in a sensible order, including matching the order of parameters in similar routines?
- Are interface assumptions documented?
- Does the routine have seven or fewer parameters?
- Is each input parameter used?
- Is each output parameter used?
- Does the routine avoid using input parameters as working variables?
- If the routine is a function, does it return a valid value under all possible circumstances?

## Key Points

- The most important reason for creating a routine is to improve the intellectual manageability of a program, and you can create a routine for many other good reasons. Saving space is a minor reason; improved readability, reliability, and modifiability are better reasons.
- Sometimes the operation that most benefits from being put into a routine of its own is a simple one.
- You can classify routines into various kinds of cohesion, but you can make most routines functionally cohesive, which is best.
- The name of a routine is an indication of its quality. If the name is bad and it’s accurate, the routine might be poorly designed. If the name is bad and it’s inaccurate, it’s not telling you what the program does. Either way, a bad name means that the program needs to be changed.
- Functions should be used only when the primary purpose of the function is to return the specific value described by the function’s name.
- Careful programmers use macro routines with care and only as a last resort.

## Chapter 8

## Defensive Programming

## Contents

- 8.1 Protecting Your Program from Invalid Inputs: page 188
- 8.2 Assertions: page 189
- 8.3 Error-Handling Techniques: page 194
- 8.4 Exceptions: page 198
- 8.5 Barricade Your Program to Contain the Damage Caused by Errors: page 203
- 8.6 Debugging Aids: page 205
- 8.7 Determining How Much Defensive Programming to Leave in Production Code: page 209
- 8.8 Being Defensive About Defensive Programming: page 210

## Related Topics

- Information hiding: "Hide Secrets (Information Hiding)" in Section 5.3
- Design for change: "Identify Areas Likely to Change" in Section 5.3
- Software architecture: Section 3.5
- Design in Construction: Chapter 5
- Debugging: Chapter 23

![](img/649c8eee28c38ca1e062691e45dc9883_223_0.png)

Defensive programming doesn’t mean being defensive about your programming—“It does so work!” The idea is based on defensive driving. In defensive driving, you adopt the mind-set that you’re never sure what the other drivers are going to do. That way, you make sure that if they do something dangerous you won’t be hurt. You take responsibility for protecting yourself even when it might be the other driver’s fault. In defensive programming, the main idea is that if a routine is passed bad data, it won’t be hurt, even if the bad data is another routine’s fault. More generally, it’s the recognition that programs will have problems and modifications, and that a smart programmer will develop code accordingly.

This chapter describes how to protect yourself from the cold, cruel world of invalid data, events that can “never” happen, and other programmers’ mistakes. If you’re an experienced programmer, you might skip the next section on handling input data and begin with Section 8.2, which reviews the use of assertions.
