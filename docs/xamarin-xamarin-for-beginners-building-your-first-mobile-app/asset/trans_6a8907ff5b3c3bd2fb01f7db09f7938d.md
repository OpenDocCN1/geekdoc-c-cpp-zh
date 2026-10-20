

```
new Contact ()
{
    Id = 1,
    FirstName = "Ahmad",
    LastName = "Saeed",
    Tel = "123456",
    EMail = "admin@example.com",
    Hobbies = "Swimming"
},
new Contact ()
{
    Id = 2,
    FirstName = "Mahmood",
    LastName = "Maktabi",
    Tel = "852136",
    EMail = "info@example.com",
    Hobbies = "Reading"
},
new Contact ()
{
    Id = 3,
    FirstName = "Mazen",
    LastName = "Najem",
    Tel = "987456",
    EMail = "it@example.com",
    Hobbies = "Swimming"
},
new Contact ()
{
    Id = 4,
    FirstName = "Sawsan",
    LastName = "Hilal",
    Tel = "741258",
    EMail = "sales@example.com",
    Hobbies = "Writing, Reading"
},
new Contact ()
{
    Id = 5,
    FirstName = "Musab",
    LastName = "Aga",
    Tel = "357159",
    EMail = "admin@example.com",
    Hobbies = "Sport"
}
};
}
public async Task<ObservableCollection<Contact>>
GetContactsAsync (string firstName, string lastName)
{
    throw new System.NotImplementedException ();
}

public async Task<bool> AddContactAsync (Contact
contactToAdd)
{
    throw new System.NotImplementedException ();
}
public async Task<bool> UpdateContactAsync (Contact
contactToUpdate)
{
    throw new System.NotImplementedException ();
}
public async Task<bool> DeleteContactAsync (Contact
contactToDelete)
{
    throw new System.NotImplementedException ();
}
}
}

这里引人注目的地方在于，联系人数据已经存在于此类别中，并且具体存在于其结构中。它存储在 contacts 变量中，并在类级别定义，并且全局类型为 ObservableCollection，我们将在下一课中讨论。现阶段只需知道它是一个元素集合，其类型为联系人类型，并且在异步编程的应用中很有用。以这种方式将数据存储在项目中是完全不现实的。假设它位于本地或远程数据库中，甚至是普通文件中。事实上，Repository 的真正强大之处在于将数据获取方法与实际程序隔离开来。

也很明显，这里的方法实际上包含一段代码，会抛出 NotImplementedException 来提醒我们它尚未准备就绪。

解决方案资源管理器最终将看起来类似于以下内容：

![](img/affff2e3b09de80cc0ffe811bbf63f5d_100_0.png)

## 结论

本课是联系人应用程序的介绍，我们将在接下来的两课中继续构建它。在本课中，我们介绍了基本的应用思路，并通过构建一个代表它的接口以及一个实现它的类，阐明了 Repository 模型的概念。通过这个类（仓库类），我们将能够处理仅包含在应用程序内存中的数据

虽然这种方法不切实际，但有必要简化问题，使其更容易理解。我们还创建了一个代表应用中联系人的项目。我们看到了它与仓库类之间的关系，通过在最后一课中对门徒的召唤。

在本课中，我们将继续在上一课中开始的工作，即构建联系人应用程序。在上一课中，我们通过声明 IContactsRepository 接口并通过 MemoryContactsRepository 类实现它，完成了存储库模型的构建。我们还创建了 Contacts 类别，它是应用中的构建块。

在本课中，我们将为存储库 MemoryContactsRepository 添加功能，使我们的应用程序可用。

## 准备仓库的功能方面

打开 MemoryContactsRepository.cs 文件并确保其内容如下：

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

```
IEnumerable<Contact> result = from contact in contacts where
    contact.FirstName
        .ToUpper()
        .Contains(firstName.ToUpper()) &&
    contact.LastName
        .ToUpper()
        .Contains(lastName.ToUpper())
    select contact;

    ObservableCollection<Contact> tmp = new
ObservableCollection<Contact>(result);
    return tmp;
    });
}
public async Task<bool> AddContactAsync(Contact contactToAdd)
{
    return await Task.Factory.StartNew(() =>
    {
        contactToAdd.Id = contacts.Count() + 1;
        contacts.Add(contactToAdd);
        return true;
    });
}
    public async Task<bool> UpdateContactAsync(Contact contactToUpdate)
{
    return await Task.Factory.StartNew(() =>
    {
        Contact result = (from contact in contacts
            where contact.Id == contactToUpdate.Id
            select contact).FirstOrDefault();

        if (result != null)
        {
            contactToUpdate.FirstName = result.FirstName;
```

```
contactToUpdate.LastName = result.LastName;
contactToUpdate.Email = result.Email;
contactToUpdate.Tel = result.Tel;
contactToUpdate.Hobbies = result.Hobbies;

return true;
} 
else 
{
return false;
}
});

public async Task<bool> DeleteContactAsync(Contact contactToDelete)
{
return await Task.Factory.StartNew(() =>
{
var result = (from contact in contacts
where contact.Id != contactToDelete.Id
select contact);

if (result != null)
{
contacts = new ObservableCollection<Contact>(result);
contactToDelete = null;
return true;
}
else 
{
return false;
}
}
});
}
```

```
}
}
```

新的是，我们为存储库中的每个基本功能分配了代码。查看以下段落，了解每个子项中代码的工作原理。

## 继续搜索 GetContactsAsync

以下是 GetContactsAsync 函数，它需要字符串参数按姓名和昵称搜索联系人：

```
public async Task<ObservableCollection<Contact>>
GetContactsAsync (string firstName, string lastName)
{
    return await Task.Factory.StartNew (() =>
    {
        IEnumerable<Contact> result = from contact in contacts where
            contact.FirstName
                .ToUpper ()
                .Contains (firstName.ToUpper ()) &&
            contact.LastName
                .ToUpper ()
                .Contains (lastName.ToUpper ())
            select contact;
        ObservableCollection<Contact> tmp = new ObservableCollection<Contact> (result);
        return tmp;
    });
}
```

