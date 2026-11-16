# Integer Types on a 32-bit Machine

| Name | Bytes | Minimum Value | Maximum Value |
|---|---|---|---|
| short int | 2 | -32,768 | 32,767 |
| unsigned short int | 2 | 0 | 65,535 |
| int | 4 | -2,147,483,648 | 2,147,483,647 |
| unsigned int | 4 | 0 | 4,294,967,295 |
| long int | 4 | -2,147,483,648 | 2,147,483,647 |
| unsigned long int | 4 | 0 | 4,294,967,295 |

# Integer Types on a 64-bit Machine

| Name | Bytes | Minimum Value | Maximum Value |
|---|---|---|---|
| short int | 2 | -32,768 | 32,767 |
| unsigned short int | 2 | 0 | 65,535 |
| int | 4 | -2,147,483,648 | 2,147,483,647 |
| unsigned int | 4 | 0 | 4,294,967,295 |
| long int | 8 | -9,223,372,036,854,775,808 | 9,223,372,036,854,775,807 |
| unsigned long int | 8 | 0 | 18,446,744,073,709,551,615 |

# sizeof() Operator

The operator sizeof() is built-in as part of the C language. It returns an integer that represents the number of bytes used to store an object on the host computer. All that is guaranteed by C is that:

```
sizeof(char) = 1
sizeof(short) <= sizeof(int) <= sizeof(long)
sizeof(unsigned) = sizeof(int)
```

Note that problems can occur if the result of an integer operation is assigned to a variable of a shorter data type.

For example:

```
long x = 10000;
long y = 10000;
short answer;
answer = x * y;
```