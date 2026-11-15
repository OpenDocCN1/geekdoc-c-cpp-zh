# 6.23 HANDLING EXCEPTION MESSAGES

```
void *ajMemAlloc(size_t nbytes, const char* file, ajint line)
{
    void *ptr;

    if(nbytes <= 0)
        ajExceptRaise(&mem_Badcount, file, line);

    ptr = malloc(nbytes);

    if(ptr == NULL)
    {
        if(file == NULL)
            AJRAISE(Mem_Failed);
        else
            ajExceptRaise(&mem_Failed, file, line);
    }
}
```