# 7.5 Identification and Access of Derived-Class Member 293

derived from both the manager group and the salesman group. The definitions of the classes are:

```
class salesman:virtual public employee //part-time salesman
{
protected:
    float CommRate;              //percentage of the sales commissions
    float sales;                //current sales
public:
    salesman();                 //constructor
    void Setsales(float sl);     //set sales
    void pay();                 //calculate monthly salary
};
class manager:virtual public employee //manager
{\protected:
    float monthlyPay;           //fixed monthly salary
public:
    manager();                  //constructor
    void pay();                 //calculate monthly salary
};
class salesman:public manager,public salesman //sales manager
{
public:
    salesman();                //constructor
    void pay();                 //calculate monthly salary
};
```

Here both salesman and manager are inherited from the virtual base class employee. So in the derived class salesman, there is only one copy of base class employee members derived from different paths, to avoid redundant copies. Each class has the function pay(). The base employee only declares the function to unify the interface of the class family. Because derived classes have different characteristics (e.g., different ways of calculating monthly salary), the function pay() declared in class employee cannot apply to every derived class. The derived classes must declare their own function pay() to hide the function declared in the base class. You will have a better understanding of it after reading the entire program in Section 7.7.

Let us compare the two examples, which respectively use scope qualifier and virtual class mechanism. In the former case, the derived class has multiple copies of the members with the same name inherited from the base classes, which are uniquely identified