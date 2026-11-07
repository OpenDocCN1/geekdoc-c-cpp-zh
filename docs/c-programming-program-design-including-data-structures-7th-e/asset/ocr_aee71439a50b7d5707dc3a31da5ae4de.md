+   f. `const double LENGTH = 26;`
+      `double list[LENGTH - 1];`
+   
+    g. `const long SIZE = 100;`
+      `int list[2 * SIZE];`

4. Determine whether the following array declarations are valid. If a declaration is invalid, explain why. (1, 2)

+   a. `string customers[];`
+   
+   b. `int numArray[50];`
+   
+   c. `const int SIZE = 30;`
+      `double list[20 - SIZE];`
+   
+   d. `int length = 50;`
+      `double list[length - 50];`
+   
+   e. `int ids[-30];`
+   
+   f. `colors[30] string;`

5. What would be a valid range for the index of an array of size 99? What is the index of the first element? What is the index of the last element? (1, 3)

6. Write C++ statement(s) to do the following: (1, 2)

+   a. Declare an array `alpha` of 50 components of type `int`.
+   
+   b. Initialize each component of `alpha` to −1.
+   
+   c. Output the value of the first component of the array `alpha`.
+   
+   d. Set the value of the twenty-fifth component of the array `alpha` to 62.
+   
+   e. Set the value of the tenth component of `alpha` to three times the value of the fiftieth component of `alpha` plus 10.
+   
+   f. Use a `for` loop to output the value of a component of `alpha` if its index is a multiple of 2 or 3.
+   
+   g. Output the value of the last component of `alpha`.
+   
+   h. Output the value of `alpha` so that 15 components per line are printed.
+   
+   i. Use a `for` loop to increment every other element (the even indexed elements).
+   
+   j. Use a `for` loop to create a new array, `diffAlpha`, whose elements are the differences between consecutive elements in `alpha`.

7. What is the output of the following program segment? (2)

```
int temp[5];

for (int i = 0; i < 5; i++)
    temp[i] = static_cast<int>(pow(i, 2.0));

for (int i = 0; i < 5; i++)
    cout << temp[i] << " ";
cout << endl;
```