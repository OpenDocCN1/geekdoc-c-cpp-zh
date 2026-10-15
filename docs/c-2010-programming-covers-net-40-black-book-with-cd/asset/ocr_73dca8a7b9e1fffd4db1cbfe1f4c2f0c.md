| Table 10.56: Classes of the System.Windows.Forms.Integration Namespace |
| Class | Description |
| IntegrationExceptionEventArgs | Provides a base class for the EventArgs class that supports the optionally-raised exceptions |
| LayoutExceptionEventArgs | Provides data for the LayoutError event |
| PropertyMap | Provides a way to translate property values between a Windows Forms control and a WPF control |
| PropertyMappingExceptionEventArgs | Provides data for the PropertyMappingError event |
| WindowsFormsHost | Allows you to host a Windows Forms control on a WPF page |

Among all these classes, the two most important classes that implement interoperation capabilities are WindowsFormsHost and ElementHost. You can use the WindowsFormsHost class while hosting a Windows Forms control on a WPF page.