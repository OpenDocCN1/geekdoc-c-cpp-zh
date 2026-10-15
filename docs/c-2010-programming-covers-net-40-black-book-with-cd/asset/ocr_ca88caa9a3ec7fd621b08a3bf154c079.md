The FlowDocumentPageViewer control can be added to a WPF application, as shown in the following code snippet:

```
<FlowDocumentPageViewer>
<!--Document-->
</FlowDocumentPageViewer>
```

The properties of FlowDocumentPageViewer control are listed in Table 11.15:

# Table 11.15: Properties of the FlowDocumentPageViewer Control

| Property | Description |
|---|---|
| CanDecreaseZoom | Retrieves a value that indicates whether the zoom level can be decreased or not |
| CanIncreaseZoom | Retrieves a value that indicates whether the zoom level can be increased or not |
| CanGoToNextPage | Retrieves a value that indicates whether you can navigate to the next page of the current document |
| CanGoToPreviousPage | Retrieves a value that indicates whether you can navigate to the previous page of the current document |
| Document | Gets or sets a IDocumentPaginatorSource object to be paginated and displayed by a viewer |
| MasterPageNumber | Retrieves the page number of the current master page |
| MaxZoom | Gets or sets the maximum allowable zoom level for FlowDocumentPageViewer |
| MinZoom | Gets or sets the minimum allowable zoom level for FlowDocumentPageViewer |
| Selection | Retrieves the selected content of FlowDocumentPageViewer |
| Zoom | Gets or sets the current zoom level for FlowDocumentPageViewer |
| ZoomIncrement | Gets or sets the zoom increment |

# The FlowDocumentReader Control

The FlowDocumentReader control combines the features of the FlowDocumentScrollViewer and FlowDocumentPageViewer controls. It lets you select whether to read content in a scrollable mode or page viewing mode. When you display the content using the FlowDocumentReader control, the page is divided into two parts: the content area and the toolbar. The content area displays the content of FlowDocument specified by the Document property. The toolbar is divided into the following parts:

+   - Find button — Enables you to search the content of a document. The Find button is not shown if the IsFindEnabled property is set to False.
+   - Page Navigation controls — Includes a button to move to the next page or the previous page. It also has indicators for the current page number and the total number of pages.
+   - Viewing mode buttons — Contains three viewing modes: Page Mode, Two Page Mode, or the Scroll Mode. Any one of the modes can be selected according to requirements and preferences.
+   - Zoom control — Enables you to increase or decrease the zoom level by clicking the plus or the minus button. It also includes a slider fro adjusting the zoom level.

> NOTE
> The default toolbar of the FlowDocumentReader control does not include a Print button.

The inheritance hierarchy of the FlowDocumentReader control is as follows:

```
System.Object
  System.Windows.Threading.DispatcherObject
    System.Windows.DependencyObject
      System.Windows.Media.Visual
        System.Windows.UIElement
          System.Windows.FrameworkElement
```