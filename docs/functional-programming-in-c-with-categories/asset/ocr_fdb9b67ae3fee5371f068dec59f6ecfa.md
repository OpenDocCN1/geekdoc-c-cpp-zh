```
public Task<Option<Employee>> GetAssignedEmployeeNameById(int clientId)
=> clients
.GetByIdAsync(clientId)
.Map(client => client.EmployeeId)
.BindT(employees.GetByIdAsync);
```

This is the same as

```
public Task<string> GetAssignedEmployeeNameById2(int clientId)
=> clients
.GetByIdAsync(clientId)
.Map(client => client.EmployeeId)
.BindT(employees.GetByIdAsync)
.Map(e => e.Case
switch
{
SomeCase<Employee>(var client) => client.Name,
NoneCase<Employee> { } => "No Client Found",
_ => throw new NotImplementedException()
});
```

Those GetAssignedEmployeeNameById returns a Task<Option<Employee>> but we could resolve the value early and return Task<string>

```
public Task<string> GetAssignedEmployeeNameById2(int clientId)
=> clients
.GetByIdAsync(clientId)
.Map(client => client.EmployeeId)
.BindT(employees.GetByIdAsync)
.Map(e => e.Case
switch
{
SomeCase<Employee>(var client) => client.Name,
NoneCase<Employee> { } => "No Client Found",
_ => throw new NotImplementedException()
});
```

Or even use the Linq syntax

```
public Task<string> GetAssignedEmployeeNameById3(int clientId) =>
(from c in clients.GetByIdAsync(clientId)
from e in employees.GetByIdAsync(c.EmployeeId)
select e)
.Map(e => e.Case
switch
{
SomeCase<Employee>(var client) => client.Name,
NoneCase<Employee> { } => "No Client Found",
_ => throw new NotImplementedException()
});
```

# 5.9 The Task - Option Monad Combination -OptionAsync<>

Coming back again to the OptionAsync we can Modify the previous example to allow the repositories to return OptionAsyncs