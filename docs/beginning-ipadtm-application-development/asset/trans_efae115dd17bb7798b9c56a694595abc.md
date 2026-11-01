

## 使用 SQLITE3

要在应用程序中使用 SQLite3 数据库，首先需要将 libsqlite3.dylib 库添加到 Xcode 项目中。通过下面的“试一试”来了解具体操作方法。你需要下载本章中此处及其他“试一试”功能所指定的代码文件。

### 试一试 准备项目以使用 SQLite3

代码文件 Databases.zip 可于 Wrox.com 下载

- 1. 使用 Xcode 创建一个新的基于视图的应用程序项目，并将其命名为 Databases。
- 2. 右键单击项目中的 Frameworks 文件夹，将 libsqlite3.dylib 库添加到项目中（参见图 10-1）。

![](img/ab1bbb3d5afcbabb6f4a47f0203b9043_305_0.png)

图 10-1

- 3. 在 DatabasesViewController.h 文件中，声明一个 sqlite3 类型的变量以及一个名为 filePath 的方法（参见粗体代码）；

```
#import <UIKit/UIKit.h>

#import "sqlite3.h"
```

## 创建并打开数据库

将所需的库添加到项目后，你就可以打开数据库并使用了。你将使用 SQLite3 附带的多种 C 函数来创建或打开数据库，如下面的“试一试”所示。

### 试一试 打开数据库

- 1. 使用之前创建的 Databases 项目，在 DatabasesViewController.m 文件中定义 openDB 方法：

```
#import "DatabasesViewController.h"

@implementation DatabasesViewController

-(NSString *) filePath {
    //...
}

-(void) openDB {
    //---create database---
    if (sqlite3_open([[self filePath] UTF8String], &db) != SQLITE_OK ) {
        sqlite3_close(db);
        NSAssert(0, @"Database failed to open.");
    }
}

- (void)viewDidLoad {
    [self openDB];
    [super viewDidLoad];
}

@end
```

### 工作原理

sqlite3_open() C 函数用于打开一个 SQLite 数据库，该数据库的文件名由第一个参数指定：

`[[self filePath] UTF8String]`

在本例中，数据库的文件名通过 NSString 类的 UTF8String 方法以 C 字符串的形式指定，因为 sqlite3_open() C 函数无法理解 NSString 对象。

第二个参数包含一个指向 sqlite3 对象的句柄，在此例中为 db。

如果数据库存在，则打开该数据库。如果找不到指定的数据库，则会创建一个新数据库。如果数据库成功打开，该函数将返回值 0（使用 SQLITE_OK 常量表示）。

使用这些参数，你首先构造一个 SQL 字符串，然后使用 sqlite3_exec() C 函数创建表，该函数的重要参数包括 sqlite3 对象、SQL 查询字符串以及用于错误消息的变量指针。如果在创建数据库时出现错误，你将使用 NSAssert 方法停止应用程序并关闭数据库连接。

如果操作成功，将会创建一个名为 Contacts 的表，包含两个字段（email 和 name）。

> 注意 如需快速入门 SQL 语言，请参阅以下网址的 SQL 教程：
> http://w3schools.com/sql/default.asp

## 插入记录

创建表之后，你可以向其中插入一些记录。下面的“试一试”展示了如何向前一节中创建的表写入三行记录。

### 试一试 插入记录

- 1. 在 Databases 项目中，按如下所示定义 insertRecordIntoTableNamed:withField1:field1Value:andField2:field2Value: 方法，并按粗体所示修改 viewDidLoad 方法：

```
#import "DatabasesViewController.h"

@implementation DatabasesViewController

-(NSString *) filePath {
    //...
}

-(void) openDB {
    //...
}

-(void) createTableNamed:(NSString *) tableName
    withField1:(NSString *) field1
    withField2:(NSString *) field2 {
    //...
}

-(void) insertRecordIntoTableNamed:(NSString *) tableName
    withField1:(NSString *) field1
    field1Value:(NSString *) field1Value
    andField2:(NSString *) field2
    field2Value:(NSString *) field2Value {

NSString *sql = [NSString stringWithFormat:
    @"INSERT OR REPLACE INTO '%@' ('%@', '%@') VALUES ('%@','%@')",
tableName, field1, field2, field1Value, field2Value];

char *err;
if (sqlite3_exec(db, [sql UTF8String], NULL, NULL, &err) != SQLITE_OK) {
    sqlite3_close(db);
    NSAssert(0, @"Error updating table.");
}
}

- (void)viewDidLoad {
    [self openDB];
    [self createTableNamed:@"Contacts" withField1:@"email" withField2:@"name"];

    for (int i=0; i<=2; i++) {
        NSString *email = [[NSString alloc] initWithFormat:
            @"user%d@learn2develop.net",i];
        NSString *name = [[NSString alloc] initWithFormat: @"user %d",i];
        [self insertRecordIntoTableNamed:@"Contacts"
            withField1:@"email" field1Value:email
            andField2:@"name" field2Value:name];
        [email release];
        [name release];
    }
    [super viewDidLoad];
}

@end
```

代码片段 DatabasesViewController.m

### 工作原理

此示例中的代码与上一个示例类似；你构造一个 SQL 字符串，然后使用 sqlite3_exec() C 函数将记录插入数据库：

```
NSString *sql = [NSString stringWithFormat:
    @"INSERT OR REPLACE INTO '%@' ('%@', '%@') VALUES ('%@', '%@')",
    tableName, field1, field2, field1Value, field2Value];

char *err;
if (sqlite3_exec(db, [sql UTF8String], NULL, NULL, &err) != SQLITE_OK) {
    sqlite3_close(db);
    NSAssert(0, @"Error updating table.");
}
```

在 viewDidLoad 方法中，你通过调用 insertRecordIntoTableNamed:withField1:field1Value:andField2:field2Value: 方法向数据库中插入了三条记录：

```
for (int i=0; i<=2; i++) {
    NSString *email = [[NSString alloc] initWithFormat:
        @"user%d@learn2develop.net",i];
    NSString *name = [[NSString alloc] initWithFormat: @"user %d",i];
    [self insertRecordIntoTableNamed:@"Contacts"
```

```
withField1:@"email" field1Value:email
andField2:@"name" field2Value:name];
}
```

## 绑定变量

构造 SQL 字符串时最常见的任务之一是需要将值插入到查询字符串中，并确保该字符串格式正确且不含无效字符。在前一节中，你看到要向数据库中插入一行，必须像这样构造 SQL 语句：

```
NSString *sql = [NSString stringWithFormat:
 @"INSERT OR REPLACE INTO '%@' ('%@', '%@') VALUES ('%@', '%@')",
 tableName, field1, field2, field1Value, field2Value];

char *err;
if (sqlite3_exec(db, [sql UTF8String], NULL, NULL, &err) != SQLITE_OK) {
 sqlite3_close(db);
 NSAssert(0, @"Error updating table.");
}
```

SQLite 支持一种称为绑定变量的功能，帮助你构造 SQL 字符串。例如，前面的 SQL 字符串可以使用绑定变量改写为如下形式：

```
NSString *sqlStr = [NSString stringWithFormat:
 @"INSERT OR REPLACE INTO '%@' ('%@', '%@') VALUES (?,?)",
 tableName, field1, field2];

const char *sql = [sqlStr UTF8String];
```

这里，? 是一个占位符，供你替换为查询的实际值。在前面的语句中，假设 tableName 是 Contacts，field1 是 email，field2 是 name，则 sql 现在为：

```
INSERT OR REPLACE INTO Contacts ('email', 'name') VALUES (?,?)
```

> 注意 ? 只能插入到 SQL 语句的 VALUES 和 WHERE 部分；例如，不能将其插入表名。以下语句是无效的：
> INSERT OR REPLACE INTO ? ('email', 'name') VALUES (?,?)

要替换 ? 的值，需要创建一个 sqlite3_stmt 对象，并使用 sqlite3_prepare_v2() 函数将 SQL 字符串编译为二进制形式，然后使用 sqlite3_bind_text() 函数插入占位符的值，如下所示：

```
sqlite3_stmt *statement;

if (sqlite3_prepare_v2(db, sql, -1, &statement, nil) == SQLITE_OK) {
```

```objective-c
sqlite3_bind_text(statement, 1, [field1Value UTF8String], -1, NULL);
sqlite3_bind_text(statement, 2, [field2Value UTF8String], -1, NULL);
}
```

> > **注意** 若要绑定整数值，请使用 `sqlite3_bind_int()` 函数。

在前面的调用之后，SQL 字符串如下所示：

```sql
INSERT OR REPLACE INTO Contacts ('email', 'name') VALUES
    ('user0@learn2develop.net', 'user0')
```

要执行该 SQL 语句，可使用 `sqlite3_step()` 函数，随后使用 `sqlite3_finalize()` 函数删除已准备好的 SQL 语句：

```objective-c
if (sqlite3_step(statement) != SQLITE_DONE)
    NSAssert(0, @"Error updating table.");

sqlite3_finalize(statement);
```

> > **注意** 在上一节中，你使用 `sqlite3_exec()` 函数执行 SQL 语句。在本例中，你实际上使用 `sqlite3_prepare()`、`sqlite3_step()` 和 `sqlite3_finalize()` 函数的组合来完成同样的操作。事实上，`sqlite3_exec()` 函数正是这三个函数的封装。对于非查询类 SQL 语句（例如创建表、插入行等），始终使用 `sqlite3_exec()` 函数会更好。

## 检索记录

现在记录已成功插入表中，是时候将它们取出来了。这也是确认它们确实已保存的好方法。下面的“试一试”展示了如何检索记录。

### 试一试 — 检索记录

- 1. 在 Databases 项目中，按如下所示定义 `getAllRowsFromTableNamed:` 方法，并按粗体所示修改 `viewDidLoad` 方法：

```objective-c
#import "DatabasesViewController.h"

@implementation DatabasesViewController

- (NSString *) filePath {
    //...
}
```

