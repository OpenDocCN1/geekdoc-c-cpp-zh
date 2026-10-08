# ## The Regular Expression Classes in C#

Regular expressions are implemented in the .NET Framework by several classes in the System.Text.RegularExpressions namespace that provide support for parsing and applying regular expression patterns and working with capturing groups.

# ### The Regex Class

The Regex class provides the implementation of the regular expression parser and the engine that applies that pattern to an input string. Using this class, you can quickly parse large amounts of text for specific patterns and easily extract and edit substrings.

The Regex class provides both instance and static members, allowing it to be used two different ways. When you create specific instances of the Regex class, the expression patterns are not compiled and cached. However, by using the static methods, the expression pattern is compiled and cached. The regular expression engine caches the 15 most recently used static regular expressions by default. You might prefer to use the static methods rather than the equivalent instance methods if you extensively use a fixed set of regular expressions.

# ### The Match and MatchCollection Classes

When a regular expression is applied to a string using the Match method of the Regex class, the first successful match found is represented by an instance of the Match class. The MatchCollection contains the set of Matches found by repeatedly applying the regular expression until the first unsuccessful match occurs.

# ### The Group and Capture Classes

The Match.Groups property represents the collection of captured groups in a single match. Each group is represented by the Group class, which contains a collection of Capture objects returned by the Captures property. A Capture represents the results from a single subexpression match.

# ### String Validation Using Regular Expressions

One of the most common uses of regular expressions is to validate a string by testing if it conforms to a particular pattern. To accomplish this, you can use one of the overloads for the IsMatch method. Listing 8.13 shows using a regular expression to validate United States Zip+4 postal codes.