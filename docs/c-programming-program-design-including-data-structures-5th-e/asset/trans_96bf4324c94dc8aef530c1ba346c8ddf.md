

```cpp
partTimeEmployee(string first = "", string last = "",
                 long id = 0,
                 double rate = 0, double hours = 0);
//Constructor with parameters
//Sets the first name, last name, payRate, and
//hoursWorked according to the parameters. If
//no value is specified, the default values are
//assumed.
//Postcondition: firstName = first, lastName = last,
//               personId = id, payRate = rate,
//               hoursWorked = hours;

private:
    double payRate;      //stores the pay rate
    double hoursWorked;  //stores the hours worked
};
```

`partTimeEmployee` 类的构造函数和函数的定义如下：

```cpp
void partTimeEmployee::set(string first, string last, long id,
                           double rate, double hours)
{
    setName(first, last);
    setId(id);
    payRate = rate;
    hoursWorked = hours;
}

void partTimeEmployee::setPayRate(double rate)
{
    payRate = rate;
}

double partTimeEmployee::getPayRate()
{
    return payRate;
}

void partTimeEmployee::setHoursWorked(double hours)
{
    hoursWorked = hours;
}

double partTimeEmployee::getHoursWorked()
{
    return hoursWorked;
}

void partTimeEmployee::print() const
{
    cout << "Id: " << getId() << endl;
    cout << "Name: ";
    personType::print();
    cout << endl;
    cout << "Wages: $" << calculatePay() << endl;
}

double partTimeEmployee::calculatePay() const
{
    return (payRate * hoursWorked);
}

//constructor
partTimeEmployee::partTimeEmployee(string first, string last,
                                    long id,
                                    double rate, double hours)
                                  : employeeType(first, last, id)
{
    payRate = rate;
    hoursWorked = hours;
}
```

下面的函数 `main` 测试这些类：

```cpp
#include <iostream>
#include "partTimeEmployee.h"
#include "fullTimeEmployee.h"

int main()
{
    fullTimeEmployee newEmp("John", "Smith", 75, 56000, 5700);
    partTimeEmployee tempEmp("Bill", "Nielson", 275, 15.50, 57);

    newEmp.print();
    cout << endl;
    tempEmp.print();

    return 0;
}
```

## 示例运行

```text
Id: 75
Name: John Smith
Wages: $61700

Id: 275
Name: Bill Nielson
Wages: $883.5
```

上面的输出不言自明。我们将其中的细节留作练习。

- 1. 保存列表元素的数组、列表。
- 2. 变量 `length`，用于存储列表的长度（即数组中当前的列表元素个数）。
- 3. 变量 `maxSize`，用于存储数组的大小（即数组中能够存储的最大元素个数）。

既然你已经知道要对列表执行的操作以及将列表存储到计算机内存中的方法，我们就可以定义将列表实现为 ADT（抽象数据类型）的类。为了便于说明，我们假设列表的元素类型为 `int`。在第 14 章讨论类模板时，我们将取消这一限制；届时，我们将开发一个可用于处理各种列表的泛型类。

下面的类将基于数组的 `int` 列表定义为 ADT：

既然你已经知道要对列表执行的操作以及如何将列表存储到计算机内存中，接下来我们将定义抽象类 `arrayListType`，它将列表实现为 ADT（抽象数据类型）。

```cpp
class arrayListType
{
public:
    bool isEmpty() const;
        //Function to determine whether the list is empty
        //Postcondition: Returns true if the list is empty;
        //               otherwise, returns false.

    bool isFull() const;
        //Function to determine whether the list is full
        //Postcondition: Returns true if the list is full;
        //               otherwise, returns false.

    int listSize() const;
        //Function to determine the number of elements in
        //the list.
        //Postcondition: Returns the value of length.

    int maxListSize() const;
        //Function to determine the maximum size of the list
        //Postcondition: Returns the value of maxSize.

    void print() const;
        //Function to output the elements of the list
        //Postcondition: Elements of the list are output on the
        //               standard output device.

    bool isItemAtEqual(int location, int item) const;
        //Function to determine whether the item is the same as
        //the item in the list at the position specified
        //by location.
        //Postcondition: Returns true if the list[location]
        //               is the same as item; otherwise,
        //               returns false.
        //               If location is out of range, an
        //               appropriate message is displayed.
        //

    virtual void insertAt(int location, int insertItem) = 0;
        //Function to insert insertItem in the list at the
        //position specified by location.
        //Note that this is an abstract function.
        //Postcondition: Starting at location, the elements of
        //              the list are shifted down,
        //              list[location] = insertItem; length++;
        //              If the list is full or location is out of
        //              range, an appropriate message is displayed.
        //

    virtual void insertEnd(int insertItem) = 0;
        //Function to insert insertItem at the end of
        //the list. Note that this is an abstract function.
        //Postcondition: list[length] = insertItem; and length++;
        //              If the list is full, an appropriate
        //              message is displayed.

    void removeAt(int location);
        //Function to remove the item from the list at the
        //position specified by location
        //Postcondition: The list element at list[location] is
        //              removed and length is decremented by 1.
        //              If location is out of range, an
        //              appropriate message is displayed.

    void retrieveAt(int location, int& retItem) const;
        //Function to retrieve the element from the list at the
        //position specified by location
        //Postcondition: retItem = list[location]
        //              If location is out of range, an
        //              appropriate message is displayed.

    virtual void replaceAt(int location, int repItem) = 0;
        //Function to replace repItem the element in the list
        //at the position specified by location.
        //Note that this is an abstract function.
        //Postcondition: list[location] = repItem
        //              If location is out of range, an
        //              appropriate message is displayed.

    void clearList();
        //Function to remove all the elements from the list.
        //After this operation, the size of the list is zero.
        //Postcondition: length = 0;

    virtual int seqSearch(int searchItem) const = 0;
        //Function to search the list for searchItem.
        //Note that this is an abstract function.
        //Postcondition: If the item is found, returns the
        //              location in the array where the item is
        //              found; otherwise, returns -1.

    virtual void remove(int removeItem) = 0;
        //Function to remove removeItem from the list.
        //Note that this is an abstract function.
        //Postcondition: If removeItem is found in the list,
        //              it is removed from the list and length
        //              is decremented by one.

    arrayListType(int size = 100);
        //Constructor
        //Creates an array of the size specified by
        //parameter size. The default array size is 100.
        //Postcondition: The list points to the array, length = 0,
        //              and maxSize = size

    arrayListType(const arrayListType & otherList);
        //Copy constructor

    virtual ~arrayListType();
        //Destructor
        //Deallocate the memory occupied by the array.

protected:
    int *list;      //array to hold the list elements
    int length;     //variable to store the length of the list
    int maxSize;    //variable to store the maximum
                    //size of the list
};
```

图 13-22 展示了类 `arrayListType` 的 UML 类图。注意，在 UML 类图中，抽象类和抽象函数的名称以斜体显示。

![](img/f97f778697507bb6fdd80c5991210cba_840_0.png)

**图 13-22** 类 `arrayListType` 的 UML 图

