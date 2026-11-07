
## QUICK REVIEW

- 1. A `struct` is a collection of a fixed number of components.

- 2. Components of a `struct` can be of different types.

- 3. The syntax to define a `struct` is:

```cpp
struct structName
{
        dataType1 identifier1;
        dataType2 identifier2;
        .
        .
        .
        dataTypen identifiern;
};
```

- 4. In C++, `struct` is a reserved word.

- 5. In C++, `struct` is a definition; no memory is allocated. Memory is allocated for the `struct` variables only when you declare them.

- 6. Components of a structure are called members of the `struct`.

- 7. Components of a `struct` are accessed by name.

- 8. In C++, the dot (.) operator is called the member access operator.

- 9. Members of a `struct` are accessed by using the dot (.) operator. For example, if employeeType is a `struct`, employee is a variable of type employeeType, and name is a member of employee, then the expression employee.name accesses the member name. That is, employee.name is a variable and can be manipulated like other variables.

- 10. The only built-in operations on a `struct` are the assignment and member access operations.

- 11. Neither arithmetic nor relational operations are allowed on struct(s).

- 12. As a parameter to a function, a `struct` can be passed either by value or by reference.

- 13. A function can return a value of type `struct`.

- 14. A `struct` can be a member of another `struct`.

## EXERCISES

- 1. Mark the following statements as true or false.

  - a. All members of a `struct` must be of different types.
  - b. A function cannot return a value of type `struct`.
  - c. A member of a `struct` can be another `struct`.
  - d. The only allowable operations on a `struct` are assignment and member selection.

- 2. Define a `struct`, `checkingAccount`, to store the following data about a checking account: account holder's name (`string`), account number (`int`), balance (`double`), and the interest rate (`double`).

- 3. Assume the definition of Exercise 2. Declare a `checkingAccount` variable and write C++ statements to store the following information: account holder's name—Jason Miller, account number—17328910, balance—24476.38, interest rate—2.5%.

- 4. Define a `struct`, `movieType`, to store the following data about a movie: movie name (`string`), movie director (`string`), producer (`string`), the year movie was released (`int`), and number of copies in stock.

- 5. Assume the definition of Exercise 4. Declare a variable of type `movieType` to store the following data: movie name—Summer Vacation, director—Tom Blair, producer—Rajiv Merchant, the year the movie released—2005, the number of copies in stock—34.

- 6. Consider the following statements:

```cpp
struct nameType      struct dateType      struct personalInfoType
{                    {                    {
    string first;        int month;           nameType name;
    string last;         int day;             int pID;
};                   int year;            dateType dob;
                     };                   };
personalInfoType person;
personalInfoType classList[100];
nameType student;
```

Mark the following statements as valid or invalid. If a statement is invalid, explain why.

  - a. person.name.first = "William";
  - b. cout << person.name << endl;
  - c. classList[1] = person;
  - d. classList[20].pID = 000011100;
  - e. person = classList[20];
  - f. student = person.name;
  - g. cin >> student;
  - h. `for (int j = 0; j < 100; j++) classList[j].pID = 00000000;`
  - i. classList.dob.day = 1;
  - j. student = name;

- 7. Consider the following statements (nameType is as defined in Exercise 6):

```cpp
struct employeeType
{
    nameType name;
    int performanceRating;
    int pID;
    string dept;
    double salary;
};
employeeType employees[100];
employeeType newEmployee;
```

Mark the following statements as valid or invalid. If a statement is invalid, explain why.

  - a. `newEmployee.name = "John Smith";`
  - b. `cout << newEmployee.name;`
  - c. `employees[35] = newEmployee;`
  - d.
    ```cpp
    if (employees[45].pID == 55533444)
        employees[45].performanceRating = 1;
    ```
  - e. `employees.salary = 0;`

- 8. Assume the declarations of Exercises 6 and 7. Write C++ statements that do the following:

  - a. Store the following information in `newEmployee`:

    ```text
    name: Mickey Doe
    pID: 111111111
    performanceRating: 2
    dept: ACCT
    salary: 34567.78
    ```

  - b. In the array `employees`, initialize each `performanceRating` to 0.
  - c. Copy the information of the 20th component of the array `employees` into `newEmployee`.
  - d. Update the salary of the 50th employee in the array `employees` by adding 5735.87 to its previous value.

- 9. Assume that you have the following definition of a struct.

```cpp
struct partsType
{
    string partName;
    int partNum;
    double price;
    int quantitiesInStock;
};
```

Declare an array, inventory, of 100 components of type partsType.

- 10. Assume the definition of Exercise 9.

  - a. Write a C++ code to initialize each component of inventory as follows: `partName` to null string, `partNum` to −1, `price` to 0.0, and `quantitiesInStock` to 0.
  - b. Write a C++ code that uses a loop to output the data stored in inventory. Assume that the variable `length` indicates the number of elements in inventory.

- 11. Assume the definition and declaration of Exercise 9. Write the definition of a void function that can be used to input data in a variable of type `partsType`. Also write a C++ code that uses your function to input data in inventory.

- 12. Suppose that you have the following definitions:

```cpp
struct timeType
{
    int hr;
    double min;
    int sec;
};

struct tourType
{
    string cityName;
    int distance;
    timeType travelTime;
};
```

  - a. Declare the variable `destination` of type `tourType`.
  - b. Write C++ statements to store the following data in `destination`: `cityName`—Chicago, `distance`—550 miles, `travelTime`—9 hours and 30 minutes.
  - c. Write the definition of a function to output the data stored in a variable of type `tourType`.
  - d. Write the definition of a value-returning function that inputs data into a variable of type `tourType`.
  - e. Write the definition of `void` function with a reference parameter of type `tourType` to input data in a variable of type `tourType`.

## PROGRAMMING EXERCISES

- 1. Assume the definition of Exercise 4, which defines the `struct` `movieType`. Write a program that declares a variable of type `movieType`, prompts the user to input data about a movie, and outputs the movie data.

- 2. Write a program that reads students’ names followed by their test scores. The program should output each student’s name followed by the test scores and the relevant grade. It should also find and print the highest test score and the name of the students having the highest test score.

- **Function `printCheck`:** This function calculates and prints the check. (Note that the billing amount should include a 5% tax.) A sample output is:

```text
Welcome to Johnny's Restaurant
Bacon and Egg       $2.45
Muffin              $0.99
Coffee              $0.50
Tax                 $0.20
Amount Due          $4.14
```

Format your output with two decimal places. The name of each item in the output must be left justified. You may assume that the user selects only one item of a particular type.

- 5. Redo Exercise 4 so that the customer can select multiple items of a particular type. A sample output in this case is:

```text
Welcome to Johnny's Restaurant
1 Bacon and Egg     $2.45
2 Muffin             $1.98
1 Coffee             $0.50
  Tax                $0.25
  Amount Due         $5.18
```

- 6. Write a program whose main function is merely a collection of variable declarations and function calls. This program reads a text and outputs the letters, together with their counts, as explained below in the function `printResult`. (There can be no global variables! All information must be passed in and out of the functions. Use a structure to store the information.) Your program must consist of at least the following functions:

  - **Function `openFile`:** Opens the input and output files. You must pass the file streams as parameters (by reference, of course). If the file does not exist, the program should print an appropriate message and exit. The program must ask the user for the names of the input and output files.

  - **Function `count`:** Counts every occurrence of capital letters A–Z and small letters a–z in the text file opened in the function `openFile`. This information must go into an array of structures. The array must be passed as a parameter, and the file identifier must also be passed as a parameter.

  - **Function `printResult`:** Prints the number of capital letters and small letters, as well as the percentage of capital letters for every letter A–Z and the percentage of small letters for every letter a–z. The percentages should look like this: “25%”. This information must come from an array of structures, and this array must be passed as a parameter.
