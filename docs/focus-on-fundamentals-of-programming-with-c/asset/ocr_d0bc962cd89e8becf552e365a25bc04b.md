Read an alphabetized file (one word per line) and writes a compressed version of the file. Words in the output file are preceded by a count (2 characters) identical to the previous word plus an offset of 48 (ASCII '0'), and these identical characters are omitted. Multiple words are output on each line until column MAX_COL is reached. At this point, the current word is made the last on the line by printing '\n'.

```
void compress(FILE *) {
    char prev[MAX_CHAR], word[MAX_CHAR], c;
    int i, key;
    int character, location = 0;
    FILE *fptr, *fopen();
    if ((fptr = fopen("Dictionary.text", "r")) == NULL) {
        fprintf(stderr, "File could not be opened for input.\n");
        exit(1);
    } else {
        fscanf(fptr, "%s", word);
        fprintf(fptr, "%s", word);
        strcpy(prev, word);
        while (fscanf(fptr, "%s", word) != EOF) {
            i = 0;
            while (prev[i] == word[i]) i++;
            if (i > 0) {
                fprintf(fptr, "%c%d%s\n", i, word[i]);
                location += i + 2;
                if (location > MAX_COL) {
                    fprintf(fptr, "\n");
                    location = 0;
                }
            }
            fprintf(fptr, "%s", word);
            strcpy(prev, word);
        }
        fclose(fptr);
    }
}
```