```
public DataAccessLayer()
{
    ConnectionStringSettingsCollection settings
    = ConfigurationManager.ConnectionStrings;

    string connectionString = settings["ConnString"].ConnectionString;

    connection = new SqlConnection(connectionString);
}

public DataTable GetCustomer(){...}

public void UpdateCustomer(DataTable dtTable){...}

private DataTable GetDetails(){...}

private void UpdateDetails(DataTable dtTable){...}
}
```

# Example 2

# Step 1 - Create table in SQL named Registration with the specified columns.

```
CREATE TABLE UserRegistration (
C_Id int IDENTITY(1, 1) NOT NULL,
C_Name varchar(100) NULL,
C_Age varchar(100) NULL,
C_Country varchar(100) NULL
);
```

# Step 2 - Create a Stored Procedure to insert, delete or update the Data from Registration Table.

```
Create procedure SpMyProcedure (
@Id int = null,
@Name varchar(100)= null,
@Age varchar(100)= null,
@Country varchar(100)= null,
@Action varchar(100)= null
) As begin if @Action = 'Insert' Insert into UserRegistration(C_Name, C_Age, C_Country)
values
(@Name, @Age, @Country) if @Action = 'Update'
Update
UserRegistration
set
C_Name = @Name,
C_Age = @Age,
C_Country = @Countrywhere C_Id = @Id if @Action = 'Delete'
Delete from
```