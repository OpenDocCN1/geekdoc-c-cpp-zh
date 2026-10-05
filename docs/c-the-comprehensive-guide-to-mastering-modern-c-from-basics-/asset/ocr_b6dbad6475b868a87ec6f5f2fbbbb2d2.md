# 28.12 Fast Conversion with \<charconv>

There are many ways to convert a string (or char*) into a number. With C++17, there is another option: from_chars from the <charconv> header. The main focus of from_chars is on performance, as it becomes increasingly important with the growing number of XML and JSON applications.

from_chars comes with the conversion function to_chars for converting numbers to strings.

from_chars shows its strengths when you have a char*, already know that you need to parse a number, and have nothing to do with locales (different decimal and thousand separators) and encodings (UTF-16, etc.).

The existing ways to convert a string to an int or the like include the following:

+   * scanf
  From C; flexible, related to printf.
* atol, atoi, atoll, atof
  From C; no way to determine the end or success of parsing.
* strtol, strtof, strtod, strtold, strtol, strtoull
  Good candidate; error checking is okay, but lacks overflow and underflow checking.
* stringstream
  C++; flexible, but slow, also lacks overflow and underflow checking.