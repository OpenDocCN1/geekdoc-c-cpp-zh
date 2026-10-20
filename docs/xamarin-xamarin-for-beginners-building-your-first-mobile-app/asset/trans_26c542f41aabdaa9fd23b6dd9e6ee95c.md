
在内部函数（lambda表达式）的最后两行，我们以全局组的形式显示搜索结果，该全局组是`ObservableCollection<Contact>`，其中它被隐式转换为`<ObservableCollection<Contact>>`类型的对象。

## 继续添加新联系人，AddContactAsync

AddContactAsync函数只需要一个Contact参数，并返回一个Task<bool>对象以指示添加操作是否成功：

```
public async Task<bool> AddContactAsync (Contact contactToAdd)
{
	return await Task.Factory.StartNew (() =>
	{
		contactToAdd.Id = contacts.Count () + 1;
		contacts.Add (contactToAdd);
		return true;
	});
}
```

此代码将新联系人添加到contacts变量下已有的联系人中，请注意以下代码：

```
contactToAdd.Id = contacts.Count () + 1;
```

这句话的作用在任何实际应用中都不存在。它给传递给函数的联系人的Id属性赋一个值。任何应用程序都不应该这样做，因为这个数字应该在联系人添加到数据库时自动生成。由于我们的应用程序依赖于内存中存在的假数据，我们不得不这样做以区分新添加的联系人。

## 继续 DeleteContactAsync

DeleteContactAsync函数只需要一个Contact参数，并返回一个Task<bool>对象以指示删除操作是否成功：

```csharp
public async Task<bool> DeleteContactAsync (Contact contactToDelete)
{
 return await Task.Factory.StartNew (() =>
 {
 var result = (from contact in contacts where contact.Id != contactToDelete.Id select contact);
 if (result != null)
 {
 contacts = new ObservableCollection<Contact> (result);
 contactToDelete = null;
 return true;
 }
 else
 {
 return false;
 }
 });
}
```

前面的代码实际上过滤了要删除的联系人，这仅意味着LINQ to Objects查询将返回除我们要删除的联系人的Id值之外的所有联系人。然后将结果赋予contacts变量，这意味着我们实际上已从内存中删除了此联系人。

## 继续 UpdateContactAsync

UpdateContactAsync函数只需要一个Contact类型参数，并返回一个Task<bool>对象以指示更新操作是否成功：

```
public async Task<bool> UpdateContactAsync (Contact contactToUpdate)
{
    return await Task.Factory.StartNew (() =>
    {
        Contact result = (from contact in contacts
                          where contact.Id == contactToUpdate.Id
                          select contact) .FirstOrDefault ();
        if (result != null)
        {
            contactToUpdate.FirstName = result.FirstName;
            contactToUpdate.LastName = result.LastName;
            contactToUpdate.EMail = result.EMail;
            contactToUpdate.Tel = result.Tel;
            contactToUpdate.Hobbies = result.Hobbies;
            return true;
        }
        else
        {
            return false;
        }
    });
}
```

此代码遵循相同的原则：LINQ to Objects查询根据联系人的Id属性值在contacts变量中搜索所需的联系人，获取后，其他属性的值也会清晰地进行更新。

这样，仓库模板就可以使用了。它将处理应用程序的所有组件，对数据执行四种不同类型的操作：搜索、添加、修改和删除。

## 结论

在本课中，我们研究了如何构建由MemoryContactsRepository类表示的存储库模型，这是通过我们了解的IContactsRepository接口实现的，我们了解了其中的四个函数，它们允许应用程序组件处理数据，而无需关注这些数据的位置。我们还学习了如何在四个依赖项中使用LINQ to Objects查询技术来执行该存储库所需的任务。在下一课中，我们将开始构建应用程序界面。

## 3

本课是有关如何使用初步数据构建联系人管理简单实用应用程序的系列课程的第三部分，也是最后一部分。在继续本课之前，您需要阅读第一部分和第二部分。

- 主界面，您可以通过它按姓名和昵称搜索联系人，也可以添加新联系人。
- 用于查看从主界面选择的联系人详细信息的界面，然后能够修改其数据甚至删除它。

此外，还需要修改App类以使应用程序可运行。

## ContactsPage 的主界面

首先，我们需要添加一个新文件夹，我们将其命名为Pages，用于放置应用程序的任何新页面。

从解决方案资源管理器窗口中，右键单击ContactsApp（Portal）项目名称，然后从出现的列表中选择“添加”选项。从子菜单中选择“新建文件夹”并将其命名为Pages。

右键单击刚刚添加的文件夹Pages，然后从“添加”菜单中选择“新建项”子菜单，会出现一个窗口，允许您选择要添加的新项。像我们在本课中已经做的那样，选择基于代码的内容页。将此页命名为ContactsPage。

现在转到ContactsPage.xaml文件，并确保其内容如下：

```
<?xml version="1.0" encoding="utf-8"?>
<ContentPage xmlns="http://xamarin.com/schemas/2014/forms" xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml" x:Class="ContactsApp.Pages.ContactsPage" Appearing="ContactsPage_Appearing">

<StackLayout>
    <StackLayout Padding="5,25,5,5">
        <StackLayout Orientation="Horizontal">
            <Label Text="First Name" />
            <Editor x:Name="txtFirstName" HorizontalOptions="FillAndExpand" TextChanged="Editor_TextChanged" />
        </StackLayout>

        <StackLayout Orientation="Horizontal">
            <Label Text="Last Name" />
            <Editor x:Name="txtLastName" HorizontalOptions="FillAndExpand" TextChanged="Editor_TextChanged" />
```

```
</StackLayout>

<Button Text="Find" x:Name="btnFind" Clicked="btnFind_Clicked" />
</StackLayout>

<StackLayout>
<ListView x:Name="lsvContacts" ItemTapped="lsvContacts_ItemTapped" />
</StackLayout>

<Button Text="+ New Contact" HorizontalOptions="FillAndExpand" Clicked="btnNewContact_Clicked" />
</StackLayout>

</ContentPage>
```

我们在此页面上使用了四个不同的事件。下面将简要介绍每个事件：

- 将Contacts页面的Appearing事件链接到ContactsPage_Appearing处理程序，以便在从负责查看联系人详细信息的页面返回时更新页面数据，我们将在本课后面看到。
- txtFirstName和txtLastName都发生了TextChanged变化，我们将其链接到Editor_TextChanged处理程序，以便在任何用户更改时清除lsvContacts列表下方出现的搜索结果。
- 点击了lsvContacts列表中的项，我们将其链接到lsvContacts_ItemTapped处理程序，以便程序在点击时移动到负责查看联系人详细信息的界面。
- 单击“添加新联系人”按钮，并将其链接到btnNewContact_Clicked处理程序。

然后，转到相应的代码文件ContactsPage.xaml.cs，并确保其内容如下：

```
using System;
using Xamarin.Forms;
using ContactsApp.Entities;

namespace ContactsApp.Pages
{
    public partial class ContactsPage: ContentPage
    {
        public ContactsPage ()
        {
            InitializeComponent ();
        }

        private async void DoFind ()
        {
            string firstName = txtFirstName.Text == null ? "" : txtFirstName.Text;
            string lastName = txtLastName.Text == null ? "" : txtLastName.Text;

            lsvContacts.ItemsSource = await ((App) Application.Current).ContactsRepository.GetContactsAsync (firstName, lastName);
        }

        private void btnFind_Clicked (object sender, EventArgs e)
        {
            DoFind ();
        }

        private void Editor_TextChanged (object sender, TextChangedEventArgs e)
        {

```

