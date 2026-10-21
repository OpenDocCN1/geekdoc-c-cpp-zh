Address : =s17/127,23
Varanasi,UP

# EXPLANATION :

In the earlier program the structure were given name address, it was not necessary so here we have removed the name. Also we have made structure as public so we can show you how to use it outside the class using an object of class person. The three data members name, age and sal are private so we initialize them using function input. The members of structure are initialized in the main using an object of person class as :

```
strcpy(p.addr.hno,"s17/127");
strcpy(p.addr.street,"23");
strcpy(p.addr.city,"Varanasi");
strcpy(p.addr.state,"UP");
```

Note : First addr is accessed using object p then member of structures are accessed using dot operator.

# 6.3 STRUCTURE IN C++

We have learned that for a class default access specifier is private i.e., if no access mode is given all data members and functions are considered as private. A structure in C++ is similar to class with the difference that default access specifier for a structure is public. Other than this there is no difference in structure and classes in C++. Given below in the left column a class is written and on the right column corresponding structure is written. Note for a class we didn't specify private specifier for the data members as default mode is private. Similarly, for the structure class we didn't specify public specifier for the member function as default mode is public.

# Table : Shows the Difference between Class and Structure

| Simple Demo Class | Corresponding Structure |
|---|---|
| Class demo
{
  int x;
  int y;
public :
  void input(int a,int b)
  {
    x = a;
    y = b;
  }
  void show()
  { | struct demo
{
  void input(int a,int b)
  {
    x=a;
    y=b;
  }
  void show()
  {
    cout<<"x="<<x<<endl;
    cout<<"y="<<y<<endl;
  }
} |