```
```objective-c
sqlite3_bind_text(statement, 1, [field1Value UTF8String], -1, NULL);
sqlite3_bind_text(statement, 2, [field2Value UTF8String], -1, NULL);
}
```
```

> > **NOTE** To bind integer values, use the `sqlite3_bind_int()` function.

After the preceding call, the SQL string looks like this:

```
```sql
INSERT OR REPLACE INTO Contacts ('email', 'name') VALUES
    ('user0@learn2develop.net', 'user0')
```
```

To execute the SQL statement, you use the `sqlite3_step()` function, followed by the `sqlite3_finalize()` function to delete the prepared SQL statement:

```
```objective-c
if (sqlite3_step(statement) != SQLITE_DONE)
    NSAssert(0, @"Error updating table.");

sqlite3_finalize(statement);
```
```

> > **NOTE** In the previous section, you used the `sqlite3_exec()` function to execute SQL statements. In this example, you actually use a combination of `sqlite3_prepare()`, `sqlite3_step()`, and `sqlite3_finalize()` functions to do the same thing. In fact, the `sqlite3_exec()` function is actually a wrapper for these three functions. For non-query SQL statements (such as for creating tables, inserting rows, and so on), it is always better to use the `sqlite3_exec()` function.

# Retrieving Records

Now that the records have been successfully inserted into the table, it is time to get them out. This is a good way to ensure that they really have been saved. The following Try It Out shows you how to retrieve your records.

# TRY IT OUT — Retrieving the Records

+   1. In the Databases project, define the `getAllRowsFromTableNamed:` method as follows and modify the `viewDidLoad` method as shown in bold:

```
```objective-c
#import "DatabasesViewController.h"

@implementation DatabasesViewController

- (NSString *) filePath {
    //...
}
```
```