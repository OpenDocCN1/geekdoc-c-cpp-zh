# LESSON 17 Using Disk Files

```
48:    }
49:
50:    fclose(fp);
51:
52:    /* Now display both arrays to show they're the same. */
53:
54:    for (count = 0; count < SIZE; count++)
55:        printf("%d\t%d\n", array1[count], array2[count]);
56:    return(0);
57: }
```

# Output

| 0 | 0 |
| 2 | 2 |
| 4 | 4 |
| 6 | 6 |
| 8 | 8 |
| 10 | 10 |
| 12 | 12 |
| 14 | 14 |
| 16 | 16 |
| 18 | 18 |
| 20 | 20 |
| 22 | 22 |
| 24 | 24 |
| 26 | 26 |
| 28 | 28 |
| 30 | 30 |
| 32 | 32 |
| 34 | 34 |
| 36 | 36 |
| 38 | 38 |

# Analysis

Listing 17.4 demonstrates the use of the fwrite() and fread() functions. This program initializes an array on lines 14 and 15. It uses fwrite() on line 26 to save the array to disk. The program uses fread() on line 44 to read the data into a different array. Finally, it displays both arrays onscreen to show they now hold the same data (lines 54 and 55).

When we save with fwrite(), much can not get wrong except some type of disk error. With fread(), be careful, however. As far as fread() is concerned, the data has no way of knowing what it represents. For example, a block of 100 bytes could be 100 char variables, 25 int variables, or 20-byte structures. If you ask fread() to read that block into memory, it obediently