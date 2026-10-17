```
static struct emp e={“bobby”, ”876876”, ”illinois”};
printf(“name=%s\n”,e.name);
printf(“phone=%s\n”,e.d.ph);
printf(“city=%s”,e.d.city);
}
```

Here you will notice that to access the element of a structure that are enclosed within another structure the dot operated is used twice.

Nesting cannot be restricted to only 2 structures and each of them can be accessed by that many dots. In the above program you can see that a variable d is declared in the nested structure that corresponds to the first structure and using this variable the elements declared in the first structure can be accessed. While printing the elements of both the structures, both the variables e and d are used along with the member name each of them separated with a dot(.)

# 8.9. THE UNIONS

A union is yet another data type in C, which allows you to overlay more than one variable in the same memory area. Usually the storage procedure is that every variable is stored in separate memory locations and each one of them has a unique address. Often you discover that the variables that you use in the program are used only in a small part of the source.

Let’s say that you require a string of length 50 bytes, by name files in the first fifty lines of your source program and assume further that you need another string variable of length 100 bytes with the name display only in the later part of the program. You may now realize that it is not necessary to declare two separate strings which will consume 150 bytes.

Since these variables are not needed simultaneously, it will be highly convenient if both the strings share the same space. A Union does that. There is a striking resemblance between the unions and the structures in the way they are declared, the way the members are accessed and so on. The general format of a union declaration is shown below:

```
union tag
{
    member1;
    member2
```