

# 148 C++ 简介

```cpp
if(found == 0)
{
    code[pos] = num;
    pos++;
}
cout << "\nCodes: ";
for(i = 0; i < pos; i++)
    cout << code[i] << '\n';
return 0;
```

**C.7.8** 编写一个程序，读取 100 个整数并将它们存储在数组中。然后，程序应该找到并显示两个最大的不同的值。

```cpp
#include <iostream>
using std::cout;
using std::cin;

int main()
{
    const int SIZE = 100;
    int i, max_1, max_2, arr[SIZE];

    for(i = 0; i < SIZE; i++)
    {
        cout << "\nEnter number: ";
        cin >> arr[i];
    }
    max_1 = max_2 = arr[0];
    for(i = 1; i < SIZE; i++)
    {
        if(max_1 != arr[i])
        {
            max_2 = arr[i]; /* 我们将该值赋值给 max_2，以便与剩余元素进行比较。 */
            break;
        }
    }
    if(i == SIZE)
    {
        cout << "\Array contains the same value: " << max_1 << '\n';
        return 0;
    }
    /* 从第二个循环结束的地方继续执行循环。 */
    for(i = i; i < SIZE; i++)
    {
        if(arr[i] > max_1)
        {
            max_2 = max_1; /* 第二大的值值成为目前为止的最高值。 */
            max_1 = arr[i];
        }
        else if(arr[i] > max_2 && arr[i] != max_1) /* 寻找与第一个值不相第二大值。 */
            max_2 = arr[i];
        }
    }
    cout << "First Max: " << max_1 << " Sec Max: " << max_2 << '\n';
    return 0;
}
```

注释：找到数组中第 n 小或大元素的典型方法是使用某种排序算法（如第 12 章介绍的算法）对数组进行排序。然后搜索 arr[n-1]。

**C.7.9** 编写一个程序，声明一个包含十个整数的数组，并为其元素赋值 [5, 20] 之间的值。程序应该检查数组是否包含重复项，如果有，则将其删除。当一个元素被删除时，后续元素应该向左移动一位。空位应该赋予值 -1。例如，如果数组是：{9, 12, 8, 12, 17, 8, 18, 19}，它应该变为：{9, 12, 8, 17, 18, 19, -1, -1}。要记住如何使用 srand() 和 rand()，参考示例 C.6.2。

```cpp
#include <iostream>
#include <cstdlib>
#include <ctime>
int main() {
    const int SIZE = 10;
    int i, j, k, size, arr[SIZE];

    srand(time(NULL));
    for(i = 0; i < SIZE; i++)
        arr[i] = rand()%16+5;

    size = SIZE;
    for(i = 0; i < size; i++) {
        j = i+1;
        while(j < size) {
            if(arr[i] == arr[j] && k < size-1, k++) {
                for(k = j; k < size-1; k++)
                    arr[k] = arr[k+1]; /* 将元素向左移动。 */
                size--; /* 减少它们的数量。/* 因为元素被删除了，我们
            }
            else {
                j++;
            }
        }
    }
    for(i = size; i < SIZE; i++)
        arr[i] = -1;
    for(i = 0; i < SIZE; i++)
        std::cout << arr[i] << ' ';
    return 0;
}
```

**C.7.10** 编写一个程序，读取 100 名游客对以下问题的偏好排序：
“你在希腊最喜欢什么？”

- 1. 自然的多样性
2. 气候
3. 岛屿
4. 夜生活
5. 遗迹
6. 人
7. 食物

每个答案根据其排名获得 1–7 分。第一个答案获得 7 分，第二个答案获得 6 分，最后一个答案获得 1 分。例如，如果两名游客回答了以下内容，程序应该显示：

| 第 1 位游客 | 第 2 位游客 | 程序输出 |
|---|---|---|
| 5 (7分) | 3 (3分) | 答案_1 获得 6 分 |
| 4 (6分) | 7 (6分) | 答案_2 获得 8 分 |
| 6 (5分) | 2 (5分) | 答案_3 获得 11 分 |
| 3 (4分) | 1 (4分) | 答案_4 获得 8 分 |
| 2 (3分) | 5 (3分) | 答案_5 获得 10 分 |
| 1 (2分) | 4 (2分) | 答案_6 获得 6 分 |
| 7 (1分) | 6 (1分) | 答案_7 获得 7 分 |

程序应该读取 [1, 7] 之间的值，并检查答案是否已经给出。如果是，程序应该显示一条消息并提示用户输入新的。

```cpp
#include <iostream>
#include <string>
using std::cout;
using std::cin;

int main() {
    const int ANSWERS = 7;
    int i, j, sel, pnts[ANSWERS] = {0}; /* 这个数组存储每个答案的分数。例如，pnts[0] 存储第一个答案的分数，pnts[1] 存储第二个答案的分数，依此类推。 */
    int given_ans[ANSWERS] = {0}; /* 此数组用于检查答案是否已经给出。 */
    /* 检查答案是否已经给出。 */
    for(i = 0; i < ANSWERS; i++) {
        cout << i+1 << "：";
        cin >> sel;
        if(sel < 1 || sel > ANSWERS) {
            cout << "错误，请输入 1-7 之间的数字。\n";
            i--;
            continue;
        }
        if(given_ans[sel-1]) {
            cout << "该答案已经给过了，请输入新的。\n";
            i--;
            continue;
        }
        given_ans[sel-1] = 1;
        pnts[sel-1] += (ANSWERS - sel); /* 根据排名给答案增加分数。 */
    }
    cout << "\n结果 *****\n";
    for(i = 0; i < ANSWERS; i++)
        cout << "答案_" << i+1 << " 获得 " << pnts[i] << " 分\n";
    return 0;
}
```

**C.7** 编写一个程序模拟在线乐票游戏。假设中奖号码是 10 个，范围在 [0, 100] 之间。程序应该以某种方式控制中奖号码。特别是，“作弊”在于之前的乐票中已经出现了 3 个中奖号码。程序应该询问用户是否想玩，如果用户回答否，则程序终止。为了简单起见，假设同一个数字可能会出现多次。

```cpp
#include <iostream>
#include <cstdlib>
#include <ctime>
using std::cout;
using std::cin;

int main()
{
    const int SIZE = 10;
    int i, pos1, pos2, pos3, ans, arr[SIZE];

    srand(time(NULL));
    // 第一轮乐票。
    for(i = 0; i < SIZE; i++)
    {
        arr[i] = rand()%101;
        cout << arr[i] << " ";
    }

    while (1)
    {
        cout << "\n继续玩吗？（0:否）：";
        cin >> ans;
        if(ans == 0)
            return 0;
        /* 选择三个随机位置。存储在位置上的数字将在下次乐票中被“抽出”。 */
        pos1 = rand()%SIZE;
        do {
            pos2 = rand()%SIZE;
        } while(pos1 == pos2);

        do {
            pos3 = rand()%SIZE;
        } while(pos1 == pos3) || (pos2 == pos3);

        // 下一轮乐票。
        for(i = 0; i < SIZE; i++)
            if((i == pos1) || (i == pos2) || (i == pos3))
            {
                cout << arr[i] << " "; // 这里就是作弊。
                continue;
                arr[i] = rand()%101;
                cout << arr[i] << " ";
            }

    }
    return 0;
}
```

注释：通过这个简单的“不公平”乐票示例，我只想向你们展示博彩软件可以以某种方式来控制结果。因此，请远离那些宣传巨大利润的在线乐票网站。

