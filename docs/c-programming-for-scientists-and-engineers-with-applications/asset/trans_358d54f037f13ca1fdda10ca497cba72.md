

## 第4 章

## 第4.1.3 节

+ 1. a. false
   b. true
   c. true
   d. true
   e. false
   f. true
   g. true
   h. true
   i. false
2. a. true
   b. true
   c. true
   d. true
   e. true
3. a. true
   b. true
   c. false
   d. true
4. a. true
   b. true
   c. true
   d. true

## 第4.2.4 节

+ 1. a. false
   b. true
   c. true
d. false
e. true
f. true
g. true

```c
if(c1) {
  if(c2) {
    stmt3;
  } else
    stmt2;
}
else
  stmt1;
```

3. a.

![](img/8356e6c3bfe3b10354682c60b1e74b1d_778_0.png)

```c
if(x > 25)
y += 20;
```

b.

![](img/8356e6c3bfe3b10354682c60b1e74b1d_778_1.png)

```c
if(z < 15)
y += x;
```

## 760 附录 C

c.

![](img/8356e6c3bfe3b10354682c60b1e74b1d_779_0.png)

```c
if(n == 40)
    scanf("%d %d d", &l, &r);
```

d.

![](img/8356e6c3bfe3b10354682c60b1e74b1d_779_1.png)

```c
if(p >= r)
    r++;
```

+ 4. a. if(stress > 50000)
{
    printf("stress = %8d\n", stress);
    printf("This stress is greater than 50,000\n");
}

+ b. if(sales > 10000)
    pay = pay + 0.05 * pay;

+ c. if(sales > 150000)
    pay = pay + 0.20 * pay;
else{
    if(sales > 100000)
        pay = pay + .15 * pay;
    else{
        if(sales > 50000)
            pay = pay + .10 * pay;
    }
}

```c
5. a. if(a == 0)
    printf("not a quadratic equation\n");
else
{
    d = b * b - 4.0 * a * c;
    if(d < 0.0)
        printf("Roots are complex");
    else
    {
        x1 = (-b + sqrt(d) / (2.0 * a));
        x2 = (-b - sqrt(d) / (2.0 * a));
        printf("Roots are: %f and %f", x1, x2);
    }
}
```

```c
b. if(sales >= 100000)
    comm = 0.25 * sales;
else
    comm = 0.15 * sales;
    printf("Sales = %d commission = %10.2f", sales, comm);
```

```c
c. s = 0.5 * (a + b + c)
    area = sqrt(s * (s - a) * (s - b) * (s - c));
    printf("Sides are %f %f %f Area is %f", a, b, c, area);
if(c * c == a * a + b * b) printf("This is a right triangle.");
```

## 第4.3.4 节

+ 1. a. true
b. true
c. true
d. true
e. true
f. true

+ 2. 不应该是分号；结束结束。
    b. 循环不会执行，因为终止条件为假。
    c. 循环不会终止，因为终止条件大于初始值且索引 i 正在递减。
    d. 在本应有分号的地方使用了逗号。

e. 嵌套的内部和外部循环使用了相同的索引变量。

f. 嵌套的内部和外部循环使用了相同的索引变量。

3. a. 在 for 循环 $i=0$ 内部

+ 在 for 循环 $i=1$ 内部
在 for 循环 $i=2$ 内部
在 for 循环 $i=3$ 内部
在 for 循环 $i=4$ 外部

b. $i=5$

+ $i=4$
$i=3$
$i=2$
$i=1$
在 for 循环 $i=0$ 外部

c. 在循环 $i=0$ 内部

+ 在循环 $i=1$ 内部
在循环 $i=2$ 内部
在循环 $i=3$ 内部
在循环 $i=4$ 外部
和 = 6

4. a. $i=0\ j=0$

+ $i=0\ j=1$
$i=0\ j=2$
$i=1\ j=0$
$i=1\ j=2$

b. $i=0$

+ $j=0$
$j=1$
$j=2$
在 $j=3$ 外部
$i=1$

j = 0
j = 1
j = 2
在 j = 3 外部
在 i = 2 外部

## 第4.4.3 节

+ 1. a. true
b. false
c. true
d. false
+ 2. ![](img/8356e6c3bfe3b10354682c60b1e74b1d_782_0.png)

## 第5 章

## 第5.1.3 节

+ 1. a. true
b. false
c. true
d. true
e. false
f. false
2. a. 函数描述
b. true
d. true
e. false
f. false
3. 它们是独立的。
4. 以上是模块的函数。
5. 作为独立模块编写的程序
6. 通过 return 语句返回值的函数
7. 通过参数列表返回值的函数

## 第5.2.5 节

+ 1. a. false
b. true
c. true
d. false
e. false
f. true
g. true
h. false
i. true
j. true
k. false
+ 2. a. float(int, int, float);
   b. float(int1, int2, float);
   c. void(double, double, int);
   d. void(double1, double2, int);

+ 3. a. 缺少分号。
   缺少参数类型。
   缺少分号和返回类型。
   b. 不应该有分号。
   缺少参数类型。
   缺少返回类型。
   c. main 可以调用全局函数 func1 和局部函数 func2
   d. main 只能调用局部函数 func2
   func2 可以调用全局函数 func1。
+ 4. 执行顺序从 Main 开始
Function1 返回到 Main
Function5 返回到 Function2
Function6 返回到 Function2
Function3 返回到 Main
Function4 返回到 Main
Function5 返回到 Function7

## 附录 C

Function6 返回到 Function7
Function7 返回到 Function4
Function8 返回到 Function4
在 Main 处结束

函数范围：
Function1, Function2, Function3 和 Function4 必须是全局的或局部的。
Function5 和 Function6 必须是全局的。
Function7 和 Function8 必须是全局的或局部的。

## 第5.3.3 节

+ 1. a. true
b. true
c. true
d. true
e. true
f. true
g. true
h. true
a. int(int, int, int);
b. float(float, float, *);
a. int(int, int, int);

```c
int largest(n1, n2, n3)
{
  int max;
  max = n1;
  if(max < n2)
    max = n2;
```

```c
if(max < n3)
max = n3;
return;
}
```

```c
b. void funcmax(int, int, int, *);

void funcmax(a, b, c, min);
{
*min = a;
*max = a;
if(*min > b)
*min = b;
if(*max < b)
*max = b;
if(*min > c)
*min = c;
if(*max < c)
*max = c;
return;
}
```

## 第5.4.3 节

+ 1. a. true
b. true
c. true
d. true
e.. false
+ 2. a. int main()
{
void angle(int *, int *);
int a, b, c;
angle(&a, &b, &c);
}

```c
void angle(s1, s2, s3)
{
    scanf("%d %d", s1, s3);
    return;
}
```

```c
b. void weeksales(id, sales)
{
    scanf("%d %f", id, sales);
    return;
}
```

```c
c. void getoutput(id, sales, comm)
{
    printf("Salesman: %d Sales: %10.2f Commission: %10.2f", id, sales, comm);
    return;
}
```

## 第5.5.5.3 节

+ 1. a. true
b. true
c. true

```c
void fibonacci(a, b, n, count)
{
    if (a==0)
    {
        count = 0;
        b = 1;
    }
    printf("%d", b);
    count++;
    if(count < n)
        fibonacci(b, a + b, n, count);
    return;
}
```

```c
int funccomb(n, k)
{
    int comb;
    if(n == 1 || k == 1)
        comb = 1;
}
else if(n > 1 && k > 1 && k <= n)
comb = funccomb(n - 1, k - 1) + funccomb(n - 1, k);
else
    printf("error in data");
    return comb;
}
```

## 第6 章

## 第6.1.4 节

+ 1. a. true
b. true
c. true
d. false
e. true
2. a. x=5
nx=15
x=25
x=30
x=50
b. in main x=5
in main x=15
in main x=25
in main x=30
in main x=50
3. 在 main x=5 必须是全局的或局部的。
in main x=15 不是一个值。
in main x=25 不是一个值。
in main x=30 不是一个值。
in main x=50 不是一个值。

## 第6.2.5 节

+ 1. a. false
b. true
c. true
d. false
e. false
f. true
g. true
2. a. int func(int, int, int);
b. float func(float, float, *);
a. int(int, int, int);

## 第6.3.2 节

+ 1. a. true
b. false
c. true
d. false
e. false
f. true
g. true
h. false
i. true
j. true
k. false
+ 2. a. float(int, int, float);
   b. float(int1, int2, float);
   c. void(double, double, int);
   d. void(double1, double2, int);

+ 3. a. 缺少分号。
   缺少参数类型。
   缺少分号和返回类型。
   b. 不应该有分号。
   缺少参数类型。
   缺少返回类型。
   c. main 可以调用全局函数 func1 和局部函数 func2
   d. main 只能调用局部函数 func2
   func2 可以调用全局函数 func1。

## 第7.1.3 节

+ 1. a. true
b. false
c. true
d. true
e. false
f. false
g. true
h. true
a. int(int, int, int);
b. float(float, float, *);
a. int(int, int, int);

```c
2. FILE *inptr;
inptr = fopen("filearrayin.dat", "r");
for(i = 0; i < 5; i++)
  fscanf(inptr, "%d", &a[i]);
```

```c
3. for(i = 4; i > 0; i--)
  scanf("%f", &a[i]);
```

```c
4. for(i = 0; i < 5; i++)
  scanf("%d %d", &x[i], &y[i]);
```

