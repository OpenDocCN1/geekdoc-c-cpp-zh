![](bbox=[0.05, 0.12, 0.65, 0.32])

# Fig. 1.15 Polymorphism arising from operand types

```
12 + 25                  (Result is 37)
12.0876 + 25.98          (Result is 38.0676)
'Indian' + 'Cricketer'   (Result is 'IndianCricketer')
```

The + operator in these three cases behaves differently. In the first case, it adds two integers; in the second case, it adds two double values; and in the third case, it concatenates two different strings into one. The string is available in C++ as a data type. + is overloaded in the string class. So, the given operation makes sense. When the operator behaves differently for different types of operands, it is also a type of ad-hoc polymorphism. In C++ parlance, this is called operator overloading. We will discuss operator overloading in Chapter 6.

In C++, both function and operator overloading are resolved at compile time. The compiler, while compiling the program, decides the operation to be performed and generates the object code that describes that operation. In the given example, when 12 + 25 is seen in the source code, the compiler provides the code that adds two integer values and adds that to the object code being generated and when 'Indian' + 'Cricketer' is seen, it adds the string concatenation routine at that place.

Similarly, when the specific Add function is called, for example, Add(20,30), the compiler changes that call to a jump instruction, which jumps to the function body that contains integer addition. Similarly, when Add('Indian','Cricketer') is called, the jump instruction will point to another function that contains the code to concatenate strings. Moreover, when we write Result = Add(FirstVal, SecondVal), the jump instruction points to the function body that adds two integers and returns the answer. When the call is to Add(FirstVal, SecondVal, ThirdVal), the jump instruction points to the function body that does not return anything but where the ThirdVal contains the summation. Thus, the decision about which function to call is done at the compile time. So, ad-hoc polymorphism is also compile time polymorphism in C++.

> When an operator behaves differently for different types of operands, it is known as operator overloading. Java has no such features.

Note It is not necessary that ad-hoc polymorphism must take place at compile time. If the language (Smalltalk is an example) resolves the function call at run-time, then the ad-hoc polymorphism happens at run-time. Such languages are sometimes denoted as late-binding languages.

# 1.8.2 Dynamic Polymorphism at Run-time

This is a case when the resolution of the function happens at run-time. The restriction here is to choose the function only from the hierarchy of classes and not from elsewhere. Let us consider the example shown in Fig. 1.16 to understand this concept.

guments as all these different functions have a different body. Hence, this is an example of polymorphism.
One more type of ad-hoc polymorphism is observed when the operators behave differently with different operands. This can be understood better using Fig. 1.15.