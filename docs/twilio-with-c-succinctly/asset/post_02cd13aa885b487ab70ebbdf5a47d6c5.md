
## Code Listing 13: The TwilioCore VerifyToken Method

```csharp
public VerifyTokenResult VerifyToken(string apikey, string userid, string token, bool tmode)
{
    if (apikey != string.Empty && userid != string.Empty && token != string.Empty)
    {
        AuthyClient client = new AuthyClient(apikey, tmode);
        return client.VerifyToken(userid, token);
    }
    else
        return null;
}
```

This method checks whether **apikey**, **userid**, **token**, and **tmode** are not empty strings. Notice that **token** is the value that the user received by SMS. We will verify whether or not it is correct—this is the purpose of using Authy with 2FA.

The verification of the token itself is done by creating an instance of the **AuthyClient** class and invoking the **VerifyToken** method from it.

When we run the main **program**, the result shown in Figure 24 is produced. Please notice that when you run your own **example**, you will receive a different verification code than the one displayed on the output screenshot in Figure 24.

![](img/7d3e41c7ef83c5fb4ef242998ad60317_34_0.png)

*Figure 24: The Output of the Main Authy App*

## Summary

In this chapter, we've explored how easy it is to get a Twilio and Authy account up and running. We've also seen how we can send SMS using the standard Twilio API and how to do that using Authy in order to do 2FA.

The process and code are very simple and easy to follow because of the way Twilio has wrapped the complexity of these services by creating friendly, easy, and approachable API libraries. Implementing a Twilio solution is a delightful experience.

At this point, you should also have a fairly good understanding of how to use Twilio to send SMS and enable 2FA with Authy by using the C# helper libraries.

In the next chapters, we'll explore more features Twilio offers, including working with calls and other useful voice-enabled applications.

## Chapter 2 Automation Using SMS

### Introduction

We've seen how Twilio empowers us to implement SMS communication in an intuitive and straightforward way and that it can even be used for enhancing authentication using 2FA.

Using the core principles and examples we've learned so far, in this chapter we'll focus on how we can build on that knowledge and create a couple of small but useful applications that we can use to optimize and automate business processes such as appointment reminders and automated, instant lead alerts.

By the end of this chapter, you should have a broad understanding of how to implement these solutions with SMS and a good appreciation of the overall business logic behind both.

Because some of the samples in this chapter require data storage, we'll be using Azure Table Storage to keep our data safe and easily accessible on the Microsoft Cloud.

The examples presented in this chapter are intended to be easy to follow and fun to implement while also being useful in a business context. We'll continue to use the TwilioCore class we developed in Chapter 1.

### Using Azure Table Storage as our backend

As you may know, Azure is Microsoft's awesome Cloud Services platform. It offers a broad range of services and works across multiple platforms.

Storage is one of its many useful services, and Azure includes a subservice for tables called Table Storage.

The Table Storage service uses a tabular format to store data. Each record represents an entity, and the columns represent the various properties of that entity (fields within a table).

Every entity has a pair of keys (a PartitionKey and RowKey) to uniquely identify it. Each entity also has a timestamp column that the Table service uses in order to know when the entity was last updated (this happens automatically, and the timestamp value cannot be overwritten—it is controlled internally by the service itself).

Extensive documentation about how the Storage and Table Storage services work can be found directly on the Azure website, which is an invaluable resource worth checking in order to gain a better understanding of both services.

Nevertheless, we'll quickly explore how we can get up and running with Azure Table Storage.

In order to get started with a Storage instance on Microsoft Azure, you'll need to sign in or sign up for Azure with a Microsoft account. You can do that by visiting https://azure.microsoft.com .

![](img/7d3e41c7ef83c5fb4ef242998ad60317_37_0.png)

Once you've signed up or signed in to the Azure Portal, you can browse through the list of Azure services and select Storage accounts (classic).

![](img/7d3e41c7ef83c5fb4ef242998ad60317_38_0.png)

*Figure 26: Filtering Through the List of Azure Services*

When you select **Storage accounts (classic)**, you’ll be presented with the following screen that allows you to add a new Storage account.

![](img/7d3e41c7ef83c5fb4ef242998ad60317_38_1.png)

*Figure 27: Storage Accounts (Classic) Panel*

In order to add a new Storage account (classic), click **Add**. Doing so will present a screen that allows you to add the account’s name and select the Azure location in which the account will be hosted.

![](img/7d3e41c7ef83c5fb4ef242998ad60317_39_0.png)

*Figure 27: Create a New Storage Account (Classic) Panel*

Once you have chosen a name and selected the location nearest you, click Create. Azure will immediately create the Storage account. Once created, it will look like Figure 28. You'll need your access keys in order to interact with the service from your code or any external tool. The keys can be found by clicking Keys.

![](img/7d3e41c7ef83c5fb4ef242998ad60317_40_0.png)

*Figure 28: Storage Account (Classic) Panel*

With the Azure Storage account now ready, you can use an open source, handy tool called Azure Storage Explorer that will allow you to easily connect to your Storage account and create, update, delete, and view any storage tables and data.

![](img/7d3e41c7ef83c5fb4ef242998ad60317_40_1.png)

*Figure 29: Azure Storage Explorer on CodePlex*

After you've downloaded and unzipped the zip file from CodePlex, you'll find an executable that will install the tool.

The installation wizard is easy to follow and self-explanatory, requiring just a few clicks, although please notice that the Azure Storage Explorer application only works on Windows.

Once installed, you'll have the following files on disk.

![](img/7d3e41c7ef83c5fb4ef242998ad60317_41_0.png)

In order to run the tool, double-click on the Azure Storage Explorer shortcut. Once the application is running, you'll need to connect your Azure Storage account to it. This can be done by clicking Add Account.

![](img/7d3e41c7ef83c5fb4ef242998ad60317_41_1.png)

When you click Add Account, you'll be requested to add your Storage account name and key, as shown in Figure 32.

![](img/7d3e41c7ef83c5fb4ef242998ad60317_42_0.png)

*Figure 32: Azure Storage Explorer Add Account Settings*

After entering the requested details, you should click Test Access in order to check if the connection works. If that is successful, you can click Save.

With these details stored, the next time you open the Azure Storage Explorer application, you’ll be able to access your Storage account from the dropdown next to the Add Account button.

With our Storage account wired up, let’s now explore how we can do some SMS automation with Twilio and use Table Storage as our backend.

## Appointment reminders

Keeping customers happy is probably the biggest challenge any company faces today. Fortunately, the right attitude and a bit of automation can make customer satisfaction an achievable goal.

Appointment reminders are a simple and effective way of automating the process of reaching out to customers before an upcoming appointment. We can write code that will allow us to accomplish this—we’ll use the `TwilioCore` class we’ve already written.

Let’s first think for a bit about how we can architect this solution. We’ll need to be able to create appointments with a future `DateTime` that we can store on Azure Table Storage. This future `DateTime` will be the appointment’s scheduled date. We’ll also need a process in place that watches when an appointment is scheduled, retrieves the information from Table Storage, and sends out an SMS to the registered phone number for that appointment.

We’ll initially explore the first action that allows us to interact with Azure Table Storage. In order to do that, let’s get the WindowsAzure.Storage NuGet package installed, then create an **Appointment** class.
