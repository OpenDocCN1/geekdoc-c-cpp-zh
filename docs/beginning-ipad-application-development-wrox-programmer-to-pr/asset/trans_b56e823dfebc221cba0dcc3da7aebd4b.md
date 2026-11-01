
```
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

### 如何工作

本示例中的代码与前一个示例类似；你制定一个 SQL 字符串并使用 sqlite3_exec() C 函数将记录插入数据库：

```
NSString *sql = [NSString stringWithFormat:
    @"INSERT OR REPLACE INTO '%@' ('%@', '%@') VALUES ('%@','%@')",
    tableName, field1, field2, field1Value, field2Value];

char *err;
if (sqlite3_exec(db, [sql UTF8String], NULL, NULL, &err) != SQLITE_OK) {
    sqlite3_close(db);
    NSAssert(0, @"Error updating table.");
}
}
```

在 viewDidLoad 方法中，你通过调用 insertRecordIntoTableNamed:withField1:field1Value:andField2:field2Value: 方法向数据库插入三条记录：

```
for (int i=0; i<=2; i++) {
    NSString *email = [[NSString alloc] initWithFormat:
        @"user%d@learn2develop.net",i];
    NSString *name = [[NSString alloc] initWithFormat: @"user %d",i];

    [self insertRecordIntoTableNamed:@"Contacts"
```

```
sqlite3_bind_text(statement, 1, [field1Value UTF8String], -1, NULL);
sqlite3_bind_text(statement, 2, [field2Value UTF8String], -1, NULL);
}
```

> **NOTE** 将整数值绑定时，使用 `sqlite3_bind_int()` 函数。

在前面的调用之后，SQL 字符串如下所示：

```
INSERT OR REPLACE INTO Contacts ('email', 'name') VALUES
('user0@learn2develop.net', 'user0')
```

要执行 SQL 语句，你使用 `sqlite3_step()` 函数，然后使用 `sqlite3_finalize()` 函数删除准备好的 SQL 语句：

```
if (sqlite3_step(statement) != SQLITE_DONE)
    NSAssert(0, @"Error updating table.");

sqlite3_finalize(statement);
```

> **NOTE** 在上一节中，你使用 `sqlite3_exec()` 函数执行 SQL 语句。在本示例中，你实际上使用 `sqlite3_prepare()`、`sqlite3_step()` 和 `sqlite3_finalize()` 函数的组合来做同样的事情。事实上，`sqlite3_exec()` 函数实际上是这三个函数的包装器。对于非查询 SQL 语句（例如创建表、插入行等），最好始终使用 `sqlite3_exec()` 函数。

### 检索记录

现在记录已成功插入到表中，是时候将它们取出来了。这是一个确保它们确实已保存的好方法。下面的试一试将向你展示如何检索记录。

### 试一试 检索记录

1. 在 Databases 项目中，按如下方式定义 getAllRowsFromTableNamed: 方法并按粗体所示修改 viewDidLoad 方法：

```
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
    //...
}

-(void) getAllRowsFromTableNamed: (NSString *) tableName {

    //---retrieve rows---
    NSString *qsql = @"SELECT * FROM CONTACTS";
    sqlite3_stmt *statement;

    if (sqlite3_prepare_v2( db, [qsql UTF8String], -1, &statement, nil) ==
    SQLITE_OK) {
        while (sqlite3_step(statement) == SQLITE_ROW) {
            char *field1 = (char *) sqlite3_column_text(statement, 0);
            NSString *field1Str = [[NSString alloc] initWithUTF8String: field1];
            char *field2 = (char *) sqlite3_column_text(statement, 1);
            NSString *field2Str = [[NSString alloc] initWithUTF8String: field2];

            NSString *str = [[NSString alloc] initWithFormat:@"%@ - %@",
                field1Str, field2Str];

            NSLog(str);

            [field1Str release];
            [field2Str release];
            [str release];
        }
        //---deletes the compiled statement from memory---
        sqlite3_finalize(statement);
    }
}

-(void)viewDidLoad {
    [self openDB];
    [self createTableNamed:@"Contacts" withField1:@"email" withField2:@"name"];

    for (int i=0; i<2; i++) {
        NSString *email = [[NSString alloc] initWithFormat:
            @"user%d@learn2develop.net",i];
```

命令如下：

- `sqlite3 mydata.sql`
- `CREATE TABLE IF NOT EXISTS Contacts (email TEXT PRIMARY KEY, name TEXT);`
- `INSERT INTO Contacts (email, name) VALUES ('weimenglee@gmail.com', 'weimenglee');`
- `SELECT * FROM Contacts`

> **NOTE** 请记住以分号 (;) 结束每个命令。
> 此外，默认情况下启动 Terminal 时，你位于主目录中。因此，运行 sqlite3 应用程序将把数据库文件保存在你的主目录中。

即使你可以使用 sqlite3 应用程序将记录插入数据库，使用图形工具来执行此操作会容易得多。为此，你可以使用 SQLite Database Browser，你可以从 http://sourceforge.net/projects/sqlitebrowser/ 免费下载。你可以使用 SQLite Database Browser（见图 10-5）对数据库文件执行各种各样的功能。

![](img/744c5ec15e15ca7891c98be71dc25d13_317_0.png)

图 10-5

### 摘要

本章提供了 iPad 上使用的 SQLite3 数据库的快速介绍。有了 SQLite3，你现在可以以高效的方式存储所有结构化数据并对数据执行复杂的聚合。

## 第三部分 高级 iPad 编程技术

- ► CHAPTER 11: 简单动画
- ► CHAPTER 12: 识别手势
- ► CHAPTER 13: 访问加速度计

### 试一试 动画球

*代码文件 Animation.zip 可在 Wrox.com 下载*

1. 使用 Xcode，创建一个新的基于视图的应用程序项目并将其命名为 `Animation`。
2. 将名为 `tennisball.jpg` 的图像拖放到 Xcode 中的 `Resources` 文件夹中。当出现添加对话框时，选中“将项目复制到目标组的文件夹中（如果需要）”选项，以便将图像复制到项目中（见图 11-1）。
3. 双击 `AnimationViewController.xib` 文件以在 Interface Builder 中编辑它。
4. 将 ImageView 拖放到 View 窗口上并将其 Image 属性设置为 `tennisball.jpg`（见图 11-2）。

   确保 ImageView 的大小适合整个网球图像。稍后，你将在屏幕上移动 ImageView，因此不要用 ImageView 填满整个屏幕很重要。
5. 选择 View（ImageView 外部）并将背景颜色更改为黑色（见图 11-3）。
6. 从库中向 View 窗口添加一个 Label 和一个 Slider 视图（见图 11-4 左下角）。将 Slider 视图的 Initial 属性设置为 0.01。

![](img/744c5ec15e15ca7891c98be71dc25d13_323_0.png)

图 11-1

![](img/744c5ec15e15ca7891c98be71dc25d13_325_0.png)

图 11-4

7. 在 AnimationViewController.h 文件中，声明以下 outlets、字段和操作：

```
#import <UIKit/UIKit.h>

@interface AnimationViewController : UIViewController {

    IBOutlet UIImageView *imageView;
    IBOutlet UISlider *slider;

    CGPoint delta;
    NSTimer *timer;

    float ballRadius;

}

@property (nonatomic, retain) UIImageView *imageView;
@property (nonatomic, retain) UISlider *slider;

- (IBAction) sliderMoved:(id) sender;

@end
```
