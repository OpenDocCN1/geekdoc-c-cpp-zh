# 1.5 Express your given name and your family name as ASCII characters in the following format:

givenName familyName

The ASCII characters should be written in their binary form and stored so as to use the smallest number of 16-bit words. Check the Web site http://asciitable.com/ for the set of ASCII characters.

# 1.6 We have the following data stored in the first 32 locations of a memory as shown.

| Memory address | Value |
|---|---|
| 00000 | 0000010 |
| | 0101001 |
| | 1000001 |
| | 0101111 |
| | 0001111 |
| | 0000011 |
| | 1110101 |
| | 1101001 |
| | 1111101 |
| | 0001111 |
| | 0011101 |
| | 0001011 |
| | 0000001 |
| | 0101111 |
| | 0101001 |
| | 0100011 |
| | 0000010 |
| | 0001101 |
| | 0111101 |
| | 0111001 |
| | 1101001 |
| | 0011101 |
| | 0000001 |
| | 0001111 |
| | 0011111 |
| | 0010001 |
| | 0111101 |
| | 1001101 |
| 11111 | 1010101 |

(a) Please identify the words at the following hexadecimal addresses.

12, F, IE, 7, 1C

(b) Please give the hexadecimal addresses for the following words in memory. 1100101, 0010111, 0100011, 0111101

# 1.7 We have the following C code fragment:

```
unsigned char a = 0xD3;
char b = 'A';
int c = 6;
int d = 9;
int e = -31564;
unsigned int f = 0xFAD7;
float g = 3.1;
float h = 0.0345;
int j;
int* cPtr = &c;
int* dPtr = &d;
int** ccPtr = &cPtr;
int** ddPtr = &dPtr;
float* gPtr = &g;
float* hPtr = &h;
```

| Variable | Memory address | Value |
|---|---|---|
| | 00000 | 1000 |
| | | 1001 |
| | | |
| | | |
| | | |
| | | |
| | | 2000 |
| | | 2001 |
| | | |
| | | |
| | | |
| | | |
| | | 3000 |
| | | 3001 |
| | | |
| | | |
| | | |
| | | |
| | | 4000 |
| | | 4001 |
| | | |
| | | |
| | | |
| | | |