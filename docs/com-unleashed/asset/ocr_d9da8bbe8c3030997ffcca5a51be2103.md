From the COM+ Application’s context menu, select the New, Application menu option. When the COM+ Application installation wizard begins, click the button. The next page you will see (see Figure 27.9) enables you to specify whether you are installing a prebuilt application or creating a new, empty COM+ Application. Because our COM+ Application doesn’t exist yet, select the latter.

# **FIGURE 27.9**  
You can add prebuilt COM+ Applications to your system as well as create new, empty applications.

![](bbox=[0.227, 0.234, 0.614, 0.454])

In the next dialog (see Figure 27.10), you need to specify the name of the application as well as the Activation Type.

# **FIGURE 27.10**  
Most COM+ Applications you create will be of the Activation Type, Server Application.

![](bbox=[0.227, 0.544, 0.614, 0.766])

Everyone has their own naming convention for creating COM+ applications. However, because our application will only contain the one component, we’ll simply use that name as the root of the application name in order to keep things easy. Therefore, name the application OCComVCApplcn. Then, select the Server Application option. Selecting the Library Application option would result in the component being activated in the client’s process (which is something we obviously don’t want for a queued component).