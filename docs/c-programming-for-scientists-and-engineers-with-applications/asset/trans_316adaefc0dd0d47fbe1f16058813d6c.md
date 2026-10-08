

## 602 字符与字符串

>*******************************************************************
/*
    funcinput: 将字符串输入列表
/*
****************************************************************
/*
    输入参数:
    strname[NUMSTR][STRLNG] - 存储空间
/*
    输出参数:
    strname[NUMSTR][STRLNG] - 名称列表
/*
/*
    使用的数据文件:
    sortin.dat - 输入数据文件
/*
********************************************************************

```c
void funcinput(char strname[ ][STRLNG]) {
    FILE *inptr;
    int i;
    inptr = fopen("sortin.dat","r");
    for(i = 0; i < NUMSTR; i++) {
        fgets(strname[i], STRLNG, inptr);
        printf("%s\n", strname[i]);
    }
    fclose(inptr);
    return;
}
```

```c
****************************************************************
/*
* funcsort: 对列表中的字符串进行排序                    */
/*
                                                       */
/*
* 输入参数:                                     */
* strname[NUMSTR][STRLNNG] - 名称列表             */
/*
* 输出参数:                                    */
* strname[NUMSTR][STRLNNG] - 排序后的列表               */
/*                                                       */
/*                                                       */
/*
void funcsort(char name1[][STRLNNG])
{
    int i, j;
    char temp[STRLNNG];

    for(i = 0; i < NUMSTR - 1; i++)
    {
        for(j = i + 1; j < NUMSTR; j++)
        {
            if(strcmp(name1[i], name1[j]) > 0)
            {
                strcpy(temp, name1[i]);
                strcpy(name1[i], name1[j]);
                strcpy(name1[j], temp);
            }
        }
    }
    return;
}
****************************************************************
/*                                                       */
/* funcoutput: 输出字符串列表               */
/*                                                       */
****************************************************************
/* */
```

```c
/* 输入参数: */
/* name1[NUMSTR][STRLNG] - 名称列表 */
/******************************************************************/
void funcoutput(char name1[][][STRLNG])
{
    int i;

    for(i = 0; i < NUMSTR; i++)
    {
        puts(name1[i], outptr);
        printf("%s\n", name[i]);
    }

    return;
}
```

# 输出

未排序的名称：

- 活塞
- 螺栓
- 螺母
- 夹具
- 阀门
- 垫片
- 油油底
- 离合器
- 油泵
- 水泵
- 油

排序后的名称：

- 螺栓
- 夹具
- 离合器
- 垫片
- 螺母
- 油
- 油油底
- 油泵
- 活塞
- 阀门
- 水泵

## 9.5.3 零件列表的顺序查找

在许多工程应用中，可能需要搜索部件名称、材料类型、组装机器部件的组件、建筑施工材料等。搜索方法取决于列表是否已排序。介绍的搜索算法是线性查找和二分查找。二分查找所需的搜索列表必须经过排序。

线性查找：在线性查找中，我们在 ID 列表中搜索特定的部件 ID。如果列表包含该字符串，搜索停止。如果列表中不包含该 ID，且列表未经过排序，则必须搜索整个列表。此程序返回 ID 在列表中的位置，如果未找到 ID 则返回负数。

问题：编写一个程序在排序后的列表中搜索 ID。

方法

- 从数据文件输入 ID。
- 搜索每个需要的 ID。
- 停止。

数据：四个 个要查找的 ID 和一个库存列表。

伪代码

```c
main:
  从数据文件输入已排序的 ID 存列表
  输入要查找的 ID 数量
  对于每个我们需要的 ID
    调用 funcinput
    对于每个要查找的 ID
      调用 funcsearch
      如果找到
        输出 ID、消息、位置
      否则
        输出 ID、消息
    结束循环
  结束
停止
```

# 字符与字符串

```c
funcinput:
对于每个 ID
    从文件输入 ID 到列表
结束循环
```

```c
funcsearch:
对于每个需要的 ID
    position = -1
    对于每个 IDj 直到找到 ID
        if (ID = search ID)
            保存位置
    结束如果
结束循环
结束循环
```

# 程序

```c
#include <stdio.h>
#include <string.h>

#define NUMSTR 10
#define STRNG 8
```

# 9.5 示例程序 607

```c
void funcinput(char [][STRNG);
int funcsearch(char [][STRNG], char .], int);

FILE ptrsr;
int main( )
{
    char ID[NUMSTR][STRNG];
    char IDS[STRNG];
    int wanted, i, location;

    ptrsr = fopen("filesrchin.dat", "r");
    funcinput(ID);
    scanf(ptrsr, "%d ", &wanted);
    for(i = 0; i < wanted; i++) {
        scanf(ptrsr, "%7c", IDS);
        IDS[6] = '\0';
        location = funcsearch(ID, IDS, NUMSTR);
    }
    if(location >= 0) 
        printf("\n%s is found in position:%4d\n", IDS, location + 1);
    } else
        printf("\n%s is not found.\n", IDS);
    }
    return 0;
}
```

```c
******************************************************************/
/* funcinput: 输入排序后的名称                  */
******************************************************************/
/* 输入参数:                             */
/*   strname1[NUMSTR][STRNG] - 空列表         */
/* 输出参数:                           */
/*   strname1[NUMSTR][STRNG] - 名称列表      */
/* 数据文件:                                   */
/*   sortin.dat - 输入数据文件                */
****************************************************************/**
```
```c
void funcinput(char strname1[][STRNG]){
    FILE *inptr;
    int i;

    inptr = fopen("sortin.dat", "r");
    for(i = 0; i < NUMSTR; i++) {
        fgets(strname1[i], STRLNG, inptr);
    }
    fclose(inptr);
    return;
}
```

****************************************************************
/* funcsearch: 在排序后的列表中搜索字符串 */
****************************************************************
/* 输入参数: */
/* ID1[NUMSTR][STRLNG] - 名称列表 */
/* ID2[STRLNG] - 需要的 */
/* 输出参数: */
/* location - 在列表中位置 */
****************************************************************
```c
int funcsearch(char ID1[][STRLNG], char ID[], int NUMSTR) {
    int i, location = -1;
    for(i = 0; i < NUMSTR; i++) {
        if(strcmp(ID1[i], ID) == 0) {
            location = i;
        }
    }
    return location;
}
```

sortin.dat

ABC245
BC376
F245
IJH90
MKS567
RPM745
SRK190
TML98
TEB27

fileschin.dat

AXB67
FDC45
MKX75
TML98

AXB67 is not found.
FDC45 is found in position:3
MKX75 is not found.
TML98 is found in position:9

