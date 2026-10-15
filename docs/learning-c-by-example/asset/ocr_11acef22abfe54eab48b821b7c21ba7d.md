We also can declare a function on below of main() function but we must declare our function name.

Add this code on **funcdemo.c** file.

```
```c
#include <stdio.h>

// implicit declaration for functions
void boo();

int main(int argc, const char* argv[]) {

    boo();
    return 0;
}

void boo(){
    printf("boo() was called\\n");
}
```
```

If we compile and run this code, we will get a response, shown in Figure below.

![](bbox=[0.125, 0.455, 0.822, 0.63])