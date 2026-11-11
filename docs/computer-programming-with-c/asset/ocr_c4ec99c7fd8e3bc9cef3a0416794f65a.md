```
```cpp
void main()
{
//create Weight objects
Weight w1(50,800);
//UN-BOXING From Object to basic value*/
long grams =(long) w1;
cout<<"Weight in grams is "<<grams<<endl;
Weight w2;
//BOXING: From Basic to Object value using a constructor*/
w2=grams;
w2.output();
}
```
```

A weight object specified in terms of kilogram and gram can be fully converted into grams as follows:

```
```cpp
kilogram*1000 + gram
```
```

Hence we have written an operator function in class Weight which overloads the type cast operator long( ) as shown below.

```
```cpp
operator long()
{
        return (kilogram*1000+gram);
}
```
```

The statement

```
```cpp
long grams =(long) w1;
```
```

applies a cast operator to object w1 to convert it into a long value. Hence, it invokes the operator long( ) function defined in class Weight. Needless to mention that object w1 has invoked this function and hence members kilogram and gram of w1 can be accessed directly within the scope of the function. As w1 has a kilogram value of 50 and gram value of 800, the cast operator function returns 50,800 which is assigned to a long type variable grams.

Let us now focus on converting long value to object of Weight. In order to achieve this, we have two options:

**Option 1:** Create a constructor in Weight class, which takes one argument of type long and initializes the kilogram and gram values as shown in Figure 13.24.

**Option 2:** Overload operator= function in class Weight, which allows assigning of long values to Weight objects. The operator= takes a long type argument and assigns the value of members kilogram and gram from it as shown in Figure 13.24.

In the given program, we have implemented option 1, but any of these options can be used interchangeably.

The statement

```
```cpp
w2 = grams ;
```
```