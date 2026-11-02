```
void display_all(const CashRegister registers[])
{
  for (int i = 0; i < NREGISTERS; i++) { registers[i].display(); }
}
```

That programmer is conscientious and declares the registers parameter variable as const. But then the call registers[i].display() will not compile. Because CashRegister::display is not tagged as const, the compiler suspects that the call registers[i].display() may modify registers[i]. But the function promised not to modify the registers array.

If you write a program with other team members who are conscientious about const, it is very important that you do your part as well. You should therefore get into the habit of using const with all accessor member functions.

# 9.6 Constructors

A constructor is called automatically whenever an object is created.

A constructor is a member function that initializes the data members of an object. The constructor is automatically called whenever an object is created. By supplying a constructor, you can ensure that all data members are properly set before any member functions act on an object.

To understand the importance of constructors, consider the following statements:

```
CashRegister register1;
register1.add_item(1.95);
int count = register1.get_count(); // May not be 1
```

Here, the programmer forgot to call clear before adding items. Therefore, the data members of the register1 object were initialized with random values. Constructors guarantee that an object is always fully initialized when it is defined.

The name of a constructor is identical to the name of its class. You declare constructors in the class definition, for example:

```
class CashRegister
{
public:
  CashRegister(); // A constructor
  ...
};
```

The name of a constructor is the same as the class name.

![](bbox=[0.6, 0.78, 0.98, 0.98])

A constructor is like a set of assembly instructions for an object.
© Ann Marie Kurtz/Stockphoto.