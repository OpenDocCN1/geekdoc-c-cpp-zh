# 3.2 Multidimensional Array

We can create multidimensional array, for instance two dimensional, we can use [] .

For testing, you can create a file, called **multiarray.c** and write this code.

```
```c
#include <stdio.h>

int main() {
    // define Multidimensional demarrary
    int matrix[3][5];

    // insert data
    int i,j;
    for(i=0;i<3;i++){
        for(j=0;j<5;j++){
            matrix[i][j] = i+j;
        }
    }

    // display data
    for(i=0;i<3;i++){
        for(j=0;j<5;j++){
            printf("%d ",matrix[i][j]);
        }
        printf("\n");
    }

    return 0;
}
```
```

Save this. Then, try to compile and run.

```
```bash
$ gcc -o multiarray multiarray.c
$ ./multiarray
```
```

A sample output can be seen in Figure below.