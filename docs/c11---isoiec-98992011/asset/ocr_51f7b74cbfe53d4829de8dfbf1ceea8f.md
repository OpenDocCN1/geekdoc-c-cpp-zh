ISO/IEC 9899:2011 (E)

© ISO/IEC 2011 – All rights reserved

# 7.13 Nonlocal jumps <jmp.h> the macro setjmp, and declares one function and

+   1 The header <jmp.h> defines the macro setjmp, and declares one function and one type, by bypassing the normal function call and return discipline.²247

+   2 The type declared is

jmp_buf which is an array type suitable for holding the information needed to restore a calling environment. The environment of a call to the setjmp macro contains information sufficient for a call to the longjmp function to return execution to the correct block and invocation of that block, if called recursively. It does not include the state of the floating-point status flags, of open files, or of any other component of the abstract machine.

+   3 It is unspecified whether setjmp is a macro or an identifier declared with external linkage. If a macro definition is suppressed in order to access an actual function, or a program defines an external identifier with the name setjmp, the behavior is undefined.

# 7.13.1 Save calling environment

# 7.13.1.1 The setjmp macro

Synopsis

```
#include <jmp.h>
int setjmp(jmp_buf env);
```

Description

+   2 The setjmp saves its calling environment in its jmp_buf argument for later use by the longjmp function.

Returns

+   3 If the return is from a direct invocation, the setjmp macro returns the value zero. If the return is from a call to the longjmp function, the setjmp macro returns a nonzero value.

Environmental limits

+   4 An invocation of the setjmp macro shall appear only in one of the following contexts:

+   — the entire controlling expression of a selection or iteration statement;

+   — one operand of a relational or equality operator with the other operand an integer constant, with the resulting expression being the entire controlling

247 These functions are useful for dealing with unusual conditions encountered in a low-level function of a program.