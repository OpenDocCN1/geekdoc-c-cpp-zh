
## 1. 引言

本文档旨在介绍一种新型的文档解析方法，该方法能够高效地从复杂版面中提取结构化信息。随着数字化办公的普及，文档格式日益多样化，传统的解析方式已难以满足需求。

本方法基于深度学习技术，结合版面分析与语义理解，实现了对标题、段落、表格、图片等元素的精准识别与定位。实验结果表明，该方法在多个公开数据集上均取得了优异的性能。

- 支持多种文档格式（PDF、Word、扫描件等）
- 高精度版面元素识别
- 输出结构化 Markdown 格式
- 提供坐标定位信息

下图展示了系统的整体架构，包括预处理模块、版面分析模块和内容提取模块。

![](img/202cface8244f523c2641baa2e00d7dd_488_0.png)

```
{
    elNum = idnum;
    currentFloor = cfloor;
    highestFloor = maxFloor;
}
void Elevator::request(int newfloor)
{
    if (newfloor < 1 || newfloor > highestFloor || newfloor == currentFloor)
        ; // do nothing
    else if (newfloor > currentFloor) // move elevator up
    {
        cout << "\nElevator " << elNum
             << " starting at floor " << currentFloor << endl;
        while (newfloor > currentFloor)
        {
            currentFloor++; // add one to current floor
            cout << " Going Up - now at floor " << currentFloor << endl;
        }
        cout << "Elevator " << elNum
             << " stopping at floor " << currentFloor << endl;
    }
    else // move elevator down
    {
        cout << "\nElevator " << elNum
             << " starting at floor " << currentFloor << endl;
        while (newfloor < currentFloor)
        {
            currentFloor--; // subtract one from current floor
            cout << " Going Down - now at floor " << currentFloor << endl;
        }
        cout << "Elevator "<< elNum
             << " Stopping at floor " << currentFloor << endl;
    }
    return;
}
```

```
int main()
{
    Elevator a;  // declare 1 object of type Elevator

    a.request(6);
    a.request(3);

    return 0;
}
```

## Point of Information

## Encapsulation

The term encapsulation refers to packaging a number of items into a single unit. For example, a function is used to encapsulate the details of an algorithm. Similarly, a class encapsulates variables and methods together in a single package. Although "encapsulation" is sometimes used to refer to the process of data hiding, this usage isn't technically accurate. The terms "information hiding" refers to encapsulating and hiding all implementation details.

Three class method calls are included in the main() function. The first statement creates an object named a of type Elevator. Because no floor has been given, the constructor's default arguments are used. This means the elevator is designated as elevator number 1, it begins operation at floor 1, and can go up to only the 15th floor. A request is then made to move the elevator to floor 6, which is followed by a request to move to floor 3. Program 10.6 produces the following output:

```
Elevator 1 starting at floor 1
Going Up - now at floor 2
Going Up - now at floor 3
Going Up - now at floor 4
Going Up - now at floor 5
Going Up - now at floor 6
Elevator 1 stopping at floor 6
```

```
Elevator 1 starting at floor 6
Going Down - now at floor 5
Going Down - now at floor 4
Going Down - now at floor 3
Elevator 1 stopping at floor 3
```

In Program 10.6, notice the control the main() function provides. This sequential control, with two calls made to the same object operation and using different argument values, is suitable for testing purposes. However, by incorporating calls to request() inside a while loop and using the random number function rand() to generate random floor requests, a continuous simulation of the elevator's operation is possible (see Exercise 6).

## EXERCISES 10.4

- 1. (Practice) Enter and run Program 10.5 on your computer.
- 2. (Modify) Modify the main() function in Program 10.5 to create a second room with a length of 9 and a width of 12. Have the program calculate this new room's area.

3. (Modify) a. Modify the main() function in Program 10.5 to create four rooms: hall, kitchen, dining room, and living room. The dimensions for these rooms are as follows:
Hall: length = 12.40, width = 3.5
Kitchen: length = 14, width = 14
Living room: length = 12.4, width = 20
Dining room: length = 14, width = 10.5.

Your program should display the area of each room and the total area of all four rooms combined.

4. (Practice) Enter and run Program 10.6 on your computer.

5. (Modify) a. Modify the main() function in Program 10.6 to put a second elevator in service starting at the 5th floor and have a maximum floor of 20. Have this second elevator move to the 1st floor and then move to the 12th floor.
b. Verify that the constructor is called by adding a message in it that’s displayed each time a new object is created. Run your program to verify its operation.

6. (Modify) Modify the main() function in Program 10.6 to use a while loop that calls the Elevator’s request() method with a random number between 1 and 15. If the random number is the same as the elevator’s current floor, generate another request. The while loop should terminate after five valid requests have been made and be satisfied by movement of the elevator. (Hint: Review Section 6.8 about the use of random numbers.)

7. (Program) Construct a class named Light that simulates a traffic light. The class’s color attribute should change from Green to Yellow to Red and then back to Green by using the class’s change() method. When a new Light object is created, its initial color should be Red.

8. (Program) a. Construct a class definition to represent an employee of a company. Each employee is defined by an integer ID number, a double-precision pay rate, and the maximum number of hours the employee should work each week. The class should provide these services: the capability to enter data for a new employee, the capability to change data for a new employee, and the capability to display existing data for a new employee.
b. Include the class definition created for Exercise 8a in a working C++ program that asks the user to enter data for three employees and then displays the entered data.
c. Modify the program written for Exercise 8b to include a menu that offers the user the following choices:

- 1. Add an employee
- 2. Modify employee data
- 3. Delete an employee
- 4. Exit this menu

In response to the user’s choice, the program should initiate an action to implement the choice.

9. (Program) a. Construct a class definition to represent types of food. A type of food is classified as basic or prepared. Basic foods are further classified as Dairy, Meat, Fruit, Vegetable, or Grain. The class should provide these services: the capability to enter data for a new food, the capability to change data for a new food, and the capability to display existing data for a new food.
b. Include the class definition created for Exercise 9a in a working C++ program that asks the user to enter data for four food items and then displays the entered data.
c. Modify the program written for Exercise 9b to include a menu that offers the user the following choices:

- 1. Add a food item
- 2. Modify a food item
- 3. Delete a food item
- 4. Exit this menu

In response to the user's choice, the program should initiate an action to implement the choice.

## 10.5 Class Scope and Duration Categories

As you learned in Section 6.4, the scope of an identifier defines the portion of a program where the identifier is valid. There are two categories of scope: local and global. In addition, each identifier has a duration, which refers to the length of time storage locations are reserved for the variable or method the identifier names (see Section 6.5).

Just as a variable is local to the method that declares it, class data members are local to the class in which they're declared. This means class data members are known only within the class, which includes the class methods. Similarly, just as a method's local variable always takes precedence over a global variable having the same name, a class data member takes precedence over a global variable of the same name. Additionally, class method names are local to the class they're declared in and can be used only by objects declared for the class. Figure 10.4 illustrates these scope rules for the following declarations:

```
double rate;  // global scope
// class declaration section
class Test
{
private:
    double amount, price, total;  // class scope
public:
    double extend(double, double); // class scope
};
```
