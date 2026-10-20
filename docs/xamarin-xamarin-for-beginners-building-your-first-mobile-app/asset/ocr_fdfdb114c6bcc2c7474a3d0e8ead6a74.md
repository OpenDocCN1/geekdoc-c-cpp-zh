```
},
new Contact()
{
    Id=3,
    FirstName = "Mazen",
    LastName="Najem",
    Tel="987456",
    Email="it@example.com",
    Hobbies="Swimming"
},
new Contact()
{
    Id=4,
    FirstName = "Sawsan",
    LastName="Hilal",
    Tel="741258",
    Email="sales@example.com",
    Hobbies="Writing, Reading"
},
new Contact()
{
    Id=5,
    FirstName = "Musab",
    LastName="Aga",
    Tel="357159",
    Email="admin@example.com",
    Hobbies="Sport"
}
};
}
public async Task<ObservableCollection<Contact>>
GetContactsAsync(string firstName, string lastName)
{
    return await Task.Factory.StartNew(() =>
    {
```