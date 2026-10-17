
```java
import java.sql.Connection;
import java.sql.PreparedStatement;
import java.sql.ResultSet;
import java.sql.SQLException;
import java.sql.Statement;
import java.io.IOException;
import java.io.File;
import java.util.Scanner;

/**
 * 将发票输入数据库。
 * 在运行此程序之前，请确保已添加 customer.sql, Invoice.sql 和 LineItem.sql。
 */
public class InvoiceEntry {
    public static void main(String[] args[]) {
        if (args.length == 0) {
            System.out.println("Usage: java " + File.pathSeparator + "InvoiceEntry");
            return;
        }
        try {
            SimpleDataSource.init(args[0]);
            Connection conn = SimpleDataSource.getConnection();
            Scanner in = new Scanner(System.in);
            addInvoice(in, conn);
        } catch (SQLException e) {
            System.out.println("Database error");
            e.printStackTrace();
        } catch (ClassNotFoundException e) {
            System.out.println("Error loading driver");
            e.printStackTrace();
        } catch (IOException e) {
            System.out.println("Error loading properties");
            e.printStackTrace();
        }
    }

    public static void addInvoice(Scanner in, Connection conn) throws SQLException {
        try {
            int customerNumber = newCustomer(conn, in);
            int id = getNext(conn, "Invoice");
            paredStatement stat = conn.prepareStatement(
                "INSERT INTO invoices VALUES (?, ?, ?)");
            stat.setInt(1, id);
            stat.setString(2, customerNumber);
            stat.executeUpdate();
            stat.close();

            boolean done = false;
            while (!done) {
                String productCode = nextLine(in, "Product code (Done, L-List)");
                if (productCode.equals("D")) { done = true; }
                else if (productCode.equals("L")) { listProducts(conn); }
                else if (findProduct(conn, productCode)) {
                    int quantity = nextInt(in, "Quantity");
                    addItem(conn, id, productCode, quantity);
                } else {
                    System.out.println("Invalid product code.");
                }
            }
            showInvoice(conn, id);
        } finally {
            conn.close();
        }
    }

    /**
     * 提示用户客户信息并创建新客户。
     * @param conn 数据库连接
     * @return 新客户的 ID
     */
    private static int newCustomer(Connection conn, Scanner in) throws SQLException {
        String name = nextLine(in, "Name");
        String address = nextLine(in, "Street address");
        String city = nextLine(in, "City");
        String state = nextLine(in, "State");
        String zip = nextLine(in, "Zip");
        int id = getNext(conn, "Customer");
        paredStatement stat = conn.prepareStatement(
            "INSERT INTO customers VALUES (?, ?, ?, ?, ?)");
        stat.setInt(1, id);
        stat.setString(2, name);
        stat.setString(3, address);
        stat.setString(4, city);
        stat.setString(5, state);
        stat.setString(6, zip);
        stat.executeUpdate();
        stat.close();
        return id;
    }
}
```

# W960 第22章 关系数据库

```java
/**
 * 在数据库中查找产品。
 * @param conn 数据库连接
 * @param code 要搜索的产品代码
 * @return 如果存在给定代码的产品则返回 true
 */
private static boolean findProduct(Connection conn, String code) throws SQLException {
    paredStatement stat = conn.prepareStatement(
        "SELECT * FROM Product WHERE Product_Code = ?");
    stat.setString(1, code);
    ResultSet result = stat.executeQuery();
    boolean found = result.next();
    return found;
}
```

```java
/**
 * 将行项目添加到数据库。
 * @param conn 数据库连接
 * @param id 发票 ID
 * @param code 产品代码
 * @param quantity 订购数量
 */
private static void addItem(Connection conn, int id, String code, int quantity) throws SQLException {
    paredStatement stat = conn.prepareStatement(
        "INSERT INTO LineItem (?, ?, ?)");
    stat.setInt(1, id);
    stat.setString(2, code);
    stat.setInt(3, quantity);
    stat.executeUpdate();
    stat.close();
}
```

```java
/**
 * 列出数据库中的所有产品。
 * @param conn 数据库连接
 */
private static void listProducts(Connection conn) throws SQLException {
    Statement stat = conn.createStatement();
    ResultSet result = stat.executeQuery(
        "SELECT Product_Code, Description FROM Product");
    while (result.next()) {
        String code = result.getString(1);
        String description = result.getString(2);
        System.out.println(code + " - " + description);
    }
    stat.close();
}
```

```
/**
 * 为表获取新 ID。此方法应该在事务内部调用，该事务同时也创建带有此 ID 的新行。
 * ID 字段名称应为 table_Number，类型为 INTEGER。
 */
```

## 22.5 应用：输入发票

```java
/**
 * @param table the table name
 * @return a new ID that has not yet been used.
 */
private static int getNext(Connection conn {
```

# 第22 章 关系数据库

```java
237 @param prompt the prompt
238 @return the string that the user entered
239 */
240 private static String nextLine(Scanner in, String prompt)
241 {
242 System.out.print(prompt + ": ");
243 return in.nextLine();
244 }
246 /*
247 提示用户并从扫描器读取一个整数。
248 @param prompt the prompt
249 @return the integer that the user entered
250 */
251 private static int nextInt(Scanner in, String prompt)
252 {
253 System.out.print(prompt + ": ");
254 int result = in.nextInt();
255 in.nextLine(); // 消费换行符
256 return result;
257 }
```

这个示例完成了 Java 数据库编程的介绍。你已经看到了如何使用 SQL 查询和更新数据库中的数据，以及 JDBC 库如何方便在 Java 程序中发布 SQL 命令。

![](img/6a52d1dde3a219cfa39d548e31d0e6ce_997_0.png)

- 9. 为什么 `nextEntry` 方法抛出 `SQLException` 而不是捕获它？
- 10. 你如何简化 `showInvoice` 方法的查询？
- 11. 该程序假设客户在输入订单时不需要付款。如何修改程序来处理付款？
- 12. 该程序没有显示欠金额。我们该如何显示它？

## 课练习

现在你可以尝试章节末的练习题：`P22.7`, `P22.8`。

## 特题 2.2：事务

数据库处理的一个重要部分是事务处理。事务是一组更新，它们要么全部成功，要么完全不执行。例如，考虑一个从一个账户转账到另一个账户的银行应用程序，这涉及两个步骤：减少一个账户的余额和增加另一个账户的余额。没有任何软件系统是完美的，错误总是可能。银行应用程序可能在执行第一部分后出现错误——那么钱就会从第一个账户中取出，但从未存入第二个账户。显然这将非常糟糕。还有许多类似的情况。例如，如果你更改了机票预订，在确认新座位之前，你不想放弃旧座位。

所有这些情况的共同点是有一组数据库操作被组合在一起执行事务。组中的所有操作都必须执行——不能容忍部分提交。在 SQL 中，你使用 `COMMIT` 和 `ROLLBACK` 命令来管理事务。

## 22.5 应用：输入发票

```sql
例如，要从一个账户转账到另一个账户，你发布以下命令：
UPDATE accounts SET Balance = Balance - 1000
WHERE Account_Number = '95667-2574'
UPDATE accounts SET Balance = Balance + 1000
WHERE Account_Number = '82041-1196'
COMMIT
```

`COMMIT` 命令执行更新。相反，`ROLLBACK` 命令会撤销自上一次 `COMMIT` 的所有的所有。

当你使用 JDBC 编程时，默认会自动提交所有数据库更新。这对于简单程序很方便，但并不是你事务处理时需要的。你应该先关闭自动提交：

```java
Connection conn;
conn.setAutoCommit(false);
Statement stmt = conn.createStatement();
```

然后执行构成事务的所有语句，并调用 `Statement` 类的 `commit` 方法：

```java
stmt.executeUpdate("UPDATE accounts SET Balance = Balance - "
+ amount + " WHERE Account_Number = " + fromAccount);
```

相反，如果你遇到错误，则调用滚动方法。这通常发生在异常处理器中：

```java
try {
    // 执行语句
} catch (Exception ex) {
    conn.rollback();
}
```
