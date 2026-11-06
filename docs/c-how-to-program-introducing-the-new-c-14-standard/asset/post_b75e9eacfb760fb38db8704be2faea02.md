
- Random-number generation, simulation and game playing. To help make programs more secure, we include a treatment of C++11’s non-deterministic random-number generation capabilities.
- Pointers. We provide thorough coverage of the built-in pointer capabilities and the intimate relationship among built-in pointers, C strings and built-in arrays.
- Visual presentation of searching and sorting, with a simple explanation of Big O.
- Printed book contains core content; additional content is online. Several online chapters and appendices are included. These are available in searchable PDF format on the book’s password-protected Companion Website—see the access card information on the inside front cover.
- Getting Started Videos. At [http://www.deitel.com/books/cpphtp10](http://www.deitel.com/books/cpphtp10), we provide links to our getting-started videos that help readers begin using Microsoft Visual Studio 2015 Community edition on Windows, Apple Xcode on OS X and GNU C++ on Linux.
- Debugger appendices. On the book’s Companion Website we provide Appendix H, Using the Visual Studio Debugger, Appendix I, Using the GNU C++ Debugger and Appendix J, Using the Xcode Debugger.

## New in This Edition

- Discussions of the new C++14 capabilities.
- Further integration of C++11 capabilities into the code examples, because the latest compilers are now supporting these features.
- Uniform initialization with list initializer syntax.
- Always using braces in control statements, even for single-statement bodies:

  ```cpp
  if (condition) {
      single-statement or multi-statement body
  }
  ```

- Replaced the `GradeBook` class with `Account`, `Student` and `DollarAmount` class case studies in **Chapters 3**, **4** and **5**, respectively. `DollarAmount` processes monetary amounts precisely for business applications.
- C++14 digit separators in large numeric literals.
- `Type &` is now `Type&` in accordance with industry idiom.
- `Type *` is now `Type*` in accordance with industry idiom.
- Using C++11 scoped `enum`s rather than traditional C `enum`s.
- We brought our terminology in line with the C++ standard.
- Key terms in summaries now appear in bold for easy reference.
- Removed extra spaces inside `[]`, `()`, `<>` and `{}` delimiters.
- Replaced most `print` member functions with `toString` member functions to make classes more flexible—for example, returning a `string` gives the client code the option of displaying it on the screen, writing it to a file, concatenating it with other `strings`, etc.
- Now using `ostringstream` to create formatted `string`s for items like the `string` representations of a `Time`, rather than outputting formatted data directly to the standard output.
- For simplicity, we deferred using the three-file architecture from **Chapter 3** to **Chapter 9**, so all early class examples define the entire class in a header.
- We reimplement **Chapter 10**’s `Array` class operator-overloading example with `unique_ptr`s in Chapter 24. Using raw pointers and dynamic-memory allocation with `new` and `delete` is a source of subtle programming errors, especially “memory leaks”—`unique_ptr` and the other smart pointer types help prevent such errors.
- Using lambdas rather than function pointers in **Chapter 16**, Standard Library Algorithms. This will get readers comfortable with lambdas, which can be combined with various Standard Library algorithms to perform functional programming in C++. We’re planning a more in-depth treatment of functional programming for *C++ How to Program, 11/e*.
- Enhanced Chapter 24 with additional C++14 features.

## Object-Oriented Programming

- Early-objects approach. The book introduces the basic concepts and terminology of object technology in **Chapter 1**. You’ll develop your first customized classes and objects in **Chapter 3**. We worked hard to make this chapter especially accessible to novices. Presenting objects and classes early gets you “thinking about objects” immediately and mastering these concepts more thoroughly.[^2]

[^2]: For courses that require a late-objects approach, consider our pre-C++11 book *C++ How to Program, Late Objects Version*, which begins with six chapters on programming fundamentals (including two on control statements) and continues with seven chapters that gradually introduce object-oriented programming concepts.

- C++ Standard Library `string`. C++ offers *two types* of strings—`string` class objects (which we begin using in **Chapter 3**) and C-style pointer-based strings. We’ve replaced most occurrences of C strings with instances of C++ class `string` to make programs more robust and eliminate many of the security problems of C strings. We continue to discuss C strings later in the book to prepare you for working with the legacy code in industry. In new development, you should favor `string` objects.
- C++ Standard Library `array`. C++ offers *three* types of arrays—`array`s and `vector`s (which we start using in **Chapter 7**) and C-style, pointer-based arrays which we discuss in **Chapter 8**. Our primary treatment of arrays uses the Standard Library’s `array` and `vector` class templates instead of built-in, C-style, pointer-based arrays. We still cover built-in arrays because they remain useful in C++ and so that you’ll be able to read legacy code. In new development, you should favor class template `array` and `vector` objects.
- Crafting valuable classes. A key goal of this book is to prepare you to build valuable reusable classes. **Chapter 10** begins with a test-drive of class template `string` so you can see an elegant use of operator overloading before you implement your own customized class with overloaded operators. In the **Chapter 10** case study, you’ll build your own custom `Array` class, then in the **Chapter 18** exercises you’ll convert it to a class template. You will have truly crafted valuable classes.
- Case studies in object-oriented programming. We provide several well-engineered real-world case studies, including the `Account` class in **Chapter 3**, `Student` class in **Chapter 4**, `DollarAmount` class in **Chapter 5**, `GradeBook` class in **Chapter 7**, the `Time` class in **Chapter 9**, the `Employee` class in **Chapters 11–12** and more.
- Optional case study: Using the UML to develop an object-oriented design and C++ implementation of an ATM. The UML™ (Unified Modeling Language™) is the industry-standard graphical language for modeling object-oriented systems. We introduce the UML in the early chapters. Online Chapters 25 and 26 include an *optional* object-oriented design case study using the UML. We design and fully implement the software for a simple automated teller machine (ATM). We analyze a typical requirements document that specifies the system to be built. We determine the classes needed to implement that system, the attributes the classes need to have, the behaviors the classes need to exhibit and we specify how objects of the classes must interact with one another to meet the system requirements. From the design we produce a complete C++ implementation. Students often report that the case study helps them “tie it all together” and truly understand object orientation.
- Understanding how polymorphism works. **Chapter 12** contains a detailed diagram and explanation of how C++ typically implements polymorphism, `virtual` functions and dynamic binding “under the hood.”
- Object-oriented exception handling. We integrate basic exception handling early in the book (**Chapter 7**). Instructors can easily pull more detailed material forward from **Chapter 17**, Exception Handling: A Deeper Look.
- Custom template-based data structures. We provide a rich multi-chapter treatment of data structures—see the Data Structures module in the chapter dependency chart (**Fig. 5**).
- Three programming paradigms. We discuss *structured programming*, *object-oriented programming* and *generic programming*.
