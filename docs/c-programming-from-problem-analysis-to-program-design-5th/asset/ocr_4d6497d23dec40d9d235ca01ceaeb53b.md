```
```cpp
infile.open("input.dat");
outfile.open("output.dat");

infile >> num1 >> num2;
outfile << "Sum = " << num1 + num2 << endl;

infile.close();
outfile.close();

}
return 0;
```
```

+   15. fstream
+   
+   17.
+      a. Same as before.
+      b. The file contains the output produced by the program.
+      c. The file contains the output produced by the program. The old contents are erased.
+      d. The program would prepare the file and store the output in the file.
+   
+   19.
+      a. `outfile.open("travel.dat");`
+      b. `outfile << fixed << showpoint << setprecision(2);`
+      c. `outfile << day << " " << distance << " " << speed << endl;`
+      d. `travelTime = distance / speed;`
+      e. fstream and iomanip.

# Chapter 4

+   1. a. false; b. false; c. false; d. true; e. false; f. false; g. false; h. false; i. false; j. true
+   
+   3. a. true; b. false; c. true; d. true; e. false
+   
+   5.
+      a. `x = y : 0`
+      b. `x != z : 1`
+      c. `y == z - 3 : 1`
+      d. `!(z > w) : 0`
+      e. `x + y < z : 0`
+   
+   7. Omit the semicolon after else. The correct statement is:
+   
+      ```cpp
+      if (score >= 60)
+          cout << "You pass." << endl;
+      else
+          cout << "You fail." << endl;
+      ```
+   
+   9. 3 1
+   
+   11.
+      ```cpp
+      if (sale > 20000)
+          bonus = 0.10
+      else if (sale > 10000 && sale <= 20000)
+          bonus = 0.05;
+      else
+          bonus = 0.0;
+      ```