The return value of *Read* is type bool and returns true as long as there are more records to read. After the last record in the data stream has been read, *Read* returns false.

Each column can be extracted from the row with a numeric indexer. Instead of numeric indexer string indexer can be used, where the string is the column name from the SQL query (the table column name is used if an asterisk, \*, is used.) String indexers are much more readable, making the code easier to maintain.

Regardless of the type of the indexer parameter, a SqlDataReader indexer will return type object.

+   * **Closing Connection**

Once used SqlDataReader, close the SqlConnection.

```
```csharp
try
{
    // data access code
}
finally
{
    // 3. close the reader
    if (sqldr != null)
    {
        sqldr.Close();
    }

    // close the connection too
}

Example
using System;
using System.Data;
using System.Data.SqlClient;

namespace ADONetDemos
{
    class ReadersDemo
    {
        static void Main()
        {
            ReadersDemo rsd = new ReadersDemo();
            rsd.DataRead();
        }

        public void DataRead()
        {
```
```