+   - `myAccount` object, `setName` “knows” the exact object to manipulate.
+   2. Next, member function `setName` stores the argument’s value in the `myAccount` object.
+   3. When `setName` completes execution, program execution returns to where `setName` was called (line 19), then continues at line 22.

# Displaying the Name That Was Entered by the User

To demonstrate that `myAccount` now contains the name the user entered, lines 22–23

```
```cpp
cout << "Name in object myAccount is: "
     << myAccount.getName() << endl;
```
```

call member function `getName` again. As you can see in the last line of the program’s output, the name entered by the user in line 18 is displayed. When the preceding statement completes execution, the end of `main` is reached, so the program terminates.