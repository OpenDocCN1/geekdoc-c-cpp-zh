
## 试一试 为项目准备使用 SQLite3

代码文件 (Databases.zip) 可在 Wrox.com 下载

- 1. 使用 Xcode，创建一个新的基于视图的应用程序项目并将其命名为 Databases。
- 2. 在项目中右键单击 Frameworks 文件夹，然后从菜单栏中选择 Project > Add to Project。
- 3. 导航到 /Developer/Platforms/iPhoneSimulator.platform/Developer/SDKs/iPhoneSimulator<version>.sdk/usr/lib 并选择名为 libsqlite3.dylib 的文件。
- 4. 当显示 Add 对话框时，取消选中 Copy Items into Destination Group's Folder (If Needed) 复选框，并对于引用类型，选择 Relative to Current SDK（参见图 12-1）。
- 5. 在 DatabasesViewController.h 文件中，声明一个类型为 sqlite3 的变量以及一个名为 filePath 的方法（参见加粗的代码）：
- 6. 在 DatabasesViewController.m 文件中，按加粗所示定义 filePath 方法：

> 注意 <version> 表示您使用的 iPhone SDK 的版本。例如，如果您使用的版本是 3.1，则路径为 /Developer/Platforms/iPhoneSimulator.platform/Developer/SDKs/iPhoneSimulator3.1.sdk/usr/lib。

![](img/aab2d775c46f70cd606f2e58e2521324_317_0.png)

```objc
#import <UIKit/UIKit.h>
#import "sqlite3.h"

@interface DatabasesViewController : UIViewController {
    sqlite3 *db;
}
-(NSString *) filePath;
@end
```

```objc
#import "DatabasesViewController.h"

@implementation DatabasesViewController

-(NSString *) filePath {
    NSArray *paths = NSSearchPathForDirectoriesInDomains(
        NSDocumentDirectory, NSUserDomainMask, YES);
    NSString *documentsDir = [paths objectAtIndex:0];
    return [documentsDir stringByAppendingPathComponent:@"database.sql"];
}
```

```objective-c
}

- (void)viewDidLoad {
    [super viewDidLoad];
}

@end
```

### 工作原理

要使用 SQLite3，您需要将应用程序链接到名为 `libsqlite3.dylib` 的动态库。您选择的 `libsqlite3.dylib` 是 SQLite3 库最新版本的别名。在实际的 iPhone 设备上，`libsqlite3.dylib` 位于 `/usr/lib/` 目录中。

要使用 SQLite 数据库，您需要创建一个类型为 `sqlite3` 的对象：

```objective-c
sqlite3 *db;
```

filePath 方法返回 SQLite 数据库的完整路径，该数据库将在您的 iPhone 上的 Documents 目录中创建（在应用程序的沙箱内）：

```objective-c
- (NSString *) filePath {
    NSArray *paths = NSSearchPathForDirectoriesInDomains(
        NSDocumentDirectory, NSUserDomainMask, YES);
    NSString *documentsDir = [paths objectAtIndex:0];
    return [documentsDir stringByAppendingPathComponent:@"database.sql"];
}
```

> **注意** 第 13 章讨论了您可以在应用程序沙箱内访问的各种文件夹。

## 创建和打开数据库

在将必要的库添加到项目后，您可以打开数据库以供使用。您将使用 SQLite3 包含的各种 C 函数来创建或打开数据库，如以下 Try It Out 所演示的。

## 试一试 打开数据库

- 1. 使用之前创建的同一项目，在 `DatabasesViewController.m` 文件中定义 openDB 方法：

```objective-c
#import "DatabasesViewController.h"

@implementation DatabasesViewController

-(NSString *) filePath {
    //...
}
```

```objective-c
-(void) openDB {
    //---create database---
    if (sqlite3_open([[self filePath] UTF8String], &db) != SQLITE_OK ) {
        sqlite3_close(db);
        NSAssert(0, @"Database failed to open.");
    }
}

-(void)viewDidLoad {
    [self openDB];
    [super viewDidLoad];
}

@end
```

### 工作原理

sqlite3_open() C 函数打开一个 SQLite 数据库，其文件名作为第一个参数指定：

[[self filePath] UTF8String]

在这种情况下，数据库的文件名使用 NSString 类的 UTF8String 方法指定为 C 字符串，因为 sqlite3_open() C 函数不理解 NSString 对象。

第二个参数包含对 sqlite3 对象的句柄，在本例中为 db。

如果数据库可用，则打开数据库。如果未找到指定的数据库，则会创建一个新数据库。如果数据库成功打开，函数将返回值为 0（使用 SQLITE_OK 常量表示）。

以下来自 http://www.sqlite.org/c3ref/c_abort.html 的列表显示了各种 SQLite 函数返回的结果代码：

```c
#define SQLITE_OK 0 /* Successful result */
#define SQLITE_ERROR 1 /* SQL error or missing database */
#define SQLITE_INTERNAL 2 /* Internal logic error in SQLite */
#define SQLITE_PERM 3 /* Access permission denied */
#define SQLITE_ABORT 4 /* Callback routine requested an abort */
#define SQLITE_BUSY 5 /* The database file is locked */
#define SQLITE_LOCKED 6 /* A table in the database is locked */
#define SQLITE_NOMEM 7 /* A malloc() failed */
#define SQLITE_READONLY 8 /* Attempt to write a readonly database */
#define SQLITE_INTERRUPT 9 /* Operation terminated by sqlite3_interrupt() */
#define SQLITE_IOERR 10 /* Some kind of disk I/O error occurred */
#define SQLITE_CORRUPT 11 /* The database disk image is malformed */
#define SQLITE_NOTFOUND 12 /* NOT USED. Table or record not found */
#define SQLITE_FULL 13 /* Insertion failed because database is full */
#define SQLITE_CANTOPEN 14 /* Unable to open the database file */
#define SQLITE_PROTOCOL 15 /* NOT USED. Database lock protocol error */
#define SQLITE_EMPTY 16 /* Database is empty */
#define SQLITE_SCHEMA 17 /* The database schema changed */
#define SQLITE_TOOBIG 18 /* String or BLOB exceeds size limit */
#define SQLITE_CONSTRAINT 19 /* Abort due to constraint violation */
#define SQLITE_MISMATCH 20 /* Data type mismatch */
```

```c
#define SQLITE_MISUSE 21 /* Library used incorrectly */
#define SQLITE_NOLFS 22 /* Uses OS features not supported on host */
#define SQLITE_AUTH 23 /* Authorization denied */
#define SQLITE_FORMAT 24 /* Auxiliary database format error */
#define SQLITE_RANGE 25 /* 2nd parameter to sqlite3_bind out of range */
#define SQLITE_NOTADB 26 /* File opened that is not a database file */
#define SQLITE_ROW 100 /* sqlite3_step() has another row ready */
#define SQLITE_DONE 101 /* sqlite3_step() has finished executing */
```

## 检查创建的数据库

如果数据库成功创建，它可以在应用程序沙箱的 Documents 文件夹中找到。如第 13 章所述，您可以在 iPhone Simulator 上在 ~/Library/Application Support/iPhone Simulator/User/Applications/<App_ID>/Documents/ 文件夹中找到应用程序的 Documents 文件夹。图 12-2 显示了数据库 .sql 文件。

![](img/aab2d775c46f70cd606f2e58e2521324_320_0.png)

图 12-2

## 创建表

在创建数据库后，您可以创建表来存储一些数据。在以下 Try It Out 中，您将学习如何创建包含两个文本字段的表。为说明目的，创建一个名为 Contacts 的表，其中包含两个字段 email 和 name。

## 试一试 创建表

这是一个一步过程。使用本章前面使用的同一项目，按如下方式定义 createTableNamed:withField1:withField2: 方法：

```objective-c
#import "DatabasesViewController.h"

@implementation DatabasesViewController

- (NSString *) filePath {
    //...
}

- (void) openDB {
    //...
}

- (void) createTableNamed:(NSString *) tableName
withField1:(NSString *) field1
```

```objective-c
withField2:(NSString *) field2 {
    char *err;
    NSString *sql = [NSString stringWithFormat:
        @"CREATE TABLE IF NOT EXISTS %@ ('%@' TEXT PRIMARY KEY, '%@' TEXT);",
        tableName, field1, field2];

    if (sqlite3_exec(db, [sql UTF8String], NULL, NULL, &err) != SQLITE_OK) {
        sqlite3_close(db);
        NSAssert(0, @"Table failed to create.");
    }
}

- (void)viewDidLoad {
    [self openDB];
    [self createTableNamed:@"Contacts" withField1:@"email" withField2:@"name"];
    [super viewDidLoad];
}
@end
```

### 工作原理

createTableNamed:withField1:withField2: 方法接收三个参数：tableName、field1 和 field2。

使用这三个参数，您首先制定一个 SQL 字符串，然后使用 sqlite3_exec( ) C 函数创建表，该函数的重要参数为 sqlite3 对象、SQL 查询字符串以及用于错误消息的变量指针。如果在创建数据库时发生错误，您将使用 NSAssert 方法停止应用程序并关闭数据库连接。

图 12-3 显示了如果操作成功创建的 Contacts 表。

| email | name |
|---|---|
|  |  |
|  |  |
|  |  |

图 12-3

> **注意** 如需快速入门 SQL 语言，请查看以下 SQL 教程：
> http://w3schools.com/sql/default.asp.
