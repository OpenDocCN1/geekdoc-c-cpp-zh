```
void funcinput(int numstr, char *strptr[] )
{
    int const STRLENGTH = 80;
    int i;
    char dirname[STRLENGTH];

    FILE *inptr;

    inptr = fopen("sortin.dat", "r");

    for(i = 0; i < numstr; i++) {
        fgets(dirname, STRLENGTH, inptr);
        strptr[i] = (char *)malloc(strlen(dirname) + 1);
        strcpy(strptr[i], dirname);
        printf("%s\n", dirname);
    }
    fclose(inptr);

    return;
}
```

```
void funcsort(int numstr, char *strptr[] )
n{
    int i, j;
    char *temp;

    for(i = 0; i < numstr - 1; i++) {
        for(j = i + 1; j < numstr; j++) {
            if(strcmp(strptr[i], strptr[j]) > 0)
```