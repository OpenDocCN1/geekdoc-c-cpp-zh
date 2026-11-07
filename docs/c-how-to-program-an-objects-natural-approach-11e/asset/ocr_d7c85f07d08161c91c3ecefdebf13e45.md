# Modern C++

Today's C++ programmers build systems and system components using Modern C++, which includes the C++20, C++17, C++14 and C++11 standards—the digits in each name indicate the year in the 2000s when that version was approved by the ISO C++ standard committee. Many of the language and library features introduced by these standards make C++ easier to use, improve runtime performance and software quality, and enable applications to take advantage of today’s multi-core systems.

C++ is over four decades old, so there is much existing C++ code using older programming idioms—this is typically referred to as legacy code. We emphasize Modern C++ idioms in this book.

# C++ Core Guidelines

Bjarne Stroustrup, Herb Sutter (the ISO C++ committee chair) and several other contributors^45^ created the evolving C++ Core Guidelines,^46^ containing extensive recommendations and sample code to help you use Modern C++ correctly and effectively. Various code-analysis tools (discussed in Preface Section 7) enable you to check your code to ensure it follows these recommendations. We cite the C++ Core Guidelines frequently throughout this book.

# ✓ Checkpoint

+   1. *(Fill-In)* Most code for general-purpose operating systems is written in __________.
+      **Answer:** C or C++.
+   2. *(Fill-In)* The __________ provide recommendations and sample code to help you use Modern C++ correctly and effectively.
+      **Answer:** C++ Core Guidelines.

# 1.7 C++ Standard Library and Open-Source Libraries

C++ programs consist of pieces called functions and classes. You can program all the pieces you’ll need yourself. Instead, most C++ Programmers reuse the rich collections of classes and functions in the C++ standard library. Thus, there are really two parts to learning C++ programming:

+   - learning the C++ language itself (often referred to as the “core language”), and
+   - learning how to use the C++ standard library’s classes and functions.

# The Boost Project and Other Open Source Libraries

There are enormous numbers of open-source C++ libraries that can help you perform significant tasks by writing only modest amounts of code. The Boost C++ libraries provide 168 powerful open-source libraries.^47^ Boost serves as a “breeding ground” for new capa-

+   45. “C++ Core Guidelines—Acknowledgments.” Accessed March 18, 2023. https://isocpp.github.io/CppCoreGuidelines/CppCoreGuidelines#SS-ack.
+   46. “C++ Core Guidelines.” Accessed March 18, 2023. https://isocpp.github.io/CppCoreGuidelines/
+   47. “Boost 1.81.0 Library Documentation.” Accessed March 18, 2023. https://www.boost.org/doc/libs/1_81_0/.