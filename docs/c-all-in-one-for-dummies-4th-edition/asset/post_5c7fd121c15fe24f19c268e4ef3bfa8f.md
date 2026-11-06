
- STL iterator pair (essentially a range)
- `boost::iterator_range<>` and `boost::sub_range<>`

The macro STL container support is generalized. Any object type that supports these two requirements will work:

- Nested iterator and `const_iterator` types
- `begin()` and `end()` methods

![](img/128ab511de4e7360e167e3b15cdd5dd0_883_0.png)

## Accessing the Operating System Using Filesystem

Working with files and directories is an important part of any application you create. Book 6 shows some standard techniques you use to work with both files and directories. However, these methods can become cumbersome and somewhat limited. Boost augments your ability to work with the file system using the File-system library. Creating and deleting both files and directories becomes a single call process. You can also perform tasks such as moving and renaming both files and directories.

The most important addition that Boost makes is defining a method to obtain error information from the operating system. This feature is found in the System library, which you must include as part of your application. Among other capabilities, the System library enables you to convert a numeric error that the operating system returns into a human-readable form. Unfortunately, the System library is still a work in progress, so this chapter can’t demonstrate how to use it in any great detail.

You must add references to the `libboost_filesystem-mgw6-mt-x32-1_73.a` and `libboost_system-mgw6-mt-x32-1_73.a` files using the technique found in the “Adding the RegEx library” section, earlier in this chapter, for the example to work. The project file may require that you change the library setting to match your system. When you set up this application properly, you should see two libraries on the Linker Settings tab of the Project Build Options dialog box, as shown in Figure 5-5.

![](img/128ab511de4e7360e167e3b15cdd5dd0_884_0.png)

**FIGURE 5-5:** Using the Filesystem library requires the System library as well.

### THE FILESYSTEM LIBRARY AND THE STANDARD LIBRARY

The developers of the Boost library continuously add to its capabilities. Some of the additions developers make are so useful that they end up in the Standard Library. The Filesystem library is one of these useful elements. In fact, it appears as part of C++ 17, as described in the article at https://www.fluentcpp.com/2019/11/22/how-c17-benefits-from-boost-libraries-part-two/.

Of course, standardized libraries require discussion from multiple groups, not just the Boost developers. Consequently, the Boost library you use today may not be precisely the same library you see added to the Standard Library. It’s important to keep up with the proposed technical changes to the Boost library as they move to the Standard Library by reviewing the documentation online.

The movement of code from one setting to another tends to confuse developers because they suddenly find that a favorite library has seemingly disappeared. These developers also question whether they should continue using the old library or move to the new one. In all cases, you want to use the Standard Library when you can because the Standard Library is fully supported by a standards group and is, well, standard. Consequently, when you begin creating new applications based on C++ 17 or above, you may want to consider moving from Boost to the Standard Library for the Filesystem library needs. (Ensure that your compiler also provides the required support.)

```cpp
    File.close();
} else
    cout << "File Data.txt Doesn't Exist!" << endl;

if (exists("Test/Data.txt")) {
    remove(path("Test/Data.txt"));
    cout << "Deleted Data.txt" << endl;
}

if (exists("Test")) {
    remove(path("Test"));
    cout << "Deleted Test" << endl;
}

return 0;
}
```

The first feature you should notice about this example is that it constantly checks to verify that the file or directory exists using the exists() function. Your applications should follow this pattern because you can't know that a file or directory will exist when you need to work with it, even if your application created it. A user or external application can easily delete the file or directory between the time you create it and when you need to work with it again.

### Boosting up a Step

To create a directory, you use create_directory(), which accepts a path as input. You create a path object using path(). Many of the other Filesystem library calls require a path object as well. For example, when you want to remove (delete) either a file or directory, you must supply a path object to remove(). Interestingly enough, remove() does remove a file without creating a path object, but it won't remove a directory. The inconsistent behavior can make an application that incorrectly uses remove() devilishly difficult to debug.

Notice that the example uses the boost::filesystem::ofstream and boost::filesystem::ifstream classes. If you try to compile the application without using the fully qualified name of the classes, you get an ambiguous reference error from Code::Blocks. Using the Boost version of the classes ensures maximum compatibility and fewer errors. Here is what you see when you run this application:

```text
Created Directory Test
Created File Data.txt
Data.txt contains 15 bytes.
This is a test!
Deleted Data.txt
Deleted Test
```

One final element to look at in this example is `file_size()`, which reports the size of the file in bytes. The Filesystem library provides a number of helpful statistics that you can use to make your applications robust and reliable. As previously mentioned, you want to spend time working with this library because it contains so many helpful additions to the standard capabilities that C++ provides.

## Index

### Symbols

- – (subtraction symbol), 60
- -- (minus minus)
  - decrement operator, 84, 92
  - prefix/postfix operators, 85
  - switch prefix, 166
- ! (bang), 92
- != (not equal to) operator, 107–108
- # (pound), 92, 96
- % (percent sign) modulus operator, 86
- & (ampersand), 92
  - reference operator, 197, 220, 496, 501, 505, 510, 647
- && (and) operator, 110–111
- ( ) (parentheses), 65–66, 92, 202
- * (star; asterisk), 92, 501
  - dereference operator, 201
  - multiplication symbol, 60, 84
  - pointer variables, 205, 220
- . (dot) operator, 92, 250, 555
- ... (ellipsis)
  - general exception catcher, 567
  - variadic operator, 422
- / (forward slash), 92
  - division symbol, 60, 86
  - in pathnames, 688, 729
  - switch prefix, 166
- /* */ (delimiters), 271
- // (double slash), 270–271
- : (colon)
  - conditional operators and comparisons, 99
  - range operator, 128
- :: (two colons)
  - classes and functions, 337, 575, 583, 593
  - scope resolution operator, 238
- ; (semicolon), 59, 153, 234
- ? (question mark), 99
- @ (at sign), 92
- [ ] (square brackets), 92, 388
- \ (backslash), 66, 90–92, 688, 734
- ^ (caret), 93
- { } (curly braces), 53, 55, 92–93
- || (or) operator, 110–111
- ~ (tilde), 92
- + (addition symbol), 60, 78, 97
- ++ (plus plus)
  - increment operator, 81, 92
  - prefix/postfix operators, 85
- ++i (pre-increment)
  - operator, 126
- += (plus equal) notation, 81, 96
- < (less than)
  - less than operator, 108–109
  - operator function, 653–654, 668
- <> (angle brackets), 93, 181–182
- << (insertion) operator, 59–60, 102, 223, 300, 661, 672, 698–699, 726, 738–741
- <= (less than or equal to)
  - operator, 108
- = (equals sign), 75, 417–418
- = 0 (pure specifier), 333–334
- == (equal equal), 92
  - equal to operator, 108–109
- <=> (spaceship) operator, 109–110, 216
- > (greater than) operator, 108–109
- -> (arrow) operator, 245, 247, 250, 555, 608
- >= (greater than or equal to)
  - operator, 108
- >> (extraction) operator, 102, 223, 277, 284, 712–714, 738, 741
- " (double quotes), 59, 67, 90, 93, 181–182
- ' (single quotes), 88, 90
- \0 (null) character, 89

### A

- absolute paths, 846, 853
- abstract classes, 333–334
- abstract virtual methods, 334
- Acronym Finder, 48
- AddFiles example, 170
- AddInteger example, 78–79
- AddInteger2 example, 79–81
- addition symbol (+), 60, 78, 97
- AddOne example, 149
- AddOne() function, 149–153
- AIDE (Android IDE), 33–34
- Alexander, Christopher, 336
- algorithms, Standard Library, 755–757
- allocating/deallocating memory
  - defined, 205
  - using new operator, 208
- American National Standards Institute (ANSI), 515–516
- ampersand (&), 92
  - reference operator, 197, 220, 496, 501, 505, 510, 647
  - and (&&) operator, 110–111
- Android IDE (AIDE), 33–34
- AndroidForums, 42
- angle brackets (< >), 93, 181–182
- anonymous functions, 398
