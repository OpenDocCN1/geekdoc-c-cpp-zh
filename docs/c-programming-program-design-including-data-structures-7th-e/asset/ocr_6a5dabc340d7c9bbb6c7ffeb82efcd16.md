```
```cpp
cout << static_cast<int>(sqrt(pow(first, temp))) << endl;

message = "Predefined functions simplify programming code!";

cout << "Length of message = "
     << message.length() << endl;

return 0;
}
```
```

13. To use the functions peek and putback in a program, which header file(s) must be included in the program? (4)

14. Suppose that num is an int variable and discard is a char variable. Assume the following input data:

#34

What value (if any) is assigned to num and discard after each of the following statements executes? (Use the same input for each statement.)
(2, 4)

+   a. ```cpp
+   cin.get(discard);
+   cin >> num;
+   ```
+   
+   b. ```cpp
+   discard = cin.peek();
+   cin >> num;
+   ```
+   
+   c. ```cpp
+   cin.get(discard);
+   cin.putback(discard);
+   cin >> discard;
+   cin >> num;
+   ```

15. Suppose that name is variable of type string. What is the effect of the following statement? (8)

```
```cpp
getline(cin, name);
```
```

16. Write a C++ statement that uses the manipulator setfill to output a line containing 35 stars, as in the following line: (7)

```
```text
***********************************
```
```

17. Suppose that age is an int variable and name is a string variable. What are the values of age and name after the following input statements execute: (8)

```
```cpp
cin >> age;
getline(cin, name);
```
```

if the input is:

+   a. `23 Lance Grant`
+   
+   b.
+   ```text
+   23
+   Lance Grant
+   ```