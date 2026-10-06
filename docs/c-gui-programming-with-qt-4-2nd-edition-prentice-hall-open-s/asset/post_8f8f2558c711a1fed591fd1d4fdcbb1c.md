
database, a public domain in-process database. [*] Qt is supplied with SQLite

[*] SQL support must be enabled when Qt is built. For example, Qt can be compiled with SQLite built-in by passing the -qt-sqlsqlite command-line option to configure script or by setting the appropriate option in the Qt installer.

For users who are comfortable with SQL syntax, the QSqlQuery class provides a means of directly executing arbitrary SQL statements and handling their results.

For users who prefer a higher-level database interface that avoids SQL syntax, QSqlTableModel and QSqlRelationalTableModel provide suitable abstractions.

These classes represent an SQL table in the same way as Qt's other classes (covered in Chapter 10). They can be used stand-alone to traverse and edit data in code, or they can be attached to views through which end-users can view and edit the data themselves.

Qt also makes it straightforward to program the common database idioms, such as master-detail and drill-down, and to view database tables using forms or GUI tables, as the examples in this chapter will demonstrate.

## Connecting and Querying

To execute SQL queries, we must first establish a connection with a database. Typically, database connections are set up in a separate function that we call at application startup. For example:

```
bool createConnection()
{
    QSqlDatabase db = QSqlDatabase::addDatabase("QMYSQL");
    db.setHostName("mozart.onkordia.edu");
    db.setDatabaseName("musicdb");
    db.setUserName("gbatstone");
    db.setPassword("T17aV44");
    if (!db.open()) {
        QMessageBox::critical( "Database Error", db.lastError().text());
        return false;
    }
    return true;
}
```

First, we call QSqlDatabase::addDatabase() to create a QSqlDatabase object. The first argument to addDatabase() specifies which database driver Qt must use to access the database. In this case, we use MySQL.

Next, we set the database host name, the database name, the user name, and the password, and we open the connection. If open() fails, we would call an error message. Typically, we call main(int argc, char *argv[]) in main():

```
int main(int argc, char *argv[]) {
    QApplication app(argc, argv);
    if (!createConnection())
        return 1;
    ...
    return app.exec();
}
```

Once a connection is established, we can use QSqlQuery to execute any SQL statement that the underlying database supports. For example, here's how to execute a SELECT statement:

```
SqlQuery query;
query.exec("SELECT title, year FROM cd WHERE year >= 1998");
```

After the exec(), we can navigate through the query's result set:

```
while (query.next()) {
    QString title = query.value(0).toString();
    int year = query.value(1).toInt();
    std::cerr << title << " : " << year << " << std::endl;
}
```

We call next() once to position the QSqlQuery on the first record of the result set. Subsequent calls to next() advance the pointer by one record time, until the end is reached, which if the query failed, the first call to next() will return false.

The value() function returns the value of a field as a QVariant. The fields are numbered from 0 in the order given in the SELECT statement. The QVariant class can hold many and Qt types, the different types of data that can be stored in a database are mapped into the corresponding C++ and Qt types. For example, a VARCHAR is represented as a QString and a DATETIME as a QDateTime.

QSqlQuery provides other functions to navigate through the result set: first(), last(), previous(), and seek(). These functions are convenient, but for easy optimization when they can be slower and more memory-hungry than next(). For operating on large datasets, we can call QSqlQuery::setForwardOnly(true) before calling exec(), and then use next() for navigating through the result set.

Earlier we specified the SQL query as an argument to QSqlQuery::exec(), and we can also pass it to the constructor, which executes it immediately.

```
QSqlQuery query("SELECT title, year FROM cd WHERE year >= 1998");
```

We can check for an error by calling isActive() on the query:

```
if (!query.isActive())
    QMessageBox::warning(this, tr("Database Error"),
        query.lastError().text());
```

If no error occurs, the query will become "active" and we can use next() to navigate through the result set.

Doing an INSERT is almost as easy as performing a SELECT:

```
QSqlQuery query("INSERT INTO cd (id, artistid, title, year) "
    "VALUES (203, 102, 'Living in America', 2002)");
```

After this, numRowsAffected() returns the number of rows that were affected by the SQL statement (or -1 on error).

If we need to insert a list of records, or if we want to avoid converting values to strings (escaping them correctly), we can use prepare() to specify a query that contains placeholders and then bind the values to insert. Qt supports both the Oracle-style and the ODBC-style syntax for placeholders, using native support where it is available and simulating the other. Here's an example that uses the Oracle-style syntax with named placeholders:

```
QSqlQuery query;
query.prepare("INSERT INTO cd (id, artistid, title, year) "
    "VALUES (:id, :artistid, :title, :year)");
query.bindValue(":id", 203);
query.bindValue(":artistid", 102);
query.bindValue(":title", "Living in America");
query.bindValue(":year", 2002);
query.exec();
```

Here's the same example using ODBC-style positional placeholders:

```
QSqlQuery query;
query.prepare("INSERT INTO cd (id, artistid, title, year) "
"VALUES (?, ?, ?, ?)");
query.addBindValue(203);
query.addBindValue(102);
query.addBindValue("Living in America");
query.addBindValue(2002);
query.exec();
```

After the call to exec(), we can call bindValue() addBindValue() to bind new values, and then call exec() again to execute the query with the new values.

Placeholders are often used to specify binary data or strings that contain non-ASCII or non-Latin-1 characters. Behind the scenes, Qt uses Unicode with those databases that support Unicode, and for those that don't, Qt transparently converts strings to the appropriate encoding.

Qt supports SQL transactions on databases where they are available. To start a transaction, we call transaction() the QSqlDatabase object representing the database connection. To finish the transaction, we either commit() or rollback(). For example, here's how we would look up a foreign key and execute an INSERT statement inside a transaction:

```
QSqlDatabase::database().transaction();
QSqlQuery query;
query.exec("SELECT id FROM artist WHERE name = 'Glucifer'");
if (query.next()) {
  int artistID = query.value(0).toInt();
  query.exec("INSERT INTO cd (id, artistid, title, year) "
  + "VALUES (201, " + QString::number(artistID)
  + ", 'Riding the Tiger, 1997')");
}
QSqlDatabase::database().commit();
```

The QSqlDatabase::database() function returns a QSqlDatabase object representing the connection we created with createConnection(). If a transaction cannot be started, QSqlDatabase::transaction() returns false. Some databases do not support transactions. For those, the transaction(), commit(), and rollback() do nothing. We can test whether a database supports transactions by hasFeature() on the QSqlDriver associated with the database:

```
QSqlDriver *driver = QSqlDatabase::database().driver();
if (driver->hasFeature(QSqlDriver::Transactions))
```

Several other database features can be tested for, including whether the database supports BLOBs (binary large objects), Unicode, and prepared queries.

It is also possible to access the low-level database driver handle and the low-level handle to a query's result set, using QSqlDriver::handle() and QSqlQuery::handle(). Both functions are dangerous unless you know exactly what you are doing and are careful.

In the examples so far, we have assumed that the application is using a single database connection. If we want to create multiple connections, we can pass a name as a second argument to addDatabase(). For example:

```
QSqlDatabase db = QSqlDatabase::addDatabase("QSQL", "OTHER");
db.setHostName("saturn.mcmanany.edu");
db.setDatabaseName("starsdb");
db.setUsername("hilbert");
db.setPassword("ixtapa7");
```

We can then retrieve a pointer to the QSqlDatabase object by passing the name to QSqlDatabase::database():

```
QSqlDatabase db = QSqlDatabase::database("OTHER");
```

To execute queries using the other connection, we pass the QSqlDatabase object to the QSqlQuery constructor:

```
QSqlQuery query(db);
query.exec("SELECT id FROM artist WHERE name = 'Mando Diao'");
```

Multiple connections are useful if we want to perform more than one transaction at a time, since each connection can handle only one active transaction. When we use multiple database connections, we can still have one unnamed connection and QSqlQuery will use that connection if none is specified.

In addition to QSqlQuery, Qt provides the QSqlTableModel class as a higher-level interface, allowing us to avoid using raw SQL for performing the most common
