```
```c
printf("%s\t% d\t%s\n",
    bond.actor,
    bond.year,
    bond.title);
}
fclose(jbdb);

return(0);
}
```
```

The source code in Listing 22-9 uses a while loop at Line 22 to read in the structures from the bond.db file. The code assumes that the file was created by writing full-size agent structures with the fwrite() function.

The fread() function returns the number of items read. It returns 0 if no data remains to be read. This value is tested in variable r at Line 25. If zero, the while loop is broken. Otherwise, the feof() function terminates the loop at Line 22.

The code uses the structure variable bond at Line 12 to read multiple items from a file. The new items overwrite any values already in the structure, just like reusing any variable.

**Exercise 22-14:** Create a new project by using the source code from Listing 22-9. Build and run to examine the bond.db file, which was created in Exercises 22-12 and 22-13.

![](bbox=[0.15, 0.72, 0.22, 0.82])

The key to effectively read and write structures to a file — like a database — is to keep all structures uniform. This way, they can be read and written to the file in chunks. They can also be read or written in any order, as long as you also use the proper C language file functions.

# Reading and rewinding

As your program reads data from a file, it keeps track of the position from whence data is read in the file. A file position index is maintained so that the location at which the code is reading or writing within a file isn't lost.

When you first open a file, this index position is located at the beginning of the file, the first byte. If you read a 40-byte record into memory, the file position index is 40 bytes from the start. If you read until the end of the file, the position index maintains that location as well.