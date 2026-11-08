+   c. Write the definition of the default constructor of the class `bagType` so that the private member variables are initialized to `""`, `0.0`, `0.0`, `0.0`, `0.0`, respectively.
+   
+   d. Write a C++ statement that prints the value of the object `newBag`.
+   
+   e. Write a C++ statement that declares the object `tempBag` of type `bagType`, and initializes the member variables of `tempBag` to `"backPack"`, `15`, `8`, `20`, and `49.99`, respectively.

8. Consider the definition of the following class:

```
class employee                                      //Line 1
{
public:                                             //Line 3
    employee();                                     //Line 4
    employee(string, int, double);                  //Line 5
    employee(int, double);                          //Line 6
    employee(string);                               //Line 7

    void setData(string, int, double);              //Line 8
    void print() const;                             //Line 9
    void updatePay(double x);                       //Line 10
    int getNumOfServiceYears() const;               //Line 11
    double getPay() const;                          //Line 12

private:                                            //Line 13
    string name;                                    //Line 14
    int numOfServiceYears;                          //Line 15
    double pay;                                     //Line 16
};                                                  //Line 17
```

+   a. Give the line number containing the constructor that is executed in each of the following declarations:
+   
+      i. `employee tempEmployee;`
+   
+      ii. `employee newEmployee("Harry Miller", 0, 25000);`
+   
+      iii. `employee oldEmployee("Bill Dunbar", 15, 55000);`
+   
+   b. Write the definition of the constructor in Line 4 so that the instance variables are initialized to `""`, `0`, and `0.0`, respectively.
+   
+   c. Write the definition of the constructor in Line 5 so that the instance variables are initialized according to the parameters.
+   
+   d. Write the definition of the constructor in Line 6 so that the instance variable `name` is initialized to the empty string and the remaining instance variables are initialized according to the parameters.

9. Consider the definition of the class `employee` as given in Exercise 8. Which function members are the accessors and which are the mutators?

10. Consider the definition of the class `employee` as given in Exercise 8. Answer the following questions: