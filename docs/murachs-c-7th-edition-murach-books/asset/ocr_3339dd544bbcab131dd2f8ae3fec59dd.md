# The code for the CustomerDB class

Page 2

```
command.Parameters.AddWithValue("@Name", customer.Name);
command.Parameters.AddWithValue("@Address", customer.Address);
command.Parameters.AddWithValue("@City", customer.City);
command.Parameters.AddWithValue("@State", customer.StateCode);
command.Parameters.AddWithValue("@ZipCode", customer.ZipCode);
connection.Open();
int count = command.ExecuteNonQuery();

if (count > 0) {
    command.CommandText = "SELECT IDENT_CURRENT('Customers') "
        + "FROM Customers";
    customer.CustomerId = Convert.ToInt32(command.ExecuteScalar());
}

public static bool UpdateCustomer(Customer oldCustomer, Customer newCustomer)
{
    string updateStatement =
        "UPDATE Customers SET " +
        "Name = @NewName, " +
        "Address = @NewAddress, " +
        "City = @NewCity, " +
        "State = @NewState, " +
        "ZipCode = @NewZipCode " +
        "WHERE CustomerID = @OldCustomerID " +
        "AND Name = @OldName " +
        "AND Address = @OldAddress " +
        "AND City = @OldCity " +
        "AND State = @OldState " +
        "AND ZipCode = @OldZipCode";
    using SqlConnection connection = new SqlConnection(
        MMABooksDB.ConnectionString);
    using SqlCommand command = new SqlCommand(
        updateStatement, connection);
    command.Parameters.AddWithValue("@NewName", newCustomer.Name);
    command.Parameters.AddWithValue("@NewAddress", newCustomer.Address);
    command.Parameters.AddWithValue("@NewCity", newCustomer.City);
    command.Parameters.AddWithValue("@NewState", newCustomer.StateCode);
    command.Parameters.AddWithValue("@NewZipCode", newCustomer.ZipCode);
    command.Parameters.AddWithValue(
        "@OldCustomerID", oldCustomer.CustomerId);
    command.Parameters.AddWithValue("@OldName", oldCustomer.Name);
    command.Parameters.AddWithValue("@OldAddress", oldCustomer.Address);
    command.Parameters.AddWithValue("@OldCity", oldCustomer.City);
    command.Parameters.AddWithValue("@OldState", oldCustomer.StateCode);
    command.Parameters.AddWithValue("@OldZipCode", oldCustomer.ZipCode);
    connection.Open();
    int count = command.ExecuteNonQuery();

    return (count > 0);
}
```