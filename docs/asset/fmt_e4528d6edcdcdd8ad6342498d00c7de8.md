
```c
#include<stdio.h>
#include<conio.h>
Void main()
{
    char str[10];
    int i;
    clrscr();
    printf("\n Enter a string \n");
    gets(str);
    for(i=0;str[i]!='\0'; i++)
    {
        if(str[i]>=97 && str[i]<=122)
        {
            str[i]=str[i]-32;
        }
        if(str[i]==' ')
        {
            if(str[i+1]>=97 && str[i+1]<=122)
            {
                str[i+1]=str[i+1]-32;
            }
        }
    }
    puts(str);
    getch();
}
```

## 97. 使用指针计算阶乘程序

```c
#include<stdio.h>
#include<conio.h>
Void main()
{
    int n,i,*p,f=1;
    clrscr();
    printf("\n Any number\n");
    scanf("%d",&n);
    p=&f;
    for(i=1;i<=n;i++)
    {
        *p=*p*i;
    }
    printf("\n Factorial is=%d", f);
    getch();
}
```

## 98. 使用指针计算字符串长度程序

```c
#include<stdio.h>
#include<conio.h>
Void main()
{
    char str[10];
    int p,count=0;
    clrscr();
    printf("\n Enter string");
    gets(str);
    p=str;
    while(*p!='0')
    {
        count++;
        p++;
    }
    printf("\n Length of string is=%d",count);
    getch();
}
```

## 99. 使用指针将字符串拷贝到另一个字符串中程序

```c
#include<stdio.h>
#include<conio.h>
Void main()
{
    char str[10],s2[10],*p1,*p2;
    clrscr();
    printf("\n Enter string");
    gets(str);
    p1=str;
    p2=s2;
    while(*p1!='0')
    {
        *p2=*p1;
        p1++;
        p2++;
    }
    *p2='\0';
    puts(s1);
    puts(s2);
    getch();
}
```

## 100. 使用指针拼接两个字符串程序

```c
#include<stdio.h>
#include<conio.h>
Void main()
{
    char s1[10],s2[10],*p1,*p2;
    int i,j;
    clrscr();
    printf("\n Enter first string\n\n");
    gets(s1);
    printf("\n Enter second string\n\n");
    gets(s2);
    p1=s1;
    p2=s2;
    while(*p1!='0')
    {
        p1++;
    }
    while(*p2!='0')
    {
        *p1=*p2;
        p1++;
        p2++;
    }
    *p1='\0'
    puts(s1);
    getch();
}
```

```c
printf("\n Enter first string");
gets(s1);

printf("\n Enter second string");
gets(s2);

p1=s1;
p2=s2;

while(*p1!='0' ||*p2!='0')
{
    if(*p1==*p2)
    {
        p1++;
        p2++;
        continue;
    }
    else
    {
        f=*p1-*p2;
        break;
    }
}
if (f==0)
    printf("\n string are equal");
else
    printf("\n string are not equal");
getch();
}
```

# ****************************

**结构**

****************************

## 102. 编写程序创建一个书籍结构体，读取并显示书籍信息。

```c
#include<stdio.h>
#include<conio.h>
struct book
{
    char name[10];
    int pages;
    float price;
};
void main()
{
    struct book b;

    printf("\n Enter information about book");

    printf("\n Enter Name of the book");
    gets(b.name);

    printf("\n Enter total pages and price of the book");
    scanf("%d%f",&b.pages,&b.price);

    printf("\n Displaying information about book");
    printf("\n name=%s",b.name);
    printf("\n pages=%d",b.pages);
    printf("\n price=%f",b.price);
    getch();
}
```

## 103. 编写程序创建一个学生结构体，读取10个学生的信息，并打印分数大于90的学生的名字。

```c
#include<stdio.h>
#include<conio.h>
struct student
{
    char name[10];
    int r_no;
    float marks;
};
```

```c
void main()
{
  struct student s[10];
  int i;
  printf("\n Enter info. about students");
  for(i=0;i<10;i++)
  {
    printf("\n Plz Enter the name of the student");
    gets(s[i].name);
    printf("\n Enter r_ no and marks");
    scanf("%d % f",&s[i].r_no,&s[i].marks);
  }
  printf("\n name of those whose have >90");
  for (i=0;i<10;i++)
  {
    if (s[i].marks>90)
      puts(s[i].name);
  }
  getch();
}
```

## 104. 编写程序读取个人信息并打印住在特定城市的人详情。

```c
#include<stdio.h>
#include<conio.h>
#include<string.h>
struct personalinfo
{
  char name[10];
  char city[20];
  char add [20];
};
void main()
{
  struct personalinfo s[10];
  int i,n;
  char ct[20];
  printf("Enter info of ten peoples");

  for (i=0;i<10;i++)
  {
    printf("\n Plz Enter the name of the Person");
    gets(s[i].name);
    printf("\n Plz Enter the name of the city");
    gets(s[i].city);
    printf("\n Plz Enter the address of the person");
    gets(s[i].add);
  }

  printf("\n Enter the city whose persons detail u want display");
  gets(ct);
  for (i=0;i<10;i++)
  {
    n=strcmp(s[i].city,ct);
    if(n==0)
    {
        puts(s[i].name);
        puts(s[i].city);
        puts(s[i].add);
    }
  }

  getch();
}
```

## 105. 编写程序创建一个复数结构体来建模，读取两个复数并将它们相加。

```c
#include<stdio.h>
#include<conio.h>
struct complex
{
    float real,image;
};
void main()
{
    struct complex c1,c2,c3;
    printf("\n Plz Enter first complex no.");
    printf("\n Plz Enter the real part");
    scanf("%f",&c1.real);
    printf("\n Plz Enter the imaginary part");
    scanf("%f",&c1.image);
    printf("\n Plz Enter the second complex no.");
    printf("\n Plz Enter the real part");
    scanf("%f",&c2.real);
    printf("\n Plz Enter the imaginary part");
    scanf("%f",&c2.image);
    c3.real=c1.real+c2.real;
    c3.image=c1.image+c2.image;
    printf("\n Sir After Addition both parts");
    printf("\n real = %f,image=%f",c3.real,c3.image);
    getch();
}
```

## 106. 编写程序创建一个距离结构体，读取以英尺和英寸为单位的距离并打印它们的和。好吧！

```c
#include <stdio.h>
#include <conio.h>
struct distance
{
float feet,inch;
};
void main()
{
  struct distance d1,d2,d3;

  printf("\n Plz Enter first distance.");
  printf("\n Plz Enter the feet");
  scanf("%f",&d1.feet);
  printf("\n Plz Enter the inches");
  scanf("%f",&d1.inch);

  printf("\n Plz Enter second distance.");
  printf("\n Plz Enter the feet");
  scanf("%f",&d2.feet);
  printf("\n Plz Enter the inches");
  scanf("%f",&d2.inch);

  d3.feet=d1.feet+d2.feet;
  d3.inch=d1.inch+d2.inch;

  while(d3.inch>=12)
  {
    d3.feet++;
    d3.inch-=12;
  }
  printf("\n Sir After Addition both parts");
  printf("\n feet = %f,inches=%f",d3.feet,d3.inch);
  getch();
}
```

## 107. 编写程序创建一个日期结构体，按天数增加日期，并应该是有效的。

```c
#include<stdio.h>
#include<conio.h>
struct date
{
  int dd,mm,yy;
};
void main()
{
  struct date d;
  int day;
  printf("\n Enter days,month,year.");
  scanf("%d%d%d",&d.dd,&d.mm,&d.yy);

  printf("\n Plz Enter no. of days you want to add");
  scanf("%d",&day);
  while(d.dd>=30)
  {
    d.mm++;
    d.dd-=30;
  }
  while(d.mm>12)
  {
    d.yy++;
    d.mm-=12;
  }

  printf("\n sir Additions");
  printf("\n %d/%d/%d",d.dd,d.mm,d.yy);
  getch();
}
```

## 108. 编写程序读取20本书的信息，并打印价格超过100元的书。

```c
#include<stdio.h>
#include<conio.h>
struct book
{
  char name[10];
  int pages;
  float price;
};
void main()
{
  struct book b[20];
  int i;
  printf("\n Plz Enter info. of 20 books.");
  for(i=0;i<20;i++)
  {
    printf("\n Enter name");
    gets(b[i].name);
    printf("\n Enter pages");
    scanf("%d",&b[i].pages);
    printf("\n Enter price");
    scanf("%f",&b[i].price);
  }
  printf("\n name of those whose price is more than 100.");
  for (i=0;i<20;i++)
  {
    if(b[i].price>100)
      puts(b[i].name);
  }
  getch();
}
```

# ***********************

**文件操作**

***********************

## 109. 编写程序从屏幕读取一行文本并存储到文件中。

```c
#include<stdio.h>
#include<conio.h>
#include<stdlib.h>
#include<string.h>
void main()
{
  FILE *fp;
  char str[20];
  fp=fopen("sample.txt","w");
  printf("\n Enter line of text");
  gets(str);
  fprintf(fp,"%s",str);
  fclose(fp);
  getch();
}
```

## 110. 编写程序从文件中读取一行文本并显示，同时在另一个文件中创建副本。

```c
#include<stdio.h>
#include<conio.h>
#include<stdlib.h>
#include<string.h>
void main()
{
  FILE *fp1,*fp2;
  char str[20];
  int i,n;
  fp1=fopen("sample.txt","r");
  if(fp1==null)
  {
    printf("\n File doesn't exist");
    exit(1);
  }
  while(!feof(fp1))
  {
    fscanf(fp1,"%s",str);
    printf("\n file contains...");
    puts(str);
  }
  rewind(fp1);
  fp2=fopen("file2.txt","w");
  while(!feof(fp1))
  {
    fscanf(fp1,"%s",str);
    fprintf(fp2,"%s",str);
  }
  getch();
}
```

## 111. 编写程序统计文件中总的字符数和单词数。
