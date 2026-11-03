now represent a Student. An alternative way to declare these identifiers is as follows:

```
```c
struct Student
{

char *Name;

int Course, ID;

char Section;

double CGPA:

} s1, s2, s3;
```
```

Another way of declaration, which is highly recommended as it shortens the declaration

of identifiers of the structure, is as follows:

```
```c
typedef struct
{

char *Name;

int Course, ID;

char Section;

double CGPA:

} Student;
```
```

# 7.2 Memory Allocation