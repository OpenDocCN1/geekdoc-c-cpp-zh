# Calling Conventions

will generate the following code if passed Left-to-Right:

```
push a
push b
call _Function
```

and will generate the following code if passed Right-to-Left:

```
push b
push a
call _Function
```

# Return value

Some functions return a value, and that value must be received reliably by the function's caller. The called function places its return value in a place where the calling function can get it when execution returns. The called function stores the return value before executing the ret instruction.

# Cleaning the stack

When arguments are pushed onto the stack, eventually they must be popped off again. Whichever the caller, or the callee, is responsible for cleaning the stack reset the stack pointer to eliminate the passed arguments.

# Calling function (the callee)

The 'parent' function that calls the subroutine. Execution resumes in the calling function directly after the subroutine call, unless the program terminates inside the subroutine.

# Called function (the callee)

The 'child' function that gets called by the 'parent.'

# Name Decoration

When C is translated to assembly code, the compiler will often 'decorate' the function name by adding extra information that the linker will use to find and link to the correct functions. For most calling conventions, the decoration is very simple (often only an extra symbol or two to denote the calling convention), but in some extreme cases (notably C++ "mangled" convention), the names are severely.

# Entry sequence (the function prologue)

a few instructions at the beginning of a function, which prepare the stack and registers for use within the function.

# Exit sequence (the function epilogue)

a few instructions at the end of a function, which restore the stack and registers to the state expected by the caller, and return to the caller. Some calling conventions clean the stack in the exit sequence.

# Call sequence