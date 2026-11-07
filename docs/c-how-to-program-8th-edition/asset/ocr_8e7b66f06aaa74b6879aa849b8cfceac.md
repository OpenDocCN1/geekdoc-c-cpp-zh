+   - **Boost.Function** (p. 939) allows you to store function pointers, member-function pointers and function objects in a function wrapper. A function can hold any function whose arguments and return type can be converted to match the function wrapper’s signature.
+   - **Boost.Random** (p. 939) allows you to create a variety of random number generators and distributions.
+   - A pseudo-random number generator uses an initial state to produce seemingly random numbers—using the same initial state produces the same sequence of numbers.
+   - Regular expressions (p. 940) are used to match character patterns in text.
+   - With **Boost.Regex** (p. 940), you can search for a particular expression in a string, replace parts of a string that match a regular expression and split a string into tokens using regular expressions.
+   - **Boost.Smart_ptr** (p. 940) defines smart pointers that help you manage dynamically allocated resources.
+   - **shared_ptrs** (p. 940) handle lifetime management of dynamically allocated objects. Memory is released automatically when there are no shared_ptrs referencing it.
+   - A **weak_ptr** (p. 940) allows you to observe a shared_ptr’s value without any management responsibilities.
+   - **Boost.Tuple** (p. 940) allows you to create sets of objects that can be used by generic functions.
+   - The **type_traits** (p. 940) classes allow you to determine specific traits of a type and perform type transformations to allow the object to be used in generic code.

# ### Section 23.5 Regular Expressions with the regex Library

+   - Regular expressions are specially formatted strings used to find patterns in text.
+   - **basic_regex** (p. 941) represents a regular expression.
+   - **Algorithm regex_match** (p. 941) returns true only if an entire string matches the regular expression.
+   - **Algorithm regex_search** (p. 941) returns true if any part of a string matches the regular expression.
+   - To use the regex library, include the header `<regex>`.
+   - A character class (p. 941) represents a group of characters.
+   - A word character (`\w`; p. 941) is any alphanumeric character or underscore. A whitespace character (`\s`; p. 941) is a space, tab, carriage return, newline or form feed. A digit (`\d`; p. 941) is any numeric character.

# ### Section 23.5.1 Regular Expression Example

+   - You must precede each character class’s backslash character with an additional backslash in strings.
+   - To specify sets of characters other than those that belong to a predefined character class, list the characters in square brackets, `[]`. Ranges of characters are represented by placing a `-` between two characters. Instances of the `-` character outside `[]` characters are treated as literals.
+   - Place `^` as the first character in the brackets to specify that a pattern should match anything other than the characters in the brackets.
+   - A **match_results** (p. 943) is an object that holds a match to a regular expression. The typedef **smatch** (p. 943) represents a match_results that provides access to the match result via a string; `const_iterator`.
+   - **regex_constants::match_not_eol** (p. 943) prevents the `.` character from matching a newline character.