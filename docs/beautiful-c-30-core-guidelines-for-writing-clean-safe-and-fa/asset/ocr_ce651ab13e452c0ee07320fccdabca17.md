```
```c
void fill_buffer(char* text, int length)
{
    char buf[256];
    strncpy(buf, text, length);
    ...
}
```
```