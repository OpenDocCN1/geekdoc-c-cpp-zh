
## NOTES

When an operator is **overloaded**, it can take **multiple forms** and its behaviour will be dependent upon the context in which the operator is used. For example, if a and b are variables of type integer, the expression a+b will perform addition of two integer values. On the other hand, if a and b are objects of type Point then the same expression a+b will perform addition of Point objects (assuming the operator + is overloaded for class Point).

C++ compiler can correctly identify which definition of the operator must be used depending on the **data types of the operands** used in the expression. Out of the multiple forms an operator takes, the compiler correctly identifies and **binds** one of the forms for each occurrence of the operator in the program. This is called **compile time binding** and the ability of the compiler to assign multiple forms to a single operator is called **compile time polymorphism**. We will discuss more on compile time binding and polymorphism in the later sections of this chapter, so don’t think much about it right now.

### Is creating programs with friendly syntax the only reason to overload any operator?

Creating programs with friendly syntax is one of the major reasons to overload any operator; but note that when an operator is overloaded the compiler also borrows all its properties like precedence, associativity etc. from its basic definition and applies them in the same way to the user-defined types. For example, when you overload operators +, - and * for objects of class Point, it means that you can use them in the way for Point objects as you could use them for primitive types. So, if P1, P2 ... P10 are different Point objects you could create an arithmetic expression to perform various operations as shown below

```
P10 = P1+P2*(P3+P4)-P5*P6+(P7-P8-P9);
```

The statement will execute using the same priority and associativity rules as they were when using these operators for basic data types. Establishing these results by creating different user-defined functions for addition, subtraction and multiplication would be possible but syntactically cumbersome, making the program difficult to create and maintain. Although we say that operator overloading is just a luxury to create programs with better syntax, there are some situations (like this one), where the programmers can’t avoid using it.

### 13.2 Overloading Operators

If we need to use a particular operator with objects, we must define an **operator function** to describe the behaviour of that operator when used with objects of a class. C++ supports a keyword operator, which is used to create an operator function. Figure 13.1 gives the syntax for creating an operator function. The operator symbol that is followed by the keyword operator will be overloaded and can be used with the objects of the class.

```
<returnType> operator<Operator Symbol>(<arguments>)
{
    ....function body
}
```

**Figure 13.1:** Syntax of creating an operator function

### What are the operations that should be performed in the operator function?

We know that a class is used to create a user-defined data type. Although the operator function facilitates the programmer to use an operator with objects of the class, the C++ compiler will not be in a position to know the set of operations that are to be performed when the operator is actually used with objects. For example, if P1 and P2 are objects of class Point and when we use operator + with P1 and P2 we should not expect the compiler to be aware of how two points must be really added. Hence the operator function must define a set of operations in its definition that will inform the compiler that when two points are added the addition of their individual x coordinates gives the x coordinate of the result and the addition of their individual y coordinates gives the y coordinate of the result. This means that the operator function explains the process (or behaviour) of the operator when used with user-defined types.

### When is the operator function executed? Do we call the operator function explicitly like other functions in C++?

We do not call the operator function explicitly. The operator function is internally invoked by the compiler when we use an operator along with the objects of the class. This makes C++ understand the exact operations to be followed when an operator is used with objects of the class.

Every C++ operator has an associated syntax as well as semantics. The **syntax of an operator** refers to the rules of using the operator which are defined by the grammar of the language, whereas **semantics of an operator** refers to the meaning of the operator describing the actual operation it performs. For instance, if we consider an operator +, the meaning or **semantic** for the operator is addition and the **syntax** to perform binary addition is as follows:

```
<ResultVariable> = <Operand1> + <Operand2>;
```

Operator overloading allows the programmer to enhance the semantics—or even change them—of the operator when redefining its behaviour for user-defined types. But the programmer can in no way attempt to change the syntax to be followed to use the operator. This means that the operator should be used with user-defined types with the same syntax as with basic types, even if it is overloaded. In fact, this is the reason why you would want to overload any operator. Although operator overloading technically allows you to drastically change the meaning/semantic of the operator for user-defined types, it is not recommended that you do so. For example, if we overload operator +, for using it with objects of class Point, then we may create the operator function as a member function of class Point as shown in Figure 13.2.

We should now be able to use operator + along with objects of class Point as shown below:

```
<ResultObject> = <PointObject1> + <PointObject2>;
```

Let us assume that the function body of the **operator+** is written by the programmer such that the operator function performs **multiplication** instead of actually performing the **addition**. This means that the meaning or semantics of operator + is now changed to **multiplication** by the programmer, which is actually defined as addition by C++.

Operator to be overloaded

```
class Point
{
    ......
    ......
    <returnType> operator+(<arguments>)
    {
        ....function body
    }
};
```

**Figure 13.2:** Creating operator function as an inline member function of the class

If P1, P2, and P3 are objects of class Point, we can use + with these objects because **operator+** is defined for class Point.

```
P3 = P1 + P2;
```

However, the meaning of the above statement will depend on the actual operations that are performed inside the body of the operator function. If the **operator+** function internally performs multiplication, the statement P3 = P1 + P2 will then actually perform multiplication of Point objects instead of addition. This reflects that we have easily changed the meaning or semantic of **operator+** for objects of class Point, but the syntax of **operator+** still remains unchanged. This action hampers the readability of the program badly. Anybody who views the statement P3 = P1 + P2 would get an impression that this is an addition at first glance, but what actually happens is multiplication! Hence, it is strongly recommended not to change the semantics of an operator when overloading it. The point we have just discussed is illustrated in Figure 13.3.

![](img/57c0d966bb33c67a5a188e6bf39e4e02_717_0.png)

- **STEP1** Operator+ can be used with objects of Point because we have overloaded operator+ using an operator function

  ```
  class Point
  {
      .........
      .........
      <returnType> operator+(<arguments>)
      {
          /*operator function internally performs multiplication*/
      }
  };
  ```

  Operator symbol + is overloaded

  ```
  P3 = P1 + P2;
  ```

- **STEP2** Operator function changes the meaning of + for the objects of class Point
- **STEP3** The statement performs multiplication of Point objects instead of performing addition. This is because the semantics of the operator+ are changed by the operator function

**Figure 13.3:** Operator function changing the semantics of the operator+

Also, other grammatical rules such as associativity and priority of the operator remain unchanged when an operator is overloaded. This means that C++ always follows the priority and rules of the operator that is actually overloaded, and it is irrespective of the new semantics defined by the programmer. Hence, even if the programmer has changed
