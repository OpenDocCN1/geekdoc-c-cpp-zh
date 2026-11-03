```
{
    case EPERM:
        puts("Operation not permitted");
        break;
    case ENOENT:
        puts("File not found");
        break;
    case EACCES:
        puts("Permission denied");
        break;
    case EROFS:
        puts("Read only file");
        break;
    case ENAMETOOLONG:
        puts("Filename is too long");
        break;
    default:
        puts("Too ugly to describe");
    }
    exit(1);
}
puts("File renamed");
return 0;
}
```

To use the errno variable, your code must include the errno.h header file, as shown in Line 3 of Listing 25-3. That header file declares errno as an external variable. It also contains common error conditions as defined constants known to numerous C library functions.

The rename() function at Line 9 attempts to rename a file. I'm assuming that the file blor fus is unavailable, so the function is designed to generate an error. If so, it returns -1 and sets the global variable errno to represent the error condition that's encountered.

The switch structure at Line 13 plows through some errors that are possible when renaming a file. The defined constants represent these error codes, which are defined in the errno.h header file.

# Exercise 25-3: Type the source code from Listing 25-3 into a new project. Build and run to witness an accurate error message.