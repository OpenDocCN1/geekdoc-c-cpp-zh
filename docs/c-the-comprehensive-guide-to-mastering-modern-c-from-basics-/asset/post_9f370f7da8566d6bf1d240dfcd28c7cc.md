
break after 72 characters. Many tools work with such a width. In higher-level languages than pure C, however, this 72-character limit is reached more quickly, which is why some teams have agreed on 80, 90, 100, 120, or even 160 characters. Ultimately, most modern tools can scroll horizontally. However, you should try not to exhaust this limit all the time: sensible breaks are best.

Where paper printouts still have to be possible in principle—for certifications and the like—the agreed-upon limit must be adhered to. It is better to create a nice wrap by hand before leaving it to the printer.

It is common to program with a fixed-width font—where iii is as wide as www. I like to use proportional fonts myself, and do well with them, but I know that I am a very rare species.

## 5.4 Lines per Function and File

If you don't let your program slide into chaos, it will be easier to maintain and service in the long term. Think about where useful “interfaces” between the program parts are at the beginning or when making extensions, and don't burden your readers with this later.

Limit the number of lines per function. If a function grows beyond this, split it up at that moment and turn it into calls to subfunctions. A common convention is to set a limit of between 20 and 100 lines. My personal rule of thumb is that a function should still fit on the screen.

The same applies to program files (mainly *.cpp files). If a file grows too much, divide it into sensible subparts. However, do not split it up arbitrarily. If you are working with classes in an object-oriented way, a common convention is to have exactly one header and one implementation file per class. If the latter is several thousand lines long, consider whether you should perhaps divide up the object hierarchy differently.

## 5.5 Brackets and Spaces

Whether you place the curly brackets on the line with if and for on the next line and then indent the brackets again or not is another question of taste and agreement within the team. One possible way to do it is this:

- Opening parenthesis to the line with the keyword
- Indent bracketed block
- Closing bracket back to indentation depth with the keyword
- Also surround single statements with brackets

For round parentheses (...) there are similar differences: Do you use a space after the if or for or the parenthesis directly after it? Are parentheses always surrounded by spaces, even after opening and before closing? A possible convention would be as follows:

- Space neither nor after the opening parenthesis
- Space after the closing parenthesis, but not before
- A space after the comma in lists, but not before

This is roughly the style you will find throughout this book. Whether you adopt it or choose a different option is ultimately irrelevant, so long as you stick to one style. For comparison, Listing 5.1 shows the style of this book and Listing 5.2 shows another one.

```cpp
// https://godbolt.org/z/eP77v498E
#include <iostream>
int func(int arg1, int arg2) {
    if(arg1 > arg2) {
        return arg1-arg2;
    } else {
        return arg2-arg1;
    }
}
int main(int argc, const char* argv[]) {
    for(int x=0; x<10; ++x) {
        for(int y=0; y<10; ++y) {
            std::cout << func(x,y) << " ";
        }
    }
    std::cout << "\n";
}
```

### Listing 5.1 Indentation, four brackets in line with keyword, few spaces.

```cpp
// https://godbolt.org/z/4TMn37ohE
#include <iostream>
int func ( int arg1, int arg2 ) {
    if (arg1 > arg2) 
        return arg1 - arg2;
    else
        return arg2 - arg1;
}
int main ( int argc, const char* argv[]) 
{
    for ( int x = 0 ; x < 10 ; ++ x)
    {
        for ( int y = 0 ; y < 10 ; ++ y)
        {
            std::cout << func ( x, y ) << " ";
        }
    }
    std::cout << "\n";
}
```

### Listing 5.2 Indentation two, curly brackets only if necessary and in own line, more spaces.

## 5.6 Names

Each identifier can be written in a specific style with the following properties:

- Capital or lowercase character at the beginning
- Capital letters throughout
- Underline _ or CamelCase for word boundaries
- Start or end with an underscore _

It makes sense to differentiate among different groups by these visual aspects and always maintain this. The same applies here: get used to a style and discuss it with your colleagues.

One possibility is as follows:

- *Variables* start with a lowercase character and continue in CamelCase, as in Value, btnCancelNow.
- *Class variables* use this style as well, but end with underscore, for example, data_, fwrite.
- *Functions and methods* are formatted like variables, as in getData(), assertEquals() or instead of CamelCase, they can use underscores, as in get_data().
- *Simple types* start with a lowercase character.
- *Classes* start with CamelCase.
- Constants are written in uppercase.
- Macros are written in uppercase.

## 6 HIGHER DATA TYPES

## Strings and Streams

- string: Basic string type in C++.
- wstring, u16string, u32string, u8string: String types for international character.
- ostream and ofstream: General output stream and the output stream for a file.
- istream and ifstream: General input stream and the input stream for a file.
- cout, cin, cerr and clog: Predefined standard streams for input and output.
- operator<< and operator>>: Operators for input and output to and from data streams.
- Manipulator: Construct to change the input and output format of a stream.
- Container: An abstract data type that serves as a receptacle for data. The stored elements all have the same type, which you specify when creating the container.
- Sequence container: Above all, vector is an all-around container and allows access by integer index.
- Algorithm: In C++, this usually refers to a function that works on elements in containers.
- Pointer: A type of reference to values that can assume the “no reference” state.
- C-array: A special form of container that works well with C, usually represented by a pointer and the end or length of the array.
