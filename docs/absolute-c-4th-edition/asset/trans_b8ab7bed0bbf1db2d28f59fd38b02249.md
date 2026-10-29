

你可能会抗议说 MAX_NUMBER_SCORES 是一个全局定义的常量，因此它可以在 fillArray 的定义中使用，而无需将其作为参数。你是对的，如果我们只在 Display 5.5 中的程序中使用 fillArray，而不在其他程序中使用，我们就可以不用将 MAX_NUMBER_SCORES 作为 fillArray 的参数来应付。然而，fillArray 是一个通用有用的函数，你可能希望在多个不同的程序中使用它。我们事实上也在下一小节讨论的 Display 5.6 中的程序中使用了函数 fillArray。在 Display 5.6 中的程序中，声明的数组大小的参数是一个不同命名的全局常量。如果我们将全局常量 MAX_NUMBER_SCORES 写进函数 fillArray 的主体中，我们就无法在 Display 5.6 中的程序中重用该函数。

即使我们只在一个程序中使用 fillArray，将声明的数组大小作为 fillArray 的参数仍然是一个好主意。将数组的声明大小作为参数显示，提醒我们函数以极其关键的方式需要此信息。

## Display 5.5 Partially Filled Array (part 1 of 3)

//Shows the difference between each of a list of golf scores and their average.
#include <iostream>
using namespace std;
const int MAX_NUMBER_SCORES = 10;

void fillArray(int a[], int size, int& numberUsed);
//Precondition: size is the declared size of the array a.
//Postcondition: numberUsed is the number of values stored in a.
//a[0] through a[numberUsed-1] have been filled with
//nonnegative integers read from the keyboard.

double computeAverage(const int a[], int numberUsed);
//Precondition: a[0] through a[numberUsed-1] have values; numberUsed > 0.
//Returns the average of numbers a[0] through a[numberUsed-1].

void showDifference(const int a[], int numberUsed);
//Precondition: The first numberUsed indexed variables of a have values.
//Postcondition: Gives screen output showing how much each of the first
//numberUsed elements of the array a differs from their average.

int main()
{
    int score[MAX_NUMBER_SCORES], numberUsed;

    cout << "This program reads golf scores and shows\n"
         << "how much each differs from the average.\n";

    cout << "Enter golf scores:\n";
```

## Display 5.5 Partially Filled Array (part 2 of 3)

```
    fillArray(score, MAX_NUMBER_SCORES, numberUsed);
    showDifference(score, numberUsed);

    return 0;
}

void fillArray(int a[], int size, int& numberUsed)
{
    cout << "Enter up to " << size << " nonnegative whole numbers.\n"
         << "Mark the end of the list with a negative number.\n";
    int next, index = 0;
    cin >> next;
    while ((next >= 0) && (index < size))
    {
        a[index] = next;
        index++;
        cin >> next;
    }
    numberUsed = index;
}

double computeAverage(const int a[], int numberUsed)
{
    double total = 0;
    for (int index = 0; index < numberUsed; index++)
        total = total + a[index];
    if (numberUsed > 0)
    {
        return (total/numberUsed);
    }
    else
    {
        cout << "ERROR: number of elements is 0 in computeAverage.\n"
             << "computeAverage returns 0.\n";
        return 0;
    }
}

void showDifference(const int a[], int numberUsed)
{
    double average = computeAverage(a, numberUsed);
    cout << "Average of the " << numberUsed
         << " scores = " << average << endl
         << "The scores are:\n";
```

## Display 5.5 Partially Filled Array (part 3 of 3)

```
    for (int index = 0; index < numberUsed; index++)
        cout << a[index] << " differs from average by "
             << (a[index] - average) << endl;
}
```

### Sample Dialogue

This program reads golf scores and shows how much each differs from the average.
Enter golf scores:
Enter up to 10 nonnegative whole numbers.
Mark the end of the list with a negative number.
69 74 68 -1
Average of the 3 scores = 70.3333
The scores are:
69 differs from average by -1.33333
74 differs from average by 3.66667
68 differs from average by -2.33333

## Example: Searching an Array

一个常见的编程任务是在数组中搜索给定值。例如，数组可能包含某门课程中所有学生的学号。为了判断某个特定学生是否已注册，数组会被搜索以查看是否包含该学生的号码。Display 5.6 中的简单程序填充一个数组，然后根据用户指定的值搜索该数组。实际的应用程序会复杂得多，但这展示了顺序搜索算法的所有要点：程序按顺序查看数组元素，从第一个到最后一个，以查看目标数字是否等于数组中的任何元素。

在 Display 5.6 中，使用函数 search 来搜索数组。在搜索数组时，你通常希望知道的不仅仅是目标值是否在数组中。如果目标值在数组中，你通常希望知道保存该目标值的索引变量的索引，因为该索引可能作为了解目标值的其他信息的指南。因此，我们设计函数 search 使其返回一个索引，表示目标值在数组中的位置，前提是目标值确实在数组中。如果目标值不在数组中，search 返回 -1。让我们更详细地看一下函数 search。

函数 search 使用 while 循环逐一检查数组元素，以查看其中是否有一个等于目标值。变量 found 用作标志，记录是否找到了目标元素。如果在数组中找到目标元素，found 被设为 true，这反过来会结束 while 循环。

sequential search

## Display 5.6 Searching an Array (part 1 of 2)

//Searches a partially filled array of nonnegative integers.
#include <iostream>
using namespace std;
const int DECLARED_SIZE = 20;

void fillArray(int a[], int size, int& numberUsed);
//Precondition: size is the declared size of the array a.
//Postcondition: numberUsed is the number of values stored in a.
//a[0] through a[numberUsed-1] have been filled with
//nonnegative integers read from the keyboard.

int search(const int a[], int numberUsed, int target);
//Precondition: numberUsed is <= the declared size of a.
//Also, a[0] through a[numberUsed-1] have values.
//Returns the first index such that a[index] == target,
//provided there is such an index; otherwise, returns -1.

int main()
{
    int arr[DECLARED_SIZE], listSize, target;

    fillArray(arr, DECLARED_SIZE, listSize);

    char ans;
    int result;
    do
    {
        cout << "Enter a number to search for: ";
        cin >> target;

        result = search(arr, listSize, target);
        if (result == -1)
            cout << target << " is not on the list.\n";
        else
            cout << target << " is stored in array position "
                 << result << endl
                 << "(Remember: The first position is 0.)\n";

        cout << "Search again?(y/n followed by Return): ";
        cin >> ans;
    } while ((ans != 'n') && (ans != 'N'));
    cout << "End of program.\n";
    return 0;
}

void fillArray(int a[], int size, int& numberUsed)
<-The rest of the definition of fillArray is given in Display 5.5->
```

## Display 5.6 Searching an Array (part 2 of 2)

```
int search(const int a[], int numberUsed, int target)
{
    int index = 0;
    bool found = false;
    while (!found && (index < numberUsed))
        if (target == a[index])
            found = true;
        else
            index++;

    if (found)
        return index;
    else
        return -1;
}
```

### Sample Dialogue

Enter up to 20 nonnegative whole numbers.
Mark the end of the list with a negative number.
10 20 30 40 50 60 70 80 -1
Enter a number to search for: 10
10 is stored in array position 0
(Remember: The first position is 0.)
Search again?(y/n followed by Return): y
Enter a number to search for: 40
40 is stored in array position 3
(Remember: The first position is 0.)
Search again?(y/n followed by Return): y
Enter a number to search for: 42
42 is not on the list.
Search again?(y/n followed by Return): n
End of program.

## Example: Sorting an Array

最常见且研究最透彻的编程任务之一，当然是排序值列表，例如必须从低到高或从高到低排序的销售额列表，或必须按字母顺序排序的单词列表。本示例描述了一个名为 sort 的函数，它将对部分填充的数字数组进行排序，使其按从小到大的顺序排列。

