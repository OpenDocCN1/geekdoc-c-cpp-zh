```
```cpp
// termination phase
average = total / 10; // integer division yields integer result

// display total and average of grades
cout << "\\nTotal of all 10 grades is " << total << endl;
cout << "Class average is " << average << endl;
} // end function determineClassAverage
```
```

**Fig. 4.9** | Class average problem using counter-controlled repetition: GradeBook source code file. (Part 3 of 3.)

Lines 44–47 (Fig. 4.9) declare local variables total, gradeCounter, grade and average to be of type int. Variable grade stores the user input. Notice that the preceding declarations appear in the body of member function determineClassAverage.

In this chapter’s versions of class GradeBook, we simply read and process a set of grades. The averaging calculation is performed in member function determineClassAverage using local variables—we do not preserve any information about student grades in the class’s data members. In Chapter 7, Arrays and Vectors, we modify class GradeBook to maintain the grades in memory using a data member that refers to a data structure known as an array. This allows a GradeBook object to perform various calculations on a set of grades without requiring the user to enter the grades multiple times.

**Good Programming Practice 4.6**

*Separate declarations from other statements in functions with a blank line for readability.*

Lines 50–51 initialize total to 0 and gradeCounter to 1 so they’re used in calculations. Counter variables are normally initialized to zero or one, depending on their use. An uninitialized variable contains a “garbage” value (also called an undefined value)—the value last stored in the memory location reserved for that variable. The variables grade and average (for the user input and calculated average, respectively) need not be initialized before they’re used—their values will be assigned as they’re input or calculated later in the function.

**Common Programming Error 4.6**

*Not initializing counters and totals can lead to logic errors.*

**Error-Prevention Tip 4.2**

*Initialize each counter and total, either in its declaration or in an assignment statement. Totals are normally initialized to 0. Counters are normally initialized to 0 or 1, depending on how they’re used.*

**Good Programming Practice 4.7**

*Declare each variable on a separate line with its own comment for readability.*