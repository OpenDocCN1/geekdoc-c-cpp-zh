# String

Chapter 11

# Chapter Objective

+   - Defining the string in C++
+   - Defining the various functions on string such as upper, lower, mid, left
+   - Searching of pattern in a string
+   - Discussing the brute force, KMP and Rabin karp algorithm.

# 11.1 INTRODUCTION

Strings are widely used in text based component of data structure. In languages like C and C++, it is represented with the help of character array. To manipulate the string, a number of functions already exist in the string header file. However, we may need more functions to accomplish many of the routine tasks such as extracting the string, searching for the specific pattern, conversion from one case to another case, etc.

In string, to achieve a single task many functions exist and each of them are representing various approaches based on their expert perspective. However, usage of these methods is governed by various factors including processing time, ease of use and resources capability.

Many string functions needed in our variety of needs have been described in the upcoming sub-section.

# 11.2 SIGNIFICANT FUNCTIONS OF STRING

To accomplish any task related to string, either we have to use the functions that are already defined in the string header file or we have to create our own functions. However, this section describes some of the complex functions that are widely needed for the string.

# 11.2.1 Converting the string case into other case

Due to variety of reasons, we need to convert the string text in upper, lower or sentence case. Therefore, function must exist that should facilitate the conversion from one case to another case. Various popular case conversion functions such as in lower case, upper case, sentence case, etc. have been defined as follows.

# A. Upper case conversion

Upper case conversion function is used to convert the string characters from lower case to