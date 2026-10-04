+   12. Right-click the site in the Solution Explorer and choose Publish Web Site. Verify that the selected Publish Profile is To local disk and click Publish.

+   13. When Visual Studio is ready with publishing, open a File Explorer and navigate to C:\BegASNET\Release. Open the web.config in Notepad or Visual Studio and verify that the file contains a combination of the original web.config file and the configuration file associated with the Publish Profile.

# How It Works

When you request the preview, the transformation engine kicks in and generates the changes it finds in the transformation file (Web.To local disk .config). For the connectionStrings and appSettings elements it finds a Locator attribute that tells it to copy the element with a matching key (for appSettings) or name (for the connection string) and overwrite only those attributes that are defined in the transformation file. That is why the preview file still contains the providerName attribute, even though it wasn't in the transformation file. This is a convenient way to update attributes without fully refining the element.

The RemoveAttributes transform on the <compilation> element simply removes the debug attribute. .NET off debugging. If you want to remove multiple attributes from an element, simply define them as a comma-separated list between the parentheses around RemoveAttributes.

The <settings> element takes a different approach. Because the differences between the source and target files are quite large, it is more convenient to replace the entire element using xt:Transform="Replace". Notice that you still need to define the parent elements (<system.net> in this example) so the transformation engine knows where to add the element in the target file.

When you publish the website using the Publish Wizard, Visual Studio tries to find a configuration file named after the Publish Profile and then creates a custom configuration file on the fly. You can easily manage your main web.config file in Visual Studio along with the differences for the production environment. When it comes to deploying your site, you can be assured that the generated Web.config file contains all settings from the main file, with the settings that are to the specific production environment merged into the final file.

Now that you have a clean copy of your website, the next step is to move the files to your production server. If your host supports FTP, you can use FTP to copy the files to the remote server. If you want to host on a server you manage yourself, you will need to configure IIS, Microsoft's web server. Installing and configuring IIS is the topic of the next section.

# RUNNING YOUR SITE UNDER IIS

Up until now, you've been using IIS Express, which ships with Visual Studio, to debug and test your application. However, because requests to this server are limited to those coming from the local host to minimize security implications, you will need to use the full IIS, which comes with most major Windows versions. To have your website run under IIS, you need to perform the following steps: