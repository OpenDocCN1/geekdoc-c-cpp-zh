
**7.4** Write and implement the member functions of a class `Counter` that simulates and slightly generalizes the behavior of this grocery store counter. The constructor should create a `Counter` object that can count up to the constructor’s argument. That is, `Counter(9999)` should provide a counter that can count up to 9999. A newly constructed counter displays a reading of 0. The member function `void reset();` sets the counter’s number to 0. The member function `void incr1();` increments the units digit by 1, `void incr10();` increments the tens digit by 1, and `void incr100();` and `void incr1000();` increment the next two digits, respectively. Accounting for any carrying when you increment should require no further action than adding an appropriate number to the private data member. A member function `bool overflow();` detects overflow. (Overflow is the result of incrementing the counter’s private data member beyond the maximum entered at counter construction.)

Use this class to provide a simulation of my mother’s little red clicker. Even though the display is an integer, in the simulation, the rightmost (lower order) two digits are always thought of as cents and tens of cents, the next digit is dollars, and the fourth digit is tens of dollars.

Provide keys for cents, dimes, dollars, and tens of dollars. Unfortunately, no choice of keys seems particularly mnemonic. One choice is to use the keys `asdf`: `a` for cents, followed by a digit 1 to 9; `s` for dimes, followed by a digit 1 to 9; `d` for dollars, followed by a digit 1 to 9; and `f` for tens of dollars, again followed by a digit 1 to 9. Each entry (one of `asdf` followed by 1 to 9) is followed by pressing the Return key. Any overflow is reported after each operation. Overflow can be requested by pressing the `o` key.

For additional online Programming Projects, click the CodeMate icons below.

![](img/9505fd46e120aa9c1406715936ff6251_296_0.png)

## Chapter 8 Operator Overloading, Friends, and References

- 8.1 Basic Operator Overloading 302
  - Overloading Basics 303
  - Tip: A Constructor Can Return an Object 308
  - Returning by const Value 309
  - Tip: Returning Member Variables of a Class Type 312
  - Overloading Unary Operators 313
  - Overloading as Member Functions 314
  - Tip: A Class Has Access to All its Objects 316
  - Overloading Function Application ( ) 317
  - Pitfall: Overloading &&, ||, and the Comma Operator 317
- 8.2 Friend Functions and Automatic Type Conversion 318
  - Constructors for Automatic Type Conversion 318
  - Pitfall: Member Operators and Automatic Type Conversion 319
  - Friend Functions 320
  - Pitfall: Compilers without Friends 323
  - Friend Classes 323
- 8.3 References and More Overloaded Operators 324
  - References 325
  - Pitfall: Returning a Reference to Certain Member Variables 327
  - Overloading >> and << 327
  - Tip: What Mode of Returned Value to Use 335
  - The Assignment Operator 336
  - Overloading the Increment and Decrement Operators 337
  - Overloading the Array Operator [ ] 337
  - Overloading Based on L-Value versus R-Value 341
- Chapter Summary 342
- Answers to Self-Test Exercises 342
- Programming Projects 345

> Eternal truths will be neither true nor eternal unless they have fresh meaning for every new social situation.
> 
> Franklin D. Roosevelt, Address at the University of Pennsylvania [September 20, 1940]

### Introduction

This chapter discusses a number of tools to use when defining classes. The first tool is operator overloading, which allows you to overload operators, such as `+` and `==`, so that they apply to objects of the classes you define. The second tool is the use of friend functions which are functions that are not members of a class but still have access to the private members of the class. This chapter also discusses how to provide automatic type conversion from other data types to the classes you define.

If you have not yet covered arrays (Chapter 5), you should skip the subsection of 8.3 entitled Overloading the Array Operator []. It covers a topic that may not make sense unless you know about array basics.

### 8.1 Basic Operator Overloading

> He’s a smooth operator.
> 
> Line from a song by Sade (written by Sade Adu and Ray St. John)

Operators such as `+`, `-`, `%`, `==`, and so forth are nothing but functions that are used with a slightly different syntax. We write `x + 7` rather than `+(x, 7)`, but the `+` operator is a function that takes two arguments (often called operands rather than arguments) and returns a single value. As such, operators are not really necessary. We could make do with `+(x, 7)` or even `add(x, 7)`. Operators are an example of what is often called syntactic sugar, meaning a slightly different syntax that people like. However, people are very comfortable with the usual operator syntax, `x + 7`, that C++ uses for types such as `int` and `double`. And one way to view a high-level language, such as C++, is as a way to make people comfortable with programming computers. Thus, this syntactic sugar is probably a good idea; at the least, it is a well-entrenched idea. In C++ you can overload the operators, such as `+` and `==`, so that they work with operands in the classes you define. The way to overload an operator is very similar to the way you overload a function name. The details are best explained through an example.

#### Overloading Basics

Display 8.1 contains the definition of a class whose values are amounts of U.S. money, such as $9.99 or $1567.29. The class has a lot in common with the `BankAccount` class we defined in Display 7.2. It represents amounts of money in the same way, as two `int`s for the dollars and cents parts. It has the same private helping functions. Its constructors and accessor and mutator functions are similar to those of the class `BankAccount`. What is truly new about this `Money` class is that we have overloaded the plus sign and the minus sign so they can be used to add or subtract two objects of the class `Money`, and we have overloaded the `==` sign so it can be used to compare two objects of the class `Money` to see if they represent the same amount of money. Let’s look at these overloaded operators.

You can overload the operator `+` (and many other operators) so that it will accept arguments of a class type. The difference between overloading the `+` operator and defining an ordinary function involves only a slight change in syntax: You use the symbol `+` as the function name and precede the `+` with the keyword `operator`. The operator declaration (function declaration) for the plus sign is as follows:

```
const Money operator +(const Money& amount1, const Money& amount2);
```

The operands (arguments) are both constant reference parameters of type `Money`. The operands can be of any type, as long as at least one is a class type. In the general case, operands may be call-by-value or call-by-reference parameters and may have the `const` modifier or not. However, for efficiency reasons, constant call by reference is usually used in place of call by value for classes. In this case the value returned is of type `Money`, but in the general case the value returned can be of any type, including `void`. The `const` before the returned type `Money` will be explained later in this chapter. For now, you can safely ignore that `const`.

Note that the overloaded binary operators `+` and `-` are not member operators (member functions) of the class `Money` and therefore do not have access to the private members of the class `Money`. That is why the definition for the overloaded operators uses accessor and mutator functions. Later in this chapter we will see other ways of overloading an operator, including overloading it as a member operator. Each of the different ways of overloading an operator has its advantages and disadvantages.

The definitions of the overloaded binary operators `+` and `-` are perhaps a bit more complicated than you might expect. The extra details are there to cope with the fact that amounts of money can be negative.

The unary minus sign operator `-` is discussed in the subsection Overloading Unary Operators, later in this chapter.

The operator `==` is also overloaded so that it can be used to compare two objects of the class `Money`. Note that the type returned is `bool` so that `==` can be used to make comparisons in the usual ways, such as in an if-else statement.

**how to overload an operator**
