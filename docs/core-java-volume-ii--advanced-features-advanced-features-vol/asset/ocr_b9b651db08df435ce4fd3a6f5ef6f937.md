```
```c
const char* cformat;
char* fmt;
jstring ret;

cformat = (*env)->GetStringUTFChars(env, format, NULL);
fmt = find_format(cformat);
if (fmt == NULL)
    ret = format;
else
{
    char* cret;
    int width = atoi(fmt);
    if (width == 0) width = DBL_DIG + 10;
    cret = (char*) malloc(strlen(cformat) + width);
    sprintf(cret, cformat, x);
    ret = (*env)->NewStringUTF(env, cret);
    free(cret);
}
(*env)->ReleaseStringUTFChars(env, format, cformat);
return ret;
}
```
```

In this function, we chose to keep error handling simple. If the format code to print a floating-point number is not of the form %w.pc, where c is one of the characters e, E, f, g, or G, then we simply do not format the number. We’ll show you later how to make a native method throw an exception.

# 12.4 Accessing Fields

All the native methods you saw so far were static methods with number and string parameters. We’ll now consider native methods that operate on objects. As an exercise, we will reimplement as native a method of the Employee class that was introduced in Volume I, Chapter 4. Again, this is not something you would normally want to do, but it does illustrate how to access fields from a native method when you need to do so.

# 12.4.1 Accessing Instance Fields

To see how to access instance fields from a native method, we will reimplement the raiseSalary method. Here is the code in Java:

```
```java
public void raiseSalary(double byPercent)
{
    salary *= 1 + byPercent / 100;
}
```
```