

```
if (lsvContacts.ItemsSource != null)
    lsvContacts.ItemsSource = null;
}

private async void lsvContacts_ItemTapped (object sender, ItemTappedEventArgs e)
{
    Contact selectedContact = (Contact) e.Item;
    ContactDetailsPage ContactDetailsPage = new
        ContactDetailsPage (selectedContact);

    await Navigation.PushAsync (ContactDetailsPage);
}

private void ContactsPage_Appearing (object sender, EventArgs e)
{
    DoFind ();
}

private async void btnNewContact_Clicked (object sender, EventArgs e)
{
    ContactDetailsPage ContactDetailsPage = new
        ContactDetailsPage (null);

    await Navigation.PushAsync (ContactDetailsPage);
}
}
}
```

该文件包含 ContactsPage 类，其中包含我们之前在相应代码页上看到的事件处理程序，此外还有一个服务依赖项，即 DoFind，其功能是根据用户想要的条件（姓名和昵称）执行搜索。事件处理程序中的代码简单明了。但我想暂停一下，看看执行搜索的 DoFind 实用程序所使用的代码：

```
string firstName = txtFirstName.Text == null? "": txtFirstName.Text;
string lastName = txtLastName.Text == null? "": txtLastName.Text;
```

```
lsvContacts.ItemsSource = await ((App) Application.Current)
.ContactsRepository
.GetContactsAsync (firstName, lastName);
```

前两行很清晰，它们从文本框 txtFirstName 和 txtLastName 中获取用户想要的搜索条件。至于最后一行，它通过调用 GetContactsAsync 函数并将搜索条件传递给它，联系存储库执行搜索并返回结果。请看这句话：

```
await ((App) Application.Current) .ContactsRepository
.GetContactsAsync (firstName, lastName);
```

Application.Current 属性返回一个表示当前正在使用的应用程序的 Application 类型对象。反过来，需要使用 Transform (App) 将其转换为 App 类型的对象，即应用程序中的主类。事实上，我已在 App 类中声明了 ContactsRepository 功能，以便从我们应用程序的任何位置访问存储库。我们很快就会看到该功能的声明。

## ContactDetailsPage 联系人详情界面

按照我们添加主界面文件时相同的方式添加此界面，即添加到 Pages 文件夹中。其名称应为 ContactDetailsPage。

你的解决方案资源管理器将如下所示：

![](img/affff2e3b09de80cc0ffe811bbf63f5d_117_0.png)

我们转到 ContactDetailsPage.xaml 符号文件，并确保其内容如下：

```
<? xml version = "1.0" encoding = "utf-8"?>
<ContentPage xmlns = "http://xamarin.com/schemas/2014/forms"
```

```
xmlns: x = "http://schemas.microsoft.com/winfx/2009/xaml"
x: Class = "ContactsApp.Pages.ContactDetailsPage"

<StackLayout Orientation = "Vertical" Padding = "5,25,5">
<Label Text = "FirstName" />
<Entry x: Name = "txtFirstName" />
<Label Text = "LastName" />
<Entry x: Name = "txtLastName" />
<Label Text = "Tel" />
<Entry x: Name = "txtTel" />
<Label Text = "EMail" />
<Entry x: Name = "txtEMail" />
<Label Text = "Hobbies" />
<Editor x: Name = "txtHobbies" />
<StackLayout Orientation = "Horizontal">
<Button Text = "Save"
x: Name = "btnSave"
Clicked = "btnSave_Clicked" />
<Button Text = "Delete"
x: Name = "btnDelete"
Clicked = "btnDelete_Clicked" />
</StackLayout>
</StackLayout>
</ContentPage>
```

这显然是一个简单的文件。我们在此页面上报告了两个事件：

- * “保存”按钮的点击事件已关联到 btnSave_Clicked 处理器，负责保存和添加。
- * “删除”按钮的点击事件已关联到 btnDelete_Clicked 处理器，负责删除联系人。

转到与之前的符号文件对应的代码文件，名为 ContactDetailsPage.xaml.cs，并确保其内容如下：

```
using System;
using Xamarin.Forms;
using ContactsApp.Entities;

namespace ContactsApp.Pages
{
    public partial class ContactDetailsPage : ContentPage
    {
        private Contact currentContact;

        public ContactDetailsPage(Contact contact)
        {
            InitializeComponent();

            this.currentContact = contact;

            if (this.currentContact != null)
            {
                txtFirstName.Text = contact.FirstName;
                txtLastName.Text = contact.LastName;
                txtEMail.Text = contact.EMail;
                txtTel.Text = contact.Tel;
                txtHobbies.Text = contact.Hobbies;

                Title = contact.ToString() + " Details";

                btnDelete.IsVisible = true;
            }
            else
```

```
{
    Title = "New Contact";

    btnDelete.IsVisible = false;
}
}

private async void btnSave_Clicked(object sender, EventArgs e)
{
    string firstName = txtFirstName.Text == null ? "" : txtFirstName.Text;
    string lastName = txtLastName.Text == null ? "" : txtLastName.Text;
    string tel = txtTel.Text == null ? "" : txtTel.Text;
    string email = txtEMail.Text == null ? "" : txtEMail.Text;
    string hobbies = txtHobbies.Text == null ? "" : txtHobbies.Text;

    if (this.currentContact != null)
    {
        this.currentContact.FirstName = firstName;
        this.currentContact.LastName = lastName;
        this.currentContact.EMail = tel;
        this.currentContact.Tel = email;
        this.currentContact.Hobbies = hobbies;

        await ((App)Application.Current).ContactsRepository
            .UpdateContactAsync(this.currentContact);
    }
    else
    {
        Contact contact = new Contact
        {
            FirstName = firstName,
            LastName = lastName,
            Tel = tel,
            EMail = email,
```

```
```csharp
Hobbies = hobbies,
};
await ((App)Application.Current).ContactsRepository
.AddContactAsync(contact);
}
await Navigation.PopAsync();
}
```
```

```
```csharp
private async void btnDelete_Clicked(object sender, EventArgs e)
{
    var result = await
        DisplayAlert("Delete Confirmation",
            "Are you sure you want to delete this contact?",
            "Yes", "No");

    if (result)
    {
        await ((App)Application.Current).ContactsRepository
            .DeleteContactAsync(this.currentContact);

        await Navigation.PopAsync();
    }
}
```
```

我们之前也解释过，此界面的功能是查看和编辑联系人的详细信息，并有可能删除联系人，此外还可以使用此界面添加新联系人。此界面通过传递给其构造函数的联系人类型对象来区分其预期用途。如果该媒介包含有效的 Contact 对象，则意味着我们要显示该对象表示的联系人，然后修改或删除它，当然这需要显示删除按钮。如果 null 作为中间对象传递给构造函数，则意味着该页面被调用来创建全新的联系人，因此隐藏删除按钮，因为在这种情况下它没有意义。传递对象的副本保存在类中名为 currentContact 的专用字段下。界面的用途在构造函数本身内确定。请查看前面代码中 btnSave_Clicked 事件处理器的定义，了解它如何处理前两种情况（修改或添加）。

## 项：App

转到 App.cs 文件，并确保其内容如下：

```
```csharp
using Xamarin.Forms;
using ContactsApp.Abstract;
using ContactsApp.Concrete;
using ContactsApp.Pages;

namespace ContactsApp
{
	public class App: Application
	{
		public IContactsRepository ContactsRepository {get; set; }
		public App ()
		{
			ContactsRepository = new MemoryContactsRepository();
			// The root page of your application
			MainPage = new NavigationPage (new ContactsPage ());
		}
		protected override void OnStart ()
		{
			// Handle when your app starts
		}
	}
}
```

