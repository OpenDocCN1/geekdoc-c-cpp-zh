

在以下每个赋值语句中，如果有值赋给给定变量，那么该值是什么？

```
7. c3 = c1 * c2;
```

```
10. r3 = real(c2) + imag(c2);
```

```
8. c3 = conj(c2);
```

```
11. c3 = r1;
```

```
9. c3 = complex<double>(r1, r2);
```

12. 对于问题7–11中声明的变量c3，应如何输入数据才能使输入语句`cin >> c3`赋给c3的值是复常数1.5 + 2.5i？

## 习题

### 7.3节

对于习题1–11，假设i1、i2和i3是int变量，r1、r2和r3是double变量，c1、c2和c3是char变量。当输入语句用给定的输入数据执行时，说明每个变量会被赋予什么值，或者解释为什么会出现错误。

```
1. cin >> i1 >> i2 >> i3
    >> r1 >> r2 >> r3;
```

输入：1   2   3
       4 5.5 6.6

```
2. cin >> i1 >> i2 >> i3;
   cin >> r1 >> r2 >> r3;
```

输入：1
       2
       3
       4
       5
       6

```
3. cin >> i1 >> r1;
   cin >> i2 >> r2;
   cin >> i3 >> r3;
```

输入：1 2.2
       3 4.4
       5 6.6

```
4. cin >> i1 >> i2 >> i3
    >> r1 >> r2 >> r3;
```

输入：1 2.2
       3 4.4
       5 6.6

```
5. cin >> i1 >> c1 >> r1
    >> i2 >> c2 >> r2
    >> i3 >> c3 >> r3;
```

输入：1 2.2
       3 4.4
       5 6.6

```
6. cin >> noskipws
    >> i1 >> c1 >> r1
    >> i2 >> c2 >> r2
    >> i3 >> c3 >> r3;
```

输入：1 2.2
       3 4.4
       5 6.6

```
7. cin >> i1 >> c1 >> i2
    >> c2 >> i3 >> c3;
```

输入：1A 2B 3C

```
8. cin >> i1 >> i2 >> i3;
```

输入：012 345 678

```
9. cin >> dec >> i1 >> i2 >> i3;
```

输入：012 345 678

```
10. cin >> oct >> i1 >> i2 >> i3;
```

输入：012 345 678

```
11. cin >> hex >> i1 >> i2 >> i3;
```

输入：12 3A BC

对于习题12–20，假设alpha和beta是实变量，值分别为2567.392和0.004，num1和num2是整型变量，值分别为12和436。精确地给出每组语句产生的输出，或者解释为什么会出现错误。

```
12. cout << num2 << num2 + 1 << num2 + 2;
```

```
13. cout << num2 << setw(4) << num2 + 1 << num2 + 2;
```

```
14. cout << num1 << num1 + 1 << num1 + 2;
```

```
15. cout << oct << num1 << num1 + 1 << num1 + 2;
```

```
16. cout << showbase << oct << num1 << num1 + 1 << num1 + 2;
```

```
17. cout << hex << num1 << num1 + 1 << num1 + 2;
```

```
18. cout << showbase << hex << num1 << num1 + 1 << num1 + 2;
```

```
19. cout << fixed << showpoint << right
    << setw(9) << setprecision(3) << alpha << endl
    << setw(10) << setprecision(5) << beta << endl
    << setw(7) << setprecision(4) << beta << endl;
```

```
20. cout << scientific << showpoint << left
    << setprecision(1) << setw(10) << alpha << endl
    << setw(5) << beta << endl
    << "Tolerance:"
    << setw(12) << setprecision(3) << beta << endl;
```

对于习题21和22，假设i和j是整型变量，值分别为15和8；ch是字符变量，值为'c'；x和y是实变量，值分别为2559.50和8.015。精确地给出产生的输出，或者解释为什么会出现错误。

```
21. cout << setw(j) << setprecision(2)
    << fixed << showpoint << right
```

```
<< "New balance =" << x << ' ' << setw(i % 10) << ch << setw(j) << setprecision(j-6) << y << endl;
```

```
22. cout << "i =" << setw(i) << i << fixed << showpoint << right << "j =" << setw(j) << setprecision(j) << j << endl << setw(j) << i << ' ' << setw(i),<< j << endl;
```

对于习题23–26，假设n1和n2是整型变量，值分别为987和−6789；r1和r2是实变量，值分别为12.3456和−0.00246；ch是字符变量，值为'T'。对于每一题，编写一个使用这些变量和格式操纵符产生给定输出的输出语句。（这里显示的下划线只是为了帮助你确定间距。）

23. 12.3 T 987
-6789TTT-0.00246

24. 12.35 -0.0025
12.345600T***987

25. Values: 12.34560 and -0.00246

26. Observations: 12.3 and -0.0
Locations: 987 and 6789

### 7.4节

习题1–26假设有以下声明：

```
string s1,
    s2 = "row, row, row your boat",
    s3 = "row",
    s4 = "boat.";
```

对于习题1–21，求出表达式的值或解释为什么会出现错误。

- 1. s2[3]
- 2. s1.size() + s4.size()
- 3. s3 < s4
- 4. s3 <= s2
- 5. s3 + s4
- 6. "f1" + s4.substr(1,3) + " a " + s4
- 7. s2.substr(1,3)
- 8. s3.substr(1,3)
- 9. s2.find("ow", 1)
- 10. s2.find("ow", 2)
- 11. s2.find("ow", 12)
- 12. s2.rfind("ow", 12)
- 13. s2.rfind("ow", 11)
- 14. s2.rfind("ow", 1)
- 15. s2.find_first_of(s4,0)
- 16. s2.find_first_of(s4,2)
- 17. s2.find_first_not_of(s4,0)
- 18. s2.find_first_not_of(s4,1)
- 19. s2.find_last_of(s3, 22)
- 20. s2.find_last_of(s3, 19)
- 21. s2.find_last_not_of(s3, s2.size() - 1)

对于习题22–26，给出产生的输出，或解释为什么会出现错误。

```
22. int i = s2.find_last_of(s3, s2.size() - 1);
    cout << s2.substr(i, s2.size() - i) << endl;
```

```
23. s1 = s3 + s4;
    s1[0] = 'g';
    s1.replace(2, 2, " f1");
    cout << s1 << endl;
```

```
24. s1 = s2;
    s1.erase(3, 10);
    s1.insert(0, "Bor");
    cout << s1 + "?\n";
```

```
25. s1 = s2;
    s1[s1.find("b", 0)] = 'g';
    for (int i = 0; i <= 10; i += 5)
        s1[i] = 'm';
    cout << s1 << endl;
```

```
26. s1 = s2;
    int i;
    i = s1.find_first_of("aeiou", 0);
    while (i != string::npos)
    {
        s1.replace(i, 1, "xx");
        i = s1.find_first_of("aeiou", i + 1);
    }
}
cout << s1 << endl;
```

27. 给定字符串变量last_first的值为"Smith, Bill"，编写语句从last_first中提取名和姓，然后组合它们，使"Bill Smith"被赋给字符串变量first_last。

28. 编写一个函数，接受一个由名、中间名或中间字母首字母和姓组成的字符串对象，返回一个由姓、逗号、名和中间名首字母组成的字符串对象。例如，对于"John Quincy Doe"，函数应返回字符串"Doe, John Q."。

29. 编写一个函数，接受月份的数字并返回月份的名称。

30. 编写一个函数，接受月份的名称并返回月份的数字。

31. 编写一个函数，给定一个由大小写字母组成的字符串，返回该字符串全部小写的副本；再编写另一个函数，给定一个由大小写字母组成的字符串，返回该字符串全部大写的副本。（提示：使用for循环和cctype中提供的函数。）

32. 如果一个字符串反转字符顺序后不改变，则该字符串称为回文。例如：

madam

463364

ABLE WAS I ERE I SAW ELBA

都是回文。编写一个函数，给定一个字符串，如果是回文则返回true，否则返回false。

### 7.5节

对于习题1-12，已知 z = 1 + 2i 且 w = 3 - 4i，计算每个表达式。

- 1. z + w
- 2. z - w
- 3. z · w
- 4. z / w
- 5. z²

- 6. z̄
- 7. w̄
- 8. (z + z)/2
- 9. (z - z)/2

- 10. $z \cdot \bar{z}$
- 12. $\frac{z + w}{z - w}$
- 11. $\frac{1}{z}$

13.–24. 对 $z = 6 - 5i$ 和 $w = 5 + 12i$ 重复习题1–12。

25.–36. 对 $z = 1 + i$ 和 $w = 1 - i$ 重复习题1–12。

对于问题37–41，假设已执行以下声明：

```
double r1 = 2.5, r2 = 6.0, r3;
complex<double> c1 = complex<double>(1, -1),
                c2 = complex<double>(-3, 4),
                c3;
```

在以下每个赋值语句中，如果有值赋给给定变量，那么该值是什么？

- 37. c3 = c1 * c2;
- 38. c3 = conj(c2);
- 39. c3 = complex<double>(r1, r2);
- 40. r3 = real(c2) + imag(c2);
- 41. c3 = r1;

## 编程问题

7.2–7.4节

- 1. 编写一个驱动程序来测试习题27中的姓名转换函数。
- 2. 编写一个驱动程序来测试习题28中的姓名转换函数。
- 3. 编写一个程序打印个性化的竞赛信件，就像经常在邮件中收到的那种。它们可能具有类似于以下示例的格式。用户应在前三行输入三个字符串，然后程序打印带有下划线位置填充内容的信件。

```
Mr. John Q. Doe
123 SomeStreet
AnyTown, AnyState 12345

Dear Mr. Doe:

How would you like to see a brand new BMW parked in front of 123 SomeStreet in AnyTown, AnyState? Impossible, you say? No, it isn't, Mr. Doe. Simply keep the enclosed raffle ticket and validate it by sending a $100.00 tax-deductible political contribution and 10 from Shyster & Sons chewing tobacco. Not only will you become eligible for the drawing to be conducted
```

