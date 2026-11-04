The syntax resembles a variable declaration preceded by the typedef keyword. The name represents the stated type. For example, the statement:

```
typedef float arr[100];
```

makes arr synonym for an array of 100 floats. Pay attention, typedef does not create a variable, nor a new type, just a new name. Therefore, the statement:

```
arr arr1;
```

declares the variable arr1 as an array of 100 floats. If we ever need to make the type of the array double, we just change float to double. The declaration of the variable remains the same.

In the same way, we can use typedef to create an alias for a structure type. For example:

```
typedef struct Mybook
{
    char title[100];
    int year;
    float price;
} book;
```

Mybook is a tag and we must add the word struct when used. On the other hand, because the typedef name, that is, book, is a synonym for the structure type, it is not allowed to add the word struct. For example:

```
book b1, b2;
```

Notice that we can use the same identifier for both the structure tag and the typedef name; their meaning is still different though. Also, we can omit the tag and use the typedef name to declare variables. For example:

```
typedef struct
{
    char title[100];
    int year;
    float price;
} book;
```

typedef is used a lot with structures and unions to save writing the word struct or union, when declaring variables. Although this is very common, we don't use it so much. We prefer to clearly show the type of the variable; why hide it? It is easier and faster to read the code; why waste time searching for hidden types? The most times we are using typedef is either if the same type appears a lot in the code or we are using a data structure (e.g., list) with elements structures (or unions).

If the data types of your application depend on the running platform, typedef might be useful. For example:

```
typedef short int size_i;
```

the type of all size_i variables will be short int. In case these variables must be int in another platform, just change short int to int and they become int.