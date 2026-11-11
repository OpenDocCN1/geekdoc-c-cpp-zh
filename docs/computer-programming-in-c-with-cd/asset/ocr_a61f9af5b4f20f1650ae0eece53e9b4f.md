```
```cpp
hgt = c;
result = len * wd * hgt;
}

void Volume::CalcVol()
{
cout << "Volume is: " << result << endl;
}

int main()
{
Volume v1(5.2,3.4,7.3), v2(10,5,6);
v1.CalcVol();
v2.CalcVol();
return 0;
}
```
```

**Output:**

```
```text
Volume is: 129.064
Volume is: 300
```
```

In Listing 16, Volume(double a, double b, double c) is an inline constructor of the Volume class. The Volume(double a, double b, double c) constructor is defined outside the boundary of the Volume class by using the inline keyword and the scope resolution (::) operator.

# Copying a Constructor

As you know, it is possible to have a constructor with parameters. You can pass a constructor parameter as a value parameter of any data type, except an object of its own class. For example, in the following code snippet, the declaration of the Product class is invalid:

```
```cpp
class Product
{
...
...
public:
Product (Product object1);          // Invalid declaration
...
}
```
```

However, a class’s own object can be passed as a reference parameter. Reference parameters are indicated by an ampersand (&) symbol that precedes the argument. For example, in the following snippet, passing a reference argument of the Product class is valid: