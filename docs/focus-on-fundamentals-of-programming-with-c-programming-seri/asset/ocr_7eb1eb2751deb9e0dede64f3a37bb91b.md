```
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
    int chrccount, linelen = 0;
    FILE *fpin, *fpout;

    fopen_s(&fpin, "dictionary.txt", "r");
    if (fpin == NULL) {
        printf("File could not be opened for input.\n");
        exit(1);
    }

    fopen_s(&fpout, "compressedDictionary.txt", "w");
    if (fpout == NULL) {
        printf("File could not be opened for output.\n");
        exit(1);
    }

    prev[0] = '\0';
    while (fgets(word, MAX_CHAR, fpin)) {
        if (strchr(word, '\n')) {
            word[strlen(word)-2] = '\0';
        }

        s = word;
        t = prev;
        chrccount = 0;
        while (*t != '\0' && (*s++ == *t++)) {
            ++chrccount;
        }

        buf[0] = chrccount + '0';
        buf[1] = '\0';
        strcat(buf, word[chrccount]);
        fputs(buf, fpout);
        linelen += 1 + strlen(&word[chrccount]);
        if (linelen >= MAX_COL) {
            linelen = 0;
            fputs("\n", fpout);
        }
        strcpy(prev, word);
    }

    fclose(fpin);
    fclose(fpout);
}
```