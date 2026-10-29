# Point of Information

**Should You Use a C-String or a string Class Object?**

The reasons for using a C-string are as follows:

+   - The programmer has control over how the C-string is stored and manipulated.
+   - Many useful functions are available for entering, examining, and processing C-strings.
+   - C-strings are an excellent way to explore advanced programming techniques with pointers (see Section 15.2).
+   - You’ll encounter them throughout your programming career, as they’re embedded in almost all existing C++ code.
+   - They’re fun to program.

The reasons for using a string class object are as follows:

+   - The string class does an automatic bounds check on every index used to access string elements. This isn’t true for C-strings, and using an invalid C-string subscript can result in a system crash.
+   - The string class automatically expands and contracts storage as needed. C-strings are fixed in length and subject to overrunning the allocated storage space.
+   - The string class provides extensive methods for operating on a string. C-strings almost always require a subsidiary set of functions.
+   - When necessary, it’s easy to convert to a C-string with the string class’s `c_str()` method. Conversely, a C-string can be converted to a string class object easily by simply assigning it to a string object.

**Table 15.1** String and Character I/O Methods (Require the Header File `iostream`)

| C++ Method | Description | Example |
|---|---|---|
| `cin.getline(str,n,ch)` | Inputs a C-string (`str`) from the keyboard, up to a maximum of n characters, that’s terminated by the character ch (typically the newline character, `\n`) | `cin.getline(str, 81, '\n');` |
| `cin.get()` | Extracts the next character from the input stream | `nextKey = cin.get();` |
| `cin.peek()` | Returns the next character from the input stream without extracting the character from the stream | `nextKey = cin.peek();` |
| `cout.put(charExp)` | Places the character value of charExp on the output stream | `cout.put('A');` |