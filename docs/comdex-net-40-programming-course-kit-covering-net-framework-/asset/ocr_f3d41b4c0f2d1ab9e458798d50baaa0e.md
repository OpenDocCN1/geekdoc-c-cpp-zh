Table 7.5 lists the noteworthy public properties of the CatalogZone class:

| **Table 7.5: Noteworthy Public Properties of the CatalogZone Class** | |
|---|---|
| **Property** | **Description** |
| `SelectedCatalogPartID` | Retrieves or initializes a string to identify the currently selected CatalogPart control in a zone |
| `SelectedPartLinkStyle` | Retrieves an object that contains style attributes for the currently selected CatalogPart control in a zone |
| `SelectTargetZoneText` | Retrieves or sets the text next to a server control in the catalog UI. This allows a user to select the zone for adding selected controls |
| `ShowCatalogIcons` | Retrieves or sets a value to indicate whether server controls in a CatalogZone control display their associated icons or not |
| `EmptyZoneText` | Shows the text when the zone is empty |
| `InstructionText` | Shows the instruction text in the zone |

Table 7.6 lists the noteworthy events of the CatalogZone class:

| **Table 7.6: Noteworthy Public Events of the CatalogZone Class** | |
|---|---|
| **Events** | **Description** |
| `DataBinding` | Invokes when the server control binds to a data source |
| `Disposed` | Invokes when the control has been disposed |

Table 7.7 lists the noteworthy methods of the CatalogZone class:

| **Table 7.7: Noteworthy Public Methods of the CatalogZone Class** | |
|---|---|
| **Events** | **Description** |
| `CatalogPartChrome` | Creates the CatalogPartChrome object used to render the UI elements of CatalogPart controls in a zone |
| `CatalogParts` | Create instances of all the controls that are declared in a CatalogZone control |

To use a CatalogZone control in a Web application, you must include CatalogPart controls in it. CatalogPart controls are controls that provide catalogs of controls that a user can add to or remove from a Web page. The following are the three types of CatalogPart controls:

+   - **DeclarativeCatalogPart**: Allows users to modify the functionality of a Web page by displaying a list of WebParts controls from which they can add controls to the Web page. The `DeclarativeCatalogPart` control is an object of the `DeclarativeCatalogPart` class. It is available in the WebParts tab of the Toolbox. You can add the `DeclarativeCatalogPart` control to a Web page by dragging the control from the Toolbox and dropping it inside the CatalogZone control in the Designer window of the Web page. Before adding a `DeclarativeCatalogPart` control to a Web page, you must ensure that the Web page contains a `CatalogZone` control, because the `DeclarativeCatalogPart` control can be added only to a specific control zone.
+   - **PageCatalogPart**: Provides a catalog for storing the references of all the closed WebParts controls on a Web page. This control enables users to close and reopen the closed WebParts controls back on the Web page. A control is said to be closed when:
+     - It is hidden on the Web page
+     - It is not rendered in the Web page
+     - It does not take part in the Web page life cycle