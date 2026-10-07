
## 7.12.14 Comparison macros

The relational and equality operators support the usual mathematical relationships between numeric values. For any ordered pair of numeric values exactly one of the relationships — less, greater, and equal — is true. Relational operators may raise the “invalid” floating-point exception when argument values are NaNs. For a NaN and numeric value, or for two NaNs, the unordered relationship is true.²⁴⁴ The following subclauses provide macros that are quiet (non floating-point exception raising) versions of the relational operators, and other macros facilitate efficient code without suffering the “invalid” floating-point exception. The synopses in this subclause, real-floating indicates that the argument should be an expression of real floating type²⁴⁵ (both arguments need not have the same type).²⁴⁶

### 7.12.14.1 The isgreater macro

#### Synopsis

```c
#include <math.h>
int isgreater(real-floating x, real-floating y);
```

#### Description

The isgreater macro determines whether its first argument is greater than its second argument. The value of isgreater(x, y) is always equal to (x > y); however, unlike (x) > (y), isgreater(x, y) does not raise the “invalid” floating-point exception when x and y are unordered.

#### Returns

The isgreater macro returns the value of (x) > (y).

### 7.12.14.2 The isgreaterqual macro

#### Synopsis

```c
#include <math.h>
int isgreaterqual(real-floating x, real-floating y);
```

> 244) IEC 60559 requires the built-in relational operators raise the “invalid” floating-point exception if the operands compare unordered, as an error indicator for programs written without consideration of NaNs; the result in these cases is false.

> 245) If any argument is of integer type, or any other type that is not a real floating type, the behavior is undefined.

> 246) Whether an argument represented in a format wider than its semantic type is converted to the semantic is unspecified.

# ISO/IEC 9899:2011 (E)

#### Description

The **isgreaterequal** macro determines whether its first argument is greater than equal to its second. The value of **isgreaterequal(x, y)** is always equal to **(x) >= (y)**; however, unlike **(x) >= (y)**, **isgreaterequal(x, y)** does not raise the “invalid” floating-point exception when **x** and **y** are unordered.

#### Returns

The **isgreaterequal** macro returns the value of **(x) >= (y).**

### 7.12.14.3 The isless macro

#### Synopsis

```c
#include <math.h>
int isless(real-floating x, real-floating y);
```

#### Description

The **isless** macro determines whether its first argument is less than its second argument. The value of **isless(x, y)** is always equal to **(x) < (y)**; however, unlike (x) < (y), isless(x, y) does not raise the “invalid” floating-point exception when x and y are unordered.

#### Returns

The **isless** macro returns the value of **(x) < (y).**

### 7.12.14.4 The islesqual macro

#### Synopsis

```c
#include <math.h>
int islesqual(real-floating x, real-floating y);
```

#### Description

The **islesqual** macro determines whether its first argument is less or equal to its second argument. The value of **islesqual(x, y)** is always equal to **(x) <= (y)**; however, unlike (x) <= (y), islesqual(x, y) does not raise the “invalid” floating-point exception when x and y are unordered.

#### Returns

The **islesqual** macro returns the value of **(x) <= (y).**

### 7.12.14.5 The islessgreater macro

#### Synopsis

```c
#include <math.h>
isslessgreater(real-floating x, real-floating y);
```

#### Description

The islessgreater macro determines whether its first argument is less or greater than its second argument. The islessgreater(x, y) macro is similar to (x) < (y) || (x) > (y); however, islessgreater(x, y) does not raise the “invalid” floating-point exception when x and y are unordered.

#### Returns

The islessgreater macro returns the value of the expression of (x) < (y) || (x) > (y).

### 7.12.14.6 The unordered macro

#### Synopsis

```c
#include <math.h>
int unordered(real-floating x, real-floating y);
```

#### Description

The unordered macro determines whether its arguments are unordered.

#### Returns

The unordered macro returns 1 if the arguments are unordered and 0 otherwise.

# ISO/IEC 9899:2011 (E)

#### Description

The relational and equality operators support the usual mathematical relationships between numeric values. For any ordered pair of numeric values exactly one of the relationships — less, greater, and equal — is true. Relational and de-relational operators may raise the “invalid” floating-point exception when argument values are NaNs. For a NaN and numeric value, or for two NaNs, the unordered relationship is true.²⁴⁴ The following subclauses provide macros that are quiet (non floating-point exception raising) versions of the relational operators, and other macros facilitate efficient code without suffering the “invalid” floating-point exception. The synopses in this subclause, real-floating indicates that the argument should be an expression of real floating type²⁴⁵ (both arguments need not have the same type).²⁴⁶

### 7.12.14.1 The isgreater macro

#### Synopsis

```c
#include <math.h>
int isgreater(real-floating x, real-floating y);
```

#### Description

The isgreater macro determines whether its first argument is greater than its second argument. The value of isgreater(x, y) is always equal to (x > y); however, unlike (x) > (y), isgreater(x, y) does not raise the “invalid” floating-point exception when x and y are unordered.

#### Returns

The isgreater macro returns the value of (x) > (y).

### 7.12.14.2 The isgreaterqual macro

#### Synopsis

```c
#include <math.h>
int isgreaterqual(real-floating x, real-floating y);
```

> 244) IEC 60559 requires the built-in relational operators raise the “invalid” floating-point exception if the operands compare unordered, as an error indicator for programs written without consideration of NaNs; the result in these cases is false.

> 245) If any argument is of integer type, or any other type that is not a real floating type, the behavior is undefined.

> 246) Whether an argument represented in a format wider than its semantic type is converted to the semantic is unspecified.

# ISO/IEC 9899:2011 (E)

#### Description

The **isgreaterequal** macro determines whether its first argument is greater than equal to its second. The value of **isgreaterequal(x, y)** is always equal to **(x) >= (y)**; however, unlike **(x) >= (y)**, **isgreaterequal(x, y)** does not raise the “invalid” floating-point exception when **x** and **y** are unordered.

#### Returns

The **isgreaterequal** macro returns the value of **(x) >= (y).**

### 7.12.14.3 The isless macro

#### Synopsis

```c
#include <math.h>
int isless(real-floating x, real-floating y);
```

#### Description

The **isless** macro determines whether its first argument is less than its second argument. The value of **isless(x, y)** is always equal to **(x) < (y)**; however, unlike (x) < (y), isless(x, y) does not raise the “invalid” floating-point exception when x and y are unordered.

#### Returns

The **isless** macro returns the value of **(x) < (y).**

### 7.12.14.4 The islesqual macro

#### Synopsis

```c
#include <math.h>
int islesqual(real-floating x, real-floating y);
```

#### Description

The **islesqual** macro determines whether its first argument is less or equal to its second argument. The value of **islesqual(x, y)** is always equal to **(x) <= (y)**; however, unlike (x) <= (y), islesqual(x, y) does not raise the “invalid” floating-point exception when x and y are unordered.

#### Returns

The **islesqual** macro returns the value of **(x) <= (y).**

### 7.12.14.5 The islessgreater macro

#### Synopsis

```c
#include <math.h>
isslessgreater(real-floating x, real-floating y);
```

#### Description

The islessgreater macro determines whether its first argument is less or greater than its second argument. The islessgreater(x, y) macro is similar to (x) < (y) || (x) > (y); however, islessgreater(x, y) does not raise the “invalid” floating-point exception when x and y are unordered.

#### Returns

The islessgreater macro returns the value of the expression of (x) < (y) || (x) > (y).

### 7.12.14.6 The unordered macro

#### Synopsis

```c
#include <math.h>
int unordered(real-floating x, real-floating y);
```

#### Description

The unordered macro determines whether its arguments are unordered.

#### Returns

The unordered macro returns 1 if the arguments are unordered and 0 otherwise.

# 7.13.1 Save calling environment

#### Synopsis

```c
#include <jmp.h>
int setjmp(jmp_buf env);
```

#### Description

The setjmp macro saves its environment in the jmp_buf argument for later use by the longjmp function.

#### Returns

If the return is from a direct invocation, the setjmp macro returns zero. If the return is from a call to longjmp, the setjmp macro returns a nonzero value.

# 7.13.2 Restore calling environment

#### Synopsis

```c
#include <jmp.h>
_Noreturn void longjmp(jmp_buf env, int val);
```

#### Description

The longjmp function restores the environment saved by the most recent invocation of setjmp macro in the same invocation of the program with the corresponding jmp_buf argument. If there has been no such invocation, or if the invocation from another thread of execution, or if the function containing the invocation of the setjmp macro has terminated execution in the interim, or if the invocation of the setjmp macro was within the scope of an identifier with variably modified type and execution has left that scope in the interim, the behavior is undefined.

All accessible objects have values, and all components of the abstract machine have state, as of the longjmp function was called, except that the values of automatic storage duration that are local to the function containing the invocation of the corresponding setjump macro do not have volatile-qualified type and have been changed between the setjmp invocation and longjmp call are indeterminate.

#### Returns

After longjmp is completed, thread execution continues as if the invocation of the setjump macro had just returned the value specified by val. longterm function cannot cause the setjmp macro to return the value 0; if val is 0, the setjmp macro returns the value 1.

5 EXAMPLE The longjmp function returns control back to the point of the setjmp invocation might cause memory associated with a variable length array object to be deallocated. by executing a return statement or because another longjmp has called a transfer to a setjmp invocation in a earlier function in the set of nested calls.

> 248) For, by executing a return statement or because another longjmp has called a transfer to a setjmp invocation in a earlier function in the set of nested calls.

> 249) This includes, but not limited to, the floating-point status flags and the state of open files.

7.13.2.1

Library
