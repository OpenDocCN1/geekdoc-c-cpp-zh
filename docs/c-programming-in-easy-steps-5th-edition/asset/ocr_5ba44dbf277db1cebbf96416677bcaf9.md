+   8. Now, use the stream output operator to load the initialized integer value into the **stringstream** object
+   
+   ```cpp
+   stringstream << number ;    // Load the integer.
+   ```

+   9. Use the stream input operator to extract content from the **stringstream** object into the uninitialized **string** variable
+   
+   ```cpp
+   stream >> text ;    // Extract the string.
+   ```

+   10. Perform concatenation on the **string** and output the result
+   
+   ```cpp
+   text += " Per Cent" ;
+   cout << "String value: " << text << endl ;
+   ```

+   11. Save, compile, and run the program to see the converted output values

![](bbox=[0.224, 0.25, 0.776, 0.352])

![](bbox=[0.118, 0.364, 0.207, 0.423])

Notice how the **stringstream** object's `str()` function is used here to reset its contents to an empty string.

![](bbox=[0.118, 0.469, 0.207, 0.529])

A non-empty **stringstream** object has bit flags indicating its status as good, bad, eof, or fail – these should be cleared before re-use by the **stringstream** object's `clear()` function, as demonstrated here.