from the binary file (use the `float` type) and stores them in a dynamically allocated memory. Then, the program should read a number and display the grades greater than that number.

```
#include <stdio.h>
#include <stdlib.h>
int main(void)
{
    FILE *fp;
    int i, grd_num;
    float *grd_arr, grd;

    fp = fopen("test.bin", "rb");
    if(fp == NULL)
    {
        printf("Error: fopen() failed\n");
        exit(EXIT_FAILURE);
    }
    if(fread(&grd_num, sizeof(int), 1, fp) != 1)
    {
        fclose(fp);
        printf("Error: fread() failed\n");
        exit(EXIT_FAILURE);
    }
    grd_arr = (float*) malloc(grd_num * sizeof(float)); /* Allocate memory to store the grades. */
    if(grd_arr == NULL)
    {
        fclose(fp);
        printf("Error: Not available memory\n");
        exit(EXIT_FAILURE);
    }
    /* Read all grades and check if they are read successfully. */
    if(fread(grd_arr, sizeof(float), grd_num, fp) == grd_num)
    {
        printf("Enter grade: ");
        scanf("%f", &grd);
        for(i = 0; i < grd_num; i++)
            if(grd_arr[i] > grd)
                printf("%f\n", grd_arr[i]);
    }
    else
        printf("Error: fread() failed to read grades\n");

    free(grd_arr);
    fclose(fp);
    return 0;
}
```

C.15.17 A common method that antivirus software uses to identify viruses is signature-based detection. The signature is a sequence of bytes (e.g., F3 BA 20 63 7A 1B) that identify a particular virus. When a file is scanned, the antivirus software searches the