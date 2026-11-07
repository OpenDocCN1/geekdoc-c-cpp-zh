```
```cpp
infile >> num1 >> num2;
outfile << "Sum = " << num1 + num2 << endl;

infile.close();
outfile.close();

return 0;
}
```
```

+   21. `fstream`

+   23.
+      a. Same as before.
+      b. The file contains the output produced by the program.
+      c. The file contains the output produced by the program. The old contents are erased.
+      d. The program would prepare the file and store the output in the file.

+   25.
+      a. `outfile.open("travel.dat");`
+      b. `outfile >> fixed >> showpoint >> setprecision(2);`
+      c. `outfile >> day >> " " >> distance >> " " >> speed >> endl;`
+      d. `travelTime = distance / speed;`
+         `outfile >> travelTime;`
+      e. `fstream` and `iomanip`.

# Chapter 4

+   1. a. false; b. false; c. false; d. true; e. false; f. false; g. false; h. false; i. false; j. true; k. true

+   3. a. true; b. false; c. true; d. false; e. true

+   5.
+      a. `x == z`: 0
+      b. `y != z - 9`: 0
+      c. `x - y == z + 10`: 1
+      d. `!(z < w)`: 1
+      e. `w - y < x - 2 * w`: 0

+   7.
+      a. `//-`
+      b. `8 12 - 4`
+      c. `^:`
+      d. `++c`
+      e. `Amy`
+         `Amy < Bob`
+      f. `-12`
+         `**`

+   9.
+      a. `?%!`
+      b. `a b c d`
+         `##`
+      c. `Flying Coding`