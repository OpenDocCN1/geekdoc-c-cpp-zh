# CHAPTER 11 One-Dimensional Arrays

(continued)

```
47
48     system("pause");
49     return 0;
50 } //end of main function
51
52 //function definitions****
53 void displayMain(double rain[], int numElements)
54 {
55     cout << << "Monthly rainfall amount:" << endl;
56     for (int x = 0; x < numElements; x += 1)
57         cout << rain[x] << endl;
58     //end for
59 }
60
61 void displayTotal(double rain[], int numElements)
62 {
63     double total = 0.0;
64     for (int x = 0; x < numElements; x += 1)
65         total = total + rain[x];
66     //end for
67     cout << << "Total rainfall: " << total << endl;
68 } //end of displayTotal function
```

Figure 11-57 Rainfall program

![](bbox=[0.312, 0.555, 0.822, 0.853])

Figure 11-58 Completed desk-table for the rainfall program