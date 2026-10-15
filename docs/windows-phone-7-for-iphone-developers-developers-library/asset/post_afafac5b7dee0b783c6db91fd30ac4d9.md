
```
<shell:ApplicationBarIconButton x:Name="appBarDelButton"
    IconUri="/Images/appbar.delete.rest.png"
    Text="Delete" Click="appBarDelButton_Click"/>
</shell:ApplicationBar>
</phone:PhoneApplicationPage.ApplicationBar>
</phone:PhoneApplicationPage>
```

And finally, here is the code-behind to the main page shown in Listing 14.6.

## Listing 14.6 MainPage.xaml.cs

```
using System;
using System.Windows;
using System.Windows.Controls;
using Microsoft.Phone.Controls;

namespace IsolatedStorageDemo
{
    public partial class MainPage : PhoneApplicationPage
    {
        // Constructor
        public MainPage()
        {
            InitializeComponent();

            DataContext = App.ViewModel;
            this.Loaded += new RoutedEventHandler(MainPage_Loaded);
        }

        private void MainListBox_SelectionChanged(object sender,
            SelectionChangedEventArgs e)
        {
            // If selected index is -1 (no selection) do nothing
            if (MainListBox.SelectedIndex == -1)
                return;

            (e.AddedItems[0] as ItemViewModel).IsSelected = true;
            if ((e.RemovedItems != null) && (e.RemovedItems.Count > 0))
            {
                (e.RemovedItems[0] as ItemViewModel).IsSelected = false;
            }
        }

        private void MainPage_Loaded(object sender, RoutedEventArgs e)
        {
            if (!App.ViewModel.IsDataLoaded)
```
```
{
	App.ViewModel.LoadData();
}
```

```
private void appBarAddButton_Click(object sender, EventArgs e)
{
	Random r = new Random();
	ItemViewModel newItem = new ItemViewModel { Name = "Customer " + r.Next(5, 100).ToString(),
		Description = "Newly Created Customer" };
	App.ViewModel.Items.Add(newItem);
	App.ViewModel.SaveToIso();
}
```

```
private void appBarDelButton_Click(object sender, EventArgs e)
{
	MessageBoxResult result = MessageBox.Show("Delete " + App.ViewModel.Items[MainListBox.SelectedIndex].Name + "?",
		"Confirm", MessageBoxButton.OKCancel);
	if (result == MessageBoxResult.OK)
	{
		App.ViewModel.Items.RemoveAt(MainListBox.SelectedIndex);
	}
	App.ViewModel.SaveToIso();
}
```

When you run this sample (there are a few files necessary for compilation not included in the source listings in this chapter that you can get from the code downloads for the book), you get something that looks similar to Figure 14.3.

![](img/04a00d46bb1059867d95707babd62ee7_208_0.png)

Figure 14.3   Running the isolated storage sample.

## Summary

This chapter started with a discussion about some of the capabilities of Core Data on the iPhone. Because no direct correlation exists between Core Data and WP7, this chapter focused on the capability to store and retrieve entire object hierarchies to and from disk using isolated storage.

With the combination of isolated storage, the WCF Data Contract Serializer, and LINQ for runtime queries of in-memory data, your application can manage virtually any kind of data with relative ease. This chapter showed you how to accomplish that using isolated storage. In the next chapter, you’ll see how to deal with remote data by building smart clients.

## Building Smart Clients

> *If Facebook were a country, it would now be the 6th most populous in the world.*
> 
> InsideFacebook.com

This chapter provides an overview of one of the most powerful application types for mobile devices—the smart client. The days of the massive, monolithic desktop application are numbered. Even applications that sit on modern desktops often communicate with services on the Internet for supplemental information, research, lookups, or even complex calculations.

A smart client is an application that takes advantage of the hardware of the host environment. It is capable of using the GPS, the accelerometer, high-resolution video, audio, and of course, network devices. These applications can be anything from casual games to weather applications to applications such as Netflix, Flixster, Facebook, Twitter, and so on. Although all these applications are fully installed WP7 applications, the real work is done elsewhere, and the real data resides in the cloud. Aside from a few niches, today's mobile phone users often won't even bother installing applications that aren't connected in some way to the world (via the Internet, GPS, Wi-Fi, and so on) around them.

This is the model that this chapter discusses, showing you how to harness the networking and storage capabilities of WP7 to build applications that talk to platform-neutral RESTful services as well as applications that talk to Windows Communication Foundation (WCF) services on .NET-based application servers.

## Consuming RESTful Services

REST is an acronym that stands for REpresentational State Transfer. To summarize quickly so we can get to the code demos as fast as possible, this boils down to treating the Web like a collection of resources. Every resource has a Unique Resource Identifier

(URI). By using verbs that are part of the standard HTTP vocabulary, such as GET, PUT, DELETE, and POST, and using the URIs as if they were nouns, we can construct a vocabulary that allows us to manipulate and query resources regardless of the underlying platform on which these resources are hosted.

Suppose you have a resource collection called Users exposed at a URI like http://my.server.com/Users. Using typical REST assumptions, issuing an HTTP GET request to this URI should give you some representation (almost always XML, often in “feed” form, although lately JSON has become a popular alternative) of that collection. Sending an HTTP GET to http://my.server.com/Users/bob should, according to convention, give you a representation of the resource known as “bob” belonging to the resource collection “Users”. Using an HTTP PUT to that same URI will replace the representation of “bob” on the server with the one you sent. Sending an HTTP DELETE to that URI should, assuming you have access, delete the resource known as “bob.”

For a full discussion of RESTful architecture, check out the extensive Wikipedia entry on it at http://en.wikipedia.org/wiki/Representational_State_Transfer. Many books talk about the various ways to implement RESTful services in different languages. One such book is RESTful .NET (ISBN: 0596519206) by Jon Flanders. If you’re into Ruby, the Practical REST on Rails 2 Projects book by Ben Scofield is another excellent guide.

It doesn’t take very much or deep thought to start to realize some of the benefits of this type of exposure of services. Rather than utilizing someone’s fixed remote procedure call (RPC) style interface, where you are invoking proprietary methods, you’re just using the basic vocabulary of the Internet itself. RESTful services have rapidly become popular, especially among social networking sites that want to make their information and APIs as easy to use and widely available as possible.

## Why LINQ to XML Is Your New Best Friend

There are two parts to communicating with RESTful services. The first is the HTTP communication where your code needs to be able to send payloads utilizing standard HTTP methods such as GET and POST. (PUT and DELETE are often left out to allow for a wider variety of client consumption, but that’s a topic better discussed in one of the aforementioned books on RESTful services.)

The second part of communicating with RESTful services is being able to read and write the payload, or resource. In most cases this payload is represented as XML—either as XML that conforms to some custom schema or as a feed type of XML, such as Atom or RSS.

This is why LINQ to XML is your new best friend. LINQ to XML will allow your C# code to rip through any XML document (obtained either locally or from the Web), process it, query it, and turn it into usable view model data quickly, efficiently, and in a way that is easy to read and understand by other developers.

The first class you need to talk to RESTful services is the WebClient class. Although more robust alternatives are available in the full version of the .NET Framework, WebClient is the go-to class that is available to Silverlight developers for making web
