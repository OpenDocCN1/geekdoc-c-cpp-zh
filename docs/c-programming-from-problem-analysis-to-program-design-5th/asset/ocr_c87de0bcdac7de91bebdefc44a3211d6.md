```
```cpp
str = "ABCDEFGHIJK";
cout << str << endl;
cout << str.length() << endl;

str[0] = 'a';
str[2] = 'd';

cout << str << endl;

return 0;
}
```
```

12. Consider the following statement:

```cpp
string str = "Now is the time for the party!";
```

What is the output of the following statements? (Assume that all parts are independent of each other.)

+   a. `cout << str.size() << endl;`
+   
+   b. `cout << str.substr(7, 8) << endl;`
+   
+   c.
+   ```cpp
+   string::size_type ind = str.find('f');
+   string s = str.substr(ind + 4, 9);
+   cout << s << endl;
+   ```
+   
+   d. `cout << str.insert(11, "best ") << endl;`
+   
+   e.
+   ```cpp
+   str.erase(16, 14);
+   str.insert(16, "to study for the exam?");
+   cout << str << endl;
+   ```

# PROGRAMMING EXERCISES

+   1.
+      a. Define an enumeration type, `triangleType`, that has the values `scalene`, `isosceles`, `equilateral`, and `noTriangle`.
+   
+      b. Write a function, `triangleShape`, that takes as parameters three numbers, each of which represents the length of a side of the triangle. The function should return the shape of the triangle. *(Note: In a triangle, the sum of the lengths of any two sides is greater than the length of the third side.)*
+   
+      c. Write a program that prompts the user to input the length of the sides of a triangle and outputs the shape of the triangle.

2. Redo Programming Exercise 14 of Chapter 4 (cell phone company) so that all of the named constants are defined in a `namespace`.

3. The Programming Example: Pig Latin Strings converts a string into the pig Latin form, but it processes only one word. Rewrite the program so that it can be used to process a text of an unspecified length. If a word ends with a punctuation mark, in the pig Latin form, put the punctuation at the end of the string. For example, the pig Latin form of `Hello!` is `ello-Hay!`. Assume that the text contains the following punctuation marks: `,` (comma),