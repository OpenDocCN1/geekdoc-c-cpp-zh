
where e1, e2.... are enumerators which take integer values. E is a data type and can be used to declare variables of its type.

- It is a specifier to a constructor. A constructor declared as explicit cannot perform implicit conversion.

- It is used to instantiate non-inline template classes and functions from separate files.

- extern is a storage class specifier which informs the compiler that the variable so declared is defined in another source file.

- It is a Boolean type constant. It can be assigned to only a bool type variable. The default numeric value of false is 0.

- It is a fundamental data type and is used to declare a variable to store a single-precision value.

- for is a control statement and is used to create a loop of iterative operations. It takes the form:

```
for(e1; e2; e3) statement;
```

- The statement is executed until the expression e2 becomes zero. The expression e1 is evaluated once in the beginning and e3 is evaluated at the end of every iteration.

- friend declares a function as a friend of the class where it is declared. A function can be declared as a friend to more than one class. A friend function, although defined like a normal function, can have access to all the members of a class to which it is declared as friend.

- goto is a transfer statement that enables us to skip a group of statements unconditionally. This statement is very rarely used.

## if

if is a control statement that is used to test an expression and transfer the control to a particular statement depending upon the value of expression. if statement may take one of the following forms:

```c
(i) if (expression)
        statement-1;
        statement-2;
(ii) if (expression)
        statement-1;
    else
        statement-2;
```

In form (i), if the expression is nonzero (true), statement-1 is executed and then statement-2 is executed. If the expression is zero (false), statement-1 is skipped. In form (ii), if the expression is nonzero, statement-1 is executed and statement-2 will be skipped; if it is zero, statement-2 is executed and statement-1 is skipped.

## inline

inline is a function specifier which specifies to the compiler that the function definition should be substituted in all places where the function is called.

## int

It is one of the basic data types and is used to declare a variable that would be assigned integer values.

## long

long is a data type modifier that can be applied to some of the basic data types to increase their size. When used alone as shown below, the variable becomes signed

```c
long int;
long m;
```

(variable) should be accessible as quickly as possible. Normally, a CPU register is used to store such variables.

## reinterpret_cast

It is a casting operator and is used to change one type into a fundamentally different type.

## return

It is used to mark the end of a function execution and to transfer the control back to the calling function. It can also return a value of an expression to the calling function. Example:

```
return(expression);
```

## short

Similar to long, it is also a data type modifier applied to integer base types. When used alone with a variable, it means the variable is signed short int.

## signed

It is a qualifier used with character and integer base type variables to indicate that the variables are stored with the sign. The high-order bit is used to store the sign bit, 0 meaning positive, 1 meaning negative. A signed char can take values between −127 to +127 whereas an unsigned char can hold values from 0 to 255. The default integer declaration assumes a signed number.

## sizeof

sizeof is an operator used to obtain the size of a type or an object, in bytes. Example:

```
int m = sizeof(char);
int m = sizeof(x);
```

where x is an object or variable.

## static

static is a storage class specifier. This can be used on both the local and global variables, but with a different meaning. When it is applied to a local variable, permanent storage is created and it retains its value between function calls in the compiler to try a particular function.

| Term | Description |
| --- | --- |
| **typedef** | typedef is used to give a new name to an existing data type. It is usually used to write complex declarations easily. |
| **typeid** | It is an operator that can be used to obtain the types of unknown objects. |
| **typename** | It is used to specify the type of template parameters. |
| **union** | It is similar to **struct** in declaration but is used to allocate storage for several data items at the same location. |
| **using** | It is a **namespace** scope directive and is used to declare the accessibility of identifiers declared within a **namespace** scope. |
| **unsigned** | It is a type modifier used with integer data types to tell the compiler that the variables store non-negative values only. This means that the high-bit is also used to store the value and therefore, the size of the number may be twice that of a signed number. |
| **virtual** | **virtual** is a qualifier used to declare a member function of a base class as “virtual” in order to perform dynamic binding of the function. It is also used to declare a base class as virtual when it is inherited by a class through multiple paths. This ensures that only one copy of the base class members are inherited. |
| **void** | **void** is a data type and is used to indicate the objects of unknown type. Example: `void *ptr;` is a generic pointer that can be assigned a pointer of any type. It is also used to declare a function that returns nothing. Another use is to |

The Table F.1 below lists all the operators supported by ANSI C++ according to their precedence (i.e., order of evaluation). Operators listed first have higher precedence than those listed next. Operators at the same level of precedence (between horizontal lines) evaluate either left to right or right to left according to their associativity.

**Table F.1 C++ Operators**

| Operator | Meaning | Associativity | Use |
| --- | --- | --- | --- |
| `::` | global scope | right to left | `::name` |
| `::` | class, namespace scope | left to right | `name::member` |
| `.` | direct member | left to right | `object.member` |
| `->` | indirect member |  | `pointer->member` |
| `[]` | subscript |  | `pointer[expr]` |
| `()` | function call |  | `expr(arg)` |
| `()` | Type construction |  | `type (expr)` |
| `++` | postfix increment |  | `m++` |
| `--` | postfix decrement |  | `m--` |
| `sizeof` | size of object | right to left | `sizeof expr` |
| `sizeof` | size of type |  | `sizeof (type)` |
| `++` | prefix increment |  | `++m` |
| `--` | prefix decrement |  | `--m` |
| `typeid` | type identification |  | `typeid(expr)` |
| `const_cast` | specialized cast |  | `const_cast<expr>` |
| `dynamic_cast` | specialized cast |  | `dynamic_cast<expr>` |
| `reinterpret_cast` | specialized cast |  | `reinterpret_cast<expr>` |
| `static_cast` | specialized cast |  | `static_cast<expr>` |
| `()` | traditional cast |  | `(type)expr` |
| `~` | one’s complement |  | `~expr` |
| `!` | logical NOT |  | `! expr` |
| `-` | unary minus |  | `- expr` |
| `+` | unary plus |  | `+ expr` |
| `&` | address of |  | `& value` |
| `*` | dereference |  | `* expr` |
| `new` | create object |  | `new type` |
| `new []` | create array |  | `new type []` |
| `delete` | destroy object |  | `delete ptr` |
| `delete []` | destroy array |  | `delete [] ptr` |
| `.*` | member dereference |  | `object.*ptr_to_member` |
| `->*` | indirect member dereference |  | `ptr->*ptr_to_member` |
| `*` | Multiply | left to right | `expr1 * expr2` |
| `/` | Divide |  | `expr1 / expr2` |
| `%` | Modulus |  | `expr1 % expr2` |
| `+` | add | left to right | `expr1 + expr2` |
| `-` | subtract |  | `expr1 - expr2` |
| `<<` | left shift | left to right | `expr1 << expr2` |
| `>>` | right shift |  | `expr1 >> expr2` |
| `<` | less than | left to right | `expr1 < expr2` |
| `<=` | less than or equal to |  | `expr1 <= expr2` |
| `>` | greater than |  | `expr1 > expr2` |
| `>=` | greater than or equal to |  | `expr1 >= expr2` |
| `==` | equal | left to right | `expr1 == expr2` |
| `!=` | not equal |  | `expr1 != expr2` |
| `&` | bitwise AND | left to right | `expr1 & expr2` |
| `^` | bitwise XOR | left to right | `expr1 ^ expr2` |
| \| | bitwise OR | left to right | expr1 \| expr2 |
| `&&` | logical AND | left to right | `expr1 && expr2` |
| \|\| | logical OR | left to right | expr1 \|\| expr2 |
| `?:` | conditional expression | left to right | `expr1 ? expr2: expr3` |
| `=` | assignment | right to left | `x = expr` |
| `*=` | multiply update |  | `x *= expr` |
| `/=` | divide update |  | `x /= expr` |
| `%=` | modulus update |  | `x %= expr` |
| `+=` | add update |  | `x += expr` |
| `-=` | subtract update |  | `x -= expr` |
| `<<=` | left shift update |  | `x <<= expr` |
