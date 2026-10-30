Save the project and solution, keeping the solution files in a separate directory.

![](bbox=[0.05, 0.21, 0.88, 0.44])

> Note: In the past we have unchecked the Create directory for solution box, but when creating solutions with multiple projects, the option can be a big help. In the solution folder, you will have only the .sln and .suo files and one folder for each project.

# Add a WCF Service

+   STEP 1: Select the solution name (Ch06WcfHelloWorld) in the Solution Explorer and select Add / New Web Site from the File menu or right-click on the Solution name in Solution Explorer.
+   STEP 2: Select the WCF Service template.
+   STEP 3: Click OK, keeping the default name of "WCFService1".

# Rename the WCF Service

+   STEP 1: In the Solution Explorer, rename the Service.vb file to "HelloWorldService.vb".
+   To complete renaming the service, you must change the name in several more locations, as described in the following steps.
+   STEP 2: Open the HelloWorldService.vb file and change the name of the service's class to HelloWorldService.

```
Public Class HelloWorldService
```

+   STEP 3: Open the Service.svc file and change the service attribute to:

```
service="HelloWorldService"
```

+   STEP 4: Open the Web.config file and scroll down to near the bottom and find the <system.serviceModel> tag. Under <services> change to:

```
<service name="HelloWorldService" behaviorConfiguration="ServiceBehavior">
```

+   STEP 5: In the Solution Explorer, rename the IService.vb file to IHelloWorldService.vb
+   STEP 6: Open the IHelloWorldService.vb file and change the name to IHelloWorldService:

```
Public Interface IHelloWorldService
```