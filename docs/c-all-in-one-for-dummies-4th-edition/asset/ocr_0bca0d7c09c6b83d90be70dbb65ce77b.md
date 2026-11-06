# # Considering the Standard Library Categories

The Standard Library documentation uses a formal approach that you're going to find difficult to read and even harder to understand; it must have been put together by lawyers more interested in the precise meaning of words rather than the usability of the document. This immense tome (1,300+ pages) requires quite a bit of time to review. Fortunately, you don't have to wade through all that legal jargon mixed indiscriminately with computer jargon and the occasional bit of English. This chapter provides the overview you need to get going quickly.

The best way to begin is to break the Standard Library into smaller pieces. You can categorize the Standard Library functions in a number of ways. One of the most common approaches is to use the following categories:

| Algorithms | Atomic Operations (C++ 11 and above) | C Compatibility |
| --- | --- | --- |
| Concepts (C++ 20 and above) | Containers | Coroutines (C++ 20 and above) |
| Filesystem (C++ 17 and above) | Input/Output | Iterators |
| Localization | Numerics | Ranges (C++ 20 and above) |
| Regular Expressions (C++ 11 and above) | Strings | Thread Support (C++ 11 and above) |
| Utilities | | |

Note that this table doesn't include the *Standard Library Extensions*, additions that add specialized (non-general) functionality, which appear at https://en.cppreference.com/w/cpp/experimental/lib_extensions_2. The following sections provide a brief description of each of these categories and tell what you can expect to find in them. Knowing the category can help you locate the function you need quickly on websites that use these relatively standard category names.

# ## Algorithms

*Algorithms* perform data manipulations such as replacing, locating, or sorting information. You've already seen some algorithms used in the book because it's hard to create a substantial application without using one. There aren't any types in the Algorithms category. The following is a list of common algorithm functions