
characters can be written to output using *p++=c:

ostreambuf_iterator<C,Tr> (§iso.24.6.4) (continues) ostreambuf_iterator p {os}; p is an iterator for os.rdbuf(); noexcept ostreambuf_iterator p {psb}; p is an iterator for the istreambuf *psb; noexcept
Section 38.6.3.2 ostreambuf_iterator 1107
ostreambuf_iterator<C,Tr> (continued) (§iso.24.6.4)

p=c If !p.failed() call the streambuf’s sputc(c)
*p Do nothing
++p Do nothing
p++ Do nothing
p.failed() Has a sputc() on p’s streambuf reached eof? noexcept

## 38.7 Advice

- [1] Define << and >> for user-defined types with values that have meaningful textual representations; §38.1, §38.4.1, §38.4.2.
- [2] Use cout for normal output and cerr for errors; §38.1.
- [3] There are iostreams for ordinary characters and wide characters, and you can define an iostream for any kind of character; §38.1.
- [4] There are standard iostreams for standard I/O streams, files, and strings; §38.2.
- [5] Don’t try to copy a file stream; §38.2.1.
- [6] Binary I/O is system specific; §38.2.1.
- [7] Remember to check that a file stream is attached to a file before using it; §38.2.1.
- [8] Prefer ifstreams and ofstreams over the generic fstream; §38.2.1.
- [9] Use stringstreams for in-memory formatting; §38.2.2.
- [10] Use exceptions to catch rare bad() I/O errors; §38.3.
- [11] Use the stream state fail to handle potentially recoverable I/O errors; §38.3.
- [12] You don’t need to modify istream or ostream to add new << and >> operators; §38.4.1.
- [13] When implementing a iostream primitive operation, use sentry; §38.4.1.
- [14] Prefer formatted input over unformatted, low-level input; §38.4.1.
- [15] Input into strings does not overflow; §38.4.1.
- [16] Be careful with the termination criteria when using get(), getline(), and read(); §38.4.1.
- [17] By default >> skips whitespace; §38.4.1.
- [18] You can define a << (or a >>) so that it behaves as a virtual function based on its second operand; §38.4.2.1.
- [19] Prefer manipulators to state flags for controlling I/O; §38.4.3.
- [20] Use sync_with_stdio(true) if you want to mix C-style and iostream I/O; §38.4.4.
- [21] Use sync_with_stdio(false) to optimize iostreams; §38.4.4.
- [22] Tie streams used for interactive I/O; §38.4.4.
- [23] Use imbue() to make an iostream reflect “cultural differences” of a locale; §38.4.4.
- [24] width() specifications apply to the immediately following I/O operation only; §38.4.5.1.
- [25] precision() specifications apply to all following floating-point output operations;
§38.4.5.1.
- [26] Floating-point format specifications (e.g., scientific) apply to all following floating-point output operations; §38.4.5.2.
- [27] #include <iomanip> when using standard manipulators taking arguments; §38.4.5.2.
- [28] You hardly ever need to flush(); §38.4.5.2.
- [29] Don’t use endl except possibly for aesthetic reasons; §38.4.5.2.
- [30] If iostream formatting gets too tedious, write your own manipulators; §38.4.5.3.
- [31] You can achieve the effect (and efficiency) of a ternary operator by defining a simple function object; §38.4.5.3.

## Locales

> *When in Rome, do as the Romans do.*  
> —Proverb

- Handling Cultural Differences
- Class `locale`
  Named `locales`; Comparing `strings`
- Class `facet`
  
  Accessing `facets` in a `locale`; A Simple User-defined `facet`; Uses of `locales` and `facets`
- Standard `facets`
  `string` Comparison; Numeric Formatting; Money Formatting; Date and Time Formatting; Character Classification; Character Code Conversion; Messages
- Convenience Interfaces
  Character Classifications; Character Conversions; String Conversions; Buffer Conversions
- Advice

## 39.1 Handling Cultural Differences

A `locale` is an object that represents a set of cultural preferences, such as how strings are compared, the way numbers appear as human-readable output, and the way characters are represented in external storage. The notion of a *locale* is extensible so that a programmer can add new `facets` to a `locale` representing locale-specific entities not directly supported by the standard library, such as postal codes (zip codes) and phone numbers. The primary use of `locales` in the standard library is to control the appearance of information written to an `ostream` and the format of data read by an `istream`.

This chapter describes how to use a `locale`, how a `locale` is constructed out of `facets`, and how a `locale` affects an I/O stream.

The notion of a locale is not primarily a C++ notion. Most operating systems and application environments have a notion of locale. Such a notion is – in principle – shared among all programs on a system, independently of which programming language they are written in. Thus, the C++ standard-library notion of a locale can be seen as a standard and portable way for C++ programs to access information that has very different representations on different systems. Among other things, a C++ `locale` is an interface to system information that is represented in incompatible ways on different systems.

Consider writing a program that needs to be used in several countries. Writing a program in a style that allows that is often called *internationalization* (emphasizing the use of a program in many countries) or *localization* (emphasizing the adaptation of a program to local conditions). Many of the entities that a program manipulates will conventionally be displayed differently in those countries. We can handle this by writing our I/O routines to take this into account. For example:

```
`void print_date(const Date& d) // printing the appropriate format`
```
```
{
switch(where_am_I) { // user-defined style indicator
case DK: // e.g., 7. marts 1999
cout << d.day() << "." << dk_month[d.month()] << " " << d.year();
break;
case ISO: // e.g., 1999-3-7
cout << d.year() << "-" << d.month() << "/" << d.day();
break;
case US: // e.g., 3/7/1999
cout << d.month() << "/" << d.day() << "/" << d.year();
break;
//...
}
}
```

This style of code does the job. However, such code is ugly and hard to maintain. In particular, we have to use this style consistently to ensure that all output is properly adjusted to local conventions. If we want to add a new way of writing a date, we must modify the application code. Worse yet, writing dates is only one of many examples of cultural differences.

Consequently, the standard library provides an extensible way of handling cultural conventions. The iostream library relies on this framework to handle both built-in and user-defined types (§38.1). For example, consider a simple loop copying (Date,double) pairs that might represent a series of measurements or a set of transactions:

```
void cpy(istream& is, ostream& os) // copy(Date,double) stream
{
Date d;
double volume;

while (is >> d >> volume)
os << d << ' ' << volume << '\n';
}
```

Naturally, a real program would do something with the records and ideally also be a bit more careful about error handling.

How would we make this program read a file that conformed to French conventions (where a comma is the character used to represent the decimal point in a floating-point number; for example,

# Section 39.1 Handling Cultural Differences 1111

12,5 means twelve and a half) and write it according to American conventions? We can define locales and I/O operations so that cpy() can be used to convert between conventions:

```
void f(istream& fin, ostream& fout, istream& fin2, ostream& fout2)
{
fin.imbue(locale{"en_US.UTF-8"}); // AmericanEnglish
fout.imbue(locale{"fr_FR.UTF-8"}); // French
```
```
cpy(fin,fout); // read American English, write French // ...
fin2.imbue(locale{"fr_FR.UTF-8"}); // French
fout2.imbue(locale{"en_US.UTF-8"}); // American English
cpy(fin2,fout2); // read French, write American English // ...
}
```

Given these streams:

```
Apr 12, 1999 1000.3
Apr 13, 1999 345.45
Apr 14, 1999 9688.321
...
3 juillet 1950 10,3
3 juillet 1951 134,45
3 juillet 1952 67,9
...
```

this program would produce:

```
12 avril 1999 1000,3
13 avril 1999 345,45
14 avril 1999 9688,321
...
July 3, 1950 10.3
July 3, 1951 134.45
July 3, 1952 67.9
...
```

Much of the rest of this chapter is devoted to describing the mechanisms that make this possible and explaining how to use them. However, most programmers will have little reason to deal with the details of locales and will never explicitly manipulate a locale. At most, they will simply retrieve a standard locale and imbue a stream with it (§38.4.5.1).

- The concept of localization (internationalization) is simple. However, practical constraints make the design and implementation of locale quite intricate:
  
- [1] A locale encapsulates cultural conventions, such as the appearance of a date. Such conventions vary in many subtle and unsystematic ways. These conventions have nothing to do with programming languages, so a programming language cannot standardize them.
  
- [2] The concept of a locale must be extensible, because it is not possible to enumerate every cultural convention that is important to every C++ user.
  
- [3] A locale is used in operations (e.g., I/O and sorting) from which people demand run-time efficiency.
  
- [4] A locale must be invisible to the majority of programmers who want to benefit from facilities “doing the right thing” without having to know exactly what “the right thing” is or how it is achieved.
  
- [5] A locale must be available to designers of facilities that deal with culture-sensitive information beyond the scope of the standard.

The mechanisms provided to compose those locales and to make them trivial to use constitute a little programming language of their own.
