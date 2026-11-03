

在所有出现的位置输出数量相等的“*”。

```
char ch;
printf("Enter text: ");
while((ch=getch())!='\r')
    printf("*");
```

## 4. 编写一个程序，将类似“124”的字符串转换为整数124。

```
char str[6];
int num= 0, i;
printf("Enter a string containing a number:");
scanf("%s",str);
for(i=0; str[i]!='\0'; i++)
{
    if(str[i]>=48 && str[i]<=57)
        num = num*10+(str[i]-48);
    else
    {
        printf("Not a valid string");
        getch();
        return;
    }
}
printf("\nThe number is: %d\n",num);
```

训练说明：函数 atoi 也能将字符串转换为整数。

## 下面程序的输出是什么？

| 1. | 7. |
|---|---|
| char c[2]= "A";<br>printf("%c",c[0]);<br>printf("%s",c);<br>输出：A A<br>从第一个 printf( ) 输出‘A’，因为数组大小为2，所以‘A’存储在第0个位置，而‘\0’(NULL)存储在第1个位置。使用第二个 printf( ) 时，输出也为‘A’，因为整个字符串（即"A"）会被打印出来。 | char str1[] = {'H','e','l','l','o',0};<br>char str2[] = "Hello";<br>printf("\n%s",str1);<br>printf("\n%s",str2);<br>输出：Hello Hello<br>因为在第一个字符串中，最后一个字符是0，也就是NULL(`\0`)字符的ASCII码。当打印str1时，会打印整个字符串"Hello"；同样str2也会被打印出来。 |

### 2. char s[] = "Get organized! learn c!!"
```
char s[] = "Get organized! learn c!!";
printf("\n%s",&s[2]);
printf("\n%s",s);
printf("\n%s",&s);
printf("\n%c",s[2]);
```
输出：
t
organized! learn c!!
Get organized! learn c!!
Get organized! learn c!!
t

通过第一个 printf( )，打印的是"t organized! learn c!!"，因为我们传入的是&s[2]来打印字符串，所以打印会从字符串的第3个字符开始。因为当只使用字符串名称时，它包含的是基地址，字符串打印会从基字符开始。

通过第二个 printf( )，这里使用了字符串名称，所以会打印整个字符串。

通过第三个 printf( )，传入的是字符串的地址（因为没有使用下标或索引，所以是基地址），与第二个 printf( ) 相同，因此会打印整个字符串。

通过最后一个 printf( )，只打印第3个字符，因为这里使用了%c格式说明符，并且打印列表中使用的是s[2]，它指向第3个字符。

### 3. printf("%c","Harry"[4]);

### 8. printf(5+"Good Morning");

输出：Morning。

这里编译器会理解上述 printf 应当从字符串的第5个字符开始打印。

### 9. printf("\n%d %d %d",sizeof('3'),sizeof("3"),sizeof(3));

输出：2 2 2

因为第一个 sizeof 包含一个字符，但在C语言中，字符会被转换为其ASCII值，编译器将其视为int，所以占用2字节。第二个 sizeof 是一个只包含单个字符的字符串，但C编译器会在每个字符串末尾自动加上空字符，所以上述字符串将包含2个字符，占用2字节。第三个 sizeof 包含3，这是一个整数值，占用2字节。

```
char a[8] ="Rhombus";
int i;
for(i = 0; i<=7; i++)
printf("\n%d",*a);
a++;
```

输出：Error。因为数组'a'不能被递增。

### 11. main()
**输出：y。**
因为当我们打印s[4]时，它会打印字符串的第5个字符。这里我们在s的位置使用了字符串“matrix”，类似地，它会打印该字符串的第5个字符，即r。

```
char a[] = {'M','A','T','R','I','X'};
int i;
for(i = 0;i<=5;i++)
printf("%c",a[i]);
```

每次在条件为真时打印数组的第i个元素。因为计数器从0开始，所以打印从第0个元素开始，一直到第5个元素。这样字符串“MATRIX”的每个字符都会被打印，并由行分隔。

```
main()
{
char s[7]="Strings";
printf("%s",s);
}
```

不可预测。这里s[]被声明为7字符数组，但其中存储了8字符的字符串。这会导致超出为数组保留的第7字节之后的内存被“0”覆盖。总是有可能……

```
{
char string[] = "Author Harry";
int a=5;
printf("a>0?%20s":"%s",string);
}
```

**输出：Author Harry**

```
main()
{
printf(5+"Computers");
}
```

**输出：ters**

```
main()
{
char s1="Matrix";
char s2="Computers";
if(s1 == s2)
printf("Equal");
else
printf("Unequal");
}
```

**输出：Unequal**

```
main()
{
printf("%c", "Matrix"[4]);
}
```

**输出：i**
15. 对于读取多词字符串，以下哪个更合适？
gets()
scanf()
puts()

输出：gets()

重要的内容会被覆盖，这可能会不安全。

6. 你怎样在屏幕上输出 \n？

输出：“\n”

## 填空题：
- 1. “A”是一个________，而‘A’是一个________。
- 2. 字符串以________结尾，写成__。
- 3. 数组 char name[10] 最多可以包含____个字符。
- 4. 数组元素总是存储在________的内存位置中。

答案：
- 1. 字符串 字符
- 2. 空字符 \0
- 3. 9
- 4. 连续的

## 实验练习 -
- 1. 编写程序连接两个字符串。
- 2. 编写程序比较两个字符串。
- 3. 编写程序从键盘读取一行文本，并在屏幕上显示以下信息：
- 1. 单词数
- 2. 字符数。
- 4. 编写程序统计用户输入字符串的长度。
- 5. 编写程序将一个字符串复制到另一个字符串。
- 6. 编写程序将两个字符串连接到第三个字符串中。
- 7. 编写程序将一个字符串以相反顺序复制到另一个字符串中。
- 8. 编写程序检查用户输入的字符串是否是回文。
- 9. 编写程序将字符串转换为小写。
- 10. 编写程序删除用户输入字符串中的所有前导空格。
- 11. 编写程序打印输入字符串的所有循环移位。例如，单词" space "的旋转为：space paces acesp cespa espac
- 12. 编写程序输入任意字符串，并以相反顺序打印。
- 13. 编写程序输入一个字符串和一个待搜索的字符，并打印该字符在字符串中出现的频率。
- 14. 编写程序输入一个字符串，并打印该字符串中出现次数最多的字符。
- 15. 编写程序输入任意字符串，并打印每个字符在字符串中出现的频率。出现多次的字符只需在输出中显示一次，并附带频率值。
- 16. 编写程序显示输入的字符串中最长的单词（长度最大的单词）。
- 17. 编写程序输入任意姓名，并按照以下格式打印：输入：shruti 输出：s sh shr shru shrut shruti
- 18. 编写程序输入任意句子，并将每个单词的字符分别按字母顺序排列，然后打印句子。例如，输入：computer program in basic. 输出：cemoprtu agmoprr in abc is.
- 19. 编写程序使用一个下标变量接收用户输入的40名学生的计算机科学成绩，并按升序在一列中打印这些成绩。
- 20. 编写程序接收用户输入的谚语（如“failures are the pillars of success.”），然后输出该谚语中出现的元音字母的频率。
21. 一家城市酒店有10层楼（1到10层），每层有60个房间。使用一维数组存储住户姓名，使用二维数组 place(a, b) 表示房间位置，其中a和b分别代表楼层和房间号。编写程序在输入住户姓名和房间号后为其分配房间。

22. 编写程序输入文本，并打印包含元音字母数量最多的单词。

23. 编写程序将字符串中两个或多个连续空格替换为单个空格。例如，如果输入是：grim return to the planet of apes!! 输出应为：grim return to the planet of apes!!

![](img/3a2b6e5e90a58a56458b0539952c0cd2_153_0.png)

![](img/3a2b6e5e90a58a56458b0539952c0cd2_154_0.png)

> 你想讨论我发给你的软件中的故障吗？不，周二不行——那“永远”怎么样——永远也不行吗？

