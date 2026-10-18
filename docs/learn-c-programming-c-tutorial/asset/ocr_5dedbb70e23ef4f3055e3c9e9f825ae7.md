```
```c
unsigned int heightValidated;
} status1;

/* define a structure with bit fields */
struct
{
    unsigned int widthValidated : 1;
    unsigned int heightValidated : 1;
} status2;

int main( )
{
    printf( "Memory size occupied by status1 : %d\n", sizeof(status1));
    printf( "Memory size occupied by status2 : %d\n", sizeof(status2));

    return 0;
}
```
```

When the above code is compiled and executed, it produces the following result:

```
```text
Memory size occupied by status1 : 8
Memory size occupied by status2 : 4
```
```

# Bit Field Declaration

The declaration of a bit-field has the following form inside a structure:

```
```c
struct
{
    type [member_name] : width ;
};
```
```

The following table describes the variable elements of a bit field:

| Elements | Description |
|---|---|
| type | An integer type that determines how a bit-field's value is |