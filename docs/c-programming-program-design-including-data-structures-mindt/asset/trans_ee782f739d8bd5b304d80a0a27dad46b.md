
```cpp
bool canGraduate();                         //Line 4
void print() const;                          //Line 5
void syntaxErrors2(int = 0,                 //Line 6
                   double = 0);
private:                                     //Line 7
    int ID;                                  //Line 8
    double gpa;                              //Line 9
};                                           //Line 10
```

## 4. 找出以下类定义中的语法错误。(1, 2, 5)

```cpp
class syntaxErrors3()                     //Line 1
{
public:                                    //Line 3
    void setXY(int, int);                  //Line 4
    isEqual(int a, int b);                 //Line 5
    int multiply();                        //Line 6
    void print() const;                    //Line 7
    syntaxErrors3(int, int = 0);           //Line 8
private:                                   //Line 9
    int x;                                 //Line 10
    int y;                                 //Line 11
};                                        //Line 12
```

## 5. 找出以下类定义中的语法错误。(1, 2, 5)

```cpp
class syntaxErrors4                      //Line 1
{
public:                                   //Line 3
    set(string, int, double);             //Line 4
    void print() const;                   //Line 5
    syntaxErrors4() const;                //Line 6
    syntaxErrors4(string, int, double);   //Line 7
private:                                  //Line 8
    string n;                             //Line 9
    int ID;                               //Line 10
    double bal;                           //Line 11
}                                         //Line 12
```

## 6. 考虑以下声明：(1, 2, 5, 7)

```cpp
class foodType
{
public:
    void set(string, int, double, int, double, double);
    void print() const;
    string getName() const;
    int getCalories() const;
    double getFat() const;
    int getSugar() const;
    double getCarbohydrate () const;
    double getPotassium () const;
    foodType();
    foodType(string, int, double, int, double, double);
private:
    string name;
    int calories;
    double fat;
    int sugar;
    double carbohydrate;
    double potassium;

};

//variable declaration
foodType fruit1;
foodType fruit2("banana", 90, 0.4, 14, 27, 422);
```

- a. 类 `foodType` 有多少个成员？
- b. 类 `foodType` 有多少个私有成员？
- c. 类 `foodType` 有多少个构造函数？
- d. 类 `foodType` 有多少个常量函数？
- e. 哪个构造函数用于初始化对象 `fruit1`？哪个构造函数用于初始化对象 `fruit2`？
- f. 重写类 `foodType` 的定义，使每个数据成员都可以单独设置。
- g. 编写一条 C++ 语句，用一个带默认参数的构造函数替换这些构造函数的定义。

## 7. 假设类 `foodType` 的定义如练习 6 所示。回答以下问题。(1, 2, 3, 5, 6)

- a. 编写成员函数 `set` 的定义，使私有成员根据参数进行设置。`int` 和 `double` 实例变量的值必须非负。
- b. 编写成员函数 `print` 的定义，打印数据成员的值。
- c. 编写成员函数 `getName`、`getCalories`、`getFat`、`getSugar`、`getCarbohydrate`、`getPotassium` 的定义，以返回实例变量的值。
- d. 编写类 `foodType` 的默认构造函数的定义，使私有成员变量分别初始化为 ""、0、0.0、0、0.0、0.0。
- e. 编写类 `foodType` 的带参数构造函数的定义，使私有成员变量根据参数进行初始化。`int` 和 `double` 实例变量的值必须非负。
- f. 编写一条 C++ 语句，打印对象 `fruit2` 的值。
- g. 编写一条 C++ 语句，声明一个类型为 **foodType** 的对象 **myFruit**，并将 **myFruit** 的成员变量分别初始化为 **"Apple"**、52.0、2.0、10、13.8 和 148.0。

## 8. 考虑以下类的定义：

```cpp
class productType                                      //Line 1
{
public:                                                //Line 2
    productType();                                     //Line 3
    productType(int, double, double);                  //Line 4
    productType(string, int, double, double);         //Line 5
    productType(string, string, string,               //Line 6
                int, double, double);                 //Line 7

    void set(string, string, string, int,              //Line 8
             double, double);
    void print() const;                                //Line 9

    void setQuantitiesInStock(int x);                 //Line 10
    void updateQuantitiesInStock(int x);              //Line 11
    int getQuantitiesInStock() const;                 //Line 12

    void setPrice(double x);                          //Line 13
    double getPrice() const;                           //Line 14
    void setDiscount(double d);                       //Line 15
    double getDiscount() const;                       //Line 16

private:                                               //Line 17
    string productName;                                //Line 18
    string id;                                         //Line 19
    string manufacturer;                               //Line 20
    int quantitiesInStock;                             //Line 21
    double price;                                      //Line 22
    double discount;                                   //Line 23
};                                                     //Line 24
```

- a. 给出以下每个声明中执行的构造函数所在的行号。
  - i. `productType product1;`
  - ii. `productType product2("Microwave", "M3562", "General", 35, 175.00, 0.1);`
  - iii. `productType product3("D1290", 25, 375.00, 0.05);`
  - iv. `productType product4(10, 8.50, 0.2);`
- b. 编写第 4 行构造函数的定义，使实例变量分别初始化为 ""、""、""、0、0.0 和 0.0。
- c. 编写第 5 行构造函数的定义，使字符串实例变量初始化为 ""、""、""，以及其他实例变量

## 11. 考虑以下声明：(1, 2, 3, 6, 7)

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

```cpp
houseType newHouse;   //variable declaration
```

- a. 类 houseType 有多少个成员？
- b. 类 houseType 有多少个私有成员？
- c. 类 houseType 有多少个构造函数？
- d. 类 houseType 有多少个常量函数？

## 12. 假设类 houseType 的定义如练习 11 所示。回答以下问题。(1, 2, 3, 5, 7)

- a. 编写成员函数 set 的定义，使私有成员根据参数进行设置。
- b. 编写成员函数 print 的定义，打印数据成员的值。
