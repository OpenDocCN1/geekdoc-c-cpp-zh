# LISTING 20-4: (continued)

```
}
/* gather input */
puts("Type something long and boring:");
fgets(input,1023,stdin);

/* resize the buffer */
len = strlen(input);
input = realloc(input,sizeof(char)*(len+1));
if( input==NULL )
{
    puts("Unable to reallocate buffer!");
    exit(1);
}
puts("Memory reallocated.");

/* output results */
puts("You wrote:");
printf("%s",input);

return(0);
}
```

The source code in Listing 20-4 is based on Listing 20-2, with code added to accommodate the realloc() function at Line 24. Here's the format:

```
p = realloc(buffer,size);
```

buffer is an existing, allocated storage area, created by the malloc() or similar function. size is the new buffer size, calculated the same as the malloc() function's size argument. Upon success, realloc() returns a pointer to buffer; otherwise, NULL is returned. And, yes, you can use the same pointer variable as both p and buffer, as shown with variable input at Line 24 in Listing 20-4.

As with malloc(), the realloc() function requires the stdlib.h header, shown in Listing 20-4 at Line 2.

The string.h header is called in at Line 3 to satisfy the use of the strlen() function at Line 23. The input string's length is gathered and saved in the len variable.

At Line 24, the realloc() function resizes the input buffer to a new value. The new value is based on the input string's length plus 1, to account for the \0 character. The point of this code is to resize the input buffer to match the string's exact length, which is the value of len plus one for the null character.