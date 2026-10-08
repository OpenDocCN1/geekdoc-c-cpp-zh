
到目前为止，你已经学习了如何编写日益复杂的 `SELECT` 查询。`SELECT` 查询的结果是一个你可以查看和分析的结果集。相关的语句 `UPDATE` 和 `DELETE` 不产生结果集。相反，它们修改数据库。`DELETE` 语句更容易使用，只需删除你需要的行。例如，要删除加州的所有客户，你会发布语句：

```
DELETE FROM Customer WHERE State = 'CA'
```

`UPDATE` 查询允许你更新满足特定条件的列。例如，在这里你可以为每一项行项目的数量增加一个单位：

```
SET Quantity = Quantity + 1
WHERE Invoice_Number = '11731'
```

你可以通过在 `SET` 子句中指定多个逗号隔开的表达式来更新多个值。`DELETE` 和 `UPDATE` 语句都返回被删除或更新的行数。

- 3. 如何查询阿拉斯加州所有客户的姓名？

- 4. 如何查询夏威夷所有客户的发票号？

现在你可以尝试章节末的练习：22.7, 22.13, 22.14。

## 在不指定条件的情况下连接表

如果你从多个表中选择数据时不加限制，结果将令人惊讶——你会得到一个包含所有值组合的结果。例如，查询：

```
SELECT Invoice_Number, Customer.Name
FROM Invoice, Customer
```

| Invoice_Number | Customer.Name |
| :--- | :--- |
| 11731 | Sam's Appliances |
| 11732 | Electronics Unlimited |
| 11733 | Electronics Unlimited |

可以看出，结果集包含了所有的发票号（11731, 11732）和客户姓名（Sam's Appliances 和 Electronics Unlimited），尽管这些组合并没有真实的数据对应。你需要提供一个 `WHERE` 子句来限制值的组合。例如，查询：

```
SELECT Invoice_Number, Customer.Name
FROM Invoice, Customer
WHERE Invoice.Customer_Number = Customer.Customer_Number
```

产生：

| Invoice_Number | Customer.Name |
| :--- | :--- |
| 11731 | Sam's Appliances |
| 11732 | Electronics Unlimited |
| 11733 | Electronics Unlimited |

# 随机数据库与隐私

大多数公司使用计算机维护客户记录和其他信息的海量数据库。数据库不仅降低了业务成本，还提高了服务质量。如今，从银行网点取款或在线支付账单有多方便已难以想象。随着这些数据库无处不在，它们给公民带来了问题。考虑一下美国政府维护的列出恐怖分子的“禁飞名单”。2007年3月1日，普林斯顿大学的宪法学者、自豪的前陆陆队员 Walter Murphy 教授被拒绝了登机牌。航空公司员工问他：“你进过任何名单吗？”就此，墨菲说：“我没有。”他解释说自己没说过这话，但在2006年9月，他在网上发表了一场讲座，对乔治·布什多次违反宪法进行了全球性批判。“我们知道墨菲不在名单上，是因为他批评了布什政府，还是因为其他危险人物使用了相同的名字。”遭遇类似不幸的旅行者想要离开名单非常困难。这类问题已变得普遍。公司和政府依赖多条可能不准确的信息，然后利用这些信息做出决策。如果你患有某种疾病，保险公司可能会拒绝承保或收取更高的保费。你可能因为信用或医疗报告而被拒绝工作。你可能并不总是知道你的信息存储在何。如果信息可以被检查（如信用报告），它是很难的。

另一个关注的问题是隐私。大多数人不在意别人想知道什么。路易·布兰代（Louis Brandeis）在1928年写道：“隐私是免不受扰的权利——这是时代最全面的权利之一，是文明人最重视的权利。”当雇主能看到你的 Facebook 帖子，律师拥有你的电子邮件并搜索 Google 向你投放“定向”广告时，你剩下的隐私寥寥可几了。

联合国1948年的《世界人权宣言》规定，任何人都不应受到对其隐私、家庭或通信的任意干涉，也不受对其荣誉和名誉的攻击。每个人都有权获得法律保护不受这种非法干涉。美国在间谍活动方面很少的法律保护，除了保护记录和租赁的联邦法律（后者是在最高法院的一个判决后通过的）。其他工业化国家更进一步，承认每个公民都有权控制有关自己的信息应该与他人交流以及在什么情况下交流。

如果你使用电子通行支付或桥梁过路费，你的记录可能不是

## 22.3 安装数据库

存在多种数据库，例如 Oracle、IBM DB2、Microsoft SQL Server、PostgreSQL 或 MySQL。

- 生产环境级数据库，例如 Apache Derby。

- 轻量级 Java 数据库，例如 Microsoft Access。

学习数据库时，你应该选择哪一个？这很大程度上取决于你的可用预算、计算资源以及安装复杂软件的经验。在有受过培训的管理员的实验室环境中，安装一个生产环境级数据库是非常有意义的。轻量级 Java

## 22.3 安装数据库

![](img/6a52d1dde3a219cfa39d548e31d0e6ce_978_0.png)

**图 10** JDBC 架构

数据库在各种平台上的安装和操作要简单得多。这些桌面数据库的 SQL 支持有限，且对于 Java 编程配置可能比较困难。

除了数据库之外，你还需要一个 *JDBC* 驱动程序。JDBC 的全称是 Java Database Connectivity（Java 连接），它是允许 Java 程序与数据库交互的技术名称。当你的程序发布 SQL 命令时，驱动程序会将它们转发到数据库，并让你的程序分析结果（见图 10）。

你需要 JDBC（Java Database Connectivity）来从 Java 程序访问数据库。

不同的数据库需要不同的驱动程序，这些程序可能由数据库制造商或第三方提供。你需要找到并安装与你的数据库匹配的驱动程序。

如果你在实验室工作，会有人为你安装数据库，你应该询问你的实验室关于如何使用它的说明。如果你需要自己提供数据库，我们建议选择 Apache Derby。它随 Java 开发工具包（JDK）一起提供。你也可以从 http://db.apache.org/der/ 下载它。

你应该运行一个测试程序来检查数据库是否工作正常。你将在本节末尾找到测试代码。接下来的章节将详细描述测试程序的实现。如果你使用 Apache Derby，请遵循以下指令：

- 1. 找到 JDBC 驱动文件 **.jar* 并将其复制到此书配套代码的 ch22/section_3目录中。

- 2. 打开终端，进入 ch22/section_3 目录，并运行

```bash
javac Test08.java
java -classpath derby.jar:Test08.properties
```

- 如果你运行 Linux、Mac 或 OS X，使用分号而不是冒号作为路径分隔符：

```bash
java -classpath derby.jar;Test08.properties
```

- 3. 如果你严格遵循了测试说明，你将看到名为 "Romeo" 的输出。你可以跳过本节的剩余部分。

如果你安装的是 Java 自带数据库以外的数据库，你需要留时间执行安装过程。安装数据库的详细说明差异很大。这里我们提供关于如何安装数据库并测试安装的通用步骤序列：

- 1. 安装数据库程序。

- 2. 启动数据库。对于大多数数据库系统（某些轻级 Java 数据库系统外），你需要在执行任何数据库操作之前启动数据库服务器。请阅读安装说明获取详细信息。

- 3. 设置用户账户。这通常涉及运行管理程序、以默认管理员账户登录管理员，并添加名称和密码。如果你是数据库的唯一用户，可能可以直接使用默认账户。再次，不同数据库之间的细节不同，你应该查阅文档。

- 4. 运行测试。找到允许你执行交互式 SQL 指令的数据库。运行程序并查看以下 SQL 指令：

```
CREATE TABLE Test (Name VARCHAR(20))
INSERT INTO Test VALUES ('Romeo')
SELECT * FROM Test
DROP TABLE Test
```

此时，你应该看到一个显示 Test 数据库单行单列的界面，包含字符串 "Romeo"。如果不是，请仔细阅读你的 SQL 工具文档以查看如何输入 SQL 语句。例如，在某些 SQL 工具中，每个 SQL 语句都需要一个特殊的终止符。

接下来，找到 JDBC 驱动程序并运行示例程序以验证安装是否成功。

以下是测试 JDBC 驱动程序的测试：

- 1. 每个 JDBC 驱动程序都包含你的 Java 程序连接数据库所需的 Java 代码。从 JDBC 驱动程序文档中找到驱动程序的类路径。这里是一个典型的示例——随 Java 开发工具包提供的 Apache JDBC 驱动程序的类路径。

```
c:\jdbc1.7.0\lib\derby.jar
```

一个 Oracle 数据库使用类路径

`/usr/local/oracle/jdbc/classes1.zip`

你将在数据库系统的文档中找到这些信息。

- 2. 如果你的 JDBC 驱动程序不完全符合 JDBC4 标准，你需要知道驱动程序的名称。例如，Oracle 数据库使用

```
oracle.jdbc.driver
```

- 3. 找到驱动程序的名称。所有的 JDBC URL 格式如下：

```
jdbc:protocol://host:port/name
```

这里是示例：

```
jdbc:derby:memory:test
jdbc:derby:thin://localhost
```

- 4. 如果你的 JDBC 驱动程序不完全符合 JDBC4 标准，你需要找到驱动程序的类路径。这里是一个典型的示例——随 Java 开发工具包提供的 Apache JDBC 驱动程序的类路径。

```
c:\jdbc1.7.0\lib\derby.jar
```

- 5. 编译程序

```bash
javac Test08.java
```

- 6. 运行程序

```bash
java -classpath derby.jar:Test08.properties
```

如果你运行 Linux、Mac 或 OS X，使用分号而不是冒号作为路径分隔符：

```bash
java -classpath derby.jar;Test08.properties
```

如果一切正常，你将得到名为 "Romeo" 的输出。

## 安装数据库

要从 Java 程序连接数据库，你需要 *JDBC* 驱动程序。JDBC 的全称是 Java Database Connectivity，它是允许 Java 程序与数据库交互的技术名称。当你的程序发布 SQL 命令时，驱动程序会将它们转发到数据库，并让你的程序分析结果（见图 10）。

你需要 JDBC（Java Database Connectivity）来从 Java 程序访问数据库。

不同的数据库需要不同的驱动程序，这些程序可能由数据库制造商或第三方提供。你需要找到并安装与你的数据库匹配的驱动程序。

如果你在实验室工作，会有人为你安装数据库，你应该询问你的实验室关于如何使用它的说明。如果你需要自己提供数据库，我们建议选择 Apache Derby。它随 Java 开发工具包一起提供。你也可以从 http://db.apache.org/der/ 下载。

你应该运行一个测试程序来检查数据库是否工作正常。你将在本节末尾找到测试代码。接下来的章节将详细描述测试程序的实现。如果你使用 Apache Derby，请遵循以下指令：

- 1. 找到 JDBC 驱动文件 **.jar* 并将其复制到此书配套代码的 ch22/section_3目录中。

- 2. 打开终端，进入 ch22/section_3 目录，并运行

```bash
javac Test08.java
java -classpath derby.jar:Test08.properties
```

- 如果你运行 Linux、Mac 或 OS X，使用分号而不是冒号作为路径分隔符：

```bash
java -classpath derby.jar;Test08.properties
```

- 3. 如果你严格遵循了测试说明，你将看到名为 "Romeo" 的输出。你可以跳过本节的剩余部分。

如果你安装的是 Java 自带数据库以外的数据库，你需要留时间执行安装过程。安装数据库的详细说明差异很大。这里我们提供关于如何安装数据库并测试安装的通用步骤序列：

- 1. 安装数据库程序。

- 2. 启动数据库。对于大多数数据库系统（某些轻级 Java 数据库系统外），你需要在执行任何数据库操作之前启动数据库服务器。请阅读安装说明获取详细信息。

- 3. 设置用户账户。这通常涉及运行管理程序、以默认管理员账户登录管理员，并添加名称和密码。如果你是数据库的唯一用户，可能可以直接使用默认账户。再次，不同数据库之间的细节不同，你应该查阅文档。

- 4. 运行测试。找到允许你执行交互式 SQL 指令的数据库。运行程序并查看以下 SQL 指令：

```
CREATE TABLE Test (Name VARCHAR(20))
INSERT INTO Test VALUES ('Romeo')
SELECT * FROM Test
DROP TABLE Test
```

此时，你应该看到一个显示 Test 数据库单行单列的界面，包含字符串 "Romeo"。如果不是，请仔细阅读你的 SQL 工具文档以查看如何输入 SQL 语句。例如，在某些 SQL 工具中，每个 SQL 语句都需要一个特殊的终止符。

接下来，找到 JDBC 驱动程序并运行示例程序以验证安装是否成功。

以下是测试 JDBC 驱动程序的测试：

- 1. 每个 JDBC 驱动程序都包含你的 Java 程序连接数据库所需的 Java 代码。从 JDBC 驱动程序文档中找到驱动程序的类路径。这里是一个典型的示例——随 Java 开发工具包提供的 Apache JDBC 驱动程序的类路径。

```
c:\jdbc1.7.0\lib\derby.jar
```

一个 Oracle 数据库使用类路径

`/usr/local/oracle/jdbc/classes11.zip`

你将在数据库系统的文档中找到这些信息。

- 2. 如果你的 JDBC 驱动程序不完全符合 JDBC4 标准，你需要知道驱动程序的名称。例如，Oracle 数据库使用

```
oracle.jdbc.driver
```

- 3. 找到驱动程序的名称。所有的 JDBC URL 格式如下：

```
jdbc:protocol://host:port/name
```

这里是示例：

```
jdbc:derby:memory:test
jdbc:derby:thin://localhost
```

- 4. 如果你的 JDBC 驱动程序不完全符合 JDBC4 标准，你需要找到驱动程序的类路径。这里是一个典型的示例——随 Java 开发工具包提供的 Apache JDBC 驱动程序的类路径。

```
c:\jdbc1.7.0\lib\derby.jar
```

- 5. 编译程序

```bash
javac Test08.java
```

- 6. 运行程序

```bash
java -classpath derby.jar:Test08.properties
```

如果你运行 Linux、Mac 或 OS X，使用分号而不是冒号作为路径分隔符：

```bash
java -classpath derby.jar;Test08.properties
```

如果一切正常，你将得到名为 "Romeo" 的输出。

```java
import java.io.File;
import java.sql.Connection;
import java.sql.ResultSet;
import java.sql.Statement;

/**
 * 通过创建和查询表测试数据库安装。
 */
public class Test08 {
    public static void main(String[] args) throws Exception {
        if (args.length == 0) {
            System.out.println("Usage: java -classpath derby.jar Test08 <properties_file>");
            return;
        }

        SimpleDataSource.init(args[0]);

        Connection conn = SimpleDataSource.getConnection();
        try {
            Statement stat = conn.createStatement();
            stat.execute("CREATE TABLE Test (Name VARCHAR(20))");
            stat.execute("INSERT INTO Test VALUES ('Romeo')");

            ResultSet result = stat.executeQuery("SELECT * FROM Test");
            if (result.next()) {
                System.out.println(result.getString("Name"));
            }
        } finally {
            conn.close();
        }
    }
}
```
