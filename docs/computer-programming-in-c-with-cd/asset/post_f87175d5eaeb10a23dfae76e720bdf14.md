
As you know, in the case of multiple inheritance, base class constructors are invoked in the order of inheritance. Now suppose a program has a virtual base class, a non virtual base class, member objects, and the derived class all together. What will be the order of constructors in such a case? In this case, the order of constructor invocation will be as follows:

- 1. Virtual base class constructors, in the order of inheritance
- 2. Non virtual base class constructors, in the order of inheritance
- 3. Member objects constructors, in the order of declaration
- 4. Derived class constructors

Listing 27 shows the order of constructors and destructors invocation when a program has a virtual base class, a non virtual base class, member objects, and derived class all together (you can find the ConsDesInvocationOrder.cpp file on the CD in the Code\Chapter7 folder).

## Listing 27: Invoking a Constructor and Destructor in a Complex Program of Inheritance

```cpp
#include<iostream.h>

class A
{
public:
    A()
    {
        cout<<"Constructor of A class"<<endl;
    }
    ~A()
    {
        cout<<"Destructor of A class"<<endl;
    }
};

class B
{
public:
    B()
    {
        cout<<"Constructor of B class"<<endl;
    }
    ~B()
    {
        cout<<"Destructor of B class"<<endl;
    }
};

class C : virtual public A
{
public:
    C()
    {
        cout<<"Constructor of C class"<<endl;
    }
    ~C()
    {
        cout<<"Destructor of C class"<<endl;
    }
};

class D : virtual public A
{
public:
    D()
    {
        cout<<"Constructor of D class"<<endl;
    }
    ~D()
    {
        cout<<"Destructor of D class"<<endl;
    }
};

class E
{
public:
    E()
    {
        cout<<"Constructor of E class"<<endl;
    }
    ~E()
    {
        cout<<"Destructor of E class"<<endl;
    }
};

class F : public B, public C, public D
{
private:
    E objE;
public:
    F()
    {
        cout<<"Constructor of F class"<<endl;
    }
    ~F()
    {
        cout<<"Destructor of F class"<<endl;
    }
};

int main()
{
    F objF;
    cout<<"Program Over"<<endl;
    return 0;
}
```

Output:

```text
Constructor of A class
Constructor of B class
Constructor of C class
Constructor of D class
Constructor of E class
Constructor of F class
Program Over
Destructor of F class
Destructor of E class
Destructor of D class
Destructor of C class
Destructor of B class
Destructor of A class
```

In Listing 27, the C and D classes are virtually inherited from class A. In other words, we can say that A is a virtual base class of the C and D classes. The F class is derived from the non virtual base classes B, C, and D. Class F is also a container class of the E class, as it contains the objE object of class E. Now, in the main() function, the objF object of class F is created to invoke the constructors and destructors of all the classes (A, B, C, D, E, and F) given in Listing 27. The constructors of these classes are called in the following order: the virtual base class, non virtual base classes, the member object, and the derived class.

It is important to note that in Listing 27, the destructors of all the classes are invoked in the opposite order to that in which the constructors are invoked, that is, the derived class, the member object, non virtual base classes, and the virtual base class.

## TEST YOUR KNOWLEDGE

Q8. Consider the inheritance structure of various classes, as shown in Figure 8:

![](img/8a6886c00caa6a1651a6c0e62bff341f_542_0.png)

In Figure 8, the Master class derives information from the Account and Admin classes, which in turn derive information from the Person class.

Now, define all four classes and write a program to create, update, and display the code information contained in the objects of the Master class.

Ans.

```cpp
#include<iostream.h>

class Person
{
    public:
        char name[20];
        int code;
        void get_name()
        {
            cout<<"Enter name : ";
            cin>>name;
            cout<<endl;
        }
        void get_code()
        {
            cout<<"Enter code : ";
            cin>>code;
            cout<<endl;
        }
        void display_namecode()
        {
            cout<<"Name : "<<name<<endl;
            cout<<"Code : "<<code<<endl;
        }
};

class Account : virtual public Person
{
    protected:
        int pay;
    public:
        void get_pay()
        {
            cout<<"Enter pay : ";
            cin>>pay;
            cout<<endl;
        }
        void display_pay()
        {
            cout<<"Pay : "<<pay<<endl;
        }
};

class Admin : virtual public Person
{
    public:
        int experience;
    public:
        void get_exp()
        {
            cout<<"Enter experience : ";
            cin>>experience;
            cout<<endl;
        }
        void display_exp()
        {
            cout<<"Experience : "<<experience<<endl;
        }
};

class Master : public Account, public Admin
{
    public:
        void getdata()
        {
            get_name();
            get_code();
            get_pay();
            get_exp();
        }
        void displaydata()
        {
            display_namecode();
            display_pay();
            display_exp();
        }
};

void main()
{
    Master m[10];
    int num,code,ch;
    char choice;
    do
    {
        cout<<"Main Menu"<<endl;
        cout<<"1 : Create"<<endl;
        cout<<"2 : Display"<<endl;
        cout<<"3 : Update"<<endl;
        cin>>ch;
        switch(ch)
        {
            case 1: cout<<"Enter no. of persons"<<endl;
                cin>>num;
                for(int i=0;i<num;i++)
                {
                    m[i].getdata();
                }
                break;

            case 2: cout<<"The details are: "<<endl;
                for(i=0;i<num;i++)
                {
                    m[i].displaydata();
                }
                break;

            case 3: cout<<"Enter the code"<<endl;
                cin>>code;
                for(i=0;i<num;i++)
                {
                    if(m[i].code==code)
                    {
                        m[i].get_name();
                        m[i].get_pay();
                        m[i].get_exp();
                        break;
                    }
                }
        }
        cout<<"Do you want to continue (Y for yes and N for No)"<<endl;
        cin>>choice;
    }while(choice=='y'||choice=='Y');
}
```

### Output

```text
Main Menu
1 : Create
2 : Display
3 : Update
1
Enter no. of persons
2
Enter name : Vandana

Enter code : 101

Enter pay : 4000

Enter experience : 1

Enter name : Shilpa

Enter code : 202

Enter pay : 7000

Enter experience : 2
Do you want to continue (Y for yes and N for No)
y
Main Menu
1 : Create
2 : Display
3 : Update
2
The details are:
Name : Vandana
Code : 101
Pay : 4000
Experience : 1
Name : Shilpa
Code : 202
Pay : 7000
Experience : 2
Do you want to continue (Y for yes and N for No)
y
Main Menu
1 : Create
2 : Display
3 : Update
3
Enter the code
202
Enter name : Shilpa

Enter pay : 8000

Enter experience : 2

Do you want to continue (Y for yes and N for No)
Y
Main Menu
1 : Create
2 : Display
3 : Update
2
The details are:
Name : Vandana
Code : 101
Pay : 4000
Experience : 1
Name : Shilpa
Code : 202
Pay : 8000
Experience : 2
Do you want to continue (Y for yes and N for No)
N
```

Let’s now learn to create and use pointer objects of C++ classes.

## 7.10 Creating and Using Pointer Objects

In C++ programming, you can also create pointer type objects of a class. A pointer is a variable that stores the memory address of another variable. You can also obtain a value a pointer refers to. This process of obtaining a value is called dereferencing the pointer. You can create a pointer to class objects in the same way as you create structure variables. The syntax to create a pointer object of a class is shown in the following code snippet:

```cpp
class Employee
{
public:
int x;
void employeeDetails()
{
...
```
