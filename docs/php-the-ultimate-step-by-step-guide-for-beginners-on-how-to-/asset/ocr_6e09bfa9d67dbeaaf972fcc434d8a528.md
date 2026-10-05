We're going to demonstrate you the charges to go down a database called store from the shell brief.

```
mysqldump - u root - p store > my_backup_of_store.sql
```

This tells mysqldump to sign into the database as the root client and to go down the store database. You will be incited for the root watchdog that chose amid establishment. The output of the command is put in a record called my_backup_of_store. sql with the assistance of the sidrack character, otherwise called the more prominent than image (>).

# Restoring a MySQL backup

The uplifting news is it's not difficult to reproduce your database from a mysqldump record. The substances of the backup record are essentially SQL statements what's more, can thusly be prepared by the MySQL charge line customer to restore the moved down information.

If you did a reinforcement of your database utilizing mysqldump - all-databases to a record called

my_backup.sql, you could restore your database:

```
mysql - u root - p < my_backup.sql
```

If you did a particular reinforcement of one and only database, it's some more intricate. To restore that kind of reinforcement record, utilize the - D charge line switch:

```
mysql - u root - p - D store < my_backup.sql
```

Since you know how to restore default dump records, we can proceed onward to some different applications with respect to sending out and importing information.

# Working with other formats

Albeit working with SQL-based records is advantageous, there may be times when you need to spare your information in different configurations. Case in point, a typical strategy for speaking to a rundown of information is in CSV (comma-isolated positions) position. The mysqldump sum underpins this configuration. You should do nothing more than specify the - no-create info, - tab, furthermore, -fields-terminated by arguments: