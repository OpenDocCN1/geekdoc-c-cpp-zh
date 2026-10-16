
In unsafe contexts, expressions can result in point types but, if that happened outside of the unsafe context, you would get an error at compile time. So, if any of the following results in a pointer type outside an unsafe context, you would get the error:

- `simple_name`
- `member_access`
- `invocation_expression`
- `element_access`

The `primary_no_array_creation_expression` and `unary_expression` will allow these constructs in an unsafe context:

```
primary_no_array_creation_expression_unsafe
    : pointer_member_access
    | pointer_element_access
    | sizeof_expression
    ;
```

```
unary_expression_unsafe
    : pointer_indirection_expression
    | addressof_expression
    ;
```

We’ll discuss these constructs now; associativity and precedence of unsafe operators are implied in the grammar.

## Pointer Indirection

This expression is an asterisk (*) and a unary_expression:

```
pointer_indirection_expression
    : '*' unary_expression
    ;
```

The unary * operator is indicating pointer indirection and it is used to obtain variables that the pointer is pointing to. Where P is a pointer type T* expression, the result of the evaluation of P will be a type T variable. If you tried to apply the * unary operator to a void* type expression, or to a non-pointer expression, you would get an error at compile time.

When you apply the * unary operator to null pointers, the effect is implementation-defined and there is no guarantee that you won’t get a System.NullReferenceException thrown.

If you assign an invalid value to the pointer, the * unary operator will have undefined behavior. Two examples of invalid values using the * operator to dereference a pointer are a variable address that is no longer in use and an address that has not been properly aligned for the type being pointed to.

If you evaluate an expression of *P and the result is a variable, it is considered to be initially assigned.

## Pointer Member Access

This expression is a primary_expression, a “- >” token, an identifier and a type_argument_list which is optional.

```
pointer_member_access
```

```
: primary_expression '- >' identifier ;
```

In a P - >I, pointer member access, P has to be an expression of any pointer type other than void* and it has to denote a member that is accessible of the type that P is pointing to.

These pointer members evaluate a (*P).I.

An example:

```
using System;
```

```
struct Point
```

```
{
    public int x;
    public int y;

    public override string ToString() {
        return "(" + x + "," + y + ")";
    }
}

class Test
{
    static void Main() {
        Point point;
        unsafe {
            Point* p = &point;
            p->x = 10;
            p->y = 20;
            Console.WriteLine(p->ToString());
        }
    }
}
```

In this, we use the -> operator for accessing fields and to invoke struct methods though pointers. Because P->I is the exact equivalent of (*P).I, we could have written the Main method like this:

```
class Test
{
```

```
static void Main() {
    Point point;
    unsafe {
        Point* p = &point;
        (*p).x = 10;
        (*p).y = 20;
        Console.WriteLine((*p).ToString());
    }
}
```

## Pointer Element Access

This expression is a primary_no_array_creation_expression, and another expression inside a set of square brackets [].

pointer_element_access
: primary_no_array_creation_expression '[' expression ']'
;

In the P[E] form of a pointer element, P has to be an expression of any pointer type that isn’t a void* and E has to be an expression that can be converted implicitly to an int, uint, long or a ulong.

A pointer element of this format is evaluated exactly as *(P + E).

An example:

```
class Test
{
    static void Main() {
        unsafe {
            char* p = stackalloc char[256];
            for (int i = 0; i < 256; i++) p[i] = (char)i;
```

moveable variable, an error would occur at compile time. In the case of it denoting a moveable variable, a fixed statement could be used to fix the variable temporarily before you get the address. Outside of a static constructor or an instance constructor for a class or a struct that has a read-only field defined, the field is not considered to be a variable; it is a value and that means you cannot get the address. In the same way, you cannot get the address of a constant.

There is no need for the argument of an & operator to be definitely assigned. However, after an & operation, the variable the operator is applied on is definitely assigned within the execution path that the operation happens in. It is down to the programmer to make sure that the variable is correctly initialized.

An example:

```
```csharp
using System;

class Test
{
	static void Main() {
		int i;
		unsafe {
			int* p = &i;
			*p = 123;
		}
		Console.WriteLine(i);
	}
}
```
```

In this i is definitely assigned after the &i operation that initialized p. The assignment inside *p will initialize i but it is down to the programmer to ensure that this initialization is included and that, if

the assignment was taken out, that there wouldn’t be a compile time error.

The rules for definitive assignment of the & operator ensure that you can avoid local variables being redundantly initialized. For example, some internal APIs will take a pointer that points to a structure that the API fills in. Calls to APIs like this generally pass a local struct variable address and, if that rule didn’t exist, there would be a requirement for the struct variable to be redundantly initialized.

## Pointer Increment and Decrement

In unsafe contexts, you can apply the ++ operator and the -- operators to pointer variables of any type except for void*. As such, for every T* type pointer, these are the implicitly defined operators:

- T* operator ++(T* x);
- T* operator --(T* x);

The first operator produces the result of x + 1 and the second produces a result of x − 1. So, for a type T* pointer variable, the ++ operator will add sizeof(T) to the address the variable contains and the -- operator will do the opposite – subtract sizeof(T) from the address the variable contains.

If an increment or a decrement of a point overflows the pointer type domain, the result will be implementation-defined but there will not be any exceptions thrown.

## Pointer Arithmetic

In unsafe contexts, you can apply the − operator and the + operator to all pointer type values with the exception of those from a void* type. So, for every T* type pointer, these are the implicitly defined operators:

```
T* operator +(T* x, int y);
T* operator +(T* x, uint y);
T* operator +(T* x, long y);
T* operator +(T* x, ulong y);
```

```
T* operator +(int x, T* y);
T* operator +(uint x, T* y);
T* operator +(long x, T* y);
T* operator +(ulong x, T* y);
```

```
T* operator -(T* x, int y);
T* operator -(T* x, uint y);
T* operator -(T* x, long y);
T* operator -(T* x, ulong y);
```

```
long operator -(T* x, T* y);
```

Assuming that you have an expression called P and it is a T* pointer type. You also have an expression of N, which is of type uint, int, long, or ulong type. The expression of P + N and the expression of N + P will both compute the type T* pointer value that comes from adding N* sizeof(T) to the address provided by P. In the same way, the expression of P − N will compute the type T* pointer value that comes from subtracting N* sizeof(T) from the address provide by P.

Assuming that you have an expression of P and an expression of Q, both of T* pointer type, the expression of P − Q will give us the difference between the addresses that P and Q both give and then the difference is divided by sizeof(T). The result type will always be a long. Effectively P -Q will be computed as ((long)(P) − (long)(Q)) / sizeof(T).

An example:

```
using System;
```

```
class Test
```

```
```csharp
{
	static void Main() {
		unsafe {
			int* values = stackalloc int[20];
			int* p = &values[1];
			int* q = &values[15];
			Console.WriteLine("p - q = {0}", p - q);
			Console.WriteLine("q - p = {0}", q - p);
		}
	}
}
```
```

p - q = -14
q - p = 14

If an operation of pointer arithmetic overflows the pointer type domain, the result will always be truncated in a similar fashion to implementation-defined but there will be no exceptions thrown.

## Pointer Comparison

- bool operator ==(void* x, void* y);
- bool operator !=(void* x, void* y);
- bool operator <(void* x, void* y);
- bool operator >(void* x, void* y);
- bool operator <=(void* x, void* y);
- bool operator >=(void* x, void* y);
