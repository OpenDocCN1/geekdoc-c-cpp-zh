The feholdexcept function returns zero if and only if non-stop floating-point exception handling was successfully installed.

# 7.6.4.3 The fesetenv function

Synopsis

```
#include <fenv.h>
int fesetenv(const fenv_t *envp);
```

Description

The fesetenv function attempts to establish the floating-point environment represented by the object pointed to by envp. The argument envp shall point to an object set by a call to fegetenv or feholdexcept, or equal to a floating-point environment macro. Note that fesetenv merely installs the state of the floating-point status flags represented through its argument, and does not raise these floating-point exceptions.

Returns

The fesetenv function returns zero if the environment was successfully established. Otherwise, it returns a nonnonzero value.

# 7.6.4.4 The feupdateenv function

Synopsis

```
#include <fenv.h>
int feupdateenv(const fenv_t *envp);
```

Description

The feupdateenv function attempts to save the currently raised floating-point exceptions in its automatic storage, install the floating-point environment represented by the object pointed to by envp, and then raise the saved floating-point exceptions. The argument envp shall point to an object set by a call to feholdexcept or fegetenv, or equal to a floating-point environment macro.

Returns

The feupdateenv function returns zero if all the actions were successfully carried out. Otherwise, it returns a nonzero value.