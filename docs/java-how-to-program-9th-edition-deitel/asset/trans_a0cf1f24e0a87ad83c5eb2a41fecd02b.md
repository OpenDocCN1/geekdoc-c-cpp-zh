

接下来，算法检查 81（数组剩余部分的中间元素）是否与查找关键字匹配。查找关键字（65）小于 81，因此将 81 以及大于 81 的元素一并丢弃。仅经过两次测试，算法就将需要检查的值数量缩减到只有三个（56、65 和 77）。然后它检查 65（确实与查找关键字匹配）并返回包含 65 的数组元素的索引。该算法仅需三次比较即可确定查找关键字是否与数组中的某个元素匹配。而使用线性查找算法则需要 10 次比较。[注意：在本例中，我们选择使用包含 15 个元素的数组，这样数组中总有一个明显的中间元素。当元素个数为偶数时，数组的中间位于两个元素之间。我们实现算法时选择这两个元素中较大的那个作为中间元素。]

## 二分查找实现

图 19.4 声明了 BinaryArray 类。这个类与 LinearArray 类似——它有两个私有实例变量、一个构造函数、一个查找方法（binarySearch）、一个 remainingElements 方法和一个 toString 方法。第 13–22 行声明构造函数。数组用 10–99 的随机整数初始化（第 18–19 行）后，第 21 行对数组 data 调用 Arrays.sort 方法。sort 方法是 Arrays 类的静态方法，默认按升序对数组中的元素排序；该方法的重载版本允许你改变排序顺序。回顾一下，二分查找算法只能作用于已排序的数组。

```
1  // Fig. 19.4: BinaryArray.java
2  // Class that contains an array of random integers and a method
3  // that uses binary search to find an integer.
4  import java.util.Random;
5  import java.util.Arrays;
6
7  public class BinaryArray
8  {
9      private int[] data; // array of values
10     private static final Random generator = new Random();
11
12     // create array of given size and fill with random integers
13     public BinaryArray( int size )
14     {
15         data = new int[ size ]; // create space for array
16
17         // fill array with random ints in range 10-99
18         for ( int i = 0; i < size; i++ )
19             data[ i ] = 10 + generator.nextInt( 90 );
20
21         Arrays.sort( data );
22     } // end BinaryArray constructor
23
24     // perform a binary search on the data
25     public int binarySearch( int searchElement )
26     {
```

图 19.4 | 包含随机整数数组和使用二分查找查找整数的方法的类。（第 1 部分，共 3 部分。）

```
27    int low = 0; // low end of the search area
28    int high = data.length - 1; // high end of the search area
29    int middle = ( low + high + 1 ) / 2; // middle element
30    int location = -1; // return value; -1 if not found
31
32    do // loop to search for element
33    {
34        // print remaining elements of array
35        System.out.print( remainingElements( low, high ) );
36
37        // output spaces for alignment
38        for ( int i = 0; i < middle; i++ )
39            System.out.print( "   " );
40        System.out.println( " * " ); // indicate current middle
41
42        // if the element is found at the middle
43        if ( searchElement == data[ middle ] )
44            location = middle; // location is the current middle
45
46        // middle element is too high
47        else if ( searchElement < data[ middle ] )
48            high = middle - 1; // eliminate the higher half
49        else // middle element is too low
50            low = middle + 1; // eliminate the lower half
51
52        middle = ( low + high + 1 ) / 2; // recalculate the middle
53    } while ( ( low <= high ) && ( location == -1 ) );
54
55    return location; // return location of search key
56 } // end method binarySearch
57
58    // method to output certain values in array
59    public String remainingElements( int low, int high )
60    {
61        StringBuilder temporary = new StringBuilder();
62
63        // output spaces for alignment
64        for ( int i = 0; i < low; i++ )
65            temporary.append( "   " );
66
67        // output elements left in array
68        for ( int i = low; i <= high; i++ )
69            temporary.append( data[ i ] + " " );
70
71        temporary.append( "\n" );
72        return temporary.toString();
73    } // end method remainingElements
74
75    // method to output values in array
76    public String toString()
77    {
```

图 19.4 | 包含随机整数数组和使用二分查找查找整数的方法的类。（第 2 部分，共 3 部分。）

```
78        return remainingElements( 0, data.length - 1 );
79    } // end method toString
80 } // end class BinaryArray
```

图 19.4 | 包含随机整数数组和使用二分查找查找整数的方法的类。（第 3 部分，共 3 部分。）

第 25–56 行声明了 binarySearch 方法。查找关键字被传入参数 searchElement（第 25 行）。第 27–29 行计算程序当前正在搜索的数组部分的低端索引、高端索引和中间索引。在方法开始时，低端为 0，高端为数组长度减 1，中间索引是这两个值的平均值。第 30 行将元素的位置变量初始化为 -1——如果未找到元素，将返回该值。第 32–53 行循环，直到 low 大于 high（这发生在未找到元素时）或 location 不等于 -1（表示已找到查找关键字）。第 43 行测试中间元素的值是否等于 searchElement。如果相等，第 44 行将 middle 赋给 location。然后循环终止，并将 location 返回给调用者。循环的每次迭代测试一个值（第 43 行），并消除数组中剩余值的一半（第 48 或 50 行）。

图 19.5 使用用户输入的查找关键字执行二分查找，以确定该关键字是否与数组中的某个元素匹配。该程序输出的第一行是按升序排列的整数数组。当用户指示程序查找 23 时，程序首先测试中间元素，即 42（如 * 所示）。查找关键字小于 42，因此程序排除数组的后半部分，并测试前半部分的中间元素。查找关键字小于 34，因此程序排除数组的后半部分，只剩下三个元素。最后，程序检查 23（与查找关键字匹配）并返回索引 1。

```
1 // Fig. 19.5: BinarySearchTest.java
2 // Use binary search to locate an item in an array.
3 import java.util.Scanner;
4 
5 public class BinarySearchTest
6 {
7     public static void main( String[] args )
8     {
9         // create Scanner object to input data
10        Scanner input = new Scanner( System.in );
11
12        int searchInt; // search key
13        int position; // location of search key in array
14
15        // create array and output it
16        BinaryArray searchArray = new BinaryArray( 15 );
17        System.out.println( searchArray );
18
```

图 19.5 | 使用二分查找在数组中定位元素（输出中的 * 标记中间元素）。（第 1 部分，共 3 部分。）

```
19      // get input from user
20      System.out.print(
21      "Please enter an integer value (-1 to quit): " );
22      searchInt = input.nextInt(); // read an int from user
23      System.out.println();
24
25      // repeatedly input an integer; -1 terminates the program
26      while ( searchInt != -1 )
27      {
28          // use binary search to try to find integer
29          position = searchArray.binarySearch( searchInt );
30
31          // return value of -1 indicates integer was not found
32          if ( position == -1 )
33              System.out.println( "The integer " + searchInt +
34              " was not found.\n" );
35          else
36              System.out.println( "The integer " + searchInt +
37              " was found in position " + position + ".\n" );
38
39          // get input from user
40          System.out.print(
41          "Please enter an integer value (-1 to quit): " );
42          searchInt = input.nextInt(); // read an int from user
43          System.out.println();
44      } // end while
45      } // end main
46  } // end class BinarySearchTest
```

```
13 23 24 34 35 36 38 42 47 51 68 74 75 85 97

Please enter an integer value (-1 to quit): 23

13 23 24 34 35 36 38 42 47 51 68 74 75 85 97
                    *
13 23 24 34 35 36 38
        *
13 23 24
    *
The integer 23 was found in position 1.

Please enter an integer value (-1 to quit): 75

13 23 24 34 35 36 38 42 47 51 68 74 75 85 97
                    *
                47 51 68 74 75 85 97
                        *
                            75 85 97
                                *
                                75
                                *
The integer 75 was found in position 12.
```

图 19.5 | 使用二分查找在数组中定位元素（输出中的 * 标记中间元素）。（第 2 部分，共 3 部分。）

