# 23.5.1 Regular Expression Example

The program in Fig. 23.2 tries to match birthdays to a regular expression. For demonstration purposes, the expression in line 11 matches only birthdays that do not occur in April and that belong to people whose names begin with "J".

```
```cpp
// Fig. 23.2: fig23_02.cpp
// Demonstrating regular expressions.
#include <iostream>
#include <string>
#include <regex>
using namespace std; // allows use of features in both std and std::tr1

int main()
{
   // create a regular expression
   regex expression( "J.*\\d[0-35-9]\\d\\-\\d\\d" );

   // create a string to be tested
   string string1 = "Jane's Birthday is 05-12-75\n"
      "Dave's Birthday is 11-04-68\n"
      "John's Birthday is 04-28-73\n"
      "Joe's Birthday is 12-17-77";

   // create a smatch object to hold the search results
   smatch match;

   // match regular expression to string and print out all matches
   while ( regex_search( string1, match, expression,
      regex_constants::match_not_dot_newline ) )
   {
      cout << match.str() << endl; // print the matching string

      // remove the matched substring from the string
      string1 = match.suffix();
   } // end while
} // end function main
```
```

```
```text
Jane's Birthday is 05-12-75
Joe's Birthday is 12-17-77
```
```

**Fig. 23.2** | Regular expressions checking birthdays.

# *Creating the Regular Expression*

Line 11 creates a **regex** object by passing a regular expression to the regex constructor. The name regex is a typedef of the basic_regex class template that uses chars. We precede each backslash character in the initializer string with an additional backslash. Recall that C++ treats a backslash in a string literal as the beginning of an escape sequence. To insert a literal backslash in a string, you must escape the backslash character with another backslash. For example, the character class \d must be represented as \\d in a C++ string literal.

The first character in the regular expression, "J", is a literal character. Any string matching this regular expression is required to start with "J". In a regular expression, the