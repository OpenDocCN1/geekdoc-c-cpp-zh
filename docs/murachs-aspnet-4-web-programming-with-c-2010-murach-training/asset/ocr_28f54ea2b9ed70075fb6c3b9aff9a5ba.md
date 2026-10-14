# How to create a web site that hosts a WCF service library

After you create and test a WCF service library, you can create a web site that hosts that library. Then, you’ll be able to run that web site under IIS.

# How to start a host web site

Figure 23-8 shows you how to create a web site that will host a WCF service library. To do that, you select the WCF Service template from the New Web Site dialog box. Then, you can use that dialog box to create either a file-system web site or a web site that runs under IIS. Although a file-system web site is fine for the initial development and testing, you’ll want to create a web site that runs under IIS to do your final testing.

When you use the WCF Service template, it automatically creates the Service.svc and Web.config files that you need to host a service. Then, you’ll typically rename the Service.svc file so it’s the same as the name of the service. In addition, you may need to make some changes to both of these files so they work correctly with the service. You’ll learn more about that in the next figure.

Earlier in this chapter, I mentioned that you can’t create a WCF service library using Visual Web Developer 2010 Express. However, you can still create a WCF service. To do that, you use the IService.cs and Service.cs files that are added to the App_Code folder of a WCF service web site by default. (This folder, along with the App_Data folder that’s also added by default, has been deleted from the web site shown in this figure since it’s not needed.) You write the code for these files just as you would for any other WCF service.

Unfortunately, when you create a WCF service directly in a WCF service web site, you can’t test the service as shown earlier in this chapter. Instead, you have to test it from a client application that uses the service. In addition, you won’t be able to host the web service in any other environments, such as a Windows application or WAS. Because of that, the service is much less flexible.

# How to add a reference to a service library

If you create a WCF service in a service library, you need to add a reference to that library to the host web site. To do that, you use the Add Reference dialog box shown in figure 23-8. From this dialog box, you can use the Browse tab of the Add Reference dialog box to navigate to the dll file for the WCF service library. In this case, I navigated to the HalloweenServiceLibrary.dll file in the bin\Debug directory of the project directory so I could debug the service from a client that uses the service. When I added a reference to this file, the files shown in the Bin directory in this figure were added to the project.