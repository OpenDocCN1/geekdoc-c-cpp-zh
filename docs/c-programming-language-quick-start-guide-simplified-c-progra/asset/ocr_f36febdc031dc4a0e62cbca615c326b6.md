Although memory is allocated to these variables at the time of declaration but these variables have been assigned nothing. No student type variable has details saved in it.

Here’s how each component of a struct type variable is initialized:

```
s1.Name = "R Khan"
s1.Course = 18;
s1.ID = 786;
s1.Section = 'A';
s1.CGPA = 3.74;
```

# 7.3 Member Access Operators

We can access a member of a struct variable in two ways. The above example uses the member access operator ".". We will now give further examples of its use and introduce the other member access operator "->". Both operators are used for same purpose. The difference lies in the caller. The dot operator is used by a structure variable while arrow is used by a pointer to structure variable.

```
typedef struct
{
char *Name;
```