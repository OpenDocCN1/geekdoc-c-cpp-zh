
请输入一个整数值（输入 -1 退出）：52

13 23 24 34 35 36 38 42 47 51 68 74 75 85 97
                                  *
                                      47 51 68 74 75 85 97
                                          *
                                      47 51 68
                                          *
                                            68
                                            *
未找到整数 52。

请输入一个整数值（输入 -1 退出）：-1

**图 19.5** | 使用二分查找在数组中定位元素（输出中的 * 标记中间元素）。（第 3 部分，共 3 部分）

## 二分查找的效率

在最坏情况下，使用二分查找搜索包含 1023 个元素的有序数组只需 10 次比较。反复将 1023 除以 2（因为每次比较后我们可以排除数组的一半）并向下取整（因为我们也移除了中间元素），得到值 511、255、127、63、31、15、7、3、1 和 0。数字 1023（2¹⁰ − 1）只需除以 2 共 10 次即可得到值 0，这表示没有更多元素需要测试。在二分查找算法中，除以 2 相当于一次比较。因此，包含 1,048,575（2²⁰ − 1）个元素的数组最多需要 20 次比较即可找到关键字，而包含超过十亿个元素的数组最多需要 30 次比较即可找到关键字。与线性查找相比，这在性能上是巨大的改进。对于包含十亿个元素的数组，这意味着线性查找平均需要 5 亿次比较，而二分查找最多只需 30 次比较！对任意有序数组进行二分查找所需的最大比较次数是大于数组中元素个数的第一个 2 的幂的指数，表示为 log₂ n。所有算法大致以相同的速率增长，因此在大 O 表示法中底数可以省略。因此二分查找的大 O 表示法为 O(log n)，也称为对数运行时间。

## 19.3 排序算法

排序数据（即将数据按某种特定顺序排列，例如升序或降序）是最重要的计算应用之一。银行按账号对所有支票排序，以便在每月月底准备个人银行对账单。电话公司按姓氏，并进一步按名字对其账户列表排序，以便轻松查找电话号码。实际上，每个组织都必须对某些数据进行排序，而且往往是海量数据。排序数据是一个引人入胜且计算密集的问题，吸引了大量的研究工作。

关于排序需要理解的一个重要点是：无论使用哪种算法对数组进行排序，最终结果——排序后的数组——都是相同的。算法的选择只影响程序的运行时间和内存使用。本章其余部分介绍三种常见的排序算法。前两种——选择排序和插入排序——易于编程但效率不高。最后一种算法——归并排序——比选择排序和插入排序快得多，但编程难度更大。我们重点讨论对基本类型数据（即 int 类型）的数组进行排序。对类对象的数组进行排序也是可能的。我们将在第 20.7.1 节讨论这一点。

### 19.3.1 选择排序

选择排序是一种简单但效率不高的排序算法。它的第一次迭代选择数组中最小的元素，并将其与第一个元素交换。第二次迭代选择第二小的元素（即剩余元素中最小的元素），并将其与第二个元素交换。算法持续进行，直到最后一次迭代选出第二大的元素，并将其与倒数第二个元素交换，从而将最大的元素留在最后一个位置。在第 i 次迭代后，数组中最小的 i 个元素将按递增顺序排列在数组的前 i 个元素中。

例如，考虑数组

34 56 4 10 77 51 93 30 5 52

实现选择排序的程序首先确定该数组中最小的元素（4），它位于索引 2 处。程序将 4 与 34 交换，结果为

4 56 34 10 77 51 93 30 5 52

然后程序确定剩余元素（除 4 之外的所有元素）中的最小值，即位于索引 8 处的 5。程序将 5 与 56 交换，结果为

4 5 34 10 77 51 93 30 56 52

在第三次迭代中，程序确定下一个最小值（10），并将其与 34 交换。

4 5 10 34 77 51 93 30 56 52

该过程持续进行，直到数组完全排序。

4 5 10 30 34 51 52 56 77 93

第一次迭代后，最小的元素位于第一个位置。第二次迭代后，两个最小的元素按顺序位于前两个位置。第三次迭代后，三个最小的元素按顺序位于前三个位置。

图 19.6 声明了 SelectionSort 类。该类有两个私有实例变量——一个名为 data 的 int 数组，以及一个用于生成随机整数以填充数组的静态 Random 对象。当实例化 SelectionSort 类的对象时，构造函数（第 13–20 行）创建并用 10–99 范围内的随机整数初始化数组 data。

```
// Fig. 19.6: SelectionSort.java
// Class that creates an array filled with random integers.
// Provides a method to sort the array with selection sort.
import java.util.Arrays;
import java.util.Random;
```

图 19.6 | 创建一个用随机整数填充的数组的类。提供使用选择排序对数组排序的方法。（第 1 部分，共 3 部分）

```
public class SelectionSort
{
    private int[] data; // array of values
    private static final Random generator = new Random();

    // create array of given size and fill with random integers
    public SelectionSort( int size )
    {
        data = new int[ size ]; // create space for array

        // fill array with random ints in range 10-99
        for ( int i = 0; i < size; i++ )
            data[ i ] = 10 + generator.nextInt( 90 );
    } // end SelectionSort constructor

    // sort array using selection sort
    public void sort()
    {
        int smallest; // index of smallest element

        // loop over data.length - 1 elements
        for ( int i = 0; i < data.length - 1; i++ )
        {
            smallest = i; // first index of remaining array

            // loop to find index of smallest element
            for ( int index = i + 1; index < data.length; index++ )
                if ( data[ index ] < data[ smallest ] )
                    smallest = index;

            swap( i, smallest ); // swap smallest element into position
            printPass( i + 1, smallest ); // output pass of algorithm
        } // end outer for
    } // end method sort

    // helper method to swap values in two elements
    public void swap( int first, int second )
    {
        int temporary = data[ first ]; // store first in temporary
        data[ first ] = data[ second ]; // replace first with second
        data[ second ] = temporary; // put temporary in second
    } // end method swap

    // print a pass of the algorithm
    public void printPass( int pass, int index )
    {
        System.out.print( String.format( "after pass %2d: ", pass ) );

        // output elements till selected item
        for ( int i = 0; i < index; i++ )
            System.out.print( data[ i ] + " " );
```

图 19.6 | 创建一个用随机整数填充的数组的类。提供使用选择排序对数组排序的方法。（第 2 部分，共 3 部分）

```
public static void main( String[] args )
{
    // create object to perform selection sort
    SelectionSort sortArray = new SelectionSort( 10 );

    System.out.println( "Unsorted array:" );
    System.out.println( sortArray + "\n" ); // print unsorted array

    sortArray.sort(); // sort array

    System.out.println( "Sorted array:" );
    System.out.println( sortArray ); // print sorted array
} // end main
} // end class SelectionSortTest
```

未排序数组：
[61, 87, 80, 58, 40, 50, 20, 13, 71, 45]
第 1 趟后： 13  87  80  58  40  50  20  61* 71  45
            --
第 2 趟后： 13  20  80  58  40  50  87* 61  71  45
            --  --
第 3 趟后： 13  20  40  58  80* 50  87  61  71  45
            --  --  --
第 4 趟后： 13  20  40  45  80  50  87  61  71  58*
            --  --  --  --
第 5 趟后： 13  20  40  45  50  80* 87  61  71  58
            --  --  --  --  --
第 6 趟后： 13  20  40  45  50  58  87  61  71  80*
            --  --  --  --  --  --
第 6 趟后： 13  20  40  45  50  58  87  61  71  80*
            --  --  --  --  --  --
第 7 趟后： 13  20  40  45  50  58  61  87* 71  80
            --  --  --  --  --  --  --
第 8 趟后： 13  20  40  45  50  58  61  71  87* 80
            --  --  --  --  --  --  --  --
第 9 趟后： 13  20  40  45  50  58  61  71  80  87*
            --  --  --  --  --  --  --  --  --
排序后的数组：
[13, 20, 40, 45, 50, 58, 61, 71, 80, 87]

图 19.7 | 测试选择排序类。（第 2 部分，共 2 部分）

## 选择排序的效率

选择排序算法以 O(n²) 时间运行。图 19.6 中第 23–40 行的 sort 方法实现了选择排序算法，包含两个 for 循环。外层 for 循环（第 28–39 行）遍历数组中的前 n−1 个元素，将剩余元素中最小的元素交换到其已排序的位置。内层 for 循环（第 33–35 行）遍历每个

