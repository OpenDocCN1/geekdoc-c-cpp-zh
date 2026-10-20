
- 可以将每个 ResultSet 列提取为特定的 Java 类型。ResultSetMetaData 的 getColumnType 方法（第 1193 页）返回一个 Types（第 1193 页）常量（包 java.sql），指示该列的类型。
- ResultSet 的 get 方法通常接收列号（int）或列名（String）作为参数，以指示要获取哪一列的值。
- ResultSet 的行号和列号从 1 开始。
- 每个 Statement 对象一次只能打开一个 ResultSet。当 Statement 返回新的 ResultSet 时，该 Statement 会关闭先前的 ResultSet。
- Connection 的 createStatement 方法有一个重载版本，接收结果类型和并发性。结果类型指定 ResultSet 的游标是能够双向滚动还是仅向前滚动，以及 ResultSet 是否对更改敏感。结果并发性（第 1199 页）指定 ResultSet 是否可更新。
- 某些 JDBC 驱动程序（第 1172 页）不支持可滚动或可更新的 ResultSet。

## 28.8.2 节 查询 books 数据库

- TableModel（第 1194 页）的 getColumnClass 方法（第 1194 页）返回一个 Class 对象，该对象表示特定列中所有对象的超类。JTable（第 1194 页）利用此信息在 JTable 中为该列设置默认单元格渲染器和单元格编辑器。
- ResultSetMetaData 的 getColumnClassName 方法（第 1200 页）获取列的全限定类名（第 1183 页）。
- TableModel 的 getColumnCount 方法（第 1194 页）返回 ResultSet 中的列数。
- TableModel 的 getColumnName 方法（第 1194 页）返回 ResultSet 中的列名。
- ResultSetMetaData 的 getColumnName 方法（第 1200 页）从 ResultSet 获取列名。
- TableModel 的 getRowCount 方法（第 1194 页）返回模型的 ResultSet 中的行数。
- TableModel 的 getValueAt 方法（第 1194 页）返回模型底层 ResultSet 中特定行和列处的 Object。
- ResultSet 的 absolute 方法（第 1200 页）将 ResultSet 游标定位到特定行。
- AbstractTableModel 的 fireTableStructureChanged 方法（第 1200 页）通知使用特定 TableModel 对象作为模型的任何 JTable：模型中的数据已更改。

## 28.9 节 RowSet 接口

- RowSet 接口（第 1207 页）配置数据库连接并自动执行查询。
- 连接型 RowSet（第 1207 页）在使用对象期间保持与数据库的连接。断开连接型 RowSet（第 1207 页）连接、执行查询，然后关闭连接。
- JdbcRowSet（第 1207 页）是一种连接型 RowSet，它包装 ResultSet 对象，并允许滚动和更新其行。与 ResultSet 对象不同，JdbcRowSet 对象默认是可滚动和可更新的。
- CachedRowSet（第 1207 页）是一种断开连接型 RowSet，它将 ResultSet 的数据缓存在内存中。CachedRowSet 是可滚动和可更新的。CachedRowSet 也是可序列化的。

## 28.10 节 Java DB/Apache Derby

- Java DB（第 1209 页）有嵌入式版本和网络版本。

## 28.11 节 PreparedStatements

- PreparedStatements（第 1211 页）经过编译，因此它们的执行效率比 Statements 更高。
- PreparedStatements 可以有参数，因此同一个查询可以使用不同参数执行。
- 在 SQL 语句中，参数用问号 (?) 指定。在执行 PreparedStatement 之前，必须使用 PreparedStatement 的 set 方法指定参数。
- PreparedStatement 的 setString 方法（第 1211 页）的第一个参数表示要设置的参数编号，第二个参数是该参数的值。
- 参数编号从 1 开始计数，从第一个问号 (?) 开始。
- setString 方法会根据需要自动转义 String 参数值。
- PreparedStatement 接口为每种受支持的 SQL 类型提供 set 方法。
- 标识列是 SQL 中表示自动递增（第 1174 页）列的标准方式。SQL IDENTITY 关键字（第 1212 页）将列标记为标识列。

## 28.12 节 存储过程

- JDBC 使程序能够使用 CallableStatement（第 1226 页）对象调用存储过程（第 1226 页）。
- CallableStatement 可以指定输入参数。CallableStatement 可以指定输出参数（第 1226 页），存储过程可以在输出参数中放置返回值。

## 28.13 节 事务处理

- 事务处理（第 1227 页）使与数据库交互的程序能够将数据库操作（或一组操作）视为单个操作——称为原子操作（第 1227 页）或事务（第 1227 页）。
- 在事务结束时，可以决定提交或回滚事务。
- 提交事务（第 1227 页）使数据库操作最终生效——不执行新的数据库操作，插入、更新和删除操作无法撤销。
- 回滚事务（第 1227 页）使数据库保持在该数据库操作之前的状态。
- Java 通过 Connection 接口的方法提供事务处理。
- setAutoCommit 方法（第 1227 页）指定每条 SQL 语句在完成后是否提交（参数为 true），还是将多条 SQL 语句分组为事务。
- 禁用自动提交时，程序必须在事务中的最后一条 SQL 语句之后调用 Connection 的 commit 方法（以将更改提交到数据库；第 1227 页）或 Connection 的 rollback 方法（以使数据库返回事务之前的状态；第 1227 页）。
- getAutoCommit 方法（第 1227 页）确定 Connection 的自动提交状态。

## 自测练习

28.1 在下列各条语句中填空：

- a) 国际标准数据库语言是 _______。
- b) 数据库中的表由 _______ 和 _______ 组成。
- c) Statement 对象以 _______ 对象的形式返回 SQL 查询结果。
- d) _______ 唯一标识表中的每一行。
- e) SQL 关键字 _______ 后接选择条件，指定在查询中选择哪些行。
- f) SQL 关键字 _______ 指定查询中行的排序顺序。
- g) 合并多个数据库表中的行称为 _______ 表。
- h) _______ 是有组织的数据集合。
- i) _______ 是其值与另一个表的主键值匹配的一组列。

## 自测练习答案 1233

- j) 使用 _________ 方法 _________ 获取到数据库的 Connection。
- k) 接口 _________ 有助于管理 Java 程序与数据库之间的连接。
- l) 使用 _________ 对象向数据库提交查询。
- m) 与 ResultSet 对象不同，_________ 和 _________ 对象默认是可滚动和可更新的。
- n) _________ 是一种断开连接型 RowSet，它将 ResultSet 的数据缓存在内存中。

## 自测练习答案

28.1 a) SQL。 b) 行、列。 c) ResultSet。 d) 主键。 e) WHERE。 f) ORDER BY。 g) 连接。 h) 数据库。 i) 外键。 j) DriverManager、getConnection。 k) Connection。 l) Statement。 m) JdbcRowSet、CachedRowSet。 n) CachedRowSet。

## 练习

28.2（books 数据库的查询应用程序）使用本章介绍的技术，为 books 数据库编写一个完整的查询应用程序。提供以下预定义查询：

- a) 从 Authors 表中选择所有作者。
- b) 选择特定作者，并列出该作者的所有图书。包括每本书的书名、年份和 ISBN。先按作者的姓氏字母顺序，再按名字的字母顺序对信息排序。
- c) 选择特定书名，并列出该书名的所有作者。先按作者的姓氏字母顺序，再按名字的字母顺序排序。
- d) 提供你认为合适的任何其他查询。

显示一个 JComboBox，为每个预定义查询提供适当的名称。同时允许用户提供自己的查询。

28.3（books 数据库的数据操作应用程序）为 books 数据库编写一个数据操作应用程序。用户应该能够编辑现有数据并向数据库添加新数据（遵循参照完整性和实体完整性约束）。允许用户通过以下方式编辑数据库：

- a) 添加新作者。
- b) 编辑作者的现有信息。
- c) 为作者添加新书名。（请记住，该书必须在 AuthorISBN 表中有一个条目。）
- d) 在 AuthorISBN 表中添加新条目，以将作者与书名关联起来。

28.4（雇员数据库）在第 10.7 节中，我们介绍了用于计算每位雇员工资的雇员工资层次结构。在本练习中，我们提供一个与雇员工资层次结构相对应的雇员数据库。（本章示例附带了创建 employees MySQL 数据库的 SQL 脚本。）编写一个应用程序，允许用户：

- a) 向 employee 表添加雇员。
- b) 为每位新雇员向适当的表添加工资信息。例如，对于固定薪金雇员，将工资信息添加到 salariedEmployees 表。

图 28.33 是 employees 数据库的实体-关系图。

28.5（雇员数据库查询应用程序）修改练习 28.4，提供 JComboBox 和 JTextArea，使用户能够执行从 JComboBox 中选择或在 JTextArea 中定义的查询。示例预定义查询如下：

- a) 选择在 SALES 部门工作的所有雇员。
- b) 选择工作超过 30 小时的按小时计酬雇员。
- c) 按佣金率降序选择所有佣金雇员。
