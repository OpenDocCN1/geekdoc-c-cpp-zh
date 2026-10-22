is equivalent into #define FOO 1020.

# 3. #undef

To undefine a macro means to cancel its definition. This is done with the #undef directive.

# Syntax:

#undef token

# define and undefine example

```
```c
#include <stdio.h>
#define PI 3.1415
#undef PI
main(){
printf("%f",PI);
}
```
```

# Output:

Compile Time Error: 'PI' undeclared

# 4. #ifdef

The #ifdef preprocessor directive checks if macro is defined by #define. If yes, it executes the code.

# Syntax:

```
```c
#ifdef MACRO
//code
#endif
```
```

# 5. #ifndef

The #ifndef preprocessor directive checks if macro is not defined by #define. If yes, it executes the code.

# Syntax: