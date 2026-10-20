```
using System.Collections.Generic;
using System.Linq;
using System.Threading.Tasks;
using System.Collections.ObjectModel;
using ContactsApp.Abstract;
using ContactsApp.Entities;

namespace ContactsApp.Concrete
{
    public class MemoryContactsRepository : IContactsRepository
    {
        private ObservableCollection<Contact> contacts;
        public MemoryContactsRepository()
        {
            contacts = new ObservableCollection<Contact>()
            {
                new Contact()
                {
                    Id=1,
                    FirstName = "Ahmad",
                    LastName="Saeed",
                    Tel="123456",
                    EMail="admin@example.com",
                    Hobbies="Swimming"
                },
                new Contact()
                {
                    Id=2,
                    FirstName = "Mahmood",
                    LastName="Maktabi",
                    Tel="852136",
                    EMail="info@example.com",
                    Hobbies="Reading"
                }
```