# CHAPTER 10

# Void Functions

(continued)

```
63
64  system("pause");
65  return 0;
66  } //end of main function
67
68  ****function definitions****
69  void displayMenu() {
70
71    cout << "1 British pounds" << endl;
72    cout << "2 Mexican pesos" << endl;
73    cout << "3 Japanese yen" << endl;
74    cout << "4 Stop program" << endl;
75  } //end of displayMenu function
76
77  void convertDols(double dollars, 
78    double convertRate,
79    double &converted)
80  {
81    converted = dollars * convertRate;
82 } //end of convertDols function
```

Figure 10-26 Code for Lab 10-1

# QUESTIONS

+   1. The main function passes three variables to the convertDols function. Which lines in the program indicate whether the variables are passed by value or by reference?

+   2. Why are the americanD and conversionRate variables passed by value? Why is the convertedCurrency variable passed by reference?

+   3. Why is the displayMenu function a void function?

+   4. Which line in the program contains the printing read? Which line contains the update read?

+   5. The convertDols function in Figure 10-26 is a void function. How would you modify the function to make it a value-returning function? What other changes would you need to make to the program?

+   6. Follow the instructions for starting C++ and opening the Lab10-1.cpp file. The file is contained in either the Cpp6\Chap10\Project folder or the Cpp6\Chap10 folder. Run the program. First, you will use the program to convert 100 American dollars to Japanese yen. Type 3 and press Enter, then type 100 and press Enter. The program displays the number 8876.26, as shown in Figure 10-25.

+   7. Use the program to convert 50 American dollars to British pounds. What is the answer?

+   8. Use the program to convert 10 American dollars to Mexican pesos. What is the answer?