
```
{ int i; float sum = 0;
 for (i = 1; i <= 20; i++) sum = sum + sqrt(i);
 printf ("\n The sum of the roots is s = %f", sum);
 }
```

该程序的流程图由下图表示。

![](img/a9b60755682bc3cf43c528c679efbca7_97_0.png)

## 练习

- 1) 编写一个简单的程序求解一次绝对值方程 |a*x + b| = k，其中参数 a、b 和 k（k > 0）从键盘输入，且 a 不为零。注意，求解需要去掉绝对值符号得到两个不带模的一次方程：i) a*x+b = -k 和 ii) a*x+b = +k。
- 2) 编写一个程序，在第一行打印一次符号 `@`，第二行打印两次，第三行打印三次，依此类推，直到对键盘提供的 n 数打印 n 次。
- 3) 创建一个程序接收摄氏温度值（C），将其转换为华氏温度（F）并打印，已知公式 C/5 = (F-32)/9。当然需要求解 F。
- 4) 编写一个程序从键盘读取两个直角边 x 和 y 的值，计算三角形的斜边 a，以及由第一条直角边（长度为 x）与斜边形成的角度的正弦和余弦（记住正弦为 y/a，余弦为 x/a），打印这三个结果。
- 5) 编写一个程序，对键盘输入的给定行数 n，每行打印整数个随机数量的符号 ‘$’（参见第 9 章的最后一个迷你程序以操作 rand() 函数）。
- 6) 编写一个程序打印质量和能量值的表格，使用质能等价方程 E = mc²。光速 c 为 3.0E+8 m/s，因此 c² 为 9.0E+16 m²/s²。程序应在表头后打印十行，第一列为质量（kg），然后为能量（焦耳 J），从键盘提供的质量值 m 开始，每次递增 1 kg，例如，若 m = 16，表格将显示 16、17、18、... 24 的计算结果。
- 7) 创建一个用于测量细菌种群增长的程序，其由指数公式 N(t)= N₀*2^(t/d) 给出。在此情况下，增长率 r = 2，双倍时间 d = 5min 已知。公式则为 N=N₀*2^(t/5)。程序要求用户从键盘提供初始细菌数 N₀ 和等待时间 t（分钟），以得到细菌数 N 的结果。
- 8) 编写一个程序计算复利投资的投资时间 t（月数），月利率为 r。用户必须通过键盘提供利率 r、本金 P 和期望金额 A。复利公式为 A = P(1+r)^t，由此求出 t，对等式两边取对数得到 log(A/P) = t*log(1+r)，因此 t = log(A/P)/log(1+r)。
- 9) 我们知道三个非共线点确定一个抛物线，或二次方程。我们也可以仅用两个具有不同纵坐标的点来确定二次方程，其中一个点为顶点。当另一个点为零纵坐标或截距 (0, c) 时则更简单。这里要求读者构建一个程序，给出二次方程 y=a*x²+b*x+c，其中截距 c 的值以及顶点坐标 xᵥ 和 yᵥ 从键盘给出，已知 xᵥ = -b/(2*a) 且 yᵥ = -(b²-4*a*c)/(4*a)。由于 c 值已给出，我们只需计算 a 和 b（只需在 xᵥ 中解出 a 并将其值代入 yᵥ 以求得 b）。
- 10) 开发一个程序计算从键盘获得的给定整数 n 以内的质数序列。质数是指恰好有两个因子，即它本身和 1 的数。注意，程序中的测试无需除以大于 n 平方根的整数，因为如果更大，则因子的另一数会更小且已在升序测试中被检验。
- 11) 创建一个程序计算通过键盘给出的两个整数 n 和 p 的最小公倍数（LCM）。这两个整数必须按升序用质数的结果除，重复用商进行操作，直到两个商都为 1。如果对于给定的质数，一个能被整除而另一个不能，则不能被整除的那个保持不变，就像它是商一样。成功除法的质数的乘积，即余数为零的那些，将为 LCM。
- 12) 在开发计算伯努利数的程序时，历史上第一个程序，Ada Byron 意识到，从下面公式中首先显示的级数中，她可以分离出 Bₙ 的值，如第二公式 II 所示，即伯努利数。这里的挑战是构建一个程序计算并打印这些数的结果，直到给定值，例如 n = 10，即数字 B₀、B₁、B₂、B₃、… B₁₀，从 B₀ = 1 开始。读者不应惊讶于 B₂ 之后的偶数下标都为零，因为那是该序列的性质。结果应以分数形式给出，这是该序列的默认值，顺便说一下，Ada 公式已经有分母 n+1。我们应回忆，m 个元素取 k 个的组合数由 C(m, k) = m! / (k!(m-k)!) 给出，因此 C(n+1, k) = (n+1)! / (k!(n+1-k)!)。你可以使用示例程序 #13A 的阶乘函数，但可能更适合使用更简单的方法，因为 m 个元素取 k 个的组合是 m-i 的乘积算子，i 从零到 k-1，除以 k-i 的乘积算子，i 从零到 k-1。Ada 说，由于机器的限制，她在 Bₙ 公式前省略了负号。有了现在的机器我们可以处理符号，将分子中的值 1 改为 -1。你还需要构建一个小的加法例程，并利用 HCF（示例程序 #9B）来简化结果中出现的分数。

(I) x/(e^x - 1) = Σ_{n≥0} Bₙ / n! xⁿ

(II) Bₙ = 1/(n+1) Σ_{k=0}^{n} (-1)^k C(n+1, k) B_k

## 附录 A

### 保留字示例

本节为 ANSI C 中的 32 个保留字提供了迷你程序。它们至少都需要以 #include <stdio.h> 开始。

#### auto

```
void Algar() {auto int i; for(i=0;i<10;i++) printf("%d",i);}
main() {Algar();}
```

#### break

```
main() {char c;int i; for(i=1;i<=1000;i++){c=getchar();
if(c=='\n') break; else printf("\a");}}
```

#### case

```
main() {char c; puts("\n Type uppercase vowel: "); c=getchar();switch(c) {case 'A':puts("Ann");break; case 'E': puts("Eve");break;case 'I': puts("Ivy");break; default: puts("O, U, Y or Error.");}}
```

#### char

```
main() {int i,j;char k[20],o[20];puts(" Type number:"); gets(k);puts("Other: ");gets(o);i=atoi(k);j=atoi(o); printf("\n%d %d",div(i,j));}
```

#### const

(注：使用 math.h)

```
main() {float x;const float pi=3.14159;x=pi/4; printf("\ncos(%f)=%f\n",x,cos(x));}
```

#### continue

```
main() {int k;while(k<10){ puts("\n Type number lower than 10 (greater to exit): "); scanf("%d",&k);printf(" Square: %d",k*k); if(k>1) continue; } }
```

#### default

```
main() {int n; puts("\n Press even digit: "); scanf("%d",&n); switch(n) {case 0: puts("Zero.");break; case 2: puts("Two."); break; default: puts("Greater than 3, or Error.");}}
```

#### do

```
main() {int k,i=1; puts(" Press odd number: "); scanf("%d",&k); do{printf(" %0d",i);i+=2;}while(i<=k);}
```

#### double

```
main() {double x; float t=1.256; x=tan(t); printf("\ntan(%f)=%f\n",t,x);}
```

#### else

```
main() {int k; srand(time(NULL)); k=rand();if(k<16383) printf("\nLower.");else printf("\nGreater.");}
```

#### enum

```
main() {enum Elem{water,fire,earth=5,air};int i;
    enum Elem subs;subs=fire;i=subs+1;
    printf("\nFire: %d, Fire+1: %d, Air: %d.",subs,i,air);}
```

#### extern

```
int Q(k){k=k*k; return k;}
main(){extern int k; int n;    puts("\nType number:");
    scanf("\n %d",&n);printf("\n Q=%d",Q(n));}
```

#### float

```
main(){float t,v;srand(time(NULL));v=rand();t=v/32767;
    printf("\nProbab=%f",t);}
```

#### for

```
main(){char c; int i,n; puts("\nType multiple of 5: ");
    scanf("%d",&n);for(i=0;i<=n;i+=5) printf(" %d",i);}
```

#### goto

```
main(){char c; puts("Type something ('e' to exit): ");
    REDO: c=getchar();putchar(c); if(c!='e') goto REDO;}
```

#### if

```
main(){if('a'<'b')        printf("\nI can compare characters by ASCII value. Ex: a<b.");}
```

#### int

```
int main() {int i; for(i=60;i>0;i--)printf(" %d",i);}
```

#### long

```
main(){long n; int i; for(i=0;i<=5000;i+=25){n=10*i;
    printf("%d ",n);}}
```

#### register

(注：使用 math.h)

```
main(){register int k; float y; for(k=0;k<41;k++) {
    y=sqrt(k); printf(" %d %1.1f",k,y);}}
```

#### return
