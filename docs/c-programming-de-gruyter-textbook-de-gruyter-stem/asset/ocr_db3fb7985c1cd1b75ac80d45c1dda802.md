# 292 — Inheritance and Derivation

```
public: //external interfaces
int nV;
void fun(){cout<<"Member of B0"<<endl;}
};\class B1: virtual public B0 //class B0 is a virtual base class of
//the derived class B1
{
public: //new external interface
int n1;
};
class B2: virtual public B0 //class B0 is a virtual base class of
//the derived class B2
{
public: //new external interface
int n2;
};\class D1: public B1, public B2 //define derived class D1
{
public: //new external interfaces
int nV;
void fun(){cout<<"Member of D1"<<endl;}
};
int main() //main()
{
D1 d1;//declare object d1 of class D1
d1.nV=;//use direct base class
d1.fun();
}
```

Note: the declaration of a virtual base class uses the key word virtual during the class derivation. In main(), a derived-class object d1 is created and d1's members nV and fun can be accessed by the member names. The execution result is:

| Member of B0 |

Consider the personnel information management problem mentioned at the beginning of this chapter. In the system, we need to take into account four groups of people. In Section 7.1, we defined the class employee and derived the class technician. Now let us consider the definitions of other groups. Both part-time salesmen and managers should be inherited from the base class employee. Since manager belongs to the manager group and sales group, it has the characteristics of the two groups. For example, a sales manager's monthly salary is composed of two parts: the fixed salary and sales commissions. This clearly shows that the sales manager should be