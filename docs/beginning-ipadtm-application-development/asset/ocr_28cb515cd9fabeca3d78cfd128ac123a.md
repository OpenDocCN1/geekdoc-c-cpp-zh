# CREATING AND OPENING A DATABASE

After the necessary library is added to the project, you can open a database for usage. You will use the various C functions included with SQLite3 to create or open a database, as demonstrated in the following Try It Out.

# TRY IT OUT Opening a Database

+   1. Using the Databases project created previously, define the openDB method in the DatabasesViewController.m file:

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

# How It Works

The sqlite3_open() C function opens a SQLite database whose filename is specified as the first argument:

`[[self filePath] UTF8String]`

In this case, the filename of the database is specified as a C string using the UTF8String method of the NSString class because the sqlite3_open() C function does not understand an NSString object.

The second argument contains a handle to the sqlite3 object, which in this case is db.

If the database is available, it opens the database. If the specified database is not found, a new database is created. If the database is successfully opened, the function will return a value of 0 (represented using the SQLITE_OK constant).