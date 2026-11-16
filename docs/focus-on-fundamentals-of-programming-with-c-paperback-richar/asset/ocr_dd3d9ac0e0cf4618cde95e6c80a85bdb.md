For example:

```
typedef struct {
   char name[30];
   double gpa;
   int year;
} Student;
```

This serves as a blueprint or template for the creation of a new data type called Student. This new user-defined data type, Student, can be used to declare variables just like any built-in data type:

```
// struct1.c

typedef struct {
   char name[30];
   double gpa;
   int year;
} Student;

int main(void) {
   Student s1, s2, s3;
   ...
   return 0;
}
```

Our declarations above create three variables of type Student: s1, s2, and s3. Each of these variables now has storage in memory for a character string, a double, and an int. Note that the name of our new data type begins with a capital letter. While it's not required, it's a good rule to follow.

Also note that the struct is declared outside of main() in the global scope. This allows the struct to be visible to all parts of the program. If the struct were only declared within main(), then it would be local to main() and only visible within main().