
and which one need not to recompile again. Even compiling these files again and again on command line is also a big problem.

The solution is make utility. This utility takes care of all these problems and it even provides some more facility to manage project in a better way.

### 15.8.1 Writing Makefile

make utility uses makefile for building project. This makefile contains commands that tell make utility how to build your project with given source files. This makefile contains the dependency rules and construction rules.

left side : right side
    cc right side ( compilation by using options for linking library )

Here in first line, left side is the target and right side is the source files on which target is dependent. Second line is for the construction. If any source file is changed then make will go for construction rule otherwise it will not do anything. We have to understand what exactly make utility does with makefile.

- 1. It reads makefile and comes to know which object file and library is needed for target and then it checks what source files are needed for each object.
- 2. It checks time and date for each object file against dependent source, if any source is of later date than its object file, then it will apply construction rule for that particular object.
- 3. Now it will check time and date of target against dependent object file if any object file is of later date than its target then it will apply construction rule for target.

Now we will see how will be our makefile for Date project then we will see what is the meaning of each line of our makefile.

Makefile 1:

```
#
#   Date project Makefile
#
#
TARGET=Dt
OBJS=Datefmt.o Valid.o Leap.o Julian.o Cmpdate.o Adddays.o Addmonth.o Addyear.o \
Subdays.o Submonth.o Subyear.o Diffymd.o Diffdays.o Weekday.o Main.o

$(TARGET):$(OBJS)
    cc -o $(TARGET) $(OBJS)
Datefmt.o:Datefmt.c
    cc -c Datefmt.c
Valid.o:Valid.c
    cc -c Valid.c
Leap.o:Leap.c
    cc -c Leap.c
Julian.o:Julian.c
    cc -c Julian.c
Cmpdate.o:Cmpdate.c
    cc -c Cmpdate.c
Adddays.o:Adddays.c
    cc -c Adddays.c
Addmonth.o:Addmonth.c
    cc -c Addmonth.c
Addyear.o:Addyear.c
    cc -c Addyear.c
Subdays.o:Subdays.c
    cc -c Subdays.c
Submonth.o:Submonth.c
    cc -c Submonth.c
Subyear.o:Subyear.c
    cc -c Subyear.c
Diffymd.o:Diffymd.c
    cc -c Diffymd.c
Diffdays.o:Diffdays.c
    cc -c Diffdays.c
Weekday.o:Weekday.c
    cc -c Weekday.c
Main.o:Main.c
    cc -c Main.c
```

We can write the makefile as also.

# Makefile2:

# Date project Makefile

```
TARGET=Dt
OBJS=Datefmt.o Valid.o Leap.o Julian.o Cmpdate.o Adddays.o Addmonth.o Addyear.o \
    Subdays.o Submonth.o Subyear.o Diffymd.o Diffdays.o Weekday.o Main.o
all:$(TARGET)
$(TARGET):$(OBJS)
cc $(OBJS) -o $@
```

### 15.8.2 Building Project With Make

We can simply execute make as-

```
$make (ENTER)
```

It will search for file makefile in current directory and will build the project. But suppose we have many makefiles for different projects, then we can use some naming convention to name makefile for projects. Like we can name our project makefile as project_makefile. Here our project is Date so we can name our makefile as Date_makefile.

We can execute this as-

```
$make -f Date_makefile (ENTER)
```

I would like to recommend you to see the unix man page of make. This can be very useful for build work, which also takes a slice of project time. Generally one person in team is devoted for handling build work of project.

### 15.9 Creation Of Library And Using In Your Program in Unix

Now we will see process for creation of library and how to call function of this library in another file

- 1. First we will compile all the files for creating .o for source files.
      `$cc -c Datefmt.c Valid.c Leap.c Julian.c Cmpdate.c Adddays.c Addmonth.c Addyear.c \ Subdays.c Submonth.c Subyear.c Diffymd.c Diffdays.c Weekday.c Main.c`
      This will produce .o file for all source .c files.
- 2. Now we will assign all .o files to one variable.
      `$OBJS= Datefmt.o Valid.o Leap.o Julian.o Cmpdate.o Adddays.o Addmonth.o Addyear.o \ Subdays.o Submonth.o Subyear.o Diffymd.o Diffdays.o Weekday.o Main.o`
- 3. Library dt will be created with archiver ar as-
      `ar ruv Libdt.a $OBJS`
- 4. Now we will write file Main.c and call the functions of dt library in it.
- 5. Now Main.c will be compiled as-
      `cc -o Dt Main.c -L. -ldt`

## Chapter 16

### Code Optimization in C

### 16.1 Optimization is a Technique

When we think about optimization, it looks like we are talking only about making our code shorter. But it's not true, sometimes shorter code takes more execution time compared to large code. So here comes performance, and it depends on whether you want shorter code that is good for maintenance but less in performance, or larger code that is bad for maintenance but good in performance. Now we will come to resource optimization. Generally resources are shared between different processes. Suppose your program takes more resources, then definitely it will affect performance of other processes that need same resources. So we have a need to write and optimize our program keeping in mind resources e.g. processor's time. You will be surprised to know that most of the time, increasing of hardware like processors comes only because of our bad programming like unnecessary variables, bad searching and sorting algorithms. This is because we think only about running our program properly, and consider about resources only after getting some problem. Companies are spending more than $50 million on resources, adding more than 12 processors in single server, only because they don't consider other things in programs and are helpless to find this individual problem. So our work is not only to write program but also to develop the habit of writing optimized programs considering the overall view of system. That's why optimization is a technique because it considers many other things in program not only codes. You will see more things later in each topic.

### 16.2 Optimization With Tool

The first tool with our code is compiler. We can do lot of optimization with our compiler itself. It provides lot of options. So firstly we should understand our compiler better. Compiler manual can help you in understanding different options. We should know what our compiler can do for us and what it cannot do. So we do whatever it does not do for us and we will not do whatever it does for us. We have some different tools, which can help us to write our code in a better way. Like we can use tool purify to know where memory leak is coming in our code. Also we can use purecov to know how much coverage is done by our code, so that we can write code that has better coverage.

### 16.3 Optimization With Loop

### 16.3.1 Loop Unrolling

We can unroll small loops. Let us take an example-

```
int a=5;
for(i=0;i<4;i++)
{
value[i]=a;
a=a+5;
}
```

This can be simply written like this-

```
int value[] = { 5, 10, 15, 20 };
```

at initialization time. Alternatively it can be written in between program like this-

```
value[0]=5;
value[1]=10;
value[2]=15;
value[3]=20;
```

This is obviously better than previous one but most of the times compiler does this automatically, but we can expect little bit advantage and even it will be better to make a habit of writing optimized code. You can get this advantage in matrix program.

### 16.3.2 Avoiding Calculations In Loops

We should avoid any calculation, which is more or less constant in value within the loop. The same thing is true for avoiding calculation or anything, which can be removed from inner loop.

```
for(i=0;i<10;i++)
{
    value[i]=b*(20-b/3*c%2)*1/2;
}
```

We can avoid this calculation and it can be written as-

```
a=b*(20-b/3*c%2)/2
for(i=0;i<10;i++)
{
    value[i]=a*1;
}
```

Always try to minimize things in inner loop because this can improve efficiency.

### 16.4 Fast Mathematics

### 16.4.1 Avoid Unnecessary Integer Division

We know that division operation is slow so we should try to minimize the division operations. Let us take an example-

```
int a, b, c, d;
d = a/b/c;
```

This division operation can be eliminated as-

```
d=a/(b*c);
```

Multiplication operation is more effective than division operation. So we should try to convert division operation to multiplication.

### 16.4.2 Multiplication And Division by Power Of 2

We know that base of computer understanding is binary( 0 or 1) i.e. base of 2. So we always need to do multiplication and division operations for numbers which are power of 2. One way is to do simple
