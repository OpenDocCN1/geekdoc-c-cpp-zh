# Fig. 8.6 A simple view of control to the members of a class

![](bbox=[0.366, 0.139, 0.635, 0.304])

# Fig. 8.7 Multilevel inheritance

A derived class with multilevel inheritance is declared as follows:

```
```cpp
class A{ }; // Base class
class B: public A { }; // B derived from A
class C: public B { }; // C derived from B
```
```

This process can be extended to any number of levels.

Let us consider a simple example. Assume that the test results of a batch of students are stored in three different classes. Class **student** stores the roll-number, class **test** stores the marks obtained in two subjects and class **result** contains the **total** marks obtained in the test. The class **result** can inherit the details of the marks obtained in the test and the roll-number of students through multilevel inheritance. Example:

```
```cpp
class student
{
protected:
int roll_number;
public:
void get_number(int);
void put_number(void);
};
void student :: get_number(int a)
```
```