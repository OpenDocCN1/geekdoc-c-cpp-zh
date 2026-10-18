```
```cpp
public:
    // ...

    auto reflection( void ) const
    {
        return std::tie( fAuthor, fTitle, fPubYear );
    }
};
```
```

+   a. Augment the TBook class with the remaining special functions.
+   
+   b. Add the overloaded `operator ==` and `operator <`, as well as the streaming operators, taking advantage of the reflection method.
+   
+   c. Extend the reflection method to operate in the class hierarchy (make it virtual).

+   21. When writing generic components using templates it is sometimes important to assure that the supplied types fulfil specific properties. For example, we may allow only signed types or types that can be compared with the `==` and `!=` operators, etc. Such generic expectations of the template arguments can be verified with the *concepts* predicates, the new powerful feature of the C++20 standard.
+   
+      a. Read and learn about the concepts (e.g. B. Stroustrup: Concepts: The Future of Generic Programming, 2017, [https://www.stroustrup.com/good_concepts.pdf](https://www.stroustrup.com/good_concepts.pdf); [https://en.cppreference.com/w/cpp/concepts](https://en.cppreference.com/w/cpp/concepts)). Write your own concept, say `exclusively_unsigned`, to assure that a type comes exclusively from the unsigned types.
+   
+      b. Refactor the `RevertEndianess` template function from Listing 4.16 to use your `exclusively_unsigned` concept. Verify the compiler messages when a signed type is tried.
+   
+      c. Design and implement concepts for the `TStackFor` template class used in Section 6.6.6.

+   22. The `std::optional`, which we used in Section 6.2.5, has two companions:
+   
+      a. The template `std::variant` that can represent many objects of potentially different types, from which only one is held at a time. Read about the `std::variant` ([https://www.bfilipek.com/2018/06/variant.html](https://www.bfilipek.com/2018/06/variant.html)) and refactor the function `GetRoots` from the code from Section 3.16 to return the `std::variant` holding either one or two roots or an error code.
+   
+      b. The non-template `std::any` which can hold an object of any type which can be further changed in the run-time for example to pass ownership of arbitrary values ([https://www.bfilipek.com/2018/06/any.html](https://www.bfilipek.com/2018/06/any.html)). Consider refactoring the `fVal` member of the `ValueLeafNode` from Listing 6.16 to the `std::any` to stand for any object representing a value such as a `int`, `double` or `std::string`. What are the differences between these two designs?

23. In Section 6.2 we processed the XML file with the grep library. However, XML files can be processed with one of many C++ libraries, such as Xerces-C++ ([http://xerces.apache.org/xerces-c/](http://xerces.apache.org/xerces-c/)) or RapidXML ([http://rapidxml.sourceforge.net/](http://rapidxml.sourceforge.net/)). With the help of one of them write a program to process XML file to extract information on the currency exchange ratios.

24. JSON is another popular format for data storage and representation. There are also some C++ libraries for processing JSON formats, e.g. by Niels Lohmann ([https://github.com/nlohmann/json](https://github.com/nlohmann/json)) or RapidJSON ([https://github.com/Tencent/rapidjson](https://github.com/Tencent/rapidjson)). Using one of these header-only libraries write a module to write and read currency information from Section 6.2 to and from the *currency.json* file.