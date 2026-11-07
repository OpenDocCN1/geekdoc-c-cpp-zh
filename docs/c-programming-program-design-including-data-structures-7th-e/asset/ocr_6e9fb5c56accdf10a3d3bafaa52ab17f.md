```
```cpp
{
    rectangleType temp = *this;   //use this pointer to copy
                                  //the value of the object

    //increment the length and width
    length++;
    width++;

    return temp;   //return the old value of the object
}
```
```

# ## GENERAL SYNTAX TO OVERLOAD THE POST-INCREMENT OPERATOR ++ AS A MEMBER FUNCTION

The general syntax to overload the post-increment operator ++ as a member function is described next.

**Function Prototype** (to be included in the definition of the class):

```
```cpp
className operator++(int);
```
```

**Function Definition:**

```
```cpp
className className::operator++(int u)
{
    className temp = *this;    //use this pointer to copy
                               //the value of the object

    //increment the object

    return temp;  //return the old value of the object
}
```
```

The post-increment operator can also be overloaded as a nonmember function of the class. In this situation, the operator function `operator++` has two parameters. The definition of the function to overload the post-increment operator for the class `rectangleType` as a nonmember is:

```
```cpp
rectangleType operator++(rectangleType& rectangle, int u)
{
    rectangleType temp = rectangle; //copy rectangle into temp

    //increment the length and width of rectangle
    (rectangle.length)++;
    (rectangle.width)++;

    return temp;    //return the old value of the object
}
```
```

# ## GENERAL SYNTAX TO OVERLOAD THE POST-INCREMENT OPERATOR ++ AS A NONMEMBER FUNCTION

The general syntax to overload the post-increment operator ++ as a nonmember function is described next.