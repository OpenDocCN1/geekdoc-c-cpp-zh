
严格来说，正是为此而设的。任何学习者只要参加本课程并认真遵循，毫无疑问必将看到努力的成果。

## 嵌套循环为新手/初学者/入门者/缺乏自信的程序员提供了良好的反复练习。

一旦学习者对编程产生兴趣，所有学习都会变得令人兴奋和激动。当学习者对自己独立开发编程逻辑有了一些信心时，这种兴趣会自然产生。为此，只需要把极少数内容练好，而本书已以适当的深度涵盖这些内容。我真诚地建议：在查阅任何其他资源之前，请先从头到尾学习并练习本书。

这本书能帮助你更快进步，它算是编程前必不可少的热身训练。我个人不认同这种说法：那些放弃学习编程的人能力较差；实际上，是付出努力这件事无法让他们感到兴奋。一个人的学习节奏无论快慢都无关紧要，重要的是对学习的投入。没有兴趣，根本不可能有真正意义上的投入。这本书的核心就是正确培养兴趣和信心——相信任何人只要朝着正确方向付出一些努力就能编程。

选择这些练习和问题，主要是为了让学习能够自然地适应任何学习者。学习者只需遵循本书中提到的分步说明。

当你自然地学习并完成训练时，对编程的信心和兴趣必将得到保证。这不仅仅是一本书，本质上是一本训练指南。初期肯定需要付出一些努力和耐心。一旦学习者理解了所需的基础知识，后续的进步将因对这门学科的巨大热爱而突飞猛进，而这种热爱会在练习过程中自然产生。这组练习是为面向初学者——即没有任何编程经验或只有一些编程经验的人——教授编程而开展实验的成果。

完成这些练习后，每个人都能在2至3个月的时间内建立起相当程度的信心。最大的亮点在于，学生们对编程产生了兴趣。编程对他们而言不再无聊，也不再是负担。学习者将能够自然培养出耐心的倾向，从而推动自己解决问题并保持完全专注。简而言之，它让学习变得有趣。

### 练习6B.1

在外层 for 循环的一次迭代中，对于外层 for 循环的每一个取值，内层 for 循环都会完整执行。内层 for 循环的完整执行被视为一条普通语句的执行。除非内层 for 循环完全执行完毕，否则外层 for 循环不会进行下一次迭代。下面的程序演示了针对每一个行值，垂直打印各列值。

**ForLoopEveryRowAllColumns.c**

```c
#include <stdio.h>

int main() {

    int TOTAL_ROWS = 3;
    int TOTAL_COLUMNS = 3;

    for( int row = 1; row <= TOTAL_ROWS ; row ++ ) {

        for( int col = 1; col <= TOTAL_COLUMNS ; col ++ ) {

            printf( "Row = %d |  Col = %d\n" , row, col);

        }

        printf("------------------------------\n");

    }

    return 0;

}
```

**输出**

```text
Row = 1 | Col = 1
Row = 1 | Col = 2
Row = 1 | Col = 3
------------------------------
Row = 2 | Col = 1
Row = 2 | Col = 2
Row = 2 | Col = 3
------------------------------
Row = 3 | Col = 1
Row = 3 | Col = 2
Row = 3 | Col = 3
------------------------------
```

### 练习6B.2. 针对行的每个迭代值，水平打印列迭代值。每个行值应位于不同的行。因此，行级迭代值会垂直打印。

**ForLoopEveryRowAllColumnsHorizontally.c**

```java
public class ForLoopEveryRowAllColumnsHorizontally {
    public static void main(String[] args) {
        int TOTAL_ROWS = 3;
        int TOTAL_COLUMNS = 3;

        for( int row = 1 ; row <= TOTAL_ROWS ; row ++ ) {
            printf( "Row = " + row + " |" );
            for( int col = 1 ; col <= TOTAL_COLUMNS ; col ++ ) {
                printf( " Col = " + col);
            }
            // control moves to the next line and this how
            // printing of row and col values happens in the next row
            printf("\n");
        }
    }
}
```

**输出**

```text
Row = 1| Col = 1 Col = 2 Col = 3
Row = 2| Col = 1 Col = 2 Col = 3
Row = 3| Col = 1 Col = 2 Col = 3
```

- **问题6B.2：** 在行数和列数均为3的情况下，编写程序输出以下结果。

```text
Row = 1| Col = 1
Row = 2| Col = 2
Row = 3| Col = 3
--------------------------------
Row = 4| Col = 1
Row = 5| Col = 2
Row = 6| Col = 3
--------------------------------
Row = 7| Col = 1
Row = 8| Col = 2
Row = 9| Col = 3
--------------------------------
```

### 练习6B.3. 按如下输出所示，将行迭代值和列迭代值打印为 (row, col)

```text
(1,1) (1,2) (1,3) (1,4) (1,5)
(2,1) (2,2) (2,3) (2,4) (2,5)
(3,1) (3,2) (3,3) (3,4) (3,5)
(4,1) (4,2) (4,3) (4,4) (4,5)
(5,1) (5,2) (5,3) (5,4) (5,5)
```

**ForLoopCoordinateRepresentation.c**

```c
#include <stdio.h>

int main() {
    int TOTAL_ROWS = 5;
    int TOTAL_COLUMNS = 5;

    for( int row = 1 ; row <= TOTAL_ROWS ; row ++ ) {
        for( int col = 1 ; col <= TOTAL_COLUMNS ; col ++ ) {
            printf("(%d,%d) ", row, col);
        }

        // moves the control to the next line and
        // prints next row iteration value

        printf("\n");
        printf("\n");
    }

    return 0;
}
```

**输出**

```text
(1,1) (1,2) (1,3) (1,4) (1,5)
(2,1) (2,2) (2,3) (2,4) (2,5)
(3,1) (3,2) (3,3) (3,4) (3,5)
(4,1) (4,2) (4,3) (4,4) (4,5)
(5,1) (5,2) (5,3) (5,4) (5,5)
```

### 练习6B.4. 针对每个 (row, col) 迭代值打印字符“*”，从而生成图案。

**RowColumnStars.c**

```c
#include <stdio.h>
int main() {
    int TOTAL_ROWS = 10;
    int TOTAL_COLUMNS = 10;
    for( int row = 1 ; row <= TOTAL_ROWS ; row++ ) {
        for( int col = 1 ; col <= TOTAL_COLUMNS ; col++ ) {
            printf("* ");
        }
        // moves the control to the next line
        // printing of "*" characters starts from next line
        printf("\n");
    }
    return 0;
}
```

**输出**

```text
* * * * * * * * * *
* * * * * * * * * *
* * * * * * * * * *
* * * * * * * * * *
* * * * * * * * * *
* * * * * * * * * *
* * * * * * * * * *
* * * * * * * * * *
* * * * * * * * * *
* * * * * * * * * *
```

- **问题6B.3：** 在行数和列数均为5的情况下，编写程序输出以下结果。

**输出**

```text
* - * - *
* - * - *
* - * - *
* - * - *
* - * - *
```

## 形状问题：为以下每种不同类型的输出编写一个程序。

### 输出-A

```text
1==1 1==2 1==3 1==4 1==5
2==1 2==2 2==3 2==4 2==5
3==1 3==2 3==3 3==4 3==5
4==1 4==2 4==3 4==4 4==5
5==1 5==2 5==3 5==4 5==5
```

### 输出-B

### 输出-C

```text
1<=1 1<=2 1<=3 1<=4 1<=5
2<=1 2<=2 2<=3 2<=4 2<=5
3<=1 3<=2 3<=3 3<=4 3<=5
4<=1 4<=2 4<=3 4<=4 4<=5
5<=1 5<=2 5<=3 5<=4 5<=5
```

### 输出-D

```text
3<1 3<2 3<3 3<4 3<5 3<6 3<7 3<8
4<1 4<2 4<3 4<4 4<5 4<6 4<7 4<8
5<1 5<2 5<3 5<4 5<5 5<6 5<7 5<8
6<1 6<2 6<3 6<4 6<5 6<6 6<7 6<8
7<1 7<2 7<3 7<4 7<5 7<6 7<7 7<8
8<1 8<2 8<3 8<4 8<5 8<6 8<7 8<8
```

### 输出-E

```text
1>1 1>2 1>3 1>4 1>5 1>6
2>1 2>2 2>3 2>4 2>5 2>6
3>1 3>2 3>3 3>4 3>5 3>6
4>1 4>2 4>3 4>4 4>5 4>6
5>1 5>2 5>3 5>4 5>5 5>6
6>1 6>2 6>3 6>4 6>5 6>6
```

### 输出-F

```text
1>=1 1>=2 1>=3 1>=4 1>=5 1>=6 1>=7 1>=8
2>=1 2>=2 2>=3 2>=4 2>=5 2>=6 2>=7 2>=8
3>=1 3>=2 3>=3 3>=4 3>=5 3>=6 3>=7 3>=8
4>=1 4>=2 4>=3 4>=4 4>=5 4>=6 4>=7 4>=8
5>=1 5>=2 5>=3 5>=4 5>=5 5>=6 5>=7 5>=8
```

### 输出-G

### 输出-F

## 如何验证逻辑条件？

让我们验证以下用7行5列表示的字母 M 的逻辑条件：

(col==1)||(col==5)||( ((row==col)||(row+col ==6) ) && row<=3 )

**VerifyAlphabetM.c**

```c
#include <stdio.h>

int main() {
    int TOTAL_ROWS = 7;
    int TOTAL_COLUMNS = 5;
    int condition; //logical condition variable
    for ( int row = 1; row <= TOTAL_ROWS; row++) {
        for ( int col = 1; col <= TOTAL_COLUMNS; col++) {
            condition = (col == 1) || (col == 5) ||
                ( ((row == col) || (row + col == 6)) && row <= 3 );
            // space(s) are used just to show formatted output.
            if (condition) {
                printf("* "); // single space
            } else {
                printf("  ");// double space
            }
        }
        printf("\n");// Move cursor to the next row
    }
    return 0;
}
```

**输出**

```text
*   *
* *  *
* *  *
*   *
*   *
*   *
*   *
```
