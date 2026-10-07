
# 8. Slow Down

Dozens of solutions exist in C++ for any given problem. Dozens of more opinions exist for which of these solutions are the best. Copying and pasting from one application to another is easy. Forging ahead with the solutions you are comfortable with is easy.

How many times have you said, “wow, this is going to take a complicated class hierarchy to implement this solution?” Or what about “I guess I need to add macros here to implement these common functions.”

- If the solution seems large or complex, stop.
- Now is a good time to go for a walk and ponder the solution.
- When you're done with your walk, discuss the design with a coworker, pet, or rubber duck¹..

Still haven't found a more straightforward solution you are happy with? Ask on Twitter or Slack if you can.

The key point is to not forge ahead blindly with the solutions with which you are comfortable. Being willing to stop for a minute. The older I get, the less time I spend programming, and the more time I spend thinking. In the end, I implement the solution as fast or faster than I used to and with less complexity.

> ¹https://rubberduckdebugging.com/

# 9. C++ Is Not Magic

This section is just a reminder that we can reason about all aspects of C++. It's not a black box, and it's not magic.

If you have a question, it's usually easy to construct an experiment that helps you answer the question for yourself.

A favorite tool of mine is this simple class that prints a debug message whenever a special member function is called.

Understanding object lifetime tool

```cpp
#include <stdio>

struct S {
S(){ puts("S"); };
S(const S&){ puts("S const S&"); };
S(S &&){ puts("S S &&"); };
S &operator=(const S&){
    puts("operator=(const S&)");
    return +this;
}
S &operator=(S&&){
    puts("operator=(S &&)");
    return +this;
}
~S() { puts("~S()"); };
};
```

# Exercise: Build your first C++ experiment.

Do you have a question about C++ that's been nagging you to? Can you design an experiment to test it? Remember that Compiler Explorer now allows you to execute code.

# Exercise: Start collecting your experiments.

Once you have created an experiment and test, be sure to save it. Consider using GitHub gists as a simple way to save and share your tests with others.

# Resources

- A quick start example with Compiler Explorer.¹

> ¹https://godbolt.org/z/3eGP56

# 10. C++ Is Not Object-Oriented

Bjarne Stroustrup in The C++ Programming Language 3rd Edition states:

C++ is a general-purpose programming language with a bias towards systems programming that

- * is a better C,
- supports data abstraction,
- supports object-oriented programming, and
- supports generic programming.

You must understand that C++ is a multi-discipline programming language to make the most of the language. C++ supports effectively all of the programming paradigms that exist today.

- Procedural
- Functional
- Object-Oriented
- Generic
- Compile-Time (constexpr and template metaprogramming)

Knowing when it is appropriate to use each of these tools is the key to writing good C++. Projects that rigidly stick to one paradigm miss out on the best features of the language.

> Don't try to use every technique possible all the time. You will end up with a mess of difficult to maintain and read code. Appropriately using the appropriate techniques at the appropriate times takes discipline and practice.

# Exercise: Question your current design.

If you could break out of the current design your project is using, what would you do differently?

# Resources

- Functional Programming in C++¹
- C++ Weekly Ep 137: C++ Is Not an Object Oriented Language²

> ¹https://www.manning.com/books/functional-programming-in-c-plus-plus?a_aid=FPinCXX&a_bid=441f12cc
²https://youtu.be/AUT201AXeJg

# 11. Learn Another Language

Considering that C++ is not an object-oriented language, you have to know many different techniques to make the most of C++.

The following exercises will help expose you to other languages. But the fact that currently, few languages are pure single paradigm languages.

Every language has its preferred way of doing things that work within the language's preferred paradigm.

Ben Deane recommends this set of languages that all programmers should learn¹:

- ALGOL family (C and descendants)
- Forth
- Lisp and dialects
- Haskell
- Smalltalk
- Erlang

# Exercise: Pick a functional language to learn

Can you find a pure functional language?

# Exercise: Pick an object-oriented language to learn

Finding a pure object-oriented language is even harder! Even Java has lambda functions these days.

# Exercise: Pick a language with a different syntax

Languages that look like C-family languages will likely be more comfortable for you. Try to find a language that looks different and stretches your mind.

# Resources

- Execution in the Kind of Nouns² - gets you thinking about different programming paradigms

> ²https://steve-ygge.blogspot.com/2006/03/execution-in-kingdom-of-nouns.html

# 12. const Everything That’s Not constexpr

Many people (like Kate Gregory and James McNellis) have said this many times.
Making objects const does two things:

- 1. It forces us to think about the initialization and lifetime of objects, which affects performance.
- 2. Communicates meaning to the readers of our code.

And as an aside, if it's a static object, the compiler is now free to move it into the constants portion of the binary, which can affect the optimizer.

> Exercise: Look for const opportunities.

As you read through your code, you should look for variables that are not const and make them const.

- If a variable is not const, ask why not?
- Would using a lambda or adding a named function allow you to make the value const?

const Everything That's Not constexpr

Using a lambda to initialize a const object.

```cpp
const auto data = [](){}; // no parameters
std::vector<int> result;
// fill result with things.
return result;
}(); // immediately invoked
```

![](img/c882530931fce4e9ed96c0621b6ce632_27_0.png)

Because of RVO, using a lambda will likely not add any overhead and may increase performance.

Did you make any static variables const in the process?
Then go to the constexpr exercise.

![](img/c882530931fce4e9ed96c0621b6ce632_27_1.png)

> You probably don't want to make class members const; it can break essential things, and sometimes silently.

# Resources

- CppCon 2014: James McNellis & Kate Gregory "Modernizing Legacy C++ Code"1
- CppCon 2019: Jason Turner "C++ Code Smells"2
- The implication of const or reference member variables in C++3
- CppNow 2018: Ben Deane "Easy to Use, Hard to Misuse: Declarative Style in C++"4 (Builds on techniques that make applying const)

^1https://youtube.be/LdxAgMe6DI8
2https://youtube.be/f_tLIQ0wUM
3https://lesylai.info/en/const-and-reference-variables/
4https://youtube.be/2ouxET5R4

# 13. constexpr Everything Known at Time

Gone are the days of #define. constexpr should be your new default! Unfortunately, people overcomplicate constexpr, so let's break down the simplest thing.

If you see something like (I've seen in real code):

```cpp
static const data known at time.
static const std::vector<int> angles{-90,45,0,45,90};
```

This really needs to be:

```cpp
static const constexpr.
static constexpr std::array<int, 5> angles{-90,45,0,45,90};
```

> static constexpr here is to make sure the object is not reinitialized each time the function is encountered. With static the variable lasts for the lifetime of the program, and we know it will be initialized exactly once.

The difference is threefold.

- The size of the array is now known at compile time
- We've removed dynamic allocations
- We no longer pay the cost of accessing a static

 main gains come from the first two, but we need a constexpr mindset looking for this kind of opportunity. The difference can be significant.

# Exercise: constexpr Your const Values

While reading code, look at all const values. Ask, “is this value known at compile time?” If it is, what would it take to make the value constexpr?

# Exercise: static constexpr Your static const Values

Go through your current code base and look for code that is currently static const. You probably have something, somewhere.

- If it's currently static const, it's likely the size and data are known at compile time.
- Can this code become constexpr?
- What is preventing it from being constexpr?
- How much work would it take to modify the functions populating the static const data so that they are also constexpr?

# Resources

- C++Now 2017: Ben Deane & Jason Turner “constexpr ALL the things”¹ (a bit out of date with modern constexpr techniques)
- C++ Weekly Eb 233: constexpr map vs std::map²

> ¹https://youtube.be/HMB9oxFobJc
²https://youtube.be/INn3xa4pMFg
