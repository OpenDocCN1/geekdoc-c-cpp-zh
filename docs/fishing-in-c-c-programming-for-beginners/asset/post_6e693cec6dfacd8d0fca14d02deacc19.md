
cout<<b1.volume(5,2,3)<<endl;
cout<<b1.calculate_base_area(2,3);
}

Above program gives various errors saying “int cuboid::length is private”.

There are three types of permission levels: private, protected and public. But here, these are even more important. These give us the power of encapsulation. Using encapsulation we can encapsulate the members and methods of the class and limit it to the derived class and also extend it to more derived classes further.

Suppose we derive another class from the base_area class as follows:

```
#include<iostream>
using namespace std;
class cuboid
{
 public:
 int length,breadth,height;
 int volume(int,int,int);
};
```

```
int cuboid::volume(int x,int y,int z)
{
 length=x;
 breadth=y;
 height=z;
 return length*breadth*height;
}
```

```
class base_area:public cuboid
{
 public:
 int calculate_base_area();
};
int base_area::calculate_base_area()
{
    return length*breadth;
}
```

```
class side_area:public base_area
{
    public:
    int calculate_side_area();
};
```

```
int side_area::calculate_side_area()
{
    return length*height;
}
```

```
int main()
{
    class side_area s1;
    cout<<"Volume of cuboid is: "<<s1.volume(2,3,4)<<endl;
    cout<<"Base area of cuboid is: "<<s1.calculate_base_area()<<endl;
    cout<<"Area of side wall of cuboid is: "<<s1.calculate_side_area();
}
```

Output
Volume of cuboid is: 24
Base area of cuboid is: 6
Area of side wall of cuboid is: 8

In the above program, we used the **public** keyword, so the base classes were accessible from the derived classes. What if we use the **private** keyword?

## Accessibility in inheritance

Consider the following program:

```
#include<iostream>

using namespace std;

class cuboid
{

    public:

    int length,breadth,height;

    int volume(int,int,int);

};

int cuboid::volume(int x,int y,int z)
{

    length=x;

    breadth=y;

    height=z;

    return length*breadth*height;

}

class base_area:private cuboid
{

    public:

    int calculate_base_area();

};

int base_area::calculate_base_area()
{
    return length*breadth;
}
```

```
int main()
{
    class base_area b1;

    cout<<"Volume of cuboid is: "<<b1.volume(2,3,4)<<endl;
    cout<<"Base area of cuboid is: "<<b1.calculate_base_area()<<endl;
}
```

This program will generate an error "[Error] 'int cuboid::volume(int, int, int)' is inaccessible" . It means there is a certain rule and classes follow them. The rule goes as:

## private inheritance:

| Permission level | private members | protected members | public members |
|---|---|---|---|
| Accessible in base class | yes | yes | yes |
| Accessible in derived class | no | yes | yes |
| Accessible outside the derived class | no | no | no |

## protected inheritance:

| Permission level | private members | protected members | public members |
|---|---|---|---|
| Accessible in base class | yes | yes | yes |
| Accessible in derived class | no | yes | yes |
| Accessible outside the derived class | no | no | no |

## public inheritance:

| Permission level | private members | protected members | public members |
|---|---|---|---|
| Accessibility | | | |
| Accessible in base class | yes | yes | yes |
| Accessible in derived class | no | yes | yes |
| Accessible outside the derived class | no | no | yes |

Now, you have understood that in the above program, we tried to access volume function, through an object of base_area class which is b1 using private inheritance but public members are not accessible through the private inheritance outside the derived class i.e. in main() function. That's why the compiler gives the corresponding error.

To remember the above chart, just remember the position of yes. You will see a pattern 123,122,122.

### Note:

- 1. Any member defined in a class is always accessible to all the functions declared or defined in that class
- 2. Private members of the base class cannot be inherited

## Types of inheritance

### Single inheritance

If we derive a class from a base class then the architecture formed is called single inheritance.

![](img/5340985153962870d4e4a3b9453b9146_205_0.png)

### Single inheritance

The first program used in this chapter is a type of single inheritance.

### Multilevel inheritance

In the above program, you can see that we have inherited a class say B from a base class say A then we inherited a class say C from the inherited class B. This is called multilevel inheritance.

![](img/5340985153962870d4e4a3b9453b9146_206_0.png)

### Multilevel inheritance

Third program used in this chapter is a type of multilevel inheritance.

### Hierarchical inheritance

If we derive multiple classes from single base class then this inheritance is Hierarchical inheritance.

![](img/5340985153962870d4e4a3b9453b9146_206_1.png)

### Hierarchical inheritance

```
#include<iostream>
using namespace std;
class cuboid
{
    public:
    int length,breadth,height;
    int volume(int,int,int);
};

int cuboid::volume(int x,int y,int z)
{
    length=x;
    breadth=y;
    height=z;
    return length*breadth*height;
}

class base_area:public cuboid
{
    public:
        int calculate_base_area();
};

int base_area::calculate_base_area()
{
    return length*breadth;
}

class side_area:public cuboid
{
    public:
        int calculate_side_area();
};

int side_area::calculate_side_area()
{
    return length*height;
}
```

```
}

int main()
{
    class base_area b1;
    class side_area s1;
    cout<<"Volume of cuboid is: "<<b1.volume(2,3,4)<<endl;
    cout<<"Base area of cuboid is: "<<b1.calculate_base_area()<<endl;
    cout<<"Volume of second cuboid is: "<<s1.volume(3,4,5)<<endl;
    cout<<"Area of side wall of second cuboid is: "<<s1.calculate_side_area();
}
```

Output
Volume of cuboid is: 24
Base area of cuboid is: 6
Volume of second cuboid is: 60
Area of side wall of second cuboid is: 15

Here, we have inherited two classes base_area and side_area both from class cuboid.

### Multiple inheritance

If we derive a class from multiple base classes then the architecture formed is called multiple inheritance.

![](img/5340985153962870d4e4a3b9453b9146_208_0.png)

### Multiple inheritance

This is an amazing type of inheritance; using this type of inheritance we can inherit a class from multiple base classes.

See here, to inherit from multiple base classes, we use the following syntax:

```
class inherited_class: permission_level class_name,permission_level class_name
{
    //Statements
}
```

Following code snippet will remove all of your confusion:

```
class cuboid:public base_area,public side_area
{
public:
int volume();
};
```

Now, consider the following program:

```
#include<iostream>
using namespace std;
class base_area
{
public:
int length,breadth;
int calculate_base_area(int,int);
};
int base_area::calculate_base_area(int p,int q)
{
length=p;
breadth=q;
return length*breadth;
}
class side_area
{
public:
    int x,z;
    int calculate_side_area(int,int);
};

int side_area::calculate_side_area(int a,int b)
{
    x=a;
    z=b;
    return x*z;
}

class cuboid:public base_area,public side_area
{
    public:
    int volume();
};

int cuboid::volume()
{
    return length*breadth*z;
}

int main()
{
    class cuboid c1;
    cout<<"Base area of cuboid is: "<<c1.calculate_base_area(3,4)<<endl;
    cout<<"Area of side wall is: "<<c1.calculate_side_area(3,5)<<endl;
    cout<<"Volume of cuboid is: "<<c1.volume()<<endl;
}
```

## Output

Base area of cuboid is: 12

Area of side wall is: 15

Volume of cuboid is: 60

### Hybrid inheritance

A combination of two or more types of inheritances is called hybrid inheritance.

![](img/5340985153962870d4e4a3b9453b9146_211_0.png)

Hybrid inheritance

In the following program, we have mixed multiple inheritance and single inheritance. You may also think it as a mixture of multiple inheritance and multilevel inheritance.

Consider the following program:

```
#include<iostream>
using namespace std;
class base_area
{
public:
int length,breadth;
int calculate_base_area(int,int);
};
int base_area::calculate_base_area(int p,int q)
{
