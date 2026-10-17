# 5 Scalars and Formatting

A set of functions accompanies each category of data in Perl. The most extensive set of such functions concerns the scalar data category. Of these functions, most manipulate strings, but several also deal with numbers. Still others deal with both strings and numbers. In the previous chapter, you investigated the use of several functions associated exclusively with strings. In this chapter, you extend your investigation to include numbers. After investigating scalar numbers and their associated functions and operations, you are in an excellent position to examine how you can use the print functions (`print()`, `printf()`, and `sprintf()`) to effect different formatting operations. The `sprintf()` function proves to be an ideal tool for casting number types, formatting decimal numbers, setting up table columns, and using generic formatting specifiers. Among topics addressed in this chapter are the following:

+   - Distinguishing defined from undefined identifiers
+   - Operators that pertain to numbers
+   - Specification of number types
+   - The `printf()` and `sprintf()` functions
+   - Creating generic formatting identifiers in Perl
+   - Formatting output for tables

# Scalars, Functions, and Numbers

Perl poses certain dangers with respect to using numbers. The dangers arise because, if you use a string as a number in a mathematical expression, the Perl interpreter processes the string as though it were a number. It processes the string as a number because it automatically reads the string as a number when you employ the string in association with a numeric operator. Consider Listing05_01: