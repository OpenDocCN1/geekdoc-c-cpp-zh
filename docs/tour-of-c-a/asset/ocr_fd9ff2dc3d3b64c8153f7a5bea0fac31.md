# 9

# Library Overview

> Why waste time learning when ignorance is instantaneous?
— Hobbes

+   - Introduction
- Standard-Library Components
- Standard-Library Organization
Namespaces; The ranges namespace; Modules; Headers
- Advice

# 9.1 Introduction

No significant program is written in just a bare programming language. First, a set of libraries is developed. Then they form the base for further work. Most programs are tedious to write in the bare language, whereas just any task can be rendered simple by the use of good libraries.

Continuing from Chapters 1–8, Chapters 9–18 give a quick tour of key standard-library facilities. I briefly present useful standard-library types, such as string, ostream, variant, vector, map, path, unique_ptr, thread, regex, system_clock, time_zone, and complex, as well as the most common ways of using them.

As in Chapters 1–8, you are strongly encouraged not to be distracted or discouraged by an incomplete understanding of details. The purpose of this chapter is to convey a clear understanding of the most useful library facilities.

The specification of the standard library is over thirds of the ISO C++ standard. Explore it, and prefer to home-made alternatives. Much thought has gone into its design, more still into its implementations, and much effort will go into its maintenance and extension.

The standard-library facilities described in this book are part of every complete C++