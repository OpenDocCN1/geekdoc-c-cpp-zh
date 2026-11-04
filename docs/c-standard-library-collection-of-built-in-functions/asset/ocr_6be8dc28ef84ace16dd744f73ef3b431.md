|  |  |
| --- | --- |
|  | the va_start macro to return. If va_end is not called before returning from the function, the result is undefined. |

# ## void va_start(va_list ap, last_arg)

# ### Description

The C library macro **void va_start(va_list ap, last_arg)** initializes **ap** variable to be used with the **va_arg** and **va_end** macros. The **last_arg** is the last known fixed argument being passed to the function i.e. the argument before the ellipsis.

This macro must be called before using **va_arg** and **va_end**.

# ### Declaration

Following is the declaration for va_start() macro.

```
    void va_start(va_list ap, last_arg);
```

# ### Parameters

+   - **ap** -- This is the object of **va_list** and it will hold the information needed to retrieve the additional arguments with **va_arg**.
+   - **last_arg** -- This is the last known fixed argument being passed to the function.

# ### Return Value

NA

# ### Example

The following example shows the usage of va_start() macro.

```
    #include<stdarg.h>
    #include<stdio.h>

    int sum(int, ...);

    int main(void)
    {
        printf("Sum of 10, 20 and 30 = %d\n", sum(3, 10, 20, 30) );
        printf("Sum of 4, 20, 25 and 30 = %d\n", sum(4, 4, 20, 25, 30) );

        return 0;
    }
```