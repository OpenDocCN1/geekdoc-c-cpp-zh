You can also use casts to alter the arrangements of rows and columns. For example, if you start out with a five by six matrix then you can convert it into a three by ten matrix using:

```
int myArray[5][6];
int (*myPointer)[10];
myPointer = (int (*[10]) myArray;
printf("%d\n", myPointer[1][2]);
```

Once you realize that the whole multi-dimensional array trick is about using casting and pointer arithmetic to implement SMFs, then suddenly everything seems so much more obvious.

# ## Strings As NULL-Terminated Arrays

Strings are the lifeblood of the user interface and C is often criticized for doing them very badly indeed. It has to be admitted that strings are not C’s best feature, but they are efficient, close to the machine and fast.

The reason they are as they are is simply that when C was being developed memory was in short supply and text demands a lot of memory. Modern languages use more sophisticated ways of representing strings – storing additional information along with each string such as how many characters it contains and adopting immutable strings. None of these approaches can compare with the simplicity of the C string.

A C string is simply an array with a sentinel value marking its end. The sentinel is always NULL i.e. zero, because zero doesn’t correspond to any displayable character. This is one occasion when NULL can be safely used as an end marker.

NULL may be safe, but not having a NULL is definitely not safe. The main danger in using C strings is that you will encounter a string that is not NULL-terminated and as a result you will read or write beyond the end into memory you don’t own. Of course, by good design and programming you can avoid this sort of problem, but when you are processing strings obtained as input, you can be the subject of an attack that you have to defend against.

A string is a NULL-terminated array and as such nothing special. However, C does provide some additional features to make working with strings easier. The most obvious is the way string literals can be used to initialize NULL-terminated char arrays. For example:

```
char myString[50] = "Hello World";
```

stores the characters in myString and ends with a final NULL. Notice that, in this case, the array is longer than the number of characters to be stored.