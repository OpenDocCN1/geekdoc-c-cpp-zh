# Table 16.17: Noteworthy Methods of the WebPartManager Class

| Method | Description |
|---|---|
| OnAuthorizeWebPart | Invokes the AuthorizeWebPart event and its handler. |
| OnBubbleEvent | Determines whether the event for a server control is passed up the user interface (UI) server control hierarchy of a Web page. |
| OnConnectionsActivated | Invokes the ConnectionActivated event to specify whether a Web page and its controls are loaded in the browser. It also indicates whether the connections on the Web page are activated to share data. |
| OnConnectionsActivating | Invokes the ConnectionActivating event to indicate that a Web page and its controls are loaded in the browser and the process of activating connections on the Web page can begin. |
| OnDataBinding | Invokes the DataBinding event. |
| OnDisplayModeChanged | Invokes the DisplayModeChanged event to specify that the process of changing the display mode on a Web page has been finished by the WebPartManager control. |
| OnDisplayModeChanging | Invokes the DisplayModeChanging event to specify that the WebPartManager control is in the process of changing the display mode on a Web page. |
| OnInit | Invokes the Init event. This is the first event in the lifecycle of the WebPartManager control. |
| OnLoad | Invokes the Load event. |
| OnPreRender | Generates the PreRender event before a WebPartManager control is rendered on a Web page. This method notifies the WebPartManager control to perform any necessary pre-rendering steps prior to saving view-state and rendering content. |
| OnSelectedWebPartChanged | Generates the SelectedWebPartChanged event after a Web Parts control is selected or its selection cleared. |
| OnSelectedWebPartChanging | Generates the SelectedWebPartChanging event while changing a selected WebPart control. |
| OnUnload | Generates the base Unload event to remove a WebPartManager instance from a Web page. |
| OnWebPartAdded | Generates the WebPartAdded event after a Web Parts control is added to a Web page. |
| OnWebPartAdding | Generates the WebPartAdding event when a Web Parts control is adding to a WebPartZoneBase zone. |
| OnWebPartClosed | Generates the WebPartClosed event to indicate the removal of a Web Parts control from a Web page. |
| OnWebPartClosing | Generates the WebPartClosing event when a Web Parts or server control is removing from a Web page. |
| OnWebPartDeleted | Generates the WebPartDeleted event after a Web Parts control is permanently deleted from a Web page. |
| OnWebPartDeleting | Raises the WebPartDeleting event, which indicates that a dynamic WebPart control (or server or user control that is contained in a WebPartZoneBase zone) is in the process of being deleted. |
| OnWebPartMoved | Generates the WebPartMoved event after a Web Parts control is moved to another location on a Web page. |