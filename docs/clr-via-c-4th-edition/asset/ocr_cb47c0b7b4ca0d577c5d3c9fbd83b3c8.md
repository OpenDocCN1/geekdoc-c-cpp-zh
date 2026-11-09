After recording information about the failing application, Windows displays the message box allowing the end user to send information about the failing application to Microsoft servers.⁷ This is called *Windows Error Reporting*, and more information about it can be found at the Windows Quality website (http://WinQual.Microsoft.com).

Companies can optionally sign up with Microsoft to view this information about their own applications and components. Signing up is free, but it does require that your assemblies be signed with a VeriSign ID (also called a Software Publisher’s Digital ID for Authenticode).

Naturally, you could also develop your own system for getting unhandled exception information back to you so that you can fix bugs in your code. When your application initializes, you can inform the CLR that you have a method that you want to be called whenever any thread in your application experiences an unhandled exception.

Unfortunately, every application model Microsoft produces has its own way of tapping into unhandled exceptions. The members that you want to look up in the FCL documentation are:

+   - For many applications, look at `System.AppDomain`’s `UnhandledException` event. Windows Store applications and Microsoft Silverlight applications cannot access this event.
+   - For a Windows Store App, look at `Windows.UI.Xaml.Application`’s `UnhandledException` event.
+   - For a Windows Forms application, look at `System.Windows.Forms.NativeWindow`’s `OnThreadException` virtual method, `System.Windows.Forms.Application`’s `OnThreadException` virtual method, and `System.Windows.Forms.Application`’s `ThreadException` virtual method.
+   - For a Windows Presentation Foundation (WPF) application, look at `System.Windows.Application`’s `DispatcherUnhandledException` event and `System.Windows.Threading.Dispatcher`’s `UnhandledException` and `UnhandledExceptionFilter` events.
+   - For Silverlight, look at `System.Windows.Application`’s `UnhandledException` event.
+   - For an ASP.NET Web Form application, look at `System.Web.UI.TemplateControl`’s `Error` event. `TemplateControl` is the base class of the `System.Web.UI.Page` and `System.Web.UI.UserControl` classes. Furthermore, you should also look at `System.Web.HttpApplication`’s `Error` event.
+   - For a Windows Communication Foundation application, look at `System.ServiceModel.Dispatcher.ChannelDispatcher`’s `ErrorHandlers` property.

Before I leave this section, I’d like to say a few words about unhandled exceptions that could occur in a distributed application such as a website or web service. In an ideal world, a server application that experiences an unhandled exception should log it, send some kind of notification back to the

⁷ You can actually disable this message box by using P/Invoke to call Win32’s `SetErrorMode` function, passing in `SEM_NOGPFAULTERRORBOX`.