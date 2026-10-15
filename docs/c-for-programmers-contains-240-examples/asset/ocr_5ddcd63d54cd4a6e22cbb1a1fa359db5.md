you can develop an array ADT that is preferable to “raw” arrays. The array class can provide many helpful new capabilities such as

+   - subscript range checking
+   - an arbitrary range of subscripts instead of having to start with 0
+   - array assignment
+   - array comparison
+   - array input/output
+   - arrays that know their sizes
+   - arrays that expand dynamically to accommodate more elements
+   - arrays that can print themselves in neat tabular format.

We create our own array class with many of these capabilities in Chapter 11. Recall that C++ Standard Library class template vector (introduced in Chapter 7) provides many of these capabilities as well. Chapter 20 explains class template vector in detail. C++ has a small set of built-in types. Classes extend the base programming language with new types.

# Software Engineering Observation 10.13

> You can create new types through the class mechanism. These new types can be designed to be used as conveniently as the built-in types. Thus, C++ is an extensible language. Although the language is easy to extend with these new types, the base language itself cannot be changed.

New classes created in C++ environments can be proprietary to an individual, to small groups or to companies. Classes can also be placed in standard class libraries intended for wide distribution. The C++ Standard includes a standard class library. Once you learn C++ and object-oriented programming, you’ll be ready to take advantage of the new kinds of rapid, component-oriented software development made possible with increasingly abundant and rich libraries.

# 10.8.2 Example: String Abstract Data Type

C++ is an intentionally sparse language that provides programmers with only the raw capabilities needed to build a broad range of systems (consider it a tool for making tools). The language is designed to minimize performance burdens. C++ is appropriate for both applications programming and systems programming—the latter places extraordinary performance demands on programs. Certainly, it would have been possible to include a string data type among C++’s built-in data types. Instead, the language was designed to include mechanisms for creating and implementing string abstract data types through classes. We introduced the C++ Standard Library class string in Chapter 3, and in Chapter 11 we develop our own String ADT. We discuss class string in detail in Chapter 18.

# 10.8.3 Example: Queue Abstract Data Type

Each of us stands in line from time to time. A waiting line is also called a queue. We wait in line at the supermarket to check out, we wait in line to get gasoline, we wait in line to