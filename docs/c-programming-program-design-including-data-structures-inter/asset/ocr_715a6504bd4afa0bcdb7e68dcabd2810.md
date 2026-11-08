9. Consider the following class definition:

```
```cpp
class temp
{
public:
    void print() const;
    void setDescription(string);
    void setX(double);
    string getDescription();
    double getX();
    temp();
    temp(string, double);

private:
    string description;
    double x;
};
```
```

What is wrong with the following class definition?

```
```cpp
class derivedFromTemp public temp
{
public:
    void print();
    void setX(double);
    double getZ();
    double power();
        //returns z to the power of z.

private:
    double z;
};
```
```

10. Assume the definition of the class temp as given in Exercise 9. Consider the following class definition:

```
```cpp
class derivedFromTemp: public temp;
{
public:
    void print();
        //outputs the values of all the instance variables.
    void setZ(double);
        //sets the value of z according to the parameter.
    double getZ();
        //returns the value of z.
    double power() const;
        //returns z to the power of z.

    derivedFromTemp();
        //sets the values of instance variables to "",
        //0.0, and 0.0, respectively.
```
```