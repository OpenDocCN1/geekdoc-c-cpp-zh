
The control you added to the Master page is part of the Optimization package and provides an easy way to render the resulting CSS file. When you installed the package, the Web.config was updated to register the webopt prefix, similar to how you registered your own Wcx prefix in this chapter:

```
<add assembly="Microsoft.AspNet.Optimization.WebForms" namespace="Microsoft.AspNet.Optimization.WebForms" tagPrefix="webopt" />
```

Bundling and minification is only active when debugging is turned off in the Web.config file. It makes it easy to debug your CSS files during development, while a single, minified file is streamed to the browser in your production environment.

Bundling and minification are fully extensible, meaning you can customize the ways files are included and minified. For more information, check out this blog post: http://tinyurl.com/c63reut.

Now that you have seen how to optimize your site for CSS and script references are handled, the next step is to publish your site.

## PREPARING FOR DEPLOYMENT

During development of your site, you use IIS Express, which ships with Visual Studio. Although this server is great for local development, it's not designed to be used in a production environment. To production, you need to deploy to a machine that runs the full version of Internet Information Services (IIS), Microsoft's professional web server. If you are using a host that supports Microsoft Web Deploy for Hosting you can simply deploy your site using the Publish command in Visual Studio. If you're hosting your site yourself and have not installed Web Deploy, you can publish your site to a local folder that you can deploy to your own IIS server. Later in this chapter, we will show you how to install and configure IIS in case you're hosting the site yourself.

Whether you are hosting the site yourself or using an web host, you're likely to have different settings in Web.config for your development and production environments. Visual Studio makes it easy to maintain multiple versions of your configuration files — for your development and production environments, for example. However, in order to use that feature what you need is called a publishing profile. The next section therefore looks at publishing first, and a later section digs into maintaining your configuration files.

## Publishing Your Site

To deploy your website to a production server, the deployment options shown in the following table are available right within VS.

| DEPLOYMENT OPTION | DESCRIPTION |
|---|--- |
| File System | Enables you to create a copy of the site on the local filesystem of your development machine or a networked machine. This option is useful if you want to move the files manually to your production server later or if your production server is accessible over the local network. |
| FTP Site | Enables you to send the files that make up your web application directly to a remote server using FTP. |
| Web Deploy | Enables you to send the files that make up your web application to a remote IIS server using Web Deploy. For this option to work, the remote server needs to have Web Deploy for Hosting Servers installed. Many providers support this option, which makes it convenient to publish your changes. Consult your provider to see if they support this option and for the necessary connection details. |
| Web Deploy Package | Enables you to create a package (.ZIP file) with all the site's files that an administrator can install on a server with IIS and Web Deploy for Hosting Servers installed. For more information, see http://bit.1y/1ckqri. |

You select among these options when you publish your site, as you'll see in the next exercise.

Before you publish your site, it's a good idea to check the state of your website. You should do a full recompile using Visual Studio all the code and pages in your website. This helps you detect any problems in your website before you deploy it to a production environment.

Deploying a site is also a good moment to do some housekeeping. To avoid slowing down the deployment process and keep your site as lean and clean as possible, you should delete the files from your website that you don't need in production.

In the next exercise you see how to publish your site to another folder on your local disk. You'll need to republish the site again when the configuration file management capabilities are discussed.

## TRY OUT Publishing Your Website

In this Try Out, you use the Publish command with the File System option to create a copy of the site. If your host supports it, you can choose FTP or the Web Deploy option, in which case your changes live immediately. However, for this exercise, you'll see how to create a local copy of the site, which you'll use in a later exercise that show how to install and configure IIS.

- 1. Open all files in Visual Studio and then Build -> Rebuild Web Site from the main menu. Doing so forces Visual Studio to recompile the entire site even if it already compiled some parts of it. Visual Studio lists any problems your site may have in the Error List. To verify that your error is free, open the Error List (choose View -> Error List from the menu) and make sure you don't have any compilation errors. Fix any errors you may have in your site.

- 2. When the Error List is empty, right-click the site in the Solution Explorer and choose Publish Web Site. Make sure you right-click the site and not its parent solution. The Publish Web dialog appears, as shown in Figure 19-3.

![](img/9e033e3b9560597824f8b22941d6d8bb_766_0.png)
FIGURE 19-3

- 3. Open the drop-down at the top of the screen and create New Profile. Enter a name such as To local disk and click OK.

- 4. On the Connection tab choose File System. In the text box for Target Location, enter C:\BegASPN\Release. This folder does not have exist yet; Visual Studio will create it for you when publishing the site. Click Next.

Note: If your host supports Web Deploy, you can choose that instead and enter the details, as the server name and your user credentials. The remaining steps in this exercise you selected File System.

- 5. In the Settings tab, Debug should be selected, which is what you need for this exercise. Click Next again.

- 6. On the Preview tab, click Publish to start the publishing process. After a short delay you should see a message in the Output window that the publishing process has completed successfully. If you had selected Web Deploy as the publish option, this dialog would have enabled you to review a preview of the changes by checking the files on the server or with local files.

- 7. On the Solution Explorer, click the Refresh icon and then expand the App_Data folder.

- 8. Open the folder C:\BegASPN\Release in Explorer. You should see a file called To local disk.pubxml in the folder. Now look at Web.config is identical to the one.

## How It Works

The File System option simply creates a copy of the site that make up your web application. You'll see on the production server that the Web Deploy and FTP options enable you deploy to the machine. In this exercise, Web.config is different from the development environment. When you select Precompiled in the Advanced Settings of Publishing, Visual Studio compiles all VB.NET and C# code into assemblies and places them in the bin folder. It leaves the markup and ASCX files alone. However, with this option turned on, the markup has been replaced with placeholder text: "This is a marker generated by the precomp process, and should not be deleted". When the page is requested by a browser, the ASP.NET run finds the appropriate content of the assemblies and serves it as if it were a normal page. This is especially great if you want to prevent other people with access to your server from altering your site after it has been deployed. Because the source and markup is compiled into .dll files, there is no way to change it on the server without uploading a new set of published files.

When you complete the Wizard, Visual Studio stores the settings in a Profile file (with .pubprofile extension) in the Profiles folder under App_Data. This file is then used whenever you publish to the site, so you don't have to enter all the details again. Visual Studio uses the profile also to maintain multiple versions of your Web.config file, as you will see next.

## Introducing Web.config Transformations

If you take a look at the current Web.config file you've been working with so far, you're likely to have a few settings that will be different on your production server. For example, your connection string will be different from the production server, and so are the settings for the mail server and maybe even the e-mail addresses you added earlier in this chapter. After overwriting the changes in the production server, developers often skip deploying the Web.config to the production server, and then manually update the settings in that file. However, this is far from ideal because you're likely to forget to add settings to the production server that you have added in. To overcome this problem, Microsoft has introduced Web.config Transformations, a mechanism to generate a Web.config file from the main Web.config in your project, but adjusted with settings that are specific for the production server (or other environments, such as a test server).
