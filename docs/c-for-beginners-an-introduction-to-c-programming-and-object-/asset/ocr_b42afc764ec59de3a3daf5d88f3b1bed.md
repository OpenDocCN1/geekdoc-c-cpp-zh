integers will return the sum as an integer. The other one will have to return a float value else the sum will lose precision. The point is, these two functions can be overloaded because they accept different types of arguments and not because they have different return types.

Let us write a small C++ code snippet of whatever we have just discussed:

```
```cpp
//Two integers
int sum ( int a , int b )
{
    return ( a + b );
}
//Two floats
float sum ( float a , float b )
{
    return ( a + b );
}
```
```

Calls to each of these functions are made as follows:

```
```cpp
int sum_int;
float sum_float;
//Call the function that accepts two integers
sum_int = sum ( 5, 60 );
//Call the function that accepts two floats
sum_float = sum ( 50.78, 60.1 );
```
```

The second function definition which accepts two float values and returns a float value could have returned an integer value and still be overloaded without problems but that would be logically incorrect as there is a very high chance of the sum of two float values being a float value.