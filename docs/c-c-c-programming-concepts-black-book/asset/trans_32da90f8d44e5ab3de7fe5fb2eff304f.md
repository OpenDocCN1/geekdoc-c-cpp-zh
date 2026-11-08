

```cpp
House(char *myName)
{
    cout<<"House::constructor_C\n";
    name_p = new char(sizeof(strlen(myName)));
    name_p = myName;
    Room::initialList(roomsList);
    Room* myRoom;
    Room::createRoom(myRoom, this, "Kitchen");
    roomsList[0] = myRoom;
    Room::createRoom(myRoom, this, "BedRoom");
    roomsList[1] = myRoom;
    Room::createRoom(myRoom, this, "Drawing Room");
    roomsList[2] = myRoom;
}
~House()
{
    cout<<"House::destructor_D\n";
    unsigned int i;
    cout<<"Delete all the Rooms ...\n";
    for(i=0; i<3; ++i)
    {
        if(roomsList[i] != NULL)
        {
            delete (roomsList[i]);
        }
    }
    delete [] roomsList;
    delete (name_p);
}
void disp()
{
    cout<<"\n\nName of the House :"<<name_p;
    if(roomsList != NULL)
    {
        unsigned int i;
        cout<<"\n\nRooms details...\n";
        for(i=0; i<3; ++i)
        {
            if(NULL != roomsList[i])
            {
                roomsList[i]->disp();
            }
        }
        cout<<"\n\n";
    }
}
private:
    char* name_p;
    Room* roomsList[3];
};
int main()
{
    cout<<"\nExample of Composition Relationship\n";
    cout<<"----------------------------------------\n\n";
    House hse("Shanti Aashram");
    cout<<"\n\nHouse details...\n";
    hse.disp();
    cout<<"Now House itself creates the Rooms and Deletes as well, before it gets deleted itself\n";
    return(0);
}
```

上述代码的输出如下：

```text
OUTPUT:
-------
Example of Composition Relationship
------------------------------------
House::constructor_C
Room::constructor_C
Room::constructor_C
Room::constructor_C
House details...
Name of the House : Shanti Aashram
Rooms details...
Kitchen
BedRoom
Drawing Room
Now House itself creates the Rooms and Deletes as well, before it gets deleted itself...
House::destructor_D
Delete all the Rooms...
Room::destructor_D
Room::destructor_D
Room::destructor_D
```

在继续之前，让我们先理解组合与聚合之间的区别。

组合是聚合的一种更强形式。它表示整体类对部分类具有独占所有权。这意味着部分可以在组合体创建之后创建，但这些部分会在组合体销毁之前被显式移除。然而，聚合与组合的不同之处在于它不蕴含所有权。在组合中，当拥有对象被销毁时，被包含的对象也会被销毁。然而，在聚合中，这不一定成立。让我们举个例子来理解这个概念。一家公司拥有许多部门，每个部门又有许多员工。如果公司某天关闭，那么部门将不复存在，但那些部门中的员工仍会保留。因此，公司可以作为与部门之间组合关系的例子；而部门则继续作为员工的聚合。

代码清单 13.20 展示了在 C++ 中实现员工与部门之间聚合关系的代码片段：

### 代码清单 13.20：实现员工与部门之间的聚合关系

```cpp
class Employee;
class Department
{
    ...
    /* Aggregation */
    Employee * members[10];
    GetSalary()
    {
        ...
    }
};
```

代码清单 13.21 展示了在 C++ 中实现员工与公司之间组合关系的代码片段：

### 代码清单 13.21：实现员工与公司之间的组合关系

```cpp
class Company
{
    private:
        /* Composition */
        Department employee[100];
        ...
};
```

在聚合中，一个对象可能只包含指向另一个对象的引用或指针，并且可能不承担其生命周期责任。有时，当组合与聚合之间的区别不重要时，聚合也被称为组合。

组合可用于存储复合数据类型的众多实例。这有时被称为包含关系，包括链表、关联数组和二叉树。

## 泛化

泛化有一个父流程和一个或多个子流程。子流程描述其父流程的一种特殊类型。例如，在商店中，我们可以通过现金或银行卡付款。因此，现金支付和银行卡支付是支付流程的两个子流程。图 13.30 展示了泛化关系：

![](img/43c5f409f9b17790a628c4b4df854b61_398_0.png)

**图 13.30：** 展示泛化关系

## 包含

如果一个流程需要另一个流程的结果，那么这两个流程之间的关系称为包含。例如，如果我们想从音像店借一张 CD，那么我们需要先确认该 CD 是否存在于店中。因此，借 CD 包含验证流程。图 13.31 展示了包含关系的图示表示：

![](img/43c5f409f9b17790a628c4b4df854b61_398_1.png)

**图 13.31：** 展示包含关系

## 扩展

根据条件，如果一个流程需要有一个子流程，那么我们可以使用扩展关系将这两个流程关联起来。例如，要享受机票折扣，我们可以有两个子流程：国内航班和国际航班，并且它们通过扩展关系与其父流程绑定。在这种情况下，条件可以是航班类型。图 13.32 说明了用于描述扩展关系的表示法：

![](img/43c5f409f9b17790a628c4b4df854b61_399_0.png)

在最后一节中，让我们概述一下数据抽象与信息隐藏。

## 数据抽象与信息隐藏

信息隐藏是 OOP 中一个非常重要的术语，其中类试图向用户隐藏其实现细节。例如，我们可以使用数组或链表的概念来实现一个栈。然而，这并不会影响栈的功能。用户只关心栈如何执行以及它提供什么功能，而不关心它是如何实现的。这个概念称为数据抽象。

考虑用于计算员工工资的 EmployeeSal 类。代码清单 13.22 展示了 EmployeeSal 类的代码：

### 代码清单 13.22：展示用于说明信息隐藏的代码

```cpp
class EmployeeSal
{
    public:
        void setSalary(double sal)
        {
            salary = sal;
        }
    private:
        double salary;
};
```

人们可能会将封装与信息隐藏混淆。封装使我们能够围绕想要封装的事物划出边界。它使我们能够就边界内部世界和外部世界进行交流。另一方面，信息隐藏是一种设计，它限制数据和实现流程的直接暴露，以防止不必要的耦合。信息隐藏是一种设计原则；而封装仅仅是编程语言的一种特性。

> 根据 John Wilkinson 的说法：“信息隐藏，或者其反面——信息泄漏，可能跨越多个对象，也可能涉及客户端代码与实现代码之间的其他耦合形式。例如，调用顺序依赖会暴露一些通常应当隐藏的信息。另一个例子可能是客户端代码所使用的默认值。有些代码虽然实现了完美的封装，却仍然存在信息隐藏问题。”

因此，封装并不等同于信息隐藏，但在某些方面，它需要一定程度的信息隐藏。

抽象、封装和信息隐藏可以使用抽象数据类型（ADT）来实现。ADT 是一种被设计为派生类接口的类。注意，ADT 不能被实例化。ADT 作为其他类的基类，而这些类将被实例化为对象。图 13.33 展示了 ADT 的不同分类：

