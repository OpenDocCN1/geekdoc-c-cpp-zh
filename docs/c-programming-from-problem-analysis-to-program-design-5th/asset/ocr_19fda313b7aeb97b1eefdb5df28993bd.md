```
cin >> firstName >> lastName;                 //Line 6
cin >> age >> weight;                         //Line 7

cout << "Name: " << firstName << " "
     << lastName << endl;                     //Line 8

cout << "Age: " << age << endl;              //Line 9
cout << "Weight: " << weight << endl;        //Line 10

return 0;                                     //Line 11
}
```

**Sample Run:** In this sample run, the user input is shaded.

```
Enter first name, last name, age, and weight, separated by spaces.
Sheila Mann 23 120.5
Name: Sheila Mann
Age: 23
Weight: 120.5
```

The preceding program works as follows: The statements in Lines 1 to 4 declare the variables `firstName` and `lastName` of type string, `age` of type `int`, and `weight` of type `double`. The statement in Line 5 is an output statement and tells the user what to do. (Such output statements are called prompt lines.) As shown in the sample run, the input to the program is:

Sheila Mann 23 120.5

The statement in Line 6 first reads and stores the string Sheila into the variable `firstName` and then skips the space after Sheila and reads and stores the string Mann into the variable `lastName`. Next, the statement in Line 7 first skips the blank after Mann and reads and stores 23 into the variable age and then skips the blank after 23 and reads and stores 120.5 into the variable weight.

The statements in Lines 8, 9, and 10 produce the third, fourth, and fifth lines of the sample run.

> **NOTE** During programming execution, if more than one value is entered in a line, these values must be separated by at least one blank or tab. Alternately, one value per line can be entered.

# Variable Initialization

Remember, there are two ways to initialize a variable: by using the assignment statement and by using a read statement. Consider the following declaration:

```
int feet;
int inches;
```

![](bbox=[0.929, 0.161, 1.0, 0.269])