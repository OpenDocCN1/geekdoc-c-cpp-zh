# Manipulating Memory Blocks

```
12:   memset(message1 + 5, '@', 10);
13:   printf("\nmessage1[] after memset():\ts", message1);
14:
15:   strcpy(temp, message2);
16:   printf("\nOriginal message: %s", temp);
17:   memcpy(temp + 4, temp + 16, 10);
18:   printf("\nAfter memcpy() without overlap:\\ts", temp);
19:   strcpy(temp, message2);
20:   memcpy(temp + 6, temp + 4, 10);
21:   printf("\nAfter memcpy() with overlap:\\ts", temp);
22:
23:   strcpy(temp, message2);
24:   printf("\nOriginal message: %s", temp);
25:   memmove(temp + 4, temp + 16, 10);
26:   printf("\nAfter memmove() without overlap:\\ts", temp);
27:   strcpy(temp, message2);
28:   memmove(temp + 6, temp + 4, 10);
29:   printf("\nAfter memmove() with overlap:\\ts\n", temp);
30:   return 0;
```

# Output

message[] before memset():    Four score and seven years ago
message[] after memset():      Four @@@@@@@@seven years ago

Original message: abcdefghijklmnopstuvxyz
After memcpy() without overlap: abcdqrstuvxyzopqrstuvxyz
After memcpy() with overlap: abcdefefefefefqrstuvxyz

Original message: abcdefghijklmnopstuvxyz
After memmove() without overlap:  abcdqrstuvxyzopqrstuvxyz
After memmove() with overlap:  abcdefghijklmnopqrstuvxyz

# Analysis

The operation of memset() is straightforward. Note how the pointer notation message1 + 5 is used to specify that memset() is to start characters at the sixth character in message1[] (Remember, all addresses are zero-based). As a result, the 6th through 15th characters in message1[] have been changed to @.

When source and destination do not overlap, memcpy() works fine. The 10 characters of temp[] starting at position 17 (the letters q through z) have been copied to positions 5 through 14, where the letters e through n were originally located. If, however, the source and destination overlap, things are different. When the function tries to copy 10 characters starting at position 4 to position 6, an overlap of 8 positions occurs. You