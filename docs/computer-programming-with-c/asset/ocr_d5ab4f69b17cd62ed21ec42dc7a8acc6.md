will invoke the member function `operate()` for object o1 because pointer `piftr` is attached to `operate()` function of class Data. The resultant value returned by the `operate()` function will be stored in variable x. Hence, variable x will contain the result of addition of members a and b of object o1.

Since the pointer ptr is attached to the member `results`, we can access the member `results` of object o1 using pointer ptr as follows:

```
o1.*ptr
```

Hence, the statement

```
cout<<"Subtraction is "<<o1.*ptr<<endl;
```

will print the value of variable `results` of object o1.

To show how to call a function with parameters using bindable pointers, we have created a function named as `sumOfProd()` which accepts two floating point values k1 and k2, multiplies member a with k1 and member b with k2 and returns the sum of products. This is invoked by creating a pointer named as pfmul in the code as follows:

```
/*Step 1: Declare a pointer which can point to a function that
  takes two floating point numbers and returns a float*/
float (Data::*pfmul)(float,float);
/*Step 2: Bind the pointer to sumOfProd function*/
pfmul = &Data::sumOfProd;
/*Step 3: Invoke function sumOfProd using object o1 by passing two
  constants to it 10.5 and 5.5*/
float res = (o1.*pfmul)(10.5,5.5);
cout<<"Sum of Products is "<<res<<endl;
```

The variable res will contain the following sum for object o1:

```
a*10.5+b*5.5
```

Assuming the value of a as 10 and b as 20 for object o1, the value of variable res will be `215.00`, which is printed on the computer screen by the cout statement.

We have mirrored similar statements for object o2 and invoked functions `input()` and `operate()` using the same pointers `pfvtr` and `piftr`, respectively. We have again used the pointer ptr to print the result of subtraction for object o2.

# 11.17  this Pointer

`this` is a built-in pointer in C++ that points to the object using which the function is invoked. The keyword `this` is generally used inside the body of the member function to determine which object has invoked the function. We know that a class can have multiple objects, and a member function can be invoked using any one of the objects of the class. You may come across a situation wherein you have already entered into the function and need to determine the exact object that invoked the function within the function body.