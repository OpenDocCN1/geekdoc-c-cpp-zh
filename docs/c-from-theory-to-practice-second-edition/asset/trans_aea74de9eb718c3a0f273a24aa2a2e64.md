

## 20

## 复习题

### C.20.1 编写一个程序，读取其命令行参数并分配内存，将它们拼接成一个字符串并显示该字符串。

```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
int main(int argc, char *argv[])
{
    char *tot_str;
    int i, tot_chars;
    if(argc == 1) /* Check if the command line contains only the name of the program. */
    {
        printf("Missing arguments ...\n");
        exit(EXIT_FAILURE);
    }
    tot_chars = 0; /* It counts the characters of all arguments. */
    for(i = 1; i < argc; i++) /* Remember that argv[1] points to the first argument, argv[2] to the second one, and so on. argv[0] points to the name of the program. */
        tot_chars += strlen(argv[i]);
    tot_str = (char*) malloc(tot_chars+1); /* Allocate an extra place for the null character. */
    if(tot_str == NULL)
    {
        printf("Error: Not available memory\n");
        exit(EXIT_FAILURE);
    }
    *tot_str = '\0'; /* Store the null character. */
    for(i = 1; i < argc; i++)
        strcat(tot_str, argv[i]);
    printf("The merged string is: %s\n", tot_str);
    free(tot_str);
    return 0;
}
```

### C.20.2 下面程序的输出是什么？

```c
#include <stdio.h>
void test(int **tmp, int i);
int main(void)
{
    int **tmp, *ptr, i, arr[] = {10, 20, 30};
    ptr = arr;
    tmp = &ptr;
    for(i = 0; i < 3; i++)
    {
        test(tmp, i);
        printf("%d ", arr[i]);
    }
    return 0;
}
```

```c
void test(int **tmp, int i)
{
    *(*(tmp + i)) += 50;
}
```

答案：tmp 被声明为一个指向整型指针的指针。语句 tmp = &ptr; 使 tmp 指向 ptr 的地址，而 ptr 指向数组 arr 第一个元素的地址。由于 *tmp 等于 ptr，我们有 *(tmp+i) = *(ptr+i) = *(arr+i) = arr[i]。因此，每次调用 test() 都会将数组 arr 的相应元素增加 50，程序显示：60 70 80。

### C.20.3 编写一个程序，读取 100 位游客对“你在希腊最享受什么？”这一问题的偏好排序：

- 1. 自然多样性
- 2. 气候
- 3. 岛屿
- 4. 夜生活
- 5. 古迹
- 6. 当地人
- 7. 美食

每个答案根据其排序位置获得 1–7 分。第一个答案得 7 分，第二个得 6 分，最后一个得 1 分。例如，如果两位游客回答如下：

| 第一位游客 | 第二位游客 |
|---|---|
| 5（7分） | 3（7分） |
| 4（6分） | 7（6分） |
| 6（5分） | 2（5分） |
| 3（4分） | 1（4分） |
| 2（3分） | 5（3分） |
| 1（2分） | 4（2分） |
| 7（1分） | 6（1分） |

程序应显示：

第一个答案得 6 分
第二个答案得 8 分

第三个答案得 11 分
第四个答案得 8 分
第五个答案得 10 分
第六个答案得 6 分
第七个答案得 7 分

程序应读取 [1,7] 范围内的有效答案，并检查该答案是否已经给出。如果已经给出，程序应显示一条消息，并提示用户重新输入一个新答案。

```c
#include <stdio.h>
#include <string.h>

#define TOURISTS 100
#define ANSWERS 7

int main(void)
{
    int i, j, sel, pnts[ANSWERS] = {0}; /* This array holds the points of each answer. For example, pnts[0] holds the points of the first answer, pnts[1] holds the points of the second answer and so on. */
    int given_ans[ANSWERS] = {0}; /* This array is used to check whether an answer is already given or not. If an element's value is 1, it means that the respective answer is chosen. For example, if the user chooses the third answer, given_ans[2] becomes 1. */
    for(i = 0; i < TOURISTS; i++)
    {
        printf("\nEnter answers of tourist_%d:\n", i+1);
        memset(given_ans, 0, sizeof(given_ans)); /* The values must be zeroed before reading the answers of a new tourist. See memset() in Appendix C. */
        for(j = 0; j < ANSWERS; j++)
        {
            while(1) /* Infinite loop until the user enters a valid answer, not already given. */
            {
                printf("Answer_%d [1-%d]: ", j+1, ANSWERS);
                scanf("%d", &sel);
                if(sel < 1 || sel > ANSWERS)
                    printf("Wrong answer ...\n");
                else if(given_ans[sel-1] == 1)
                    printf("Error: This answer is already given ...\n");
                else
                    break;
            }
            pnts[sel-1] += ANSWERS - j; /* For example, if the first answer (j = 0) is the first one, then pnts[sel-1] - pnts[5-1] - pnts[4] += 7-0 = 7; that is, 7 more points are added to the points of the fifth choice. */
            given_ans[sel-1] = 1;
        }
    }
    printf("\n***** Answer Results *****\n");
    for(i = 0; i < ANSWERS; i++)
        printf("Answer_%d gets %d points\n", i+1, pnts[i]);
    return 0;
}
```

### C.20.4
编写一个程序，要求两个命令行参数，分别对应一个 double 类型二维数组的维度（行和列）。程序应分配内存以创建该数组，并为其元素赋随机值，使得每一行元素之和等于 1。程序在终止前应显示数组的元素。

注意：要将命令行参数转换为整数，请使用 atoi() 函数。参见附录 C 中该函数的原型。

```c
#include <stdio.h>
#include <stdlib.h>
#include <time.h>

int main(int argc, char *argv[])
{
    int i, j, rows, cols;
    double **arr, sum_line;

    if(argc < 3)
        printf("Error: missing arguments...\n");
    else if(argc == 3)
    {
        rows = atoi(argv[1]); /* Convert the second argument to integer. */
        cols = atoi(argv[2]); /* Do the same for the third argument. */
        srand(time(NULL));
        arr = (double**) malloc(rows * sizeof(double*));
        if(arr == NULL)
        {
            printf("Error: Not available memory\n");
            exit(EXIT_FAILURE);
        }
        for(j = 0; j < rows; j++)
        {
            arr[j] = (double*) malloc(cols * sizeof(double));
            if(arr[j] == NULL)
            {
                printf("Error: Not available memory\n");
                exit(EXIT_FAILURE);
            }
        }
        for(i = 0; i < rows; i++)
        {
            sum_line = 0;
            for(j = 0; j < cols-1; j++)
            {
                arr[i][j] = (rand()%101/(cols-1))/100.0;
                sum_line += arr[i][j]; /* As an example, assume that the number of columns is 5. For the first four rows' elements rand()%101 generates an integer in [0, 100]. Dividing it by the number of the columns minus 1, that is, 4, we get an integer in [0, 25] and dividing that integer with 100.0 we get a number in [0, 0.25]. In this way, the sum of the first four elements is constrained in [0, 1]. */
            }
            arr[i][j] = 1-sum_line; /* To satisfy the requirement that the sum of the elements of each row must be equal to 1, the value of the last element is calculated by subtracting from 1 the sum of the remaining elements. */
        }
        for(i = 0; i < rows; i++)
        {
            for(j = 0; j < cols; j++)
                printf("%6.2f", arr[i][j]);
            printf("\n");
        }
        for(j = 0; j < rows; j++)
            free(arr[j]);
        free(arr);
    }
    else
        printf("Error: too many arguments...\n");
    return 0;
}
```

### C.20.5
系统要连接到某个互联网地址，其网卡必须发送一个封装了特殊 TCP 报文段的网际协议（IP）数据包。IPv4 头部格式如图 20.1 所示。

![](img/b8da5dcf9ba7f1fad5213c453d095246_655_0.png)

图 20.1
IPv4 头部。

![](img/b8da5dcf9ba7f1fad5213c453d095246_656_0.png)

图 20.2
TCP 头部。

TCP 头部格式如图 20.2 所示。

编写一个程序，读取 x.x.x.x 格式的源 IP 地址（每个 x 是 [0, 255] 范围内的整数）、x.x.x.x 格式的目标 IP 地址，以及 TCP 目标端口（[1, 65535] 范围内的整数），并创建一个封装了相应 TCP 报文段的 IP 数据包。程序必须将 IP 数据包的内容以十六进制格式存储到用户选择的文本文件中。每行必须包含 16 个字节。在 IPv4 头部中设置以下值：

- a. 版本（Version）= 4。
- b. IHL = 5。
- c. 总长度 = IP 数据包的总长度，包括 TCP 数据。
- d. 协议 = 6。
- e. 生存时间（Time to Live）= 255。
- f. 目标地址 = 目标 IP 地址。
- g. 源地址 = 源 IP 地址。

在 TCP 头部中设置以下值：

- a. 目标端口 = 目标 TCP 端口。
- b. 源端口 = 1500。
- c. 窗口 = 允许的最大值。
- d. SYN 位 = 1。

将其余字段设置为 0，并假设不存在选项（Options）字段。

该程序有一个限制：如果目标 IP 地址以 130.140 或 160.170 开头，并且目标 TCP 端口为 80，则不创建 IP 数据包，并显示相关消息。

```c
#include <stdio.h>
#include <stdlib.h>

typedef unsigned char BYTE;
```

