
## Chapter 30 Good Code, 7th Dan: Guidelines

- **Chapter Telegram**
  - **C++ Core Guidelines**  
    Collection of guidelines for programming good C++ code; maintained by C++ users, initiated and managed by Bjarne Stroustrup and Herb Sutter.
  - **Guideline Support Library (GSL)**  
    Part of the C++ Core Guidelines. Defines a few types whose use primarily allows automated tools to detect typical errors. There is at least one implementation of the GSL and at least one tool that already uses it.

C++ is a comprehensive language. It intentionally gives programmers a lot of freedom so they can get the most out of the language if necessary. It allows pursuing your own approaches and exploring new paths more than other languages.

The downside to this freedom is that not everything always happens automatically. For many features, there is a recommended way that is most likely to lead to success. Based on many programming experiences already gathered, the best way has crystallized for one thing or another. It's worth knowing the recommendations of the experts to benefit from this knowledge.

In this book, I tried to give you an idea of what I call *modern C++*. I talked about the advantages of RAII and const, as well as how to use the standard library. There's more to it than that, though. You can find lots of other tips in the literature. I want to mention one new development in this chapter. Bjarne Stroustrup, the creator of C++, and Herb Sutter, a top Microsoft C++ expert, have launched an initiative to develop the *C++ Core Guidelines*. I think this is a great idea and have been following it closely.

There are other collections of tips, other guidelines, and many may be correct, deeper, better, or worse. The special thing about the C++ Core Guidelines is that they have the potential to become a quasi-standard and can serve as a foundation for further guidelines.

In this chapter, I provide an overview of the guidelines. Otherwise, I recommend reading the complete C++ Core Guidelines, or at least a selection of them. There you will also find explanations, examples, and discussions. Unfortunately, all explanations do not fit in this book; they would take up their own 500 pages. At the end, I give specific tips on some topics and list the most relevant rules.

### 30.1 Guideline Support Library

The “GSL: Guideline Support Library” section of the C++ Core Guidelines introduces some new language elements that help in adhering to the rules. These are things that

- are particularly common sources of errors, and
- would be particularly difficult to detect with automated tools.

Microsoft already provides an implementation of this GSL.¹ It is a collection of headers that you can simply include in your program with `#include <gsl/gsl>`. If you do this, Visual Studio also offers a plug-in that can help you spot a few typical errors.

Here you will find an excerpt of the GSL constructs. These are consistently designed so that they do not negatively impact runtime performance. In some cases, such as with `owner`, they are merely a kind of semantic annotation and actually do “nothing”:

- **`owner<T>`**  
  Use this owning raw pointer in appropriate places instead of `T*`.
- **not_null**  
  This marks raw pointers that can never be `nullptr`.
- **Expects() and Ensures()**  
  Used in functions for the formal definition of preconditions and postconditions.
- **finally(...)**  
  This helper function creates an object that is executed at the end of the current code block and is more suitable than an extra `try-catch` block if you do not want to write your own RAII wrapper.

The GSL is still in flux and is based on the C++ Core Guidelines. You can find motivation and introduction by Herb Sutter.²

In short, when using the bare C++ language, it is impossible to prove the correctness of a given program regarding type safety and resource correctness or to have it calculated by an automatic tool. The GSL is intended to make this possible. With the constructs from the GSL, you enable a tool to do this automatically. The GSL itself is platform-independent. Microsoft has integrated it into Visual Studio, and there is a plug-in that helps in checking the C++ Core Guidelines along with the GSL.

### 30.2 C++ Core Guidelines

To apply the guidelines, it is important to understand the intent of the guidelines’ authors. In this section, I will describe the “how and why” of the guidelines. After that, I will take a problem-oriented look at some aspects of everyday programming and apply specific guidelines to them.³

Each guideline has an identification. This consists of one (or more) letters and a number—for example, *F.22*. The letter determines the section from which the guideline originates. The section *F* refers, for example, to *functions*.

The sections are further divided into subsections. For example, guidelines F.1 to F.9 together form the F.def subsection.

Ahead, I will use the identifications of the guidelines and subsections so that you can easily find them again. I will quote some selected guidelines. I cannot list the entire explanation of any guideline here, but I have added a few explanatory words [in brackets] at some points.

### 30.2.1 Motivation

I can hardly say it better than the editors of the guidelines, so here I provide you with an excerpt of the abstract.

> **Abstract⁴**
>
> This document is a set of guidelines for using C++ well. The aim of this document is to help people to use modern C++ effectively. By “modern C++” we mean effective use of the ISO C++ standard (currently C++20, but almost all of our recommendations also apply to C++17, C++14 and C++11). In other words, what would you like your code to look like in 5 years’ time, given that you can start now? In 10 years’ time?
>
> The guidelines are focused on relatively high-level issues, such as interfaces, resource management, memory management, and concurrency. Such rules affect application architecture and library design. Following the rules will lead to code that is statically type safe, has no resource leaks, and catches many more programming logic errors than is common in code today. And it will run fast—you can afford to do things right.
>
> We are less concerned with low-level issues, such as naming conventions and indentation style. However, no topic that can help a programmer is out of bounds.
>
> Many of the rules are designed to be supported by an analysis tool. Violations of rules will be flagged with references to the relevant rule. We do not expect you to memorize all the rules before trying to write code. One way of thinking about these guidelines is as a specification for tools that happens to be readable by humans.

The general goal of the guidelines is to create a codebase over time that is shared by multiple developers worldwide. A style should emerge that looks similar here and there and pursues similar goals. This way, everyone can more easily familiarize themselves with new projects over time, and their code is also quicker to read for others, and thus self-documenting. Adhering to the guidelines partially fulfills itself, as one guideline is that code should document itself as much as possible.

However, the guidelines should not force anyone to use only a part of the language, nor is code that does not follow the guidelines necessarily bad. The primary guideline is still that C++ is expressive and performant, and an author must be able to exploit this when it is right and important.

But if you follow the guidelines, you can expect your code to become more correct, safer, and more maintainable without becoming slower.

### 30.2.2 Type Safety

Many of the guidelines aim to make your life easier overall by relying more on the static type system of C++.

### Do Not Weaken the Type Safety of C++

Type safety is weakened by the use of `void*` or `reinterpret_cast`, with limitations by other forms of explicit type conversions, and by (unmarked) `union`.

If you need to use one of these-mentioned operations because a third party requires it, then hide it behind a layer maintained by you. Do not let `void*` spread in your code.

### Avoid “Type Dumpsters”

Do not use `string` and `int` for everything. Be more specific by introducing, for example, `Month`.

Trick question: What does the following function do?

```cpp
Color createColor(int a, int b, int c);
Color createColor(int a, int b, int c, int d);
```

There is no correct answer here. You should make the interface cleaner, for which there are many possibilities:

```cpp
Color createColor(Red r, Green g, Blue b);
Color createColor(Cyan c, Magenta m, Yellow y, Black k);
```

This is even better than just naming the parameters r, g, and b. This way, you can hide in the data type whether the red component is specified from 0 to 100, from 0 to 255, or even as a double between 0.0 and 1.0.

You avoid accidentally swapping the components this way. And what if you actually wanted to call `createColor(a, b, c, d)` but forgot a component and instead called `createColor(a, c, d)`? Then you have called the completely wrong function.

- ¹ https://github.com/Microsoft/GSL, [2023-12-03]
- ² Writing Good C++14... By Default, Herb Sutter, https://www.youtube.com/watch?v=hEx5DNLWGgA, 2015, [2017-05-14]
- ³ https://isocpp.github.io/CppCoreGuidelines/CppCoreGuidelines, [2023-12-03]
- ⁴ https://isocpp.github.io/CppCoreGuidelines/CppCoreGuidelines, [2024-06-02]
