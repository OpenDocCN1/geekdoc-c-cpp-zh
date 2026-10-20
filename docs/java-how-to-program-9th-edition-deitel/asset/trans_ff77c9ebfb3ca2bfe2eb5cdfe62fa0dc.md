

// multiply each element of an array by 2
public static void modifyArray( int[] array2 )
{
    for ( int counter = 0; counter < array2.length; counter++ )
        array2[ counter ] *= 2;
} // end method modifyArray

// multiply argument by 2
public static void modifyElement( int element )
{
    element *= 2;
    System.out.printf(
        "Value of element in modifyElement: %d\n", element );
} // end method modifyElement

} // end class PassArray

传递整个数组引用的效果：
原始数组的值为：
  1  2  3  4  5

修改后数组的值为：
  2  4  6  8  10

传递数组元素值的效果：
modifyElement调用前array[3]的值：8
modifyElement中element的值：16
modifyElement调用后array[3]的值：8

图7.13 | 向方法传递数组和单个数组元素。（第2部分，共2部分。）

第16-17行的增强for语句输出数组的5个int元素。第19行调用方法modifyArray，并将array作为参数传递。方法modifyArray（第36-40行）接收数组引用的副本，并使用该引用将数组的每个元素乘以2。为了证明数组的元素已被修改，第23-24行再次输出数组的5个元素。如输出所示，方法modifyArray使每个元素的值翻倍。我们不能在第38-39行使用增强for语句，因为我们要修改数组的元素。

图7.13接下来演示，当将单个原始类型数组元素的副本传递给方法时，在调用方法中修改该副本不会影响调用方法的数组中该元素的原始值。第26-28行在调用方法modifyElement之前输出array[3]的值。请记住，在调用modifyArray中被修改后，该元素的值现在是8。第30行调用方法modifyElement并将array[3]作为参数传递。请记住，array[3]实际上是数组中的一个int值(8)。因此，程序传递的是array[3]值的副本。方法modifyElement（第43-48行）将接收到的参数值乘以2，将结果存储在其参数element中，然后输出element的值（16）。由于方法参数与局部变量一样，在其声明所在的方法执行完毕时就不再存在，因此方法modifyElement终止时，方法参数element被销毁。当程序将控制权返回给main时，第31-32行输出array[3]未修改的值（即8）。

学生成绩。但这将使得计算成绩总和并确定班级平均分的代码变得臃肿，而且班级一次最多只能处理10个成绩。我们通过将成绩存储在数组中来解决这个问题。

## 在GradeBook类中使用数组存储学生成绩

GradeBook类（图7.14）使用一个int数组来存储若干学生在一次考试中的成绩。这样就无需重复输入相同的成绩集合。数组grades被声明为实例变量（第7行），因此每个GradeBook对象都维护自己的成绩集合。构造函数（第10-14行）有两个参数——课程名称和一个成绩数组。当应用程序（例如图7.15中的GradeBookTest类）创建GradeBook对象时，应用程序会将一个现有的int数组传给构造函数，构造函数将该数组的引用赋给实例变量grades（第13行）。grades数组的大小由传给构造函数的数组长度决定。因此，GradeBook对象可以处理可变数量的成绩。传入的数组中的成绩值可以由用户输入，也可以从磁盘上的文件读取（如第17章所述）。在我们的测试应用程序中，我们用一个包含成绩值的数组进行初始化（图7.15，第10行）。一旦这些成绩存储在GradeBook类的实例变量grades中，该类的所有方法即可根据需要随时访问grades的元素以执行各种计算。

方法processGrades（第37-51行）包含一系列方法调用，输出一份总结成绩的报告。第40行调用方法outputGrades来打印grades数组的内容。方法outputGrades中的第134-136行使用for语句输出学生成绩。在这种情况下必须使用计数器控制的for，因为第135-136行使用计数器变量student的值来将每个成绩输出到特定学生编号旁边（见图7.15的输出）。虽然数组下标从0开始，但教授通常会从1开始对学生编号。因此，第135-136行输出student + 1作为学生编号，以产生“Student 1: ”“Student 2: ”等成绩标签。

// Fig. 7.14: GradeBook.java
// GradeBook class using an array to store test grades.

public class GradeBook
{
    private String courseName; // name of course this GradeBook represents
    private int[] grades; // array of student grades

    // two-argument constructor initializes courseName and grades array
    public GradeBook( String name, int[] gradesArray )
    {
        courseName = name; // initialize courseName
        grades = gradesArray; // store grades
    } // end two-argument GradeBook constructor

    // method to set the course name
    public void setCourseName( String name )
    {
        courseName = name; // store the course name
    } // end method setCourseName

```
21
22 // method to retrieve the course name
23 public String getCourseName()
24 {
25     return courseName;
26 } // end method getCourseName
27
28 // display a welcome message to the GradeBook user
29 public void displayMessage()
30 {
31     // getCourseName gets the name of the course
32     System.out.printf( "Welcome to the grade book for\n%s!\n\n",
33         getCourseName() );
34 } // end method displayMessage
35
36 // perform various operations on the data
37 public void processGrades()
38 {
39     // output grades array
40     outputGrades();
41
42     // call method getAverage to calculate the average grade
43     System.out.printf( "\nClass average is %.2f\n", getAverage() );
44
45     // call methods getMinimum and getMaximum
46     System.out.printf( "Lowest grade is %d\nHighest grade is %d\n\n",
47         getMinimum(), getMaximum() );
48
49     // call outputBarChart to print grade distribution chart
50     outputBarChart();
51 } // end method processGrades
52
53 // find minimum grade
54 public int getMinimum()
55 {
56     int lowGrade = grades[ 0 ]; // assume grades[ 0 ] is smallest
57
58     // loop through grades array
59     for ( int grade : grades )
60     {
61         // if grade lower than lowGrade, assign it to lowGrade
62         if ( grade < lowGrade )
63             lowGrade = grade; // new lowest grade
64     } // end for
65
66     return lowGrade; // return lowest grade
67 } // end method getMinimum
68
69 // find maximum grade
70 public int getMaximum()
71 {
72     int highGrade = grades[ 0 ]; // assume grades[ 0 ] is largest
```

```
// loop through grades array
for ( int grade : grades )
{
    // if grade greater than highGrade, assign it to highGrade
    if ( grade > highGrade )
        highGrade = grade; // new highest grade
} // end for

return highGrade; // return highest grade
} // end method getMaximum

// determine average grade for test
public double getAverage()
{
    int total = 0; // initialize total

    // sum grades for one student
    for ( int grade : grades )
        total += grade;

    // return average of grades
    return (double) total / grades.length;
} // end method getAverage

// output bar chart displaying grade distribution
public void outputBarChart()
{
    System.out.println( "Grade distribution:" );

    // stores frequency of grades in each range of 10 grades
    int[] frequency = new int[ 11 ];

    // for each grade, increment the appropriate frequency
    for ( int grade : grades )
        ++frequency[ grade / 10 ];

    // for each grade frequency, print bar in chart
    for ( int count = 0; count < frequency.length; count++ )
    {
        // output bar label ( "00-09: ", ..., "90-99: ", "100: " )
        if ( count == 10 )
            System.out.printf( "%5d: ", 100 );
        else
            System.out.printf( "%02d-%02d: ",
                count * 10, count * 10 + 9 );

        // print bar of asterisks
        for ( int stars = 0; stars < frequency[ count ]; stars++ )
            System.out.print( "*" );

        System.out.println(); // start a new line of output
    } // end outer for
} // end method outputBarChart
```

