+   - Certain APIs don't use lists as return types but give views or iterators instead. For example, the dictionary methods dict.keys(), dict.items(), and dict.values() return views instead of lists.
- Integers have only one type now (“long” integers for those who know them in other languages)
- The default value for division (e.g. 1/2) is to return a float value. To have truncating behavior, i.e. return just the whole number, you must use a double forward slash: 1//2.
- All text (a.k.a. “strings”) is Unicode; 8-bit strings are no longer.
- “!=” is the only way to state “not equal to”; the old way (“<>”) has been removed.
- Calling modules from within functions is essentially gone. The statement “from module import *” can only be used at the module level, not in functions.
- String formatting has been changed, removing the need for the “%” formatting operator.
- The exception APIs have been changed to clean them up and add new, powerful features.
- raw_input() has been changed to just input().
- The C language API has been modified, such as removing support for several operating systems.

If you need to port Python 2.x code to version 3.0, there is a simple utility called “2to3” that will automatically correct and modify the legacy code to the new version. Generally speaking, you simply call the 2to3 program and let it run; it is robust enough to handle the vast majority of code changes necessary. However, the library is flexible enough to allow you to write your own “fixer” code if something doesn't work correctly.