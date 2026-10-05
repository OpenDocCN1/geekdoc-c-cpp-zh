# Operator Overloading, Type Conversion, New Style Casts, and RTTI 225

```
/*Beginning of A.cpp*/
#include"A.h"
A::A(int p)
{
    x = p;
nA::operator - ()
{
    return A(-x);
}
/*End of A.cpp*/
```

The operator can be overloaded by a friend function also (as shown in Listing 8.16).

Listing 8.16 Overloading the unary minus operator through a friend function

```
/*Beginning of A.h*/
class A
{
    int x;
    A(int = 0);
    public:
        friend A operator - (const A&);
};
/*End of A.h*/
```

```
/*Beginning of A.cpp*/
#include"A.h"
A::A(int p)
{
    x = p;
nA operator - (const A& Aobjj)
{
    return A(-Aobjj.x);
}
/*End of A.cpp*/
```

Overloading the unary plus operator is left as an exercise for the reader.

# 8.2.3 Overloading Arithmetic Operators

Arithmetic operators are binary operators. Therefore, the syntax for overloading them through member functions is illustrated in Listing 8.17.

Listing 8.17 Syntax for overloading the arithmetic operators through member functions

```
class <class_name>
{
    public:
        //prototype
        <return_type> operator<arith_op_symbol>(<param_list>);
};
//definition
<return_type> <class_name>::operator<arith_op_symbol>(<param_list>
```

* Note