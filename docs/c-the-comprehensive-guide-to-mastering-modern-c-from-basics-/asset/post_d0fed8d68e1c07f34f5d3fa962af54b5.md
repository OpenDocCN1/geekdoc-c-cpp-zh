
- condition_variable::notify_one, notify_all, wait, wait_for, and wait_until

## 29.9.4 <condition variable> Header

The wait methods are used for communication between multiple threads using a unique_lock, in RAII style. With notify, waiting threads are informed about a possible change of a condition_variable. The wait methods wait for such a change.

- condition_variable_any
Communication between threads with any kind of lock.

- notify_all_at_thread_exit
Helper function to inform other threads about the end of a thread of a condition_variable.

- async-free function

## 29.9.5 <future> Header

Starting a new thread or deferring the execution of a computation; returns a future.

- future and shared_future-get(), valid(), wait..., and share()
Encapsulates the result of a computation that is retrieved only upon get(). valid() checks if the result is already available. wait, wait_for, and wait_until until the result is available or for a specified duration. shared() converts a future into a shared_future.

- promise-get_future, set_value, set_exception, ... at_thread_exit
Manually creates a future when async is not used.

- packaged_task–operator(), get_future(), valid(), reset
Prepares a function for later execution and provides the result via future.

- atomic<T>, atomic_ref<, atomic<shared_ptr<>>, atomic_flag, atomic_int, etc...load, store, exchange, etc.
Data types whose methods cannot be interrupted by other threads. For all built-in data types and many of the aliases, there is a predefined atomic equivalent. atomic_ref and the specialization for shared_ptr and floating-point types are available from C++20.

## 29.9.6 <atomic> Header

- memory_order–from cst_seq to relaxed
Depending on the use case, optional parameters for the methods of the atomic data types.

- atomic_thread_fence, atomic_signal_fence
Creates a barrier in the machine code that you can use to synchronize non-atomic data structures similarly to an atomic or to synchronize with one.

- atomic_load, atomic_store, atomic_exchange, etc.–free functions
Interaction of a nonatomic data type with an atomic one.

## 29.9.7 <coroutine> Header

For writing your own coroutines and collaborating with co_yield, co_await, and co_return (from C++20):

- coroutine_handle
Pointer to a coroutine that was interrupted with co_await OR co_yield.

- coroutine_traits
The way to get from a return type to the appropriate promise-type.

- suspend_never, suspend_always
Helper classes for collaborating with co_await and co_yield.

# 30 GOOD CODE, 7TH DAN: GUIDELINES

# Chapter Telegram

- C++ Core Guidelines
Collection of guidelines for programming good C++ code; maintained by C++ users, initiated and managed by Bjarne Stroustrup and Herb Sutter.
- Guideline Support Library (GSL)
Part of the C++ Core Guidelines. Defines a few types whose use primarily allows automated tools to detect typical errors. There is at least one implementation of the GSL and at least one tool that already uses it.

C++ is a comprehensive language. It intentionally gives programmers a lot of freedom so they can get the most out of the language if necessary. It allows pursuing your own approaches and exploring new paths more than other languages.

The downside to this freedom is that not everything always happens automatically. For many features, there is a recommended way that is most likely to lead to success. Based on many programming experiences already gathered, the best way has crystallized for one thing or another. It's worth knowing the recommendations of the experts to benefit from this knowledge.

In this book, I tried to give you an idea of what I call *modern C++. I talked about the advantages of RAII and const, as well as how to use the standard library. There's more to it than that, though. You can find lots of other tips in the literature. I want to mention one new development in this chapter. Bjarne Stroustrup, the creator of C++, and Herb Sutter, a top Microsoft C++ expert, have launched an initiative to develop the C++ Core Guidelines. I think this is a great idea and have been following it closely.

There are other collections of tips, other guidelines, and many may be correct, deeper, better, or worse. The special thing thinking about the C++ Core Guidelines is that they have the potential to become a quasi-standard and can serve as a foundation for further guidelines.

In this chapter, I provide an overview of the guidelines. Otherwise, I recommend reading the complete C++ Core Guidelines, or at least a selection of them. You will also find explanations, examples, and discussions. Unfortunately, full explanations do not fit in this book; they would take up their own 500 pages. At the end, I give specific tips on some topics and list the most relevant rules.

# 30.1 Guideline Support Library

The "GSL: Guideline Support Library" section of the C++ Core Guidelines introduces some new language elements that help in adhering to the rules. These are things that:

- are particularly common sources of errors, and
- would be particularly difficult to detect with automated tools.

Microsoft already provides an implementation of this GSL.[87]. It is a collection of headers that you can simply include in your program with #include <gsl/gsl>. If you do this, Visual Studio also offers a plug-in that can help you spot a few typical errors.

Here will find an excerpt of the GSL constructs. These are consistently designed so that they do not negatively impact runtime performance. In some cases, such as with owner, they are merely a kind of semantic annotation and actually do “nothing”:

- owner<T*>
Using this raw pointer in appropriate places instead of T*.

- not_null
This marks raw pointers that can never be nullptr.

- Expects() and Enures()
Used in functions for the formal definition of preconditions and postconditions.

- finally(..)
This helper function creates an object that is executed at the end of the current code block and is more suitable than an extra try-catch block if you do not want to write your own RAII wrapper.

The GSL is still in flux and is based on the C++ Core Guidelines. You can find motivation and introduction by Herb Sutter.[88]

In short when using the bare language, it is impossible to prove the correctness of a given program the GSL is intended to make this possible. The GSL is platform-independent. Microsoft has integrated it into Visual Studio.

# 30.2 C++ Core Guidelines

To apply the guidelines, it is important to understand the intent of the authors. In this section, I will describe the “how and why” of the guidelines. After that, I will take a problem-oriented look at some aspects of everyday and apply specific guidelines to them.

Each guideline has an identification. This consists of one (or more) letters and a number—for example, F.22. The letter determines the section from which the guideline originates. The section F refers, for example, to functions.

The sections are further divided into subsections. For example, guidelines F.1 to F.9 together form the F.def subsection.

Ahead, I will use the identifications of the guidelines and subsections so that you can easily find them. I will quote some selected guidelines. I cannot list the entire explanation of any guideline here, but I have added a few explanatory words [in brackets] at some points.

> I can hardly say it better than the editors of the guidelines, here I provide you with an excerpt of the abstract. Abstract

This document is a set of guidelines for using C++ well. The aim of this document is to help people to use modern C++ effectively. By “modern C++” we mean effective use of the ISO C++ standard (currently C++20, but almost all of our recommendations also apply to C++17, C++14 and C++11). In other words, what would you like your code to look like in 5 years’ time, given that you can start now? In 10 years’ time?

The guidelines are focused on relatively high-level issues, such as interfaces, resource management, memory management, and concurrency. Such rules affect application architecture and library design. Following the rules will lead to code that is statically type safe, has no resource leaks, and catches many more programming logic errors than is common in code today. And it will run fast—you can afford to do things right.

Many of the rules are designed to be supported by an analysis tool. Violations of rules will be flagged with references to the relevant rule. We do not expect you to memorize all the rules before trying to write code. One way of thinking about these
