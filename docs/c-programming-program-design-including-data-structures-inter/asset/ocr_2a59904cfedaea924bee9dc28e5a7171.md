```
```cpp
case 's':
    if (gpa >= 3.75)
        dues = 75.00;
    else
        dues = 120.00;
    break;
case 'j':
    if (gpa >= 3.75)
        dues = 50.00;
    else
        dues = 100.00;
    break;
case 'h':
    if (gpa >= 3.75)
        dues = 25.00;
    else
        dues = 75.00;
    break;
default:
    cout << "Invalid class standing code." << endl;
}
```
```

# Chapter 5

+   1. a. false; b. true; c. false; d. true; e. true; f. true; g. true; h. false
+   3. 181.00
+   5. if ch > 'Z' or ch < 'A'
+   7. Sum = 94
+   9. Sum = 37
+   11.
+      a. 29
+      b. 28
+      c. 8 13 21 34
+      d. The value of num1 + num2 becomes larger than the largest int value and the value of temp overflows its memory space. Some of the values output by the program are:
+         4 7 11 18 29 47 76 123 199 322 521 843 1364 2207 3571 5778 9349 15127 24476 39603 64079 103682 167761 271443 439204 710647 1149851 1860498 3010349 4870847 7881196 12752043 20633329 33385282 54018521 87403803 141422324 228826127 370248451 599074578 969323029 1568397607
+   13. Replace the while loop statement with the following:
+       while (response == 'Y' || response == 'y')
+       Replace the cout statement:
+       cout << num1 << " + " << num2 << " = " << (num1 - num2)
+           << endl;