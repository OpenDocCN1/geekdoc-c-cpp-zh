Table 14-12 describes several events for the Chart class to handle user actions related to annotations.

# **TABLE 14-12:** Class Events Handling Annotations

| EVENT | DESCRIPTION |
| --- | --- |
| AnnotationPlaced | Occurs when the end-user places an annotation on the chart. |
| AnnotationPositionChanged | Occurs when the annotation position is changed. |
| AnnotationPositionChanging | Occurs when the annotation position is about to change. This event uses the AnnotationPositionChangingEventArgs argument that allows checking the new position before the change is committed. |
| AnnotationSelectionChanged | Occurs when a selection of the annotation is changed. |
| AnnotationTextChanged | Occurs when the annotation text is changed. |

All events except AnnotationPositionChanging EventArgs arguments. The sender object passed to the event handler holds a reference to the affected annotation instance.

# # Binding Data to Series

Earlier in this chapter, you saw examples (Listing 14-2 and Listing 14-3) that used the chart’s DataSource property to bind data from a LINQ expression. The DataSource property accepts many types of data for binding, including the following:

+   * DataView
* Data Readers (SQL, OleDB).
* DataSet
* Arrays
* Lists
* SqlCommand/OleDbCommand
* SqlDataAdapter/OleDbDataAdapter
* All IEnumerable objects

You can bind data to a series by using the XValueMember and YValueMember properties. Data binding can also be used to bind information coming from the data source to other properties of a Chart instance. Go to the Data property category of the chart and expand the (DataBinding) property to see what chart properties can be bound to a data source.