```
pst->fname, pst->lname, pst->letters);
}
```

```
void cleanup(struct namect * pst)
{
    free(pst->fname);
    free(pst->lname);
}
```

```
char * s_gets(char * st, int n)
{
    char * ret_val;
    char * find;

    ret_val = fgets(st, n, stdin);
    if (ret_val)
    {
        find = strchr(st, '\n');    // look for newline
        if (find)                   // if the address is not NULL,
            *find = '\0';          // place a null character there
        else
            while (getchar() != '\n')
                continue;           // dispose of rest of line
    }
    return ret_val;
}
```

Here is some sample output:

```
Please enter your first name.
Floresiensis
Please enter your last name.
Mann
Floresiensis Mann, your name contains 16 letters.
```

# Compound Literals and Structures (C99)

C99’s compound literal feature is available for structures as well as for arrays. It’s handy if you just need a temporary structure value. For instance, you can use compound literals to create a structure to be used as a function argument or to be assigned to another structure. The syntax is to preface a brace-enclosed initializer list with the type name in parentheses. For example, the following is a compound literal of the struct book type:

```
(struct book) {"The Idiot", "Fyodor Dostoyevsky", 6.99}
```