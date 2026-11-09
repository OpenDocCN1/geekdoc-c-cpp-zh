
- 3. Right-click the Packages Installed branch, point to New on the shortcut menu, and then click Package. The Package Wizard dialog box appears.
- 4. Click the Create An Empty Package button. (You will learn how the Install Pre-Built Packages button is used in the "Importing a Package" section later in this chapter.)
- 5. Type a name for the new package (the name can include spaces). Click Next.
- 6. Set the package identity. You can change the identity later in the Package. During development, you want to use the Interactive User. This setting uses the credentials of the logged on user. A side effect of using the Interactive User is that all output appears in the current WinStation. A problem with this setting is that it requires someone to be logged on for the package to execute.
- 7. In a production environment, you should select the This User option. When you select This User, you can type in a particular user's credentials, which will be implemented when the server needs to access shared resources such as files. Be aware that you should never display output with this setting. The output will not appear in the current WinStation. For example, if you attempt to display a message box, the message would not be visible and your program will appear frozen as it waits for user interaction.
- 8. Click Finish.

## Adding Objects to a Package

Although you can add objects to a package using a variety of mechanisms, you can most easily accomplish this by using a drag-and-drop operation to move the DLL that contains the classes into the Components folder underneath your package.

To add objects to a package using drag-and-drop, do the following:

- 1. Make sure that the Components folder is selected.
- 2. In Windows Explorer, drag the DLL file into the right pane of the MTS Explorer window. MTS will add all the objects described in the type library.

You can also add objects to a package without drag-and-drop.

To add classes to the package without a drag-and-drop operation, do the following:

- 1. Expand the package branch where you want to insert components. Right-click the Components folder, point to New on the shortcut menu, and then select Component.
- 2. Click Install New Component(s) if you want to add every component in a certain DLL. This option is similar to using the drag-and-drop operation and does not require that the DLL be preregistered.
- 3. If you want to select a component by its ProgID from the list of registered components, click **Import Component(s) That Are Already Registered**. This procedure is the only way to add individual components from a DLL. Use this method if you want to add some components to one package and some components to another package.

When creating packages, make sure to add any type libraries on which your objects depend, as well as your proxy-stub DLL if you need one. This will come in handy when deploying your package on another computer.

## Package Properties

A package has many properties of which you need to be aware. You can right-click a package and select Properties from the shortcut menu to view the Package Properties dialog box.

On the General tab, notice that you can type a description for a package. This is useful when importing a package in another computer. The Security tab contains a check box for enabling security for a package. Notice that the default is No Security. This tab also contains the authentication level for calls made between a client and a package.

The Advanced tab provides a setting called Server Process Shutdown, which is used to determine when to shut down the server process. This is an optimization in MTS that you can use after all references to your objects have been released. After the server has deleted all instances of objects in a package, the server will remain loaded for the amount of time specified in the Server Process Shutdown setting. This improves performance for clients initiating a conversation with the server within the specified amount of time.

> **Note**
> 
> During development, you should set the Server Process Shutdown setting as low as possible because you will be unable to rebuild your code when the server is running and the server DLL is loaded.

The Advanced tab also has two permission settings: Disable Deletion and Disable Changes. By enabling these settings, you are locking the package from users of MTS Explorer. If you make the Disable Changes option available, users will not be able to modify this package. All the options in the property dialog box, except for the permission settings, will be made unavailable. To make modifications later, you must unlock the package; clearing the permission options unlocks the package.

The Identity tab allows you to choose the Security Identifier (SID) that MTS will use when accessing shared resources, such as files on the network. This is the user ID and password that your server will impersonate when making outbound calls. For example, your code might access files on another computer.

You might use a specific user ID and password to access that other computer, or you might use the interactive user—the user currently logged on. However, your server might not have anyone logged on, which will render your server unusable; or the logged-on user might not have security to access the shared resource.

Therefore, in a production environment, you should use a specific user with enough security to reach shared resources. Probably the most important property you can set for a package is the activation type, found on the Activation tab. The choices are Library Package or Server Package. A library package is simply a package to be used in-process. A server package is one that will be loaded into the MTS surrogate process Mtx.exe. A library package has a few limitations over a server package; the most notable is that library packages do not control security. The process that is loading them determines their security.

## Object Properties

Objects also have a series of declarative properties. Perhaps the most important of these properties is transaction support.

MTS is in charge of initiating a transaction and calling on the services of MS DTC to enlist resource managers and control the flow of the transaction. Components dictate when MTS starts a transaction through declarative settings. An administrator can change the transaction requirements of a component by changing the Transaction properties of the component.

To do so, right-click the component you want to modify and select Properties on the shortcut menu. Next, click the Transactions tab. On the Transactions tab, you can choose from four options: Requires a Transaction, Requires a New Transaction, Supports Transactions, and Does Not Support Transactions.

MTS starts a transaction when an object marked as Requires a New Transaction or Requires a Transaction is created and activated (after the first method call).

The object that makes MTS begin the transaction is known as the root of the transactions.

Other objects can participate in the same transaction if they are created from within an object already in the transaction. For an object to participate in the same transaction, it must be part of the same activity. In other words, it must be created with the CreateInstance() function of the IContextObject interface. The component must also be marked as Requires a Transaction or Supports Transactions.

If the secondary component is marked as Requires a New Transaction, MTS will create a new transaction for the object; the object will not be able to participate in the transaction of the creator. Components marked as Does Not Support Transactions cannot participate in the same transaction.

As you can see, changing the Transaction property setting in a component can have a huge impact on how your application behaves. Just imagine what would happen if you had coded object B with the idea that it would be in the same transaction as object A, and an MTS administrator decided to mark object B as Requires a New Transaction. You cannot do much to prevent an administrator from doing this. However, you can set a default transaction setting for each of your components in the type library. To do so, first include the file Mtxattr.h in the top of your IDL file as follows:

```
#include <mtxattr.h>
```

This file declares certain attributes that you can use as coclass attributes. These attributes are TRANSACTION_REQUIRED, TRANSACTION_SUPPORTED, TRANSACTION_NOT_SUPPORTED, and TRANSACTION_REQUIRES_NEW. To use these attributes, simply add them to the coclass attributes as follows:

```
[
    uuid(01C72192-8CB0-11D3-81E1-00B0BAA1DBA9),
    helpstring("ctxobj1 Class"),
    TRANSACTION_REQUIRED
]
coclass ctxobj1
{
    [default] interface Ictxobj1;
};
```

These attributes do not prevent an administrator from changing the property; they only give MTS the default transaction setting for the component. That is, when the component is added to a package, the transaction setting will be set according to the default setting.

## Deploying MTS-Based Objects

MTS provides a mechanism for exporting a package definition along with its components and importing the package in another server. MTS also provides a way to generate a setup program that will install the necessary registry information to activate a server component in client computers that do not have MTS installed.
