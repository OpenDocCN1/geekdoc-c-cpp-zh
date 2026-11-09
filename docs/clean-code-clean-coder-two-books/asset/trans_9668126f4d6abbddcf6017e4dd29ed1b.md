
作为我意图的演示，让我们使用一个取自Knuth的精彩著作《*文学化编程*》¹中的经典示例。清单10-5展示了Knuth的`PrintPrimes`程序的一个Java翻译版本。为了对Knuth公平起见，这并非他原始编写的程序，而是由他的WEB工具输出的程序。我使用它，是因为它是将一个大函数分解为许多更小函数和类的绝佳起点。

## 清单10-5 PrintPrimes.java

```java
package literatePrimes;

public class PrintPrimes {
  public static void main(String[] args) {
    final int M = 1000;
    final int RR = 50;
    final int CC = 4;
    final int WW = 10;
    final int ORDMAX = 30;
    int P[] = new int[M + 1];
    int PAGENUMBER;
    int PAGEOFFSET;
    int ROWOFFSET;
    int C;

    int J;
    int K;
    boolean JPRIME;
    int ORD;
    int SQUARE;
    int N;
    int MULT[] = new int[ORDMAX + 1];

    J = 1;
    K = 1;
    P[1] = 2;
    ORD = 2;
    SQUARE = 9;

    while (K < M) {
        do {
            J = J + 2;
            if (J == SQUARE) {
                ORD = ORD + 1;
                SQUARE = P[ORD] * P[ORD];
                MULT[ORD - 1] = J;
            }
            N = 2;
            JPRIME = true;
            while (N < ORD && JPRIME) {
                while (MULT[N] < J)
                    MULT[N] = MULT[N] + P[N] + P[N];
                if (MULT[N] == J)
                    JPRIME = false;
                N = N + 1;
            }
        } while (!JPRIME);
        K = K + 1;
        P[K] = J;
    }
    {
        PAGENUMBER = 1;
        PAGEOFFSET = 1;
        while (PAGEOFFSET <= M) {
            System.out.println("The First " + M +
                    " Prime Numbers --- Page " + PAGENUMBER);
            System.out.println("");
            for (ROWOFFSET = PAGEOFFSET; ROWOFFSET <
                    PAGEOFFSET + RR; ROWOFFSET++) {
                for (C = 0; C < CC; C++)
                    if (ROWOFFSET + C * RR <= M)
                        System.out.format("%10d", P[ROWOFFSET + C * RR]);
                System.out.println("");
            }
            System.out.println("\f");
            PAGENUMBER = PAGENUMBER + 1;
        }
    }
  }
}
```

```java
import java.io.PrintStream;

public class RowColumnPagePrinter {
    private int rowsPerPage;
    private int columnsPerPage;
    private int numbersPerPage;
    private String pageHeader;
    private PrintStream printStream;

    public RowColumnPagePrinter(int rowsPerPage,
                                int columnsPerPage,
                                String pageHeader) {
        this.rowsPerPage = rowsPerPage;
        this.columnsPerPage = columnsPerPage;
        this.pageHeader = pageHeader;
        numbersPerPage = rowsPerPage * columnsPerPage;
        printStream = System.out;
    }

    public void print(int data[]) {
        int pageNumber = 1;
        for (int firstIndexOnPage = 0;
             firstIndexOnPage < data.length;
             firstIndexOnPage += numbersPerPage) {
            int lastIndexOnPage =
                Math.min(firstIndexOnPage + numbersPerPage - 1,
                         data.length - 1);
            printPageHeader(pageHeader, pageNumber);
            printPage(firstIndexOnPage, lastIndexOnPage, data);
            printStream.println("\f");
            pageNumber++;
        }
    }

    private void printPage(int firstIndexOnPage,
                           int lastIndexOnPage,
                           int[] data) {
        int firstIndexOfLastRowOnPage =
            firstIndexOnPage + rowsPerPage - 1;
        for (int firstIndexInRow = firstIndexOnPage;
             firstIndexInRow <= firstIndexOfLastRowOnPage;
             firstIndexInRow++) {
            printRow(firstIndexInRow, lastIndexOnPage, data);
            printStream.println("");
        }
    }

    private void printRow(int firstIndexInRow,
                          int lastIndexOnPage,
                          int[] data) {
        for (int column = 0; column < columnsPerPage; column++) {
            int index = firstIndexInRow + column * rowsPerPage;
            if (index <= lastIndexOnPage)
                printStream.format("%10d", data[index]);
        }
    }

    private void printPageHeader(String pageHeader,
                                 int pageNumber) {
        printStream.println(pageHeader + " --- Page " + pageNumber);
        printStream.println("");
    }

    public void setOutput(PrintStream printStream) {
        this.printStream = printStream;
    }
}
```

## 清单10-8 PrimeGenerator.java

```java
package literatePrimes;

import java.util.ArrayList;

public class PrimeGenerator {

    private static int[] primes;
    private static ArrayList<Integer> multiplesOfPrimeFactors;

    protected static int[] generate(int n) {
        primes = new int[n];
        multiplesOfPrimeFactors = new ArrayList<Integer>();
        set2AsFirstPrime();
        checkOddNumbersForSubsequentPrimes();
        return primes;
    }

    private static void set2AsFirstPrime() {
        primes[0] = 2;
        multiplesOfPrimeFactors.add(2);
    }

    private static void checkOddNumbersForSubsequentPrimes() {
        int primeIndex = 1;
        for (int candidate = 3;
             primeIndex < primes.length;
             candidate += 2) {
            if (isPrime(candidate))
                primes[primeIndex++] = candidate;
        }
    }

    private static boolean isPrime(int candidate) {
        if (isLeastRelevantMultipleOfNextLargerPrimeFactor(candidate)) {
            multiplesOfPrimeFactors.add(candidate);
            return false;
        }
        return isNotMultipleOfAnyPreviousPrimeFactor(candidate);
    }

    private static boolean
    isLeastRelevantMultipleOfNextLargerPrimeFactor(int candidate) {
        int nextLargerPrimeFactor = primes[multiplesOfPrimeFactors.size()];
```

## 清单10-9 一个必须为了变更而开放的类

```java
public class Sql {
    public Sql(String table, Column[] columns)
    public String create()
    public String insert(Object[] fields)
    public String selectAll()
    public String findByKey(String keyColumn, String keyValue)
    public String select(Column column, String pattern)
    public String select(Criteria criteria)
    public String preparedInsert()
    private String columnList(Column[] columns)
    private String valuesList(Object[] fields, final Column[] columns)
    private String selectWithCriteria(String criteria)
    private String placeholderList(Column[] columns)
}
```

当我们添加一种新类型的语句时，`Sql`类必须变更。当我们修改单个语句类型的细节时，它也必须变更——例如，如果我们需要修改select功能以支持子查询。这两个变更原因意味着`Sql`类违反了SRP。

我们可以从简单的组织角度发现这种SRP违规。`Sql`的方法轮廓显示，有一些私有方法，如`selectWithCriteria`，似乎只与select语句相关。

仅适用于类中一小部分子集的私有方法行为，可以作为识别潜在改进领域的有用启发。然而，采取行动的主要诱因应该是系统变更本身。如果`Sql`类在逻辑上是完整的，那么我们就不必担心分离职责。如果在可预见的未来我们不需要更新功能，那么我们应该让`Sql`保持原样。但是，一旦我们发现自己在打开一个类进行修改，就应该考虑修复我们的设计。

如果我们考虑像[清单10-10]中那样的解决方案会怎样？在[清单10-9]中的先前`Sql`中定义的每个公共接口方法都被重构为`Sql`类的自己的派生类。注意，私有方法（如`valuesList`）直接移动到需要它们的地方。常见的私有行为被隔离到一对工具类`Where`和`ColumnList`中。

```java
@Override public String generate()
```

```java
public class PreparedInsertSql extends Sql {
    public PreparedInsertSql(String table, Column[] columns)
    @Override public String generate() {
    private String placeholderList(Column[] columns)
}
```

```java
public class Where {
    public Where(String criteria)
    public String generate()
}
```

```java
public class ColumnList {
    public ColumnList(Column[] columns)
    public String generate()
}
```

每个类中的代码变得极其简单。我们理解任何类所需的时间减少到几乎为零。一个函数破坏另一个函数的风险变得微乎其微。从测试的角度来看，证明此解决方案中的所有逻辑位变得更加容易，因为所有类都彼此隔离。

同样重要的是，当需要添加更新语句时，现有的类都不需要变更！我们在`Sql`的一个名为`UpdateSql`的新子类中编写构建更新语句的逻辑。系统中的其他代码不会因为此变更而破坏。

我们重构后的`Sql`逻辑集所有优点于一身。它支持SRP。它还支持另一个关键的面向对象类设计原则，即开闭原则（Open-Closed Principle，OCP）。<sup>4</sup> 类应该对扩展开放，但对修改关闭。我们重构后的`Sql`类通过子类化开放以允许新功能，但我们可以在保持其他所有类关闭的情况下进行此变更。我们只需将`UpdateSql`类直接放到适当位置。

我们希望构建我们的系统，以便在使用新功能或变更功能更新系统时，尽可能少地改动。在一个理想的
