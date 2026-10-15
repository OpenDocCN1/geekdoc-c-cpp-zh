Create a new Class Library project named NorthwindData. This project will represent a subset of the code you would use to manage the Northwind database. In this case, it will only access the employees table. Delete the default Class1 that is added to the project and add the following interface:

```
Public Interface INorthwindRepository
    Function AllEmployees() As List(Of Employee)
    Function GetEmployeeByID(ByVal id As Integer) As Employee
    Function FindEmployeeByLastName(ByVal lastname As String) As Employee
    Sub InsertEmployee(ByVal value As Employee)
    Sub DeleteEmployee(ByVal id As Integer)
End Interface
```

Code snippet from NorthwindData

This interface represents the actions that the data access component will be able to perform. While it isn't a complete set of CRUD (Create, Retrieve, Update, and Delete) functions, it should provide you with enough to test. This is added as an interface to make it easier when you create the test implementation in the next section. Add a new class, DbRepository, that implements the preceding interface:

```
Imports System.Collections.Generic

Public Class DbRepository
    Implements INorthwindRepository

    Dim db As New NorthwindClassesDataContext

    Public Function AllEmployees() As List(Of Employee) _
        Implements INorthwindRepository.AllEmployees
        Dim result As List(Of Employee)
        result = (From e In db.Employees Select e).ToList
        Return result
    End Function

    Public Sub DeleteEmployee(ByVal id As Integer) _
        Implements INorthwindRepository.DeleteEmployee
        Dim emp As Employee
        emp = (From e In db.Employees
            Where e.EmployeeID = id
            Select e).FirstOrDefault
        db.Employees.DeleteOnSubmit(emp)
        db.SubmitChanges()
    End Sub

    Public Function FindEmployeeByLastName(ByVal lastname As String) As Employee _
        Implements INorthwindRepository.FindEmployeeByLastName
        Dim result As Employee
        result = (From e In db.Employees
            Where e.LastName.StartsWith(lastname)
            Select e).FirstOrDefault
        Return result
    End Function

    Public Function GetEmployeeByID(ByVal id As Integer) As Employee _
        Implements INorthwindRepository.GetEmployeeByID
        Dim result As Employee
        result = (From e In db.Employees
            Where e.EmployeeID = id
            Select e).FirstOrDefault
        Return result
    End Function

    Public Sub InsertEmployee(ByVal value As Employee) _
        Implements INorthwindRepository.InsertEmployee
        db.Employees.InsertOnSubmit(value)
```