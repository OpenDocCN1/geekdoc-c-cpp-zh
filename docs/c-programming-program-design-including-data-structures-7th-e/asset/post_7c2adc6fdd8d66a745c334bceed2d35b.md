
8. Consider the definition of the following class: (1, 2, 3, 5, 7)

```cpp
class employee                       //Line 1
{                                    //Line 2
public:                              //Line 3
    employee();                      //Line 4
    employee(string, int, double);   //Line 5
    employee(int, double);           //Line 6
    employee(string);                //Line 7

    void setData(string, int, double); //Line 8
    void print() const;                //Line 9
    void updateSalary(double x);       //Line 10
    int getNumOfServiceYears() const;  //Line 11
    double getSalary() const;          //Line 12

private:                               //Line 13
    string name;                       //Line 14
    int numOfServiceYears;             //Line 15
    double salary;                     //Line 16
};                                     //Line 17
```

- a. Give the line number containing the constructor that is executed in each of the following declarations:
  - i. `employee tempEmployee;`
  - ii. `employee newEmployee("Harry Miller", 0, 25000);`
  - iii. `employee oldEmployee("Bill Dunbar", 15, 55000);`
- b. Write the definition of the constructor in Line 4 so that the instance variables are initialized to "", 0, and 0.0, respectively.
- c. Write the definition of the constructor in Line 5 so that the instance variables are initialized according to the parameters.
- d. Write the definition of the constructor in Line 6 so that the instance variable name is initialized to the empty string and the remaining instance variables are initialized according to the parameters.

9. Consider the definition of the class employee as given in Exercise 8. Which function members are accessors and which are mutators? (4)

10. Consider the definition of the class employee as given in Exercise 8. Answer the following questions: (1, 2, 3, 5)

- a. Write the definition of the function setData so that the instance variables are set according to the parameters.
- b. Write the definition of the function print to output the values of the instance variables.
- c. Write the definition of the function updateSalary to update the value of the instance variable salary by adding the value of the parameter.
- d. Write the definition of the function getNumOfServiceYears to return the value of the instance variable numOfServiceYears.
- e. Write the definition of the function `getSalary` to return the value of the instance variable `salary`.
- f. Write a program to test the `class employee`.

11. Consider the following declarations: (1, 2, 3, 5, 7)

```cpp
class houseType
{
public:
    void set(string, int, int, int, int, int, double, double);
    void print() const;
    void setStyle(string);
    string getStyle() const;
    void setNumOfBedrooms(int);
    int getNumOfBedrooms() const;
    void setNumOfBathrooms(int);
    int getNumOfBathrooms() const;
    void setNumOfCarsGarage(int);
    int getNumOfCarsGarage() const;
    void setYearBuilt(int);
    int getYearBuilt() const;
    void setFinishedSquareFootage(int);
    int getFinishedSquareFootage() const;
    void setPrice(double);
    double getPrice() const;
    void setTax(double);
    double getTax() const;
    houseType(string = "", int = 0, int = 0, int = 0, int = 0,
              int = 0, double = 0, double = 0);
private:
    string style;
    int numOfBedrooms;
    int numOfBathrooms;
    int numOfCarsGarage;
    int yearBuilt;
    int finishedSquareFootage;
    double price;
    double tax;
};
```

`houseType newHouse;`  // variable declaration

- a. How many members does `class houseType` have?
- b. How many `private` members does `class houseType` have?
- c. How many constructors does `class houseType` have?
- d. How many constant functions does `class houseType` have?

- b. Write the definition of the member function `manipulate` that returns a decimal number as follows: If the value of `description` is "rectangle", it returns `first * second`; if the value of `description` is "circle", it returns the area of the circle with radius `first`; if the value of `description` is "sphere", it returns the volume of the sphere with radius `first`; if the value of `description` is "cylinder", it returns the volume of the cylinder with radius `first` and height `second`; otherwise, it returns the value -1.
- c. Write the definition of the function `print` to print the values of the instance variables and the values returned by the function `manipulate`. For example, if `description == "rectangle"`, `first == 8.5`, and `second == 5`, it should print:

```
rectangle: length = 8.50, width = 5.00, area = 42.50
```

- d. Write the definition of the constructor so that it initializes the instance variables using the function `set`.
- e. Write the definition of the remaining functions to set or retrieve the values of the instance variables. Note that the function `get` retrieves the values of all instance variables.

15. Assume the definition of class `temporary` as given in Exercise 13. What is the effect of the following statements? (1, 5)

```
temporary object1;
temporary object2("rectangle", 3.0, 5.0);    //Line 2
temporary object3("circle", 6.5, 0.0);        //Line 3
temporary object4("cylinder", 6.0, 3.5);      //Line 4
```

16. Assume the definition of class `temporary` as given in Exercise 13 and the definitions of the member functions and the constructor as specified in Exercise 14. What is the output of the following statements? (3, 5)

```
temporary object1;
temporary object2("rectangle", 8.5, 5);
temporary object3("circle", 6, 0);
temporary object4("cylinder", 6, 3.5);

cout << fixed << showpoint << setprecision(2);

object1.print();
object2.print();
object3.print();
object4.print();

object1.set("sphere", 4.5, 0);
object1.print();
```

17. What are the built-in operations on classes? (3)

18. What is the main difference between a `struct` and a `class`? (8)

19. Consider the definition of the following class: (1, 2, 3, 5, 7)

```cpp
class testClass
{
public:
    int sum();
        //Returns the sum of the private member variables
    void print() const;
        //Prints the values of the private member variables
    testClass();
        //Default constructor
        //Initializes the private member variables to 0
    testClass(int a, int b);
        //Constructors with parameters
        //Initializes the private member variables to the values
        //specified by the parameters
        //Postcondition: x = a; y = b;
private:
    int x;
    int y;
};
```

- a. Write the definitions of the member functions as described in the definition of the class testClass.
- b. Write a test program to test the various operations of the class testClass.

20. Given the definition of the class clockType with constructors (as described in this chapter), what is the output of the following C++ code? (1, 2, 3, 5)

```cpp
clockType clock1;
clockType clock2(23, 13, 75);

clock1.printTime();
cout << endl;
clock2.printTime();
cout << endl;

clock1.setTime(6, 59, 39);
clock1.printTime();
cout << endl;

clock1.incrementMinutes();
clock1.printTime();
cout << endl;

clock1.setTime(0, 13, 0);

if (clock1.equalTime(clock2))
    cout << "clock1 time is the same as clock2 time."
         << endl;

else
    cout << "The two times are different." << endl;
```

21. Assume the definition of the class `personType` as given in this chapter. (1, 3)

- a. Write a C++ statement that declares `student` to be a `personType` object, and initialize its first name to "Buddy" and last name to "Arora".
- b. Write a C++ statement that outputs the data stored in the object `student`.
- c. Write a C++ statement that changes the first name of `student` to "Susan" and the last name to "Gilbert".

22. Explain why you would need both `public` and `private` members in a class. (2, 9, 10)

23. What is a constructor? Why would you include a constructor in a class? (5)

24. Which of the following characters appears before a destructor's name? (5)

- a. `#`
- b. `!`
- c. `~`
- d. `$`

25. What is a destructor and what is its purpose? (5)

26. Write the definition of a class that has the following properties: (1, 2, 3, 5)

- a. The name of the class is `secretType`.
- b. The class `secretType` has four member variables: `name` of type `string`, `age` and `weight` of type `int`, and `height` of type `double`.
- c. The class `secretType` has the following member functions. (Make each accessor function constant.)
  - `print`—outputs the data stored in the member variables with the appropriate titles
  - `setName`—function to set the name
  - `setAge`—function to set the age
  - `setWeight`—function to set the weight
  - `setHeight`—function to set the height
  - `getName`—value-returning function to return the name
  - `getAge`—value-returning function to return the age
  - `getWeight`—value-returning function to return the weight
  - `getHeight`—value-returning function to return the height
  - `constructor`—with default parameters: The default value of `name` is the empty string `""`, and the default values of `age`, `weight`, and `height` are 0.
- d. Write the definition of the member functions of the class `secretType`, as described in Part c.
