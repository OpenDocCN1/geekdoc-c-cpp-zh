```
void debug_msg(char * str, const unsigned int error_level)
{
 if (error_level <= GLOBAL_ERROR_LEVEL)
 {
 if (error_level == 0)
 printf("\n**************%s", str, "**************\n");
 else
 printf("\n%s", str);

 fflush(stdout);

 if (error_level == 0)
 exit(0);
 }
}

#define DEBUG_MSG(x, level) debug_msg(x, level)
#else
#define DEBUG_MSG(x, level)
#endif
#endif
```

In this example, we've created five levels of debug messages. Where the debug version of the software is not used, these messages are stripped from the executable in a way that does not cause compilation errors.

```
#define DEBUG
#include "debug_msg.h"
unsigned int GLOBAL_ERROR_LEVEL = DEBUG_ERR_LVL_WARNING;

int main(int argc, char *argv[])
{
 DEBUG_MSG("Error from level four", DEBUG_ERR_LVL_INFO);
 DEBUG_MSG("Error from level three", DEBUG_ERR_LVL_WARNING);
 DEBUG_MSG("Error from level two", DEBUG_ERR_LVL_PROBLEM);
 DEBUG_MSG("Error from level one", DEBUG_ERR_LVL_SERIOUS);
 DEBUG_MSG("Error from level zero", DEBUG_ERR_LVL_CRITICAL);

 return 0;
}
```

To call the function, you simply place the macro into the code as shown in the previous example. This will work fine in host code, but will not work on device code without some minor modifications.

First, you have to be aware of some issues when printing a message within a kernel. Kernel level printf is only supported for compute 2.x capability. If you try to use printf in a kernel that is being compiled for compute 1.x devices, you will get an error saying you cannot call printf from a global or