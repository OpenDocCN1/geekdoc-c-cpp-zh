In C++, `struct` is a reserved word. The members of a struct, even though enclosed in braces (that is, they form a block), are not considered to form a compound statement. Thus, a semicolon (after the right brace) is essential to end the `struct` statement. A semicolon at the end of the `struct` is, therefore, a part of the syntax.

The statement:

```
struct houseType
{
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

defines a struct houseType with eight members. The member style is of type string, the members numOfBedrooms, numOfBathrooms, numOfCarsGarage, yearBuilt, and finishedSquareFootage are of type int, and the members price and tax are of type double.

Like any type definition, a struct is a definition, not a declaration. That is, it defines only a data type; no memory is allocated.

Once a data type is defined, you can declare variables of that type.

For example, the following statement defines newHouse to be a struct variable of type houseType:

```
//variable declaration
houseType newHouse;
```

The memory allocated is large enough to store style, numOfBedrooms, numOfBathrooms, numOfCarsGarage, yearBuilt, finishedSquareFootage, price, and tax (see Figure 9-1).

![](bbox=[0.182, 0.725, 0.909, 0.92])

**FIGURE 9-1**  `struct newHouse`