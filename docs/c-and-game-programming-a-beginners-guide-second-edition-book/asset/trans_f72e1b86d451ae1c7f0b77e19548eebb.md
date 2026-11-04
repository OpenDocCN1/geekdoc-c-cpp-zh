

```
int[] our_array = new int[array_size];
int number, total;

CreateArray(our_array, array_size);

Console.WriteLine("Enter a number between 1-100:");
input = Console.ReadLine();
number = int.Parse(input);

total = Comparison (our_array, number, array_size);
Console.WriteLine("That number occurred {0} times", total);
}

// creates a random array with values between 1 and 100
static void CreateArray (int[] random_array, int size) {
Random rnd = new Random();

for (int index = 0; index < size; index++)
    random_array[index] = (int)Math.Round (rnd.NextDouble () *
100);
}

// searches that array with a linear search
static int Comparison (int[] array, int input, int size) {
int count = 0;
for (int index = 0; index < size; index++)
    if (array[index] == input) count++;
return count;
}
}
```

### 示例 4.21. 冒泡排序和二分查找（在数组中查找一个数字）。

```
using System;

namespace Chapter4 {
    class Class1 {
        static void Main() {
            string ScreenInput;
            const long array_size = 100;
            long[] our_array = new long[array_size];
            long input;
```

## C# 与游戏编程

```
bool found = false;

CreateArray (our_array);
BubbleSort (our_array);

while (true) {
    Console.WriteLine("Enter a number between 1-100:");
    ScreenInput = Console.ReadLine();
    input = long.Parse(ScreenInput);

    BinarySearch(our_array, array_size, input, array_size - 1,
                 0, ref found);

    if (found)
        Console.WriteLine("Value found!");
    else
        Console.WriteLine("Value not found!");

    found = false;
}

// This function creates a random array of numbers
// with values between 1 and 100
static void CreateArray (long[] random_array) {
    Random rnd = new Random ();

    for (int index = 0; index < random_array.Length; index++)
        random_array[index] = (long)(rnd.NextDouble() * 100+1);
}

static void BubbleSort (long[] my_array) {
    long temp = 0;
    Console.WriteLine("\nRandom numbers inputted in this order");

    for (int i = 0; i < my_array.Length; i++) {
        Console.WriteLine(my_array[i]);}
    // sort
    for (int i = 0; i < my_array.Length; i++) {
        for (int j = 0; j < my_array.Length-1; j++) {
            if (my_array[j] > my_array[j+1]) {
                temp = my_array[j];
                my_array[j] = my_array[j+1];
                my_array[j+1] = temp;
            }
        }
    }
}
```

```
}
}
Console.WriteLine("\nSorting...\n"
    + "\nIn ascending order");

for (int index = 0; index < my_array.Length; index++) {
    Console.WriteLine(my_array[index]);
}

Console.WriteLine();
}

// this function searches and compares
// data using a binary search pattern.
static void BinarySearch(long[] array, long size, long input,
    long high, long low, ref bool found) {
    if (input < array[(size / 2) - 1]) {
        if (low == array[high - 1])
            found = true;
        else if (input < array[(high / 2) - 1])
            BinarySearch(array, size, input, high / 2, low,
                ref found);
        else if (high > low)
            BinarySearch(array, size, input, (high - 1), low,
                ref found);
    }
    else if (input > array[(size / 2) - 1]) {
        if (low < 0 && input == array[low])
            found = true;
        else if (input > array[((high + low) / 2) - 1] &&
                (high - low) >= 2)
            BinarySearch(array, size, input, high,
                (high + low) / 2, ref found);
        else if (low < high)
            BinarySearch(array, size, input, high, (low + 1),
                ref found);
    }
}
}
}
}
```

## C# 中的动态数组

动态一词被定义为适应或更改原本受限的一组编码的能力。最突出的例子是动态变量（我们所认为的标准变量）。与“常量”不同，这个变量在编译时和执行期间几乎可以调整为任何值。虽然 C# 数组的定义比 C++ 或 C 版本的定义要动态得多，但它仍然是一个常量参数，在程序运行过程中不能更改。不过，我们可以使用非常量整数变量类型，让数组包含在运行时进行的动态计算评估。同样，这与在原生 C++ 下创建动态数组所使用的方法相当相似，其编码实际上与基本 C# 引用相匹配。

声明数组最不方便的方面在于它需要一个常量变量或字面常量，这总是迫使程序员进行猜测，从而可能导致数组要么太小（使其无法完成任务），要么过大（不必要地占用大量急需的系统资源）。这两个问题的解决方案都在于使用动态数组。顾名思义，动态数组是在声明时不需要预定常量的数组，但一旦分配了该值，它们确实需要固定的大小，这几乎是同一回事，但它确实提供了一些新的选择。

由于 C# 总是使用 new 关键字来声明数组，我们实际上不必改变引用这些值的方式就能使其动态化。此外，由于 .Net 结构提供了托管堆，我们不需要引用释放方法（就像在 C++ 中使用 delete 一词所做的那样）。不过，我们至少应该正式定义 new 这个词。该关键字允许我们使用标准变量声明动态数组，然后从堆内部引用这些变量。堆是保留给动态数组、引用变量等的特殊内存区域。要分配数组的参数，只需遵循示例 4.22 中列出的格式（char my_array = new char [array_size];）。

### 示例 4.22. 动态数组。

```
using System;

namespace Chapter4 {
    class Class1 {
        static void Main() {
            string input;
            int array_size;

            Console.Write("How many students in the classroom? ");
            input = Console.ReadLine();
            array_size = int.Parse(input);
```

```
```
```csharp
foreach (char find in integer) {
    if (find == 'I')
        Console.WriteLine("I found {0}", find);
}
}
}
}
}
```
```
```

## 枚举常量整数

另一类有限的集体值版本是称为枚举器的整数数据类型。这种常量整数类型（如带符号和无符号的 short、integer 和 long 值）是一种基本的聚合类型，便于简单的引用操作。它还允许一些独特的引用，例如用户定义的数据结构和对这些声明的赋值列表。初始结构使用关键字 enum 声明，这些值的实例像类引用一样被声明和赋值。如果没有为这些引用分配值，则初始点将为零，并且每个新组件将自动递增一。但是，我们也可以通过从某个任意点（例如 2000）开始来缩短这一过程，或者可以单独声明每个值（参见示例 4.24）。

### 示例 4.24. 枚举整数。

```
```csharp
using System;

namespace Chapter4 {
    class Class1 {
        public enum Months {
            Jan = 1, Feb, Mar, Apr,
                    May, Jun, Jul, Aug, Sep, Oct, Nov, Dec}
        public enum Day {
            AprilFools = 1, Birthday = 16,
            XMas = 25, Feb29 = 29, NYeve = 31}

        public enum Year {Year2 = 2002, Year3, LeapYear}

        static void Main() {
            string input;
            int TheMonth, TheDay, TheYear;
```

```
while (true) {
    Console.Write("Enter the current Month (Example: \"Jan\" = 1): ");
    input = Console.ReadLine();
    TheMonth = int.Parse(input);

    Console.Write("What day of the Month is it? ");
    input = Console.ReadLine();
    TheDay = int.Parse(input);

    Console.Write("What year is it 2002, 2003... ");
    input = Console.ReadLine();
    TheYear = int.Parse(input);

    if (TheMonth == (int)Months.Feb &&
        TheDay == (int)Day.Feb29 &&
        TheYear == (int)Year.LeapYear)
        Console.WriteLine("Happy Leap Year!");

    if (TheMonth == (int)Months.Apr &&
        TheDay == (int)Day.AprilFools)
        Console.WriteLine("April Fool's");

    if (TheMonth == (int)Months.Sep &&
        TheDay == (int)Day.Birthday)
        Console.WriteLine("Happy Birthday!");

    if (TheMonth == (int)Months.Dec) {
        if (TheDay == (int)Day.XMas)
            Console.WriteLine("Merry Christmas!");
        if (TheDay == (int)Day.NYEve)
            Console.WriteLine("Happy New Year!");
    }
}
}
```

## 指针

指针是一种特殊类型的变量，用于访问传统变量所占用的内存空间。它们指向这些位置中保存的值，尽管它们能够评估甚至更改该信息，但它们仍然

