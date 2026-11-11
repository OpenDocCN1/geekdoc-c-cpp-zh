```
```java
PreparedStatement stat = conn.prepareStatement("SELECT Cover FROM BookCovers WHERE ISBN=?");
...
stat.setInt(1, isbn);
try (ResultSet result = stat.executeQuery())
{
    if (result.next())
    {
        Blob coverBlob = result.getBlob(1);
        Image coverImage = ImageIO.read(coverBlob.getBinaryStream());
    }
}
```
```

Similarly, if you retrieve a Clob object, you can get character data by calling the `getSubString` or `getCharacterStream` method.

To place a LOB into a database, call `createBlob` or `createClob` on your Connection object, get an output stream or writer to the LOB, write the data, and store the object in the database. For example, here is how you store an image:

```
```java
Blob coverBlob = connection.createBlob();
int offset = 0;
OutputStream out = coverBlob.setBinaryStream(offset);
ImageIO.write(coverImage, "PNG", out);
PreparedStatement stat = conn.prepareStatement("INSERT INTO Cover VALUES (?, ?)");
stat.setInt(1, isbn);
stat.set(2, coverBlob);
stat.executeUpdate();
```
```

| `java.sql.ResultSet` | 1.1 |
|---|---|
| • `Blob getBlob(int columnIndex)` | 1.2 |
| • `Blob getBlob(String columnLabel)` | 1.2 |
| • `Clob getClob(int columnIndex)` | 1.2 |
| • `Clob getClob(String columnLabel)` | 1.2 |

gets the BLOB or CLOB at the given column.

| `java.sql.Blob` | 1.2 |
|---|---|
| • `long length()` | |

gets the length of this BLOB.

| • `byte[] getBytes(long startPosition, long length)` | |

gets the data in the given range from this BLOB.