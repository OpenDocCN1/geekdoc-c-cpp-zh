declare x to have this structure type. Initialize the members of x, memberB and memberC, to the values 1 and 2, respectively.

(Note: This requests an initialization, not an assignment of the members. This distinction is important and will be made in a later chapter.)

5. Here is an initialization of a structure type. Tell what happens with each initialization. Note any problems with these initializations.

```
struct Date
{
    int month;
    int day;
    int year;
};
```

a. Date dueDate = {12, 21};

b. Date dueDate = {12, 21, 20, 22};

c. Date dueDate = {12, 21, 20, 22};

d. Date dueDate = {12, 21, 22};

6. Write a definition for a structure type for records consisting of a person’s wage rate, accrued vacation (which is some whole number of days), and status (which is either hourly or salaried). Represent the status as one of the two char values 'H' and 'S'. Call the type EmployeeRecord.

7. Give a function definition corresponding to the following function declaration. (The type ShoeType is given in Self-Test Exercise 2.)

```
void readShoeRecord(ShoeType& newShoe);
//Fills newShoe with values read from the keyboard.
```

8. Give a function definition corresponding to the following function declaration. (The type ShoeType is given in Self-Test Exercise 2.)

```
ShoeType discount(ShoeType oldRecord);
//Returns a structure that is the same as its argument,
//but with the price reduced by 10%.
```

9. Give the structure definition for a type named StockRecord that has two member variables, one named shoeInfo of the type ShoeType given in Self-Test Exercise 2 and one named arrivalDate of type Date given in Self-Test Exercise 5.

10. Declare a variable of type StockRecord (given in the previous exercise) and write a statement that will set the year of the arrival date to 2006.