

# 列表 4-36 一个不相同的示例

```fsharp ownlet internal q18 = query {
for student in db.Student do
join selection in db.CourseSelection on
student.StudentID = selection.StudentID
select student.Name
distinct }
```

showResult q18

执行结果
"Anita"
"Brent"
"Lisa"

# 使用 contains，exists 和 find 运算符

contains 和 exists 运算符用于判断集合是否包含满足给定条件的元素。列表 4-37 检查是否存在一个名为 Lisa 的学生。

# 列表 4-37 使用 contains = 和 exists 的示例

```fsharp
let internal q19 = query {
for student in db.Student do
select student.Name
contains "Lisa" }

showResult [ q19 ]

let internal q20 = query {
for student in db.Student do
exists (student.Name = "Lisa") }

showResult [ q20 ]
```

contains 和 exists 运算符仅返回布尔值。如果你需要查看第一个元素是否符合某些标准，可以使用列表 4-38 所示的 find。如果没有符合标准的学生，则将抛出 System.InvalidOperationException。

# 列表 4-38 一个 find 示例

```fsharp
let internal q21 = query {
  for student in db.Student do
    find (student.Age >? 20 )
}
showResult [ q21.Name ]
```

执行结果
"Lisa"

# 使用 exactlyOne 和 all 运算符

all 运算符用于测试所有元素是否符合标准。列表 4-39 用于检查学生的姓名是否以字母 L 开头。

列表 4-39 一个 all 示例

```fsharp
let internal q22 = query {
  for student in db.Student.Name,
  all (SqlClient.SqlMethods.Like(student.Name, "L%%"))
}
showResult [ q22 ]
```

> 注意：该示例在 SqlEntityConnection 中无效，但在 SqlDataConnection 中有效。

检查一个类是否仅有一个名为 Lisa 的学生并返回其信息，可以使用 exactlyOne 或 exactlyOneOrDefault。如果没有精确匹配，exactlyOne 操作将产生 System.InvalidOperationException。参见列表 4-40。

列表 4-40 一个 exactlyOne 示例

```fsharp
let internal q23 = query {
  for student in db.Student do
    where (student.Name = "Lisa")
    exactlyOne }
}
showResult [ q23.Name ]
```

# SQL 查询 F# 查询

上一个节提供了许多查询运算符。对于某些读者：

- T-SQL 中的关键字用于检查某个值是否在指定的值列表中，如列表 4-41 所示。该 T-SQL 代码在 F# 查询中的示例见列表 4-42。

列表 4-41 SQL 示例

```sql
SELECT * FROM Student
WHERE Student.StudentID IN (1, 2, 3)
```

列表 4-42 in 的 F# 语法

```fsharp
let ids = query { for id in [1; 2; 3] do select id }

query {
  for student in db.Student do
  where (ids.Contains(student.StudentID))
  select student }
```

- T-SQL 中的 top 关键字用于返回返回结果列表顶部的若干元素。乍一看，F# 查询似乎没有等价的运算符。然而，仔细检查会发现 take 运算符可以完全相同的功能。

- T-SQL 中的 like 关键字是 SQL 中的一种字符映射运算符。虽然 like 不是 F# 查询中的关键字，但你可以使用 SqlMethods.Like，如列表 4-39 所示。SqlMethods 还包含其他可以处理日期时间差异的方法。更多细节请参见表 4-5。

表 4-5 SqlMethods 成员列表

| 函数名 | 对应的 SQL 运算符 | 描述 |
| :--- | :--- | :--- |
| DateDiffDay | DATEDIFF | 计算天数差值 |
| DateDiffHour | DATEDIFF | 计算小时数差值 |
| DateDiffMicrosecond | DATEDIFF | 计算微秒差值 |
| DateDiffMillisecond | DATEDIFF | 计算毫秒差值 |
| DateDiffMinute | DATEDIFF | 计算分钟差值 |
| DateDiffMonth | DATEDIFF | 计算月份差值 |

| 函数名 | 对应的 SQL 运算符 | 描述 |
| :--- | :--- | :--- |
| DateDiffNanosecond | DATEDIFF | 计算纳秒差值 |
| DateDiffSecond | DATEDIFF | 计算秒差值 |
| DateDiffYear | DATEDIFF | 计算年份差值 |
| Like | LIKE | 决定输入是否匹配特定模式 |

- T-SQL 中的 between 关键字不是 F 查询中的关键字，但你可以结合比较运算符和 && 来相同的结果。

- union 和 intersection T-SQL 关键字提供的功能可以通过 F# 查询实现，如列表 4-43 和列表 4-44 所示。

# 列表 4-43 SQL 合并与交集

```sql
SELECT * from Student
UNION
SELECT * from AnotherStudentTable

SELECT * from Student
INTERSECT
SELECT * from AnotherStudentTable
```

# 列表 4-44 F# 查询 union

```fsharp
let q0 = query { for student in db.Student select student.Name }
let q1 = query { for student in db.AnotherStudentTable do select student.Name }

// 合并两个查询结果
q1.Union(q0)

// 取交两个查询结果
q1.Intersect(q0)
```

- T-SQL case 关键字通过使用 if 语句在 F# 查询支持。参见列表 4-45 和列表 4-46。

# 列表 4-45 SQL case 示例

```sql
SELECT student.Name,
CASE student.Age
WHEN 0 then 1000
ELSE student.Age
END
FROM Student
```

# 列表 4-46 使用 if 语句的 F# 查询

```fsharp
let q = query {
    for student in db.Student do
    select ( if student.Age >= -1 then student.Name, Nullable<int>(1000)
    else(student.Name, student.Age) ) }
```

# 其他运算符

在本节中，我将介绍一些让代码更具读性的 F# 运算符。contains 和 exists 运算符用于判断集合是否包含满足给定条件的元素。列表 4-37 检查是否存在一个名为 Lisa 的学生。

contains 和 exists 运算符仅返回布尔值。如果你需要查看第一个元素是否符合某些标准，可以使用列表 4-38 所示的 find。如果没有符合标准的学生，则将抛出 System.InvalidOperationException。

```fsharp
let internal q19 = query {
  for student in db.Student do
  select student.Name
contains "Lisa" }

showResult [ q19 ]

let internal q20 = query {
  for student in db.Student do
  exists (student.Name = "Lisa") }

showResult [ q20 ]
```

```fsharp
let internal q21 = query {
  for student in db.Student do
    find (student.Age >? 20 )
}
showResult [ q21.Name ]
```

all 运算符用于测试所有元素是否符合标准。列表 4-39 用于检查学生的姓名是否以字母 L 开头。

```fsharp
let internal q22 = query {
  for student in db.Student.Name,
  all (SqlClient.SqlMethods.Like(student.Name, "L%%"))
}
showResult [ q22 ]
```

> 注意：该示例在 SqlEntityConnection 中无效，但在 SqlDataConnection 中有效。

检查一个类是否仅有一个名为 Lisa 的学生并返回其信息，可以使用 exactlyOne 或 exactlyOneOrDefault。如果没有精确匹配，exactlyOne 操作将产生 System.InvalidOperationException。参见列表 4-40。

```fsharp
let internal q23 = query {
  for student in db.Student do
    where (student.Name = "Lisa")
    exactlyOne }
}
showResult [ q23.Name ]
```

