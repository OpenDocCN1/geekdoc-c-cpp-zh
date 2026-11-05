
The .NET Compact Framework types enable to accomplish a range of common programming tasks, including tasks such as interface design, leveraging XML, database access, thread management and file I/O.

## Some Key Class Libraries are,

- 1. Windows Forms - For developing windows client application.
- 2. Base Classes - Enables advanced features such as Threading, Network resources etc.
- 3. GDI - Basic support for GDI for building graphics.
- 4. Data and XML - Enables easy handling of Data and XML content.
- 5. Web Service - To enable development of web service clients.

![](img/3005a4307e6d8f3bb7e76eea28a92357_885_0.png)

Fig. 28.1.2 .NET Compact Framework class libraries

- The Compact Framework supports a subset of the core types supported in the desktop Framework. These are often referred to as the Common Type System (CTS) types because they are the foundational types. It should be noted that in each case, some of the overloaded methods and properties found in the desktop Framework are not supported in the Compact Framework.
- Compact Framework has dropped out certain namespaces but for some new functionality below mentioned namespaces have been added to the framework.

| Additional Compact Framework Namespaces |
|---|---|
| **Namespace** | **Use** |
| Microsoft.WindowsCE.Forms | Contains the **InputPanel**, **MessageWindow**, and **Message** classes. The **InputPanel** class is used to control the soft input panel (SIP) on a Pocket PC, the primary means of entering data. The **MessageWindow** and **Message** classes are used primarily to communicate with unmanaged (or managed) applications using standard Windows messaging. |
| System.Data.SqlServerCE | Contains approximately 30 classes used to communicate with SQL Server CE if installed on the device. |

## 28.1.4 .NET Compact Framework - Common Functionality

### 1. Form-related Classes

- The .NET Compact Framework implements a subset of the System.Windows.Forms and System.Drawing classes, which allows to construct rich Windows CE-based user interface for device applications. The Form Designer in Visual Studio.NET manages much of the interaction with these classes on behalf of the application.
- The implementation of Windows Forms under the .NET Compact Framework includes support for forms, most controls found in the .NET Framework, hosting third-party controls, bitmaps and menus. Below table lists the controls included with the .NET Compact Framework.

| Control | Description |
|---|---|
| Button | simple command button |
| CheckBox | common checkbox |
| ComboBox | dropdown list of items |
| ContextMenu | implements a context sensitive menu |
| DataGrid | grid that can be bound to a data source |
| DomainUpDown | list of items that can be navigated via a scroll bar |
| HScrollBar | horizontal scroll bar |
| ImageList | container that stores images |
| InputPanel | controls the Soft Input Panel, or SIP |
| Label | simple control for displaying text |
| ListBox | provides a list of items |
| ListView | provides four views of data: large icon, small icon, list and details |
| MainMenu | implements a menu on a form |
| NumericUpDown | numeric input field that includes a scroll bar |
| OpenFileDialog | provides access to the native open file dialog |
| Panel | container used to hold other controls |
| PictureBox | displays images |
| ProgressBar | visual indicator of a task's progress |
| RadioButton | common radio button |
| SaveFileDialog | provides access to the native save file dialog |
| StatusBar | simple panel for displaying text |
| TabControl | provides a tab interface for an application |
| TextBox | standard text input field |
| Timer | basic timer component |
| ToolBar | implements a toolbar on a form |
| TrackBar | slider interface used with numeric data |
| TreeView | presents data in a hierarchical format |
| VScrollBar | vertical scroll bar |

**Table 28.1.1 Controls included with the .NET Compact Framework**

- Since the .NET Compact Framework is a subset of the full .NET Framework, the included controls have a subset of .NET framework functionality. Due to size and performance considerations, some control properties, methods and events have been omitted from .NET Compact Framework controls. With a little coding, one can implement these omitted features as needed. This is because the .NET Compact Framework allows to create own controls by inheritance from the base control class.

From this foundation, one can add own properties, methods and events to create the control as required.

### 2. Data and XML Classes

- The .NET Compact Framework includes a set of classes that allow to easily incorporate data (whether from a relational or non-relational data source), including XML content, into mobile applications. These classes are defined under the System.Data and System.Xml namespaces. The implementation of both data and XML classes in the .NET Compact Framework is a subset of that found in the .NET Framework.

### 3. Web Services

- The .NET Framework is much about Web services. In the .NET Compact Framework System.Web namespace, has a scaled-down version of the capabilities and functionality offered in the corresponding .NET Framework namespace. Most significantly, one can create Web services clients but are not able to host Web services under the .NET Compact Framework.
- These XML Web service clients can be either synchronous or asynchronous. Creating an XML Web service client that targets the .NET Compact Framework is easy. The Visual Studio .NET IDE does much of the work for developer.

### 4. GDI Support

- The .NET Compact Framework provides support for the basic GDI drawing elements including bitmaps, brushes, fonts, icons and pens through the System.Drawing namespace.

### 5. Base classes

- The .NET Compact Framework provides a robust set of base classes that expose a wide-range of functionality for use by developers. This underlying infrastructure enables to write rich .NET applications including being able to create multi-threaded applications (System.Threading), leveraging networking resources (System.Net), and working with files (System.IO).

### 6. IrDA (Infra-Red Data Association) Support

- Windows CE devices, such as the Pocket PC and Pocket PC 2002, include infrared (IR) communication capabilities. In support of this, the .NET Compact Framework includes classes that allow to leverage IR communication from within the application. These classes are part of the System.Net.IrDA namespace. One can use IR to communicate with Pocket PCs, printers and other IR-enabled devices.

### 7. Bluetooth Support

- The .NET Compact Framework does not natively provide support for Bluetooth. One can access most third-party Pocket PC implementations of Bluetooth via either serial port communications or through a provider's API.

### 8. Visual Basic Support

- Visual Basic .NET makes liberal use of helper functions that are located in a Visual Basic Helper library. The .NET Compact Framework includes a subset of these functions as well. These functions are considered by Visual Basic developers to be a core part of the language, which is the reason for their inclusion.

## 28.1.5 .NET Compact Framework - On Demand Features

- To conserve resources on the target device, Microsoft divided the .NET Compact Framework into logical components. By delivering components as separate DLLs-or assemblies as they are referred to within the .NET Compact Framework-Microsoft has provided the option of picking and choosing the features as per developer needs, and only those features that the target device has the space to hold.
- An example of this is the System.SR assembly, which contains error message strings. Including this assembly with the application allows access to detailed descriptions of any errors encountered, which is certainly helpful during a debugging session, but not frequently needed in an application once it is released to production. Excluding this assembly does not affect the performance or functionality of the application; it simply means that there will not be access to detailed error messages.
- Another example of the .NET Compact Framework ala carte approach is SQL Server CE components, delivered in a set of DLLs having size just over 1MB. Unless the reference is added explicitly to the System.Data.SqlServerCe assemblies, these DLLs will not be included with the application.

## 28.1.6 .NET Compact Framework - Unsupported Features

- As mentioned earlier, the .NET Compact Framework is a subset of the full .NET Framework and major sections were ignored because they implemented features that were specific to the PC platform, which did not make sense in the device world. Some serious trimming had to be made to the .NET Framework so that it could fit into the operating constraints of Windows CE.
- The following is a brief summary of the features that are excluded from the .NET Compact Framework.
