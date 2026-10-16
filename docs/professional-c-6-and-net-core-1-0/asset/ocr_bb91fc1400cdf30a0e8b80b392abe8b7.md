```
"WHERE Prod.ProductId = @ProductId";

var command = new SqlCommand(sql, connection);
var productIdParameter = new SqlParameter("ProductId", SqlDbType.Int);
productIdParameter.Value = productId;
command.Parameters.Add(productIdParameter);
\await connection.OpenAsync();

using (SqlDataReader reader = await command.ExecuteReaderAsync(
    CommandBehavior.CloseConnection))
{
    while (await reader.ReadAsync())
    {
        int id = reader.GetInt32(0);
        string name = reader.GetString(1);
        DateTime from = reader.GetDateTime(4);
        DateTime? to = reader.IsDBNull(5) ? (DateTime?)null:
            reader.GetDateTime(5);
        decimal standardPrice = reader.GetDecimal(6);
        WriteLine($"{id} {name} from: {from:d} to: {to:d};" +
            $"price: {standardPrice}");
    }
}
```

Using the asynchronous method calls is not only advantageous with Windows applications but also useful on the server side for making multiple calls simultaneous. The asynchronous methods of the ADO.NET API have overloads to support the CancellationToken for an earlier stop of a long-running method.

> NOTE For more information about asynchronous method calls and the CancellationToken, read Chapter 15, “Asynchronous Programming.”

# Transactions

By default, a single command is running within a transaction. If you need to issue multiple commands, and either all of these or none happen, you can start and commit transactions explicitly.

Transactions are described by the term ACID. ACID is a four-letter acronym for atomicity, consistency, isolation, and durability:

+   - **Atomicity**—Represents one unit of work. With a transaction, either the complete unit of work succeeds or nothing is changed.
+   - **Consistency**—The state before the transaction was started and after the transaction is completed must be valid. During the transaction, the state may have interim values.
+   - **Isolation**—Transactions that happen concurrently are isolated from the state, which is changed during a transaction. Transaction A