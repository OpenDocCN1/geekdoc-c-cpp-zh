# Chapter 35, “Creating Documents with WPF.”

What’s the future of WPF? Isn’t the UWP the UI platform to use for new applications going forward? UWP has advantages in supporting mobile devices as well. As long as some of your users have not upgraded to Windows 10, you need to support older operating systems such as Windows 7. UWP apps don’t run on Windows 7 or Windows 8. You can use WPF. In case you also would like to support mobile devices, it’s best to do as much code sharing as possible. You can create apps with both WPF and UWP by using as much common code as possible by supporting the MVVM pattern. This pattern is covered in Chapter 31, “Patterns with XAML Apps.”

# Universal Windows Platform

The Universal Windows Platform (UWP) is a strategic platform from Microsoft. When you use the UWP to create Windows apps, you’re limited to Windows 10 and newer versions of Windows. But you’re not bound to the desktop version of Windows. With Windows 10 you have a lot of different options, such as Phone, Xbox, Surface Hub, HoloLens, and IoT. There’s one API that works on all these devices!

One API for all these devices? Yes! Each device family can add its own Software Development Kit (SDK) to add features that are not part of the API that’s available for all devices. Adding these SDKs does not break the application, but you need to programmatically check whether an API from such an SDK is available on the platform the app is running. Depending on how many API calls you need to differentiate, the code might grow into a mess; dependency injection might be a better option.

> NOTE Dependency injection is discussed in Chapter 31, along with other patterns useful with XAML-based applications.

You can decide what device families to support with your applications. Not all device families will be useful for every app.

Will there be newer versions of Windows after Windows 10? Windows 11 is not planned. With Windows apps (which are also known as Metro apps, Windows Store apps, Modern apps, and Universal Windows apps) you’ve targeted either Windows 8 or Windows 8.1. Windows 8 apps typically were also running on Windows 8.1, but not the other way around. Now this is very different. When you create an app for the Universal Windows Platform, you target a version such as 10.0.10130.0 and define what minimum version is available and what latest version was tested, and the assumption is that it runs on future versions as well. Depending on the features you can use for your app and what version you’re expecting the user to have, you can decide what minimum version to support. Personal users will typically automatically update to newer versions; Enterprise users might stick to older versions.