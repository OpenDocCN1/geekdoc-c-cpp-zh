```
```c
// compress.c

/*
Reads an alphabetized file (one word per line) and writes a compressed
version of the file. Words in the output file are preceded by a count
of characters identical to the previous word plus an offset of 48
(ASCII '0'), and these identical characters are omitted. Multiple words
are output on each line until column MAX_COL is reached. At this point,
the current word is made the last on the line by printing '\n'.
*/

void compress(void) {
    char prev[MAX_CHAR], word[MAX_CHAR], buf[MAX_CHAR];
    char *s, *t;
    int chrccount, lineno = 0;
    FILE *fpIn, *fpOut;

    if ((fpIn = fopen("dictionary.txt", "r")) == NULL) {
        fprintf("File could not be opened for input.\n");
        exit(1);
    }

    if ((fpOut = fopen("compressedDictionary.txt", "w")) == NULL) {
        fprintf("File could not be opened for output.\n");
        exit(1);
    }

    prev[0] = '\0';
    while (fgets(word, MAX_CHAR, fpIn)) {
        if (strchr(word, '\n')) {
            word[strlen(word)-2] = '\0';
        }
        s = word;
        t = prev;
        chrccount = 0;
        while ((*t != '\0') && (*s++ == *t++)) {
            ++chrccount;
        }
        buf[0] = chrccount + '0';
        buf[1] = '\0';
        strcat(buf, word[chrccount]);
        fputs(buf, fpOut);
        lineno += 1 + strlen(word[chrccount]);
        if (lineno >= MAX_COL) {
            lineno = 0;
            fputs("\n", fpOut);
        }
        strcpy(prev, word);
    }
    fclose(fpIn);
    fclose(fpOut);
}
```
```