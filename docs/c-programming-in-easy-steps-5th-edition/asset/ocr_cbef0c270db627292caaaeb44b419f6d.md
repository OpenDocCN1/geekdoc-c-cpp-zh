# Making arrays of pointers

A variable of the regular **char** data type can be assigned a single character value, but a pointer to a constant **char** array can usefully be assigned a string of characters. The string is actually stored as an array of characters, with one character per element, but referencing the **char** pointer will automatically retrieve the entire string.

This ability to retrieve a string value from a **char** pointer using just its variable name resembles the way that a string can be retrieved from a regular **char** array using its variable name.

Multiple strings can be stored in a constant **char** pointer array, with one string per element. You can even store multiple **char** pointer arrays in a “master” **char** pointer array -- one array per element.

![](bbox=[0.118, 0.297, 0.188, 0.344])

+   1. Start a new program by specifying the C++ library classes to include, and a namespace prefix to use.
+   
+   ```cpp
+   #include <iostream>
+   using namespace std;
+   ```

+   2. Add a main function containing a final **return** statement and declaring two initialized variables -- a regular character array, and a character pointer with identical **string** values.
+   
+   ```cpp
+   int main()
+   {
+       char letters[8] = {'C', '+', '+', ' ', 'F', 'u', 'n', '\0'};
+       const char* text = "C++ Fun";
+       // Add more statements here.
+       return 0;
+   }
+   ```

+   3. In the main function, insert statements to declare, and initialize two further character pointer variables, with unique **string** values.
+   
+   ```cpp
+   const char* term = "Element";
+   const char* lang = "C++";
+   ```

+   4. Next, insert a statement to declare a character pointer array, initialized with three **string** values.
+   
+   ```cpp
+   const char* ap1[3] = {"Great", "Program", "Code"};
+   ```

![](bbox=[0.118, 0.675, 0.208, 0.735])

Character values must be enclosed in single quotes, but string values must be enclosed in double quotes -- even when they are being assigned to a **char** pointer.

+   5. Now, insert a statement to declare a second character pointer array, initialized with three string values -- making one of the pointer variables its first element value.
+   
+   ```cpp
+   const char* ap2[3] = {lang, "is", "Fun"};
+   ```

+   6. Declare two “master” character pointer arrays, each initialized with three elements of the **char** pointer arrays.
+   
+   ```cpp
+   const char* ap3[3] = {ap2[0], ap2[1], ap1[0]};
+   const char* ap4[3] = {ap1[2], ap2[1], ap2[2]};
+   ```

+   7. After the declarations, insert statements to output the identical **string** values of the first two variables.