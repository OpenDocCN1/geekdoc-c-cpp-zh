

operators for user-defined objects for providing I/O operations. On the contrary, objects are not available in C I/O stream and it has no mechanism to provide such natural I/O to user-defined objects.

- 2. C++ I/O stream contains richer formatting options than C. It is possible to have the programmer's own format operators known as user-defined manipulators in C++. We will be learning about manipulators in Section 12.11.

- 3. Though not apparent at first glance, C++ I/O is much easier to use. We have seen the use of cin without the '&' operator unlike scanf(). We have also used overloaded << and >> operators for I/O. For file manipulation, C++ provides constructor functions, which makes it very easy to use files. Writing to and reading from text files can be performed using >> and << operators. We will be looking at those operations in Chapter 13.

> Note C++ I/O streams are object-oriented, contain richer formatting options, and are more user-friendly than C-type I/O.

## 12.3 OLD C++ I/O VS ANSI C++ I/O

ANSI C++ I/O has the following two important differences as compared to the original C++ I/O.

- **Richer set of operations**: ANSI C++ I/O has more number of operations than the old I/O. The old I/O was supported by iostream.h file, whereas the new I/O is supported by iostream file. There are some new data types and new features in the newer version of the I/O library. The ios class contains the fundamental operations that are possible to be performed on the stream. These operations are provided as member functions. The ios class also contains a number of variables that can be manipulated to achieve the desired effect on the stream that is being dealt with. I/O has been enhanced to a large extent in the newer version.

- **Separate namespace and no global sharing**: The old library used to work in the global namespace, but the new library works in the std namespace. The difference will be clearer when we study namespaces in Chapter 16. At the moment, consider namespaces as a type of wrapper. If the C++ standard library contains one function, one cannot create another function with the same name in the same namespace.

> There are two important differences between old and new C++ I/O; the new C++ I/O is richer in operations and uses a separate namespace.

> Two functions with the same name can be differentiated if they are a part of two different namespaces.

> Third-party library developers can name functions in their own way without worrying about colliding with names used by the standard library or some other library developer.

Suppose there are two abs() functions, one for absolute values (provided by the standard library) and another for displaying the absent students in an educational organization, with the same set of arguments. In such cases, the compiler is bound to get confused and hence the program will not be compiled. As per the programmer's wish, this is possible because the library functions are not available in the global namespace. If the function abs() is now defined for absent percentage, one can differentiate between both the functions, abs() (programmer's function) and std::abs() (the standard library function). Note that here it is assumed that one has not written using namespace std as usual.

This facility makes life easier for the programmers of the third-party libraries while naming their global variables and functions. They can name them as they like. If there is a need to develop a library for a client, it is possible to define functions without having to bother about possible conflicts. Without namespaces, there would have been a need to ensure that the programmer does not name the functions the same as those in the C++ standard library itself (or some other third-party library, which is already installed in the target machine). The identifier names of the programmer now have no chance of collision with the standard library identifier names.

## 12.4 PREDEFINED AND WIDE CHARACTER STREAMS

C++ has a few predefined streams. Whenever a C++ program starts execution, these streams automatically open on their own. Table 12.1 lists the predefined streams.

| Stream | Meaning | Default source/destination |
|--------|---------|---------------------------|
| cin | Standard input stream | Keyboard |
| cout | Standard output stream | Screen |
| cerr | Standard error stream with no buffer | Screen |
| clog | Standard error stream with buffer | Screen |

To receive an international standardization from the International Organization for Standardization (ISO), the designers of C++ have added some specific features to enable to work globally. One such feature is the support for wide character streams. Some of the languages (e.g., Chinese) cannot accommodate themselves in the small 8-bit footprint of ANSI. They require bigger 16-bit Unicode to represent their character set. These streams are wcin, wcout, wcerr, and wclog.

## 12.5 C++ STREAMS CLASSES HIERARCHY

![](img/0da15892b2796544fb447dc5727e9ab4_496_0.png)

The I/O hierarchy shown in Fig. 12.1 is usually mentioned without the prefix basic_, that is, basic_ios is usually referred to as ios. The ios_base class contains the details not needed for templatization. basic_ios and its descendants are all templatized. basic_streambuf provides the mechanism to access the stream using lower-level functions. It also provides services to other classes. There are a few more items in the hierarchy that are not mentioned here. One can refer to Stroustrup's classic The C++ Programming Language for further details.

## 12.6 FORMATTED AND UNFORMATTED I/O

We have already studied about formatted I/O using cout. The operator << is usually used with cout object to support formatted output. Though not used much, there are other ways of unformatted I/O. Later on, we will see how rich formatting is possible using operator <<. Besides the default << operator, there are other ways to provide unformatted I/O.

### 12.6.1 put() and get() Functions for cout

The functions cout.get() and cout.put() are used for reading and writing to the stream. These functions are similar to getc() and putc() functions available in C. cout.get() has two different versions. The first has the prototype void get(char&) and the other has the prototype char get(void). The following program looks at both the versions and also shows how put() function is used for display. Both functions operate on char and are very simple to understand. get() reads a char at a time from the input stream and put() writes a char at a time to the output stream.

```cpp
//GetAndPut.cpp
#include <iostream>
using namespace std;

int main()
{
	char ch;
	char Data1Read[100];
	char Data2Read[100];
	for(int i = 0; ; i++)
	{
		cin.get(ch);
		if(ch == '\n')
		{
			Data1Read[i] = '\0';
			break;
		}
		Data1Read[i] = ch;
	}
	for(i = 0; ch = Data1Read[i]; i++)
	{
		cout.put(ch);
	}
	cout.put('\n');
	for(int i = 0; ; i++)
	{
		ch = cin.get();
		// Other version of get()
		if(ch == '\n')
		{
			Data2Read[i] = '\0';
			break;
		}
		Data2Read[i] = ch;
	}
	for(i = 0; ch = Data2Read[i]; i++)
	{
		cout.put(ch);
	}
	cout.put('\n');
}
```

**Output**

```
This is testing of first get and put
This is testing of first get and put
This is testing of second get and put
This is testing of second get and put
```

Note two versions of get(). The first is cin.get(ch). Here, the character read from the stream is bound to the argument (ch). In the other case ch = cin.get(), the value returned from the get() function is assigned to ch. There are no arguments to the get() function at the moment.

### 12.6.2 getLine(), read(), and write() Functions

C has gets() and puts() functions for reading and writing strings. They are better than using scanf() because scanf() with %s option has a problem of terminating when a white space is encountered, whereas gets() does not suffer from this problem. These functions also provide easier management than scanf() and printf(). A similar functionality is provided in C++ using getline(), read(), and write() functions. In addition to the string parameter for reading and writing by gets() and puts(), these three functions have one additional parameter indicating the size of the string. The prototypes for these three functions are as follows:

```
cin.getline(string variable, maximum size of string that can be input)
cin.read(string variable, maximum size of string that can be input)

cout.write(string variable, maximum size of string that can be output)
```

> scanf() terminates when a white space is encountered, whereas gets() does not suffer from this problem.

> getline() terminates when a new line is entered, whereas read() is not affected by a new line.

These functions are used with old C-style strings. The C++ strings are discussed in Chapter 15. The difference between getline() and read() is that getline() terminates when a new line is entered, whereas read() does not stop when a new line is encountered. It stops only when end of file (ctrl-Z or ^Z for DOS and Windows files, and ctrl-d or ^D for Linux or UNIX files) is encountered. getline() also stops reading from the input if end of file is specified.

Let us look at Program 12.1 to understand this. The maximum number of characters has been specified as 100 while reading, but only 50 while printing; so, some portion of the string is not printed when we write cout.write.

```cpp
//GetlineAndWrite.cpp
#include <iostream>
using namespace std;

int main()
{
	char Message[100];
	cin.getline(Message, 100);
	cout.write(Message, 50);
	cout << endl;
	cin.read(Message, 100);
	cout.write(Message, 50);
	cout.write("\n", 1) ;
}
```

**Output**

```
This is testing of getline and then we have read test
```

