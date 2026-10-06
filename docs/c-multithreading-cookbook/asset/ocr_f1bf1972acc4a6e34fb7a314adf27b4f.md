# How it works...

We are presenting event usage and we've removed posting messages to the main window message queue. There is an advantage to this. We're independent of whether or not the application has a window. However, there is a down side. As the working thread fires an event (like a routine), all manipulation with UI elements, such as changing the value of the progress bar or label text, must be done by invoking a proper method. We intentionally created an example like this only to point out the cross-thread operations. This is very important to understand before doing anything asynchronously in .NET, which involves UI controls manipulation. Let's review the code. The MyForm constructor is invoked in a way that the first six lines of code are creating new instances of events and delegates. We've declared delegates to base attributes instead of locally-declared variables because more than one method will use them. We've added a static void that will be called on the EndTask EventHandler. And finally, inside the StartAddress method, instead of using the PostMessage API, we are raising an event to the user if they want to continue. So, by following a slightly different approach, we're using EAP in the way, which the .NET framework provides.

# There's more...

In order to understand the built EAP, we'll give an example of the WebClient::DownloadDataAsync method:

```
String szUrl = "http://cplplus.expert.its.me/testfile.txt";
WebClient* client = gcnew WebClient();
client->DownloadDataCompleted += 
gnew DownloadDataCompletedEventHandler(
&MyForm::AsyncDownloadDataCompleted);
client->DownloadDataAsync(gcnew Uri(szUrl));

static void AsyncDownloadDataCompleted(Object* sender,
DownloadDataCompletedEventArgs* e)
{
    String szResult;
System::Text::Encoding* enc = System::Text::Encoding::UTF8;
szResult = enc->GetString(e->Result);

if (e->Error == nullptr
&& String::IsNullOrEmpty(szResult))
{
    System::IO::File::WriteAllText(
L"C:\\testfile.txt", szResult);
MessageBox::Show("L Download commplete.");
}
}
```