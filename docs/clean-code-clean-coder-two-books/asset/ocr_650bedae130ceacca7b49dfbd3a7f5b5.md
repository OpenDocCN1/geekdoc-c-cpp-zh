```
```java
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
```

# **Listing 10-8 PrimeGenerator.java**

```
```java
package literatePrimes;

import java.util.ArrayList;

public class PrimeGenerator {
```
```