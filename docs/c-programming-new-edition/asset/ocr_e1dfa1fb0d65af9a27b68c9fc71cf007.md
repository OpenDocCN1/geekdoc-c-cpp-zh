```
scanf("%s",cap);
printf("%s is the capital of your country",cap);
}
```

Start with line 5 since the preceding ones must be quite easy to decipher. Line 5 is where the dynamic initialization of the array takes place. It indicates to the compiler that an array is to be created which can accommodate 10 elements that are of character type. The line 7 accepts the string of characters that is entered by the user based on the display statement in line 6. Line 8 retrieves the stored string from the array and displays it back onto the screen.

Another feature of dynamic initialization of character arrays is that it facilitates the inclusion of blank spaces in between the characters of the string. This can be accomplished by altering the format specifier in the scanf statement in the following way:

```
scanf("%[^\n]", arrayname);
```

If the above statement is not specified and a blank space is even attempted to be inserted into the string the characters present after the string will be terminated without any mercy. The compiler refuses to acknowledge any characters after the blank.

# 4.11. ARRAY OVERFLOW

If at all any criticisms can be barraged on C it will be only in this aspect. Array over flow can be simply put as crossing the boundaries. To explain it in terms of C when an array of a particular size is declared only that many elements can be inserted into an array.

If that size limit is exceeded an error is formed which results in an irregularity in the functioning of the program and C conventionally does not check for array overflow. For example, if you declare an array like sal[10] and you enter 12 elements then an illegal operation is performed which results in an irreparable loss. Not only inserting but also accessing the element whose size is not declared is an illegal operation.

Things don’t stop after an error is performed, there are possibilities that the program might be reduced to shambles. This purely depends on how significant those variables that have been overwritten are and where they are used subsequently in the program. The result of the blemish can jolt you immediately or take its toll in due course of the program. This kind