# 716 Introduction to C++

the private member the publishing firm (of type string). Also, define the Car class derived from public access from the Product with private member horsepower. Add appropriate functions in the classes so that the following program works.

```
int main()
{
    Car b(1
```

**U.21.3 Write a program that implements a simplified vehicle application..** Define the Vehicle class with private member name of the owner. Also that the owner owns a car and a motorcycle. Define the Car and Moto classes with public access from the Vehicle with private members, the plate number (of type string) and the insurance cost of each vehicle. Define the Insurance derived from public access from the Car and Moto classes with private member the name of the insurance company. When an Insurance object is created a single sub-object of the Vehicle class should be created. Define the f() function that takes a vector of Insurance elements and displays the name of the owner who pays the largest amount, as well as the details of his and the name of the insurance company. Assume that there is only one owner with the highest total cost. Add appropriate functions in the classes so that the following program works.

```
int main()
{
    vector<Insurance> v;
    Insurance ins1("Alpha","1.2",10,"3.4",20,"Ins 1");
ins2("Beta","5.6",30); /* In this example, for
name of the owner should become Alpha, the plate number of the
1.2, the insurance cost 10, the plate number of the motorcycle 3.4,
the insurance cost 20, and the name of the insurance company Ins 1. For
each Insurance object a single Vehicle sub-object should be created.
Create more Insurance objects and store them in v. Then, call f(). For
example, if v contains only these two elements, the program should
display Beta 5.6 7.8 Ins 2, because the total insurance cost is 30+40
70, which is greater than 10+20 = 30 of the first owner.*/
    return 0;
}
```