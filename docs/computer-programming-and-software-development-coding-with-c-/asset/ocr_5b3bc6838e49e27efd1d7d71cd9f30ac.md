```
public interface IPersonReader
{
    IEnumerable<Person> GetPeople();
    Person GetPerson(int id);
}
```

What if we wanted to add update functionality? One way to do this is with interface inheritance. Here is an IPersonRepository interface that has both read and write functionality. The write functionality comes from the AddPerson, UpdatePerson, and DeletePerson methods in the interface. It inherits the IPersonReader interface.

```
public interface IPersonRepository : IPersonReader
{
    void AddPerson(Person newPerson);
    void UpdatePerson(int id, Person updated);
    void DeletePerson(int id);
}
```

This means that it also includes the read operations, GetPeople and GetPerson. When a class implements the IPersonRepository interface, it must implement all of the methods. Here we have a SQLRepository class that implements the IPersonRepository interface.