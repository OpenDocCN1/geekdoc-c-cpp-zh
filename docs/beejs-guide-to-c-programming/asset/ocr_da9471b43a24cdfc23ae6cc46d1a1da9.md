# Chapter 12. Manual Memory Allocation

return NULL;

```
// Main loop--read until newline or EOF
while (c = fgetc(fp), c != '\n' && c != EOF) {

    // Check if we're out of room in the buffer accounting
// for the extra byte for the NUL terminator
if (offset == bufsize - 1) ( // -1 for the NUL terminator
    bufsize *= 2; // 2x the space

    char *new_buf = realloc(buf, bufsize);

    if (new_buf == NULL) {
        free(buf); // On error, free and bail
        return NULL;
    }

    buf = new_buf; // Successful realloc
}

buf[offset++] = c; // Add the byte onto buffer

// We hit newline or EOF...

// If at EOF and we read bytes, free the buffer and
// return NULL to indicate we're at EOF:
if (c == EOF && offset == 0) {
    free(buf);
    return NULL;
}

// Shrink to fit
if (offset < bufsize - 1) { // If we're short of the end
    char *new_buf = realloc(buf, offset + 1); // +1 for NUL terminator

    // If successful, point buf to new_buf;
    // otherwise we'll leave buf where it is
    if (new_buf != NULL)
        buf = new_buf;
}

// Add the NUL terminator
buf[offset] = '\0';

return buf;
```

```
int main(void)
{
    FILE *fp = fopen("foo.txt", "r");

    char *line =;
```