
general error and the error can be corrected by the user. In the above example, the error can be corrected by passing a nonzero value for the second parameter.

- **Error State** - The ErrorState is also an integer value between 1 and 255. The RAISERROR() function can only generate custom errors if the Error State value is set between 1 and 127.
- In SQL Server 2000, in order to detect errors, the @@Error system function is used. The @@Error system function returns a NON-ZERO value if there is an error, otherwise, ZERO, which indicates that the previous SQL statement executed without any error.

## Using @@Error System Function in SQL Server

- A modified version of the above stored procedure to make use of the @@ERROR system function is as shown below.

```sql
ALTER PROCEDURE spDivideTwoNumber
@Number1 INT,
@Number2 INT
AS
BEGIN
DECLARE @Result INT
SET @Result = 0
IF(@Number2 = 0)
BEGIN
RAISERROR('Second Number Cannot be zero',16,1)
END
ELSE
BEGIN
SET @Result = @Number1 / @Number2
END

IF(@@ERROR <> 0)
BEGIN
PRINT 'Error Occurred'
END
ELSE
BEGIN
PRINT 'RESULT IS :'+CAST(@Result AS VARCHAR)
END
END
```

When the above stored procedure is executed passing 100 and 0, it gives the below output.

```text
Msg 8134, level 16, state 1, procedure spDivideTwoNumber, Line 21: divide by zero error encountered.
RESULT IS : 0
```

## Predefined Error Terms in Details

- Whenever an error occurs under a program like dividing a number by zero, violation of primary key, violation of Check constraint, etc., the system displays an error message conveying to the application the problem encountered in the code. Every error that occurs in the program is associated with four attributes.
  - 1. Error Number
  - 2. Error Message
  - 3. Severity Level
  - 4. Error State

### Example

Message 8134 (Error Number), Level 16 (Severity Level), State 1 (State), Divide by Zero error encountered (Error Message)

- **Error Number:** The error number is a unique identifier given for each and every error that occurs in SQL Server. This value will be below 50,000 for predefined errors and must be above 50,000 for errors defined by the user.
- **Error Message:** It is a piece of brief information describing the error that occurred, which should be a maximum of 2047 characters.
- **Severity Level:** This tells about the importance of the error which can range between 0 and 24. In which:
  - 1. 0 to 9: are not severe, which can be considered as information or status messages.
  - 2. 11 to 16: Indicates these errors can be created by the user.
  - 3. 17 to 19: Indicates these are software errors that cannot be corrected by the user and must be reported to the system administrator.
  - 4. 20 to 24: Indicates fatal errors and if these errors occur they can damage the system or database. So here the connection immediately terminates with the database.
- **Error state:** It is an arbitrary value that is not that important and can range between 0 and 127. This is used whenever the same error has to occur in multiple places.

```sql
Set @val1=8;
Set @val2=@val1/0; /* Error Occur Here */
END TRY
BEGIN CATCH
Print 'Error Occur that is:'
Print Error_Message()
END CATCH
```

Output:

```text
Error Occur that is:
Divide by zero error encountered
```

## 2. User Defined Exception

This type of exception is user generated, not system generated.

### Example - User Defined Exception

```sql
Declare @val1 int;
Declare @val2 int;
BEGIN TRY
Set @val1=8;
Set @val2=@val1%2;
if @val1=1
Print 'Error Not Occur'
else
Begin
Print 'Error Occur';
Throw 60000,'Number Is Even',5
End

END TRY
BEGIN CATCH
Print 'Error Occur that is:'
Print Error_Message()
END CATCH
```

### Output

```text
Error Occur
Error Occur that is:
Number Is Even
```

Here 60000 denotes the error number and 5 denotes the state to associate with the message.

## 13.2.5.5 Error Information Using - System Functions

- The error message that is a system-generated message can be displayed after collecting information about the error using a system function called the ERROR_MESSAGE().

Consider the below error message. In context with it, all the parts of the error message are discussed below.

![](img/3005a4307e6d8f3bb7e76eea28a92357_395_0.png)

SQL Server has six predefined system functions used in the Catch block.

- 1) **ERROR_MESSAGE()** - This function will return a text message explaining the error. One can embed or add one's own message along with the predefined message.

```sql
BEGIN TRY
SELECT 1/0
END TRY
BEGIN CATCH
SELECT 'AN ERROR OCCURRED:' + ERROR_MESSAGE() AS Custom_Error
END CATCH
```

The result is "AN ERROR OCCURRED: Divide by zero error encountered."

- 2) **ERROR_NUMBER()** - Returns the number of the error. Normally these numbers work as conditions in the Catch block, which helps writing custom messages. Every SQL Server error has uniquely defined error messages along with numbers.

All the system errors can be seen by running the below query.

```sql
SELECT * FROM master.dbo.sysmessages
```

- 3) **ERROR_SEVERITY()** - Returns the severity of the error. While executing the above query it can be noticed that the second column is named severity. This indicates the nature of the error.

```sql
SELECT DISTINCT severity
FROM master.dbo.sysmessages
ORDER BY severity
```

For example, if the below code is executed the output would be as shown.

```sql
BEGIN TRY
SELECT 1/0
END TRY
BEGIN CATCH
SELECT 'ERROR SEVERITY: ' + CAST(ERROR_SEVERITY() AS VARCHAR(2)) AS Error
END CATCH
```

The result is ERROR SEVERITY: 16.

Severity level 16 indicates that the error has occurred due to a user problem and it can be fixed by the user.

- 4) **ERROR_STATE()** - This function will return an integer value that indicates the exact location in the code where the error has occurred. In a multi-user environment, the "state" of the error can help locate and diagnose errors with ease.

```sql
SELECT ERROR_STATE() AS ErrorState
```

- 5) **ERROR_PROCEDURE()** - Returns the name of the procedure that threw the error. This can be done by adding the following line inside the catch block.

```sql
SELECT ERROR_PROCEDURE() AS Stored_Procedure
```

If it is not a procedure, but a query, then it will return as NULL.

- 6) **ERROR_LINE()** - Returns the line number where the actual error has occurred.

This helps developers to pinpoint the place of error (code) and fix it.

## 13.2.5.6 Advanced SQL Error Handling

The exception handling can be done for transactions as well. This can be achieved by running and analyzing the XACT_STATE function that reports transaction state.

This function returns one of the following three values,

- 1 - the transaction is committable
- -1 - the transaction is uncommittable and should be rolled back
- 0 - there are no pending transactions

The only crucial aspect here is to remember to actually do this inside the catch statement because it would be required to better stop the transactions rather than starting them and then committing them or rolling them back.

## 13.3 Reflections and Attributes

### 13.3.1 Application Metadata Attributes

### Concept

- 1. Attributes are a mechanism for adding metadata, such as compiler instructions and other data about data, methods, and classes, to the program itself. Attributes are inserted into the metadata and are visible through ILDasm and other metadata-reading tools.

### Explanation

- 2. An attribute is a declarative tag. A declarative tag is depicted by square ([ ]) brackets placed above the element it is used for.
- 3. Attributes are used for adding metadata, such as compiler instructions and other information such as comments, descriptions, methods and classes to a program. The .NET Framework provides two types of attributes: *the pre-defined attributes and custom-built attributes*.
- 4. Attributes get inherited in the derived classes.

### 13.3.1.1 Types of Attribute

Attributes can be either **Predefined attributes (intrinsic)** or custom. **Intrinsic attributes** are supplied as part of the Common Language Runtime (CLR), and they are integrated into .NET. **Custom attributes** are attributes one creates for one's own purposes. Most programmers will use only intrinsic attributes, though custom attributes can be a powerful tool when combined with reflection.

### Attribute targets

The entity on which the attribute is applied is termed as the target. Some attributes are applied to an assembly, others to a class or interface, and some, such as [WebMethod], are applied to class members. These are called the attribute targets. **Possible attribute targets are described below.**

| Member name | Usage |
|---|---|
| All | Applied to any of the following elements: assembly, class, constructor, delegate, enum, event, field, interface, method, module, parameter, property, return value, or struct |
| Assembly | Applied to the assembly itself |
| Class | Applied to instances of the class |
| Constructor | Applied to a given constructor |
| Delegate | Applied to the delegated method |
| Enum | Applied to an enumeration |
