```
ghi.prev = &def;
ghi.next = &jkl;
jkl.prev = 3;
jkl.next = &ghi;
jkl.next = &abc;
x=abc.next->next->prev->next->i;
printf("%d",x);
}
```

```
6. struct A_X
{
 int x, y;
};
struct A_A origin, *ptr;
void main()
{
 ptr = &origin;
 printf("Value of ptr is %d - %d
",(*ptr).x,(*ptr).y);
 printf("Value of ptr is %d - %d
",ptr->x,ptr->y);
}
```

```
7. void main()
{
 struct student
 {
 char name[30];
 struct date dob;
 }stud;
 struct date
 {
 int dd, mm, yy;
 };
 scanf("%s %d %d %d", stud.name,
 &stud.dob.dd,&stud.dob.mm,
 &stud.dob.yy);
}
```

```
8. void main()
{
 struct date;
 struct student
 {
 int rollno;
 char name[30];
 struct date dob;
 }stud;
 struct date
 {
 int dd, mm, yy;
 };
 scanf("%s %d %d %d", stud.name,
 &stud.dob.dd,&stud.dob.mm,
 &stud.dob.yy);
}
```

```
9. There were 10 records stored in
"somefile.dat" but the following
program printed 11 names. What went
wrong?
void main()
{
 struct student
 {
 char name[30];
 int rollno;
 }stu;
 FILE *fp;
 fp=fopen("c:\somefile.dat","r+");
 while((!feof(fp))
```

```
fread(&stud,sizeof(stud),1,fp);
puts(stud.name);
printf("%s - %d",
stud.name,stud.rollno);
}
```

```
10. Is the following code legal?
struct a
{
 int x;
 struct a b;
};
```

```
11. Is the following code legal?
struct a
{
 int x;
 struct a *b;
};
```

```
12. Is the following code legal?
typedef struct a
{
 int x;
 Type *b;
}Type;
```

```
13. Is the following code legal?
typedef struct a Type;
struct a
{
 int x;
 Type *b;
};
```

```
14. Is the following code legal?
void main()
{
 typedef struct a Type;
 Type someVariable;
 struct a
 {
 int x;
 Type *b;
 };
}
```

```
15. void main()
{
 struct X
 {
 int x;
 float y;
 };
 struct X v1, v2;
 v1.x = 10;
 v1.y = 20.5;
 v2 = v1;
 printf("\t%d%f\t%f%d\t%f",
 v1.x,v1.y,v2.x,v2.y);
}
```