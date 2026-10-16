```
{    public Either<string, Client> GetById(int id) =>        clients.FirstOrNone(x => x.Id == id)        .ToEither("No client Found");}
```

Using toEither in order to convert the possible None, to an Either. Left with a more specific message

```
public class MockEmployeeRepository{
    public Either<string, Employee> GetById(int id) => clients.FirstOrNone(x => x.Id == id)        .ToEither("No employee Found");
}
```

```
public class Controller{
    MockEmployeeRepository employees = new MockEmployeeRepository();
    MockClientRepository clients = new MockClientRepository();
    public string GetAssignedEmployeeNameById(int clientId) =>
        clients
        .GetById(clientId)
        .Map(client => client.EmployeeId)
        .Bind(employees.GetById)
        .MatchWith((
            left: (e) => "there was an issue:" + e,
            right: (employee) => employee.Name
        ));
}
```

Run This: .Net Fiddle
Run This: ASP.NET MVC Fiddle

# 5.5.2 Using language-ext Either<>

Using the language-ext library Either gives us the same code since it has the same implementation for Bind

```
public string GetAssignedEmployeeNameById(int clientId) =>
    clients
        .GetById(clientId)
        .Map(client => client.EmployeeId)
        .Bind(employees.GetById)
        .Match(
            Right: (employee) => employee.Name,
            Left: (e) => $"error{e}"
        );
```