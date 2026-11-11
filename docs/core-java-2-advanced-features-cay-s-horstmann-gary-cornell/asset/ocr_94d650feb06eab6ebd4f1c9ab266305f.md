| java.sql.Clob 1.4 (Continued) |
|---|
| • Reader getCharacterStream()<br>• Reader getCharacterStream(long startPosition, long length)<br>returns a reader (not a stream) to read the characters from this CLOB or from the given range.<br>• Writer setCharacterStream(long startPosition) 1.4<br>returns a writer (not a stream) for writing into this CLOB, starting at the given position. |

| java.sql.Connection 1.1 |
|---|
| • Blob createBlob() 6<br>• Clob createClob() 6<br>creates an empty BLOB or CLOB. |

# 5.5.3 SQL Escapes

The “escape” syntax features are commonly supported by databases but use database-specific syntax variations. It is the job of the JDBC driver to translate the escape syntax to the syntax of a particular database.

Escapes are provided for the following features:

+   - Date and time literals
+   - Calling scalar functions
+   - Calling stored procedures
+   - Outer joins
+   - The escape character in LIKE clauses

Date and time literals vary widely among databases. To embed a date or time literal, specify the value in ISO 8601 format (www.cl.cam.ac.uk/~mgk25/iso-time.html). The driver will then translate it into the native format. Use d, t, ts for DATE, TIME, or TIMESTAMP values:

```
    { d '2008-01-24' }
    { t '23:59:59' }
    { ts '2008-01-24 23:59:59.999' }
```