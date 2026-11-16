Once again, we can write our own code to perform a string concatenation:

```
// strcat1.c
void strcat(char s1[], char s2[]) {
    int i = 0, j = 0;
    while (s1[i] != '\0') {
        ++i;
    }
    while (s2[j] != '\0') {
        s1[i] = s2[j];
        ++i;
        ++j;
    }
    s1[i] = '\0';
}
```

We can simplify the code:

```
// strcat2.c
void strcat(char s1[], char s2[]) {
    int i = 0, j = 0;
    while (s1[i]) {
        ++i;
    }
    while (s2[j]) {
        s1[i++] = s2[j++];
    }
    s1[i] = '\0';
}
```