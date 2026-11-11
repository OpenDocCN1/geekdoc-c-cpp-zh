

- 三维数组

让我们从一维数组开始讨论。

## 一维数组

在 C++ 中，一维数组是一种结构化元素集合，可通过单个索引值指定元素位置来单独访问其中的元素。例如，当我们声明 array[10] 时，数组中元素的索引值为 array[0]、array[1]、……、array[9]。以下是一维数组的声明语法：

```cpp
data_type Array_Name [count];
```

在前面的语法中，`data_type` 描述数组每个元素中存储的数据类型，`count` 表示数组的大小。数组的大小指定数组中元素的数量。要创建数组，`count` 的值必须大于 0。一维数组的索引值范围为 0 到 count-1。例如，当你声明一个包含 10 个元素的一维数组时，该数组的索引值范围为 0 到 9。一维数组也称为线性数组。这是因为一维数组按顺序存储数据。以下代码片段展示如何声明一维数组：

```cpp
int roll[50];
```

当 C++ 编译器编译前面的代码片段时，它会创建一个名为 roll 的数组，该数组可存储 50 个元素；每个元素都能保存一个 int 值。换句话说，roll 数组有 50 个元素，其数据类型为 int。使用一维数组的示例见清单 3（你可以在 CD 的 code/chapter3 文件夹中找到 Array2.cpp 文件）：

### ▶ 清单 3：创建一维数组

```cpp
#include <iostream.h>
int main()
{
  int array[5];
  int index, temp;
  for(index=0; index<5; index++)
  {
    cout<<"Enter the value of array["<<index<<"]: ";
    cin>>array[index];
  }
  cout<<"The values you enter are: ";
  for(index=0; index<5; index++)
  {
    cout<<array[index]<<", ";
  }
  cout<<endl;
  // sorting an array
  for (int i=0; i<5; i++)
  {
      for(int j=0; j<=i; j++)
      {
          if(array[i] < array[j])
          {
              temp = array[i];
              array[i] = array[j];
              array[j] = temp;
          }
      }
  }
  cout<<"After sorting values are: ";
  for(index=0; index<5; index++)
  {
      cout<<array[index]<<" ";
  }
  return 0;
}
```

**输出：**

```text
Enter the value of array[0]: 23
Enter the value of array[1]: 45
Enter the value of array[2]: 11
Enter the value of array[3]: 24
Enter the value of array[4]: 77
The values you enter are: 23, 45, 11, 24, 77,
After sorting values are: 11, 23, 24, 45, 77,
```

在清单 3 中，array[5] 是一个一维数组，用于存储该数组中的元素。在将元素存储到 array[5] 后，我们按升序对这些元素排序，并显示最终排序后的元素。

除了创建一维数组，你还可以创建具有多个维度的数组。下一节我们将讨论二维数组。

## 二维数组

具有两个维度的数组称为二维数组（array[10][10]）。换句话说，能以表格形式（即按行和列的形式）存储值的数组称为二维数组。一维数组是线性数组，因为它们按顺序存储数据。另一方面，二维数组是非线性数组，因为它以表格形式存储数据。在一维数组中，只使用一个索引值来声明和访问数组元素；而在二维数组中，使用两个索引值来访问数组元素。以下是二维数组的声明语法：

```cpp
data-type Array_Name [rows][columns];
```

在前面的语法中，`data_type` 是数组存储的数据类型。`Array_Name` 是数组名，rows 和 columns 表示数组中可存储的元素数量。例如，以下代码片段声明一个二维数组：

```cpp
int Arr2[2][3];
```

在前面的代码片段中，Arr2 数组创建为 2 行 3 列，可存储 6 个整数值。对于二维数组，索引值范围为 [0][0] 到 [row-1][column-1]。因此，Arr2 数组的第一个元素可通过 Arr2[0][0] 访问，最后一个元素可通过 Arr2[1][2] 访问。Arr2 数组的表格表示如下：

|  |  |  |
|---|---|---|
| Arr2[0][0] | Arr2[0][1] | Arr2[0][2] |
| Arr2[1][0] | Arr2[1][1] | Arr2[1][2] |

初始化二维数组与初始化一维数组类似。以下代码片段展示二维数组的初始化：

```cpp
int Arr2[2][3]={
    {2,4,6},
    {8,10,12}
};
```

在前面的代码片段中，通过指定两个维度来创建二维数组。不过，你也可以按下述代码片段所示初始化二维数组：

```cpp
int Arr2[][3]={
    {2,4,6},
    {8,10,12}
};
```

在前面的代码片段中，数组的行未指定，编译器会根据数组中初始化的行数自动指定。这就是为什么 Arr2 数组的两种初始化方式相同且都正确。

![](img/8a6886c00caa6a1651a6c0e62bff341f_164_0.png)

> 尽管指定数组的第一个维度是可选的，但在初始化二维数组时，你必须记住指定第二个维度。

对于一维数组，使用循环来访问其元素。对于二维数组和三维数组，使用嵌套循环来访问其各个元素。清单 4 展示了使用嵌套 for 循环访问二维数组元素的示例（你可以在 CD 的 code/chapter3 文件夹中找到 Array3.cpp 文件）：

### ▶ 清单 4：创建二维数组

```cpp
#include <iostream.h>
#include <string.h>

int main()
{
    int matrix[3][4];
    int i,j;
    for(i=0; i<3; i++)
    {
        for(j=0; j<4; j++)
        {
            cout<<"Enter the element of matrix["<<i<<"]["<<j<<"] :";
            cin>>matrix[i][j];
        }
    }

    cout<<endl;
    cout<<"The element of matrix are: "<<endl;
    for(i=0; i<3; i++)
    {
        for(j=0; j<4; j++)
        {
            cout<<matrix[i][j]<<"  ";
        }
        cout<<endl;
    }

    return 0;
}
```

**输出：**

```text
Enter the element of matrix[0][0] :3
Enter the element of matrix[0][1] :6
Enter the element of matrix[0][2] :1
Enter the element of matrix[0][3] :5
Enter the element of matrix[1][0] :2
Enter the element of matrix[1][1] :7
Enter the element of matrix[1][2] :4
Enter the element of matrix[1][3] :2
Enter the element of matrix[2][0] :4
Enter the element of matrix[2][1] :3
Enter the element of matrix[2][2] :8
Enter the element of matrix[2][3] :5
The element of matrix are:
3 6 1 5
2 7 4 2
4 3 8 5
```

在清单 4 中，创建了二维数组 matrix[3][4]。然后还创建了两个嵌套 for 循环。第一个 for 循环用于接收存储在数组元素中的值。第二个 for 循环用于访问并显示这些元素的值。

## 三维数组

用三个维度声明的数组称为三维数组。换句话说，由二维数组构成的数组可称为三维数组。以下是三维数组的声明语法：

```cpp
data_type Array_Name[dimension1][dimension2][dimension3];
```

在前面的语法中，`data_type` 是数组中将要存储的数据类型，`Array_Name` 是数组名，`dimension1`、`dimension2` 和 `dimension3` 是数组的三个维度。这三个维度表示数组中可存储的元素数量。例如，以下代码片段展示三维数组的声明：

```cpp
int Arr3[2][2][2];
```

在前面的代码片段中，`Arr3` 数组是一个三维数组，可存储八个（2x2x2）整数值。对于三维数组，索引值范围从 `[0][0][0]` 到 `[dimension1-1][dimension2-1][dimension3-1]`。例如，前面代码片段中声明的 Arr3 数组的第一个元素可通过 `Arr3[0][0][0]` 索引访问，最后一个元素可通过 `Arr3[1][1][1]` 索引访问。

三维数组的初始化与一维数组和二维数组的初始化非常相似。以下代码片段展示前面代码片段中声明的 Arr3 数组的初始化：

```cpp
int Arr3[2][2][2]={
                        {
                          {1,2},
                          {3,4},
                        },
                        {
                          {5,6},
                          {7,8},
                        }
                     };
```

