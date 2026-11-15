| Validate() | Memory Snapshot |
| :--- | :--- |
| Step 1: if (red > MAXVAL) overflowFlag = overflowFlag | RMASK; | Pixel p1 | 278 | unsigned red |
| | | | 298 | unsigned green |
| | | | 150 | unsigned blue |
| | | | 4 | unsigned short overflowFlag |
| Step 2: if (green > MAXVAL) overflowFlag = overflowFlag | GMASK; | Pixel p1 | 278 | unsigned red |
| | | | 298 | unsigned green |
| | | | 150 | unsigned blue |
| | | | 6 | unsigned short overflowFlag |
| Step 3: if (blue > MAXVAL) overflowFlag = overflowFlag | BMASK; | | | |

When the bitwise or is performed in step 1 with the operands overflowFlag (00000000) and RMASK (00000100), the result is 4, as illustrated below:

```
00000000  overflowFlag
00000100  RMASK
----------
00000100  result of bitwise or
```

The result of the operation is assigned to overflowFlag, thus replacing the previous value. When the bitwise or is performed in step 2 with the operands overflowFlag (00000100) and GMASK (00000010), the result is 6, as illustrated below:

```
00000100  overflowFlag
00000010  GMASK
----------
00000110  result of bitwise or
```

The resulting value of overflowFlag indicates that there is overflow in the data member red, overflow in the data member green, and no overflow in the data member blue. Thus, the statement pixel1.overflow() will return a Boolean value of true, as illustrated below:

```
00000110  overflowFlag
00000111  CHECK
----------
00000110  result of bitwise and
```

We will now write a small driver program to test the new methods of the Pixel class.