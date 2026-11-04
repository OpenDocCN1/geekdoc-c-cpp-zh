```
```c
void cipher(FILE *fp_in, FILE *fp_out, int key)
{
    int ch;

    while(1)
    {
        ch = getc(fp_in);
        if(ch == EOF)
            return;
        /* Only the lower and upper case characters are encrypted. */
        if(ch >= 'A' && ch <= 'Z')
        {
            ch += key;
            if(ch > 'Z')
                ch -= 26;
        }
        else if(ch >= 'a' && ch <= 'z')
        {
            ch += key;
            if(ch > 'z')
                ch -= 26;
        }
        putc(ch, fp_out);
    }
}

void decipher(FILE *fp_in, FILE *fp_out, int key)
{
    int ch;

    while(1)
    {
        ch = getc(fp_in);
        if(ch == EOF)
            return;
        /* Only the lower and upper case characters are decrypted. */
        if(ch >= 'A' && ch <= 'Z')
        {
            ch -= key;
            if(ch < 'A')
                ch += 26;
        }
        else if(ch >= 'a' && ch <= 'z')
        {
            ch -= key;
            if(ch < 'a')
                ch += 26;
        }
        putc(ch, fp_out);
    }
}
```
```