Whether the Web role works using HTTP, HTTPS, or a combination of the two — If your application receives any secure information from the user, you should use HTTPS. Otherwise, HTTP should be good enough for most uses.

In addition, you configure the endpoints using the Endpoints tab of the configuration (see Figure E-15). This tab enables you to define the ports used by the Web role, as well as the certificate to use for HTTPS.

![](bbox=[0.09, 0.199, 0.425, 0.418])

![](bbox=[0.455, 0.191, 0.865, 0.416])

You use the Settings tab to define any additional settings for your project, just as you do for other projects. However, while you’re working in the development environment, it is a good idea to set the application to use the connection strings appropriate to the development environment, rather than attempt to access the services deployed to the cloud. Click the Add Setting button, and name the new setting DataConnectionString, and the type ConnectionString. Click the ellipses on the value property to display the Storage Connection String dialog (see Figure E-16).

![](bbox=[0.472, 0.458, 0.88, 0.663])

For now, select the first option, “Use development storage.” As you can probably guess, when it comes time to deploy this application to the cloud, you will need to enter your credentials in order to access the services. Once you have saved the setting, the Settings tab should look like Figure E-17.

![](bbox=[0.09, 0.749, 0.708, 0.915])