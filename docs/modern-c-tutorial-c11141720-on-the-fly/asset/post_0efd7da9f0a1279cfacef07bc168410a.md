
- Contract . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 87
- Range . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 87
- Coroutine . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 87
- Conclusion . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 87
- Further Readings . . . . . . . . . . . . . . . . . . . . . . . . 87

## Appendix 1: Further Study Materials 88

## Appendix 2: Modern C++ Best Practices 88
- Common Tools . . . . . . . . . . . . . . . . . . . . . . . 88
- Coding Style . . . . . . . . . . . . . . . . . . . . . . 88
- Overall Performance . . . . . . . . . . . 2 88
- Code Security . . . . . . . . . . . . . . . . . . . 88
- Maintainability . . . . . . . . . . . . . . . 8 89
- Portability . . . . . . . . . . . . . . . . . . . . 89

## Preface

## Introduction

C++ user group is fairly large. From the advent of C++98 to the official finalization of C++11, it has accumulated over a decade. C++14/17 is an important complement and optimization for C++11, and C++20 brings this language to the door of modernization. The extended features of all these new standards are given to the C++ language, infused with new vitality. C++ programmers, who are still using traditional C++ (this book refers to C++98 and its previous C++ standards as traditional C++), may even be amazed by the fact that they are not using the same language while reading modern C++ code.

Modern C++ (this book refers to C++11/14/17/20) introduces a lot of features into traditional C++, which makes the whole C++ language modernized. Modern C++ not only enhances the usability of the C++ language itself, but the modification of the `auto` keywords gives us more confidence in manipulating extremely complex template types. At the same time, a lot of enhancements have been made to the language runtime. The emergence of Lambda expressions has made C++ have the "closure" feature of "anonymous functions", which is almost in modern programming languages (such as Python/Swift). It has become commonplace, and the emergence of reference has solved the problem of temporary object efficiency that C++ has been criticized.

C++17 is the direction that has been promoted by the C++ community in the past three years. It also points out an important development direction of modern C++ programming. Although it does not appear as much as C++11, it contains a large number of small and beautiful languages and features (such as structured binding), and the appearance of these features again corrects our programming paradigm in C++.

Modern C++ also adds lot of tools and methods to orient its standard library, such as `std::thread` at the level of the language itself, which supports concurrent programming and no longer depends on the underlying system on different platforms. The APIs implement cross-platform support at the language level; `std::regex` provides full regular expression support and more. C++98 has been proven to be a very successful "paradigm", and the emergence of modern C++ further promotes this paradigm, making C++ a better language for system programming and library development. Concepts verification on the compile-time of parameters, enhancing the usability of the language.

In conclusion, as an advocate and practitioner of C++, we always maintain an open mind to accept new things, and we can promote the development of C++ faster, making this old and new language more vibrant.

## Targets

- This book assumes that readers are already familiar with traditional C++ (i.e. C++98 or earlier), at least they do not have any difficulty in reading traditional C++ code. In other words, those who have long experience in traditional C++ and people who desire to quickly understand the features...

## CHAPTER 01: TOWARDS MODERN C++

### Purpose
This book introduces to a certain extent the dark magic of modern C++. However, these magics are very limited, they are not suitable for readers who want to learn advanced C++. The purpose of book is offering a quick start for modern C++. Its intent is to provide a comprehensive introduction to the relevant features regarding modern C++ (before 2020). Readers can choose interesting content according to following table to learn and quickly familiarize themselves. In addition, author would like to encourage readers should be able to use modern C++ directly in their new projects and migrate their old projects gradually after reading book.

### Code
Each chapter of book has a lot of code. If you encounter problems when writing your own code with introductory features of the book, you might as well read the source attached. All code organized by chapter, folder name is chapter number.

### Exercises
There are few Exercises at the end of each chapter for testing whether you can use the knowledge points in chapter. You can find possible answer here, folder name is chapter number.

### Chapter 01: Towards Modern C++
Compilation Environment: This book will use clang as the only compiler, and always use `-std=c++17` flag in your code.
```
clang++ -v
Apple LLVM version 10.0.1 (clang-10.0.4)
```

### 1.1 Deprecated Features
Before learning modern C++, let's take a look at the main features that have deprecated:
**Note:** Deprecated is not completely unusable, it only intended to imply that features will disappear from future standards and should be avoided. However, deprecated features are still part of the standard library, and many of them are actually "permanently" reserved for compatibility reasons.

- The string literal is no longer allowed to be assigned to `char*`. If you need to assign and initialize `char*` with string literal, you should use `char const` or `auto`.
```cpp
char* str = "hello world"; // A warning will appear
```
- C++98 exception description, `exception_handler`, `set_exception()` and other related features are deprecated and should use `noexcept`.
- `auto_ptr` is deprecated and `unique_ptr` should be used.
- `register` keyword is deprecated and can be used but no longer has any practical meaning.
- The destructor, properties for which it generates copy constructors and copy assignment operators are deprecated.
- C language type conversion is deprecated (i.e. using `convert_type`) before `static_cast`, `reinterpret_cast`, `const_cast` should be used for type conversion.
- In particular, some of the C standard libraries are deprecated in the latest C++17 standard, such as `<complex>`, `<cstdalign>`, `<cmath>`
- And many more

There are other features such as parameter binding (C++11 provides `std::bind` and `std::function`), export, and etc. also deprecated. These features mentioned above if you have never used or heard of, please don't try to understand them. You should move closer to the new standard and learn new features directly. After all, technology is moving forward.

## 1.2 Compatibilities with C

![](img/e38a3926c5c5106839ec75b97aea207_10_0.png)
Figure 1.2: Compatabilities between ISO C and ISO C++

##1.2 Compatibilities with C
For some force majeure and historical reasons, we had to use some C code (even old C code) in C++, for example, Linux system calls. Before the advent of modern C++, most people talked about "what is the difference between C and C++". Generally speaking, in addition to answering the object-oriented class features and the template features of generic programming, there is no other opinion, or even a direct answer. "Almost" is also a lot of people. The Venn diagram in Figure 1.2 roughly answers the C and C++ compatibility.

From now on, you should have the idea that "C++ is not a superset of C" in your mind (and not from the beginning, later References for further reading: the difference between C++98 and C99 is given). When writing C++, you should also avoid using program styles such as `void*` whenever possible. When you have to use C, you should pay attention to the use of `extern "C"`, separate the C language code from the C++ code, and unify the link, for instance:

```cpp
// foo.h
#ifdef __cplusplus
extern "C" {
#endif

add(int x, int y);

#ifdef __cplusplus
```
