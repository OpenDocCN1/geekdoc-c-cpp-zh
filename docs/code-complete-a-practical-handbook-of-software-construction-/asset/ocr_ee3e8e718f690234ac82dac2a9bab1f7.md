+   - Does C code treat string pointers and character arrays differently?
+   - Does C code follow the convention of declaring strings to be length CONSTANT+1?
+   - Does C code use arrays of characters rather than pointers, when appropriate?
+   - Does C code initialize strings to NULLs to avoid endless strings?
+   - Does C code use strncpy() rather than strcpy()? And strncat() and strncmp()?

# Boolean Variables

+   - Does the program use additional boolean variables to document conditional tests?
+   - Does the program use additional boolean variables to simplify conditional tests?

# Enumerated Types

+   - Does the program use enumerated types instead of named constants for their improved readability, reliability, and modifiability?
+   - Does the program use enumerated types instead of boolean variables when a variable’s use cannot be completely captured with true and false?
+   - Do tests using enumerated types test for invalid values?
+   - Is the first entry in an enumerated type reserved for “invalid”?

# Named Constants

+   - Does the program use named constants for data declarations and loop limits rather than magic numbers?
+   - Have named constants been used consistently—not used as named constants in some places and as literals in others?

# Arrays

+   - Are all array indexes within the bounds of the array?
+   - Are array references free of off-by-one errors?
+   - Are all subscripts on multidimensional arrays in the correct order?
+   - In nested loops, is the correct variable used as the array subscript, avoiding loop-index cross-talk?