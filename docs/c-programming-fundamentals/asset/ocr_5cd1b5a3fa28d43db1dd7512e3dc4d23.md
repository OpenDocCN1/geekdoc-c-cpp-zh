+   33. `fseek()` should be preferred over `rewind()` mainly because
+      a. In `rewind()`, there is no way to check if the operations were completed successfully
+      b. `rewind()` does not work for empty files
+      c. `rewind()` does work for empty files
+      d. All of the above

+   34. Which function is used to return to the first position back from the end of a file object?
+      a. `Seekg`
+      b. `Seekp`
+      c. Both seekg and seekp
+      d. None of the above

+   35. Which among following is used to open a file in binary mode?
+      a. `ios::app`
+      b. `ios::out`
+      c. `ios::in`
+      d. `ios::binary`

+   36. How can we get to the position at the nth byte of fileObject?
+      a. `fileObject.seekg( 'filename', n );`
+      b. `fileObject.seekg( n, 'filename' );`
+      c. `fileObject.seekg( n );`
+      d. `fileObject.seekg( n, ios::app );`

+   37. Where is a file temporarily stored before a read or write operation is performed in C++?
+      a. RAM
+      b. Notepad
+      c. Buffer
+      d. Hard disk