# Introduction

As you can guess from the title, this book is set up so that you can teach yourself the C programming language in 22 one-hour lessons. Despite stiff competition from languages such as C++, Java, and C#, C remains the language of choice for people who are just learning programming. For reasons detailed in Lesson 1, "Getting Started with C;" you can't go wrong selecting C as your programming language.

You've made a wise decision selecting this book as your means of learning C. Although there are many books on C, this book presents C in the most logical and easy-to-learn sequence. The fact that the six previous editions have been on best-seller lists indicates that readers agree! This book is designed for you to work through the lessons on a daily basis. You don't need any previous programming experience with another language, such as BASIC, might help you learn faster. Also no assumptions are made about your computer or compiler; this book concentrates on teaching the C language, regardless of whether you use a PC, a Mac, or a UNIX system.

# This Book’s Special Features

This book contains some special features to aid you on your path to C enlightenment. Syntax boxes show you how to use C concepts. Each box provides concrete examples and a full explanation of the C command or concept. To get a feel for the style of the syntax boxes, look at the following example. (Don't try to understand the material; you've never reached Lesson 1!)

# Syntax

```
#include <stdio.h>
printf( format-string[arguments,...]);
```

printf() is a function that accepts a series of arguments, each applying to a conversion specifier in the given format string. It prints the formatted information to the standard output device, usually the display screen. When using printf(), you need to include the standard input/output header file, stdio.h.