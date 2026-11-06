Lines 21–22 output `string string1`, `string string2`, `string string3`, `double double1`, `string string4`, `int integer`, `string string5` and the address of `int integer`—all to `outputString` in memory. Line 25 uses the stream insertion operator and the call `outputString.str()` to display a copy of the `string` created in lines 21–22. Line 28 demonstrates that more data can be *appended* to the `string` in memory by simply issuing another stream insertion operation to `outputString`. Lines 29–30 display `string outputString` after appending additional characters.

An `istringstream` object inputs data from a `string` in memory to program variables. Data is stored in an `istringstream` object as characters. Input from the `istringstream` object works identically to input from any file. The end of the `string` is interpreted by the `istringstream` object as *end-of-file*.

# Demonstrating `istringstream`

**Figure 21.12** demonstrates input from an `istringstream` object. Lines 9–10 create `string input` containing the data and `istringstream` object `inputString` constructed to contain the data in `string input`. The `string input` contains the data

```
input test 123 4.7 A
```