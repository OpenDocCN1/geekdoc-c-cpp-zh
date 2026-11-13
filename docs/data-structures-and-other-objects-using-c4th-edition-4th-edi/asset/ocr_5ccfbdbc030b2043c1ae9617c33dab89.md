# **Parameter Matching for Member Functions of Template Classes**

In the implementation of a template function, we are careful to help the compiler by providing template parameter for each of the function’s parameters. (See “Mismatches for Template Function Arguments” on page 299.) However, this help is not needed for member functions of a template class. For example, we can use a simple size_type parameter for the bag’s reserve function. Unlike an ordinary template function, the compiler is able to match a size_type parameter of a member function with any of the usual integer arguments (such as int or const int). If b is a bag object of our new template class, then we may call b.reserve(42), with the actual argument being the integer 42. The compiler will convert this integer to the equivalent size_type value.

# **Using the Template Class**

Using the bag template class is easy. A program includes the bag4.h header file, and then any kind of bag can be declared. To declare a bag, you write the class name, bag, followed by the name of the data type for the template parameter (in angle brackets). For example, if a program needs one bag of characters and one bag of double numbers, then the program uses these two declarations:

```
bag<char> letters;
bag<double> scores;
```

When an actual bag is declared, as in these examples, the template parameter is said to be instantiated. In the letters bag, the template parameter is instantiated as a character; in the scores bag, the template parameter is instantiated as a double number. A program that includes the string header file can even create a bag of strings, as shown here:

```
bag<string> verbs;
```

Figure 6.3 on page 310 shows a program that uses a bag of integers and two bags of strings. The program asks the user to type several adjectives, numbers, and names. These items are placed in the bags, and then items are grabbed out of the bags in order for the program to write a silly story called “Life.”
The bags are declared in the demonstration program as you would expect:

```
bag<string> adjectives; // Contains adjectives typed by user
bag<int> ages; // Contains ages in the teens
bag<string> names; // Contains names typed by user
```

After these declarations, the program can use the bags adjectives and names just like any other bag of strings, whereas ages can be used just like any other bag of integers. Let’s discuss the details of the story-writing program.