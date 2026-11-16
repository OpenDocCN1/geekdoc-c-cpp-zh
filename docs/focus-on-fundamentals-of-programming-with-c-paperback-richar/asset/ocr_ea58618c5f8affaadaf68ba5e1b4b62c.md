```
// expand.c

/*
Reads a compressed file created by compress() and writes a standard
ASCII file, one word per line.
*/

void expand(void) {
    char prev[MAX_CHAR], word[MAX_CHAR];
    int samechr;
    FILE *fpin, *fpOut;

    if (!((fpin = fopen("compressedDictionary.txt", "r"))) {
        printf("File could not be opened for input.\n");
        exit(1);
    }
    if (!((fpOut = fopen("newDictionary.txt", "w"))) {
        printf("File could not be opened for output.\n");
        exit(1);
    }

    prev[0] = '\0';
    while ((samechr = getWord(word, fpin)) >= 0) {
        strcpy(prev,samechr], word);
        fputs(prev, fpOut);
        fputs("\n", fpOut);
    }
    fclose(fpin);
    fclose(fpOut);
}

int getWord(char *t, FILE *fpin) {
    int c, count;
    while ((c = fgetc(fpin)) < 'a') {
        count = c - '0';
        if (c == EOF) {
            return (-1);
        }
    }
    ungetc(c, fpin);
    while ((c = fgetc(fpin)) >= 'a') {
        *t++ = c;
    }
    ungetc(c, fpin);
    *t++ = '\0';
    return(count);
}
```

Implementation of compress() on a 50,000 word dictionary containing 482,884 bytes results in a file of 185,339 bytes, resulting in a compression of 61.62%.