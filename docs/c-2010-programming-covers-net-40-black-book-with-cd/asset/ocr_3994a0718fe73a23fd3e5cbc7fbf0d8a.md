| Table 16.36: Noteworthy Properties of the ConnectionsZone Class |
| Property | Description |
| NewConnectionErrorMessage | Gets or sets a message string that is displayed in a connection UI when an error occurs while creating a new connection. |
| NoExistingConnectionInstructionText | Gets or sets the text contained in the body of a connection UI when there is no existing connection associated with a WebPart control. |
| NoExistingConnectionTitle | Gets or sets the title text of a connection UI when there is no existing connection associated with a WebPart control. |
| ProvidersInstructionText | Gets or sets the instructional text contained in the providers section of a connection UI, when a connection already exists. |
| ProvidersTitle | Gets or sets the title text above in the providers section of a connection UI, when a connection already exists. |
| SendText | Gets or sets the text present before the name of provider in the connection UI. This provider sends data to consumer. |
| SendToText | Gets or sets the text present in the connection UI before the name of the consumer to which a provider sends data. |

# NOTE

> All Web Parts controls reside inside the <form> element of a Default.aspx page. However, there are some Web Parts Controls that cannot be used alone and require some specific control to work with. For example, the LayoutEditorPart or BehaviorEditorPart control cannot be used without the EditorZone control in the <form> element.

Now that you have good grasp on Login and Web Parts controls, let’s move on to the next section, Immediate Solutions, for learning how to use the login and Web Parts in your ASP.NET 4.0 applications,.