
and at line 6, fun2 has definition fun4. Finally, fun1 and fun2 has definition fun4. After macro substitution, the line 10 become: int fun4 = 1, fun4 = 2, fun3 = 3, fun4 = 4; Multiple definition of variable fun4 is available, hence compiler throws an error.

## 25. c

Explanation: Not required.

## 26. a

Explanation: Not required.

## 27. b

Explanation: The given program, at preprocessing phase after the substitution of macro abc is written as follows:

```
#include<stdio.h>
int main()
{
    int main = 10;
    printf("the value of abc: %d", main);
    return 0;
}
```

The local variable can have the name main. Function printf() returns value 10.

## 28. b

Explanation: The given program after macro substitution :

```
#include<stdio.h>
int main()
{
    (int a ; a = 10);
    printf("%d", a);
    return 0;
}
```

Here, we are giving the definition of 'a' inside parenthesis that is not allowed. Hence, the compiler throws an error.

## 29. b

Explanation: In the given program, we are using '#' as macro definition, as we discussed, the ‘#’ converts element of macro to string. At line 3, fun(i) gets substituted with printf("var is %s,",i"); The printf will print "var is i".

- 30. c
Explanation: Not required. Hint: After macro substitution, two definitions of function max are present.

- 31. c
Explanation: After macro substitution, line 2 become: int y = x+2*x+2; -> y = 2+2*2*2; -> y = 8.

- 32. Nil
Explanation: The (i) "include" directive searches the stdio.h header file in the standard binary of gcc compiler and the (ii) "include" directive searches stdio.h header file in the local directory then searches in the standard bin directory.

Explanation: Discussed in explanation of question 18. Hint: typedef is not visible in fun().

- 34. d
Explanation: In the given program will not give any error. The following facts about enum should be known : (i) enum can be local or/and global. (ii) If any element of enum is not initialized, it takes value 0 if it is the first element or the value one than its previous element. (iii) Element of enum can have a negative value. The enum for a given program is enum block(one = 0, two = 5 , three = 6 , four = 10, five = 11); The printf() function prints 0 6 11.

- 35. d
Explanation: The printf() in main() function takes the enum elements from local enum block.

- 36. d
Explanation: The enum element must be of type integer only, floating-point numbers are not allowed as the value of enum element.

- 37. d

Explanation: Once enum elements get initialized we cannot change their value. In line 3, we are trying to change the value of element two, compiler throws an error: l-value required as increment operand.

- 38. d

Explanation: We cannot pass an enum to the function as its argument, we can only pass its element.

- 39. d

Explanation: In the given program, till printf() all statements are valid. If the condition gets true at line 2, the value of enum variable 'a' of type "block" becomes equal to the value of enum "block" element "first" that is 1. Now in printf() statement we are comparing an integer value 1 with a string "first" by strcmp(). Hence, the error comes at runtime.

- 40. d

Explanation: Two enums cannot have the same name of the variable in the same scope. In the given program, enum block1 and enum block2 have the same scope, and both have element "two" is not allowed.

- 41. c

Explanation: Not required. Hint: The enum element must be of type int, in the given code we are initializing elements one and two with string.

- 42. a

Explanation: The given program does not report any error, here we are initializing block elements with character literals. C, implicitly type casting from character to integer is provided, and an element one gets value 97 (ASCII value of char 'a') and element two gets value 98 (ASCII value of 'b'). Hence, the printf() statement prints the character value of element one, an integer value of element two gets printed.

- 43. d

Explanation: Not required.

- 44. d
Answer: d

**Explanation:** We cannot have an enum element with name as data type (e.g. int is here).

- 45. d
**Explanation:** Not required.

- 46. d

**Explanation:** In (i) and (ii) const is present before '*p', the string pointed by p becomes constant, and (iii) const is suffixed after '*' and before 'p', here, 'p' is not constant whereas 'p' is constant. Hence, (i) and (ii) are equivalent but (iii) is not equivalent to either (i) or (ii).

- 47. a

**Explanation:** A constant variable can be initialized by the return value of the function.

- 48. d

**Explanation:** We can have an enum element with name as data type (e.g. int is here). In the given code, we are initializing the element of an enum with a value returned by a function that is not allowed.

- 49. c

**Explanation:** In the given program, at line 1, we are trying to assign an enum element to the enum block that is not allowed. We can assign an enum element to a variable of enum, not with enum itself. This concept is also true for struct variables. If we do as: enum block = two; then it is allowed.

- 50. a

**Explanation:** The enum element represents an integer value. In line 1

- 51. c

Explanation: We can't have two enum elements, of different enum, with the same name, same variables in the scope.

- 52. c
Explanation: Not required. Hint: The enum element one initialized with value 3 and two with value 4.

- 53. d
Explanation: The enum is another way of defining integer variable if we define as const a = 10; it is exactly equivalent to enum {a = 10}; In the given program, we are providing two definitions of variable sun, one definition at line 2 and one definition at line 3. We cannot have multiple definitions of a variable in the same scope. Hence, the compiler throws an error.

- 54. d
Explanation: Not required, another version of question 53.

- 55. d
Explanation: In a given program, we are creating an enum block type variable 'a' that can hold a value of type enum element, enum elements are of type integer that is why variable 'a' is also of type integer. The sizeof() operator returns the size of an integer data type that is 4.

- 56. d
Explanation: Union is a user-defined data type. In the given program, we are defining a union unit, the unit has fields (i) variable marks of type integer (ii) variable roll of type integer but we are providing the value of marks in the definition that is not allowed, we cannot provide value to union field without creating an instance of it. The same thing is also true for struct user-defined data types. Hence, the compiler throws an error.

- 57. c
Explanation: This program is showing how union elements can get accessed from other functions. We can access the union element using the dot(.) operator.

- 58. c

Explanation: The union has a property that it does not allocate memory for all elements, it allocates memory equal to the size of the largest element. Here, the largest element is 'c' of data type double. The memory allocated for the union is equal to the size of the double, that is 8B. Hence, sizeof(obj) returns 8.

- 59. d

Explanation: As we discussed earlier, the union does not get allocated memory for all of elements, it gets memory that can accommodate the biggest element. For the given program, the union unit will get memory of 4 bytes, any modification done by any the elements will be reflected on these 4 bytes only. In line 1, these 4 bytes are assigned a number 100. In line 2, these 4 bytes can be printed using '%s' format specifier. It prints string "d", (ASCII value of 'd' is 100). In line 3, the string "baby" gets copied into these 4 bytes. In line 5, these 4 bytes are printed using integer format specifier (%d) and string format specifier (%s). The integer equivalent of "baby" gets printed and the string value will be 2036490594. If the program is run the "baby" integer value will be 2036490594. This value will be evaluated as follow.

```
binary of 2036490594::: '01111001 01100001 01100001 01100010'
[Little Endian: Lower bytes come at higher address, 'y' is coming at MSB, 'b' is coming at LSB ]
```

```
binary(ascii('b'))::: '01100010'
binary(ascii('a'))::: '01100001'
binary(ascii('b'))::: '01100010'
binary(ascii('a'))::: '01111101'
```

- 60. c

Explanation: As we discussed in previous groups, we are following the big-endian mode for storage for simplifying the concepts and for our convenience.
