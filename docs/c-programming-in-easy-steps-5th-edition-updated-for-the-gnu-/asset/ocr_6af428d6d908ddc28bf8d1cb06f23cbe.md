The ftell() function returns the current file position of the specified stream, or -1 if an error occurs

```
int fgetpos( FILE *stream , fpos_t *ptr )
```

The fgetpos() function records the current file position of the specified stream in the specified ptr pointer as a special fpos_t type. This function returns a non-zero value if an error occurs

```
int fsetpos( FILE *stream , const fpos_t *ptr )
```

The fsetpos() function positions the file pointer in the specified stream at the position recorded by fgetpos() in the ptr pointer. This function returns a non-zero value if an error occurs