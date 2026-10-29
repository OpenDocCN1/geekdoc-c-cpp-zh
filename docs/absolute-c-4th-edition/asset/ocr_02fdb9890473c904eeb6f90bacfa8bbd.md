# SUMMARY OF FILE I/O STATEMENTS

In this example the input comes from a file with the name `infile.txt`, and the output goes to a file with the name `outfile.txt`.

+   - Place the following include directives in your program file:
+   
+   ```cpp
+   #include <fstream>    // For file I/O
+   #include <iostream>   // For cout
+   #include <cstdlib>    // For exit
+   ```

Add the following using directives (or something similar):

```
using std::ifstream;
using std::ofstream;
using std::cout;
using std::endl;  // if endl is used
```

+   - Choose a stream name for the input stream and declare it to be a variable of type `ifstream`. Choose a stream name for the output file and declare it to be of type `ofstream`. For example:
+   
+   ```cpp
+   ifstream inStream;
+   ofstream outStream;
+   ```

+   - Connect each stream to a file using the member function `open` with the external file name as an argument. Remember to use the member function `fail` to test that the call to open was successful:
+   
+   ```cpp
+   inStream.open("infile.txt");
+   if (inStream.fail())
+   {
+       cout << "Input file opening failed.\n";
+       exit(1);
+   }
+   outStream.open("outfile.txt");
+   if (outStream.fail())
+   {
+       cout << "Output file opening failed.\n";
+       exit(1);
+   }
+   ```

+   - Use the stream `inStream` to get input from the file `infile.txt` just like you use `cin` to get input from the keyboard. For example:
+   
+   ```cpp
+   inStream >> someVariable >> someOtherVariable;
+   ```