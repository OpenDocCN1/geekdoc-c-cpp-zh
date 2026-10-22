# # Chapter 17 Advanced Data Representation

```
```c
puts("No entries!");
return; /* quit function if tree is empty */
}

puts("Please enter name of pet you wish to find:");
s_gets(temp.petname, SLEN);
puts("Please enter pet kind:");
s_gets(temp.petkind, SLEN);
uppercase(temp.petname);
uppercase(temp.petkind);
printf("%s the %s ", temp.petname, temp.petkind);
if (InTree(&temp, pt))
printf("is a member.\n");
else 
printf("is not a member.\n");
```
```

```
```c
void dropet(Tree * pt)
{
Item temp;
if (TreeIsEmpty(pt))
{
puts("No entries!");
return; /* quit function if tree is empty */
}

puts("Please enter name of pet you wish to delete:");
s_gets(temp.petname, SLEN);
puts("Please enter pet kind:");
s_gets(temp.petkind, SLEN);
uppercase(temp.petname);
uppercase(temp.petkind);
printf("%s the %s ", temp.petname, temp.petkind);
if (DeleteItem(&temp, pt))
printf("is dropped from the club.\n");
else 
printf("is not a member.\n");
}
```
```

```
```c
void uppercase(char * str)
{
while (*str)
{
*str = toupper(*str);
str++;
}
}
```
```