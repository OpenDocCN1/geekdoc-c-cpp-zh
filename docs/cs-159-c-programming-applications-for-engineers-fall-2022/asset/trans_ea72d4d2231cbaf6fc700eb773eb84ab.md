

## 使用以下代码段解决第 28–30 题

```c
int main(void)
{
   printf("Result #1: %.2lf\n", CtoF(FtoC(104)));
   printf("Result #2: %.2lf\n", FtoC(CtoF(45)));
   return(0);
}

double FtoC(double F)
{
   return(5 / 9 * (F - 32));
}

double CtoF(double C)
{
   return(C * 9 / 5 + 32);
}
```

- 28. 生成的第一行输出是什么？
- A) Result #1: 32.00
- B) Result #1: 72.00
- C) Result #1: 104.00
- D) 以上皆非。

- 29. 生成的第二行输出是什么？
- A) Result #2: 0.00
- B) Result #2: 25.00
- C) Result #2: 45.00
- D) 以上皆非。

- 30. 关于上述代码段中数据类型转换，以下哪项陈述为真？
- A) 第 15 行存在赋值类型转换。
- B) 第 20 行存在显式类型转换。
- C) 字面常量 45 在传递给第 9 行的 FtoC 时会安全转换为 double。
- D) 以上皆非。

31. 下面给出的公式可用于近似 x 的阶乘。

![](img/e25602f5611b32eaf448a241a988eedc_57_0.png)

以下哪项表达式正确表示了上述公式？

- A) pow(x, x) * pow(M_E, -x) * pow(( 2 * x + 1 / 3 ) * M_PI, 1 / 2)
- B) pow(x, x) * pow(M_E, -x) * sqrt(( 2 * x + (double) (1 / 3) ) * M_PI)
- C) pow(x, x) * pow(M_E, -x) * sqrt(( 2 * x + 1.0 / 3.0 ) * M_PI)
- D) 以上皆非。

## 使用以下代码段解决第 32–33 题

```c
#define SIZE 10

int main(void)
{
    int result = 0;
    int *data;
    data = (int*)malloc(sizeof(int) * SIZE);
    result = populateArray(data);

    printf("result 1 = %d\n", result);
    printf("result 2 = %d\n", *data + SIZE);

    return(0);
}

int populateArray(int *array)
{
    int i = 0;
    int result = 0;

    while(i < SIZE)
    {
        *(array + i) = 2 * i - 1;
        result += *(array + i);
        i++;
    }

    return(result);
}
```

- 32. 上述代码段生成的第一行输出是以下哪项？
- A) result 1 = 80
- B) result 1 = 100
- C) result 1 = 90
- D) 以上皆非。

- 33. 上述代码段生成的第二行输出是以下哪项？
- A) result 2 = 11
- B) result 2 = 10
- C) result 2 = 9
- D) 以上皆非。

- 34. 关于 malloc 函数，以下哪项陈述为假？
- A) 动态内存分配函数由 stdlib.h 库提供。
- B) 新分配内存的起始地址由 malloc 函数返回。
- C) malloc 函数分配的内存中所有元素都初始化为零。
- D) 以上皆非。

- 35. 根据 C 语言规则，以下哪项是有效标识符？
- A) score-two
- B) 2ndScore
- C) score_No2
- D) 以上皆非。

## 使用以下代码段解决第 36–37 题

```c
int main(void)
{
    int index;
    int data[10] = {13, 3, 4, 9, 11, 10, 12, 1, 15, 10};
    randomArray(data);
    index = data[8] % 10;
    printf("result 1 = %d\n", data[index]);
    index = data[5] % 10;
    printf("result 2 = %d\n", *(data + index));
    return(0);
}
void randomArray(int *data)
{
    int i;
    for(i = 0; i < 9; i++)
    {
        *(data + i) = data[i] % 2 ? data[i] / 2 : data[i] * 2;
    }
}
```

- 36. 上述程序生成的第一行输出是以下哪项？
- A) result 1 = 0
- B) result 1 = 6
- C) result 1 = 20
- D) 以上皆非。

- 37. 上述程序生成的第二行输出是以下哪项？
- A) result 2 = 5
- B) result 2 = 13
- C) result 2 = 6
- D) 以上皆非。

- 38. 关于指针变量，以下哪项陈述为假？
- A) 间接运算符 (*) 是一元运算符，其操作数必须是数据变量。
- B) 间接运算符和地址运算符互为逆运算，在表达式中组合时会相互抵消。
- C) 指针变量存储的内存地址在程序执行期间可以改变。
- D) 以上皆非。

39. 在下面的数组上使用二分查找算法，目标值为 17 时，`first` 和 `last` 变量的最终值是以下哪项？

```
18 21 24 26 28 35 38 40 49 49 49 55
```

| A | B | C | D |
|---|---|---|---|
| first = 1 last = 0 | first = 0 last = 0 | first = 0 last = -1 | 以上皆非。 |

40. 在下面的数组上使用二分查找算法，目标值为 41 时，`first` 和 `last` 变量的最终值是以下哪项？

```
18 21 24 26 28 35 38 40 49 49 49 55
```

| A | B | C | D |
|---|---|---|---|
| first = 9 last = 8 | first = 8 last = 8 | first = 8 last = 7 | 以上皆非。 |

41. 在下面的数组上使用二分查找算法，目标值为 49 时，返回的 `index` 是以下哪项？

```
18 21 24 26 28 35 38 40 49 49 49 55
```

| A | B | C | D |
|---|---|---|---|
| index = 8 | index = 9 | index = 10 | 以上皆非。 |

42. 关于本学期介绍的搜索算法，以下哪项陈述为假？

- A) 顺序查找有可能在数组中比二分查找更快地定位目标。
- B) 在每次不成功的比较后，二分查找都会排除数组中大约一半的剩余元素作为目标的潜在位置。
- C) 在有序数组上使用顺序查找时，可能在不比较数组中每个元素的情况下确定目标值不存在。
- D) 以上皆非。

43. 给定原始数组如下：

```
10 21 49 55 65 28
```

以及经过排序算法两趟后的数组：

```
10 21 49 28 55 65
```

应用了以下哪种算法？

- A) 选择排序。
- B) 冒泡排序。
- C) 插入排序。
- D) 以上多于一项。

44. 给定下列数组：

```
18 33 13 8 25 19
```

经过选择排序算法两趟后，以下哪项不是数组的可能配置？

- A) {33, 25, 13, 8, 18, 19}
- B) {18, 33, 25, 19, 13, 8}
- C) {19, 18, 13, 8, 25, 33}
- D) 以上皆非。

```c
int main(void)
{
   int list[10] = {10, 2, 4, 3, 6, 8, 7, 9, 5, 1};
   sortArray(list, 10);
   return(0);
}

void sortArray(int list[], int last)
{
   int counter;
   int temp;
   int located;
   int current;

   for(current = 1; current < last; current++)
   {
      located = 0;
      temp = list[current];
      counter = current - 1;

      while(counter >= 0 && !located)
      {
         if(temp < list[counter])
         {
            list[counter + 1] = list[counter];
            counter--;
         }
         else
         {
            located = 1;
         }
         list[counter + 1] = temp;
      }
   }
}
```

- 45. 上述程序实现的是以下哪种排序算法？
- A) 选择排序。
- B) 冒泡排序。
- C) 插入排序。
- D) 以上皆非。

- 46. 关于上述程序排序过程两趟后数组中的数据，以下哪项陈述为真？
- A) 两趟后索引 0 处的元素是 10。
- B) 两趟后索引 8 处的元素是 5。
- C) 两趟后索引 2 处的元素是 2。
- D) 以上皆非。

## 使用以下代码段解决第 47–48 题

```c
int a = 0;
int b = 3;

int *x;
int *y;
int *z;

x = &a;
y = &b;

z = x;
*z = 2;

x = y;
*x = 1;

printf("total = %d\n", *y + *z);

y = z;
*y = 4;

printf("final = %d\n", a + b);
```

- 47. 上述代码段生成的第一行输出是以下哪项？
- A) total = 2
- B) total = 3
- C) total = 4
- D) 以上皆非。

- 48. 上述代码段生成的第二行输出是以下哪项？
- A) final = 6
- B) final = 5
- C) final = 7
- D) 以上皆非。

- 49. 以下哪项可用于永久更改变量的声明数据类型？
- A) 隐式类型转换。
- B) 显式类型转换。
- C) 赋值类型转换。
- D) 以上皆非。

- 50. 关于学期结束，以下哪项陈述为真？
- A) 对旧作业的复分要求或 Brightspace 错误必须在离开校园结束学期之前，将您的担忧打印出来并滑到教师办公室门下。
- B) 每个字母等级的最低分数线的任何更改将于星期二 5 月 10 日下午 5:00 前在 Brightspace 上公布。
- C) 成绩仅根据获得的分数计算；在分配课程成绩时不能考虑课程外的事项。
- D) 以上皆是！

