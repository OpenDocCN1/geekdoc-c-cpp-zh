After the `Page_Load` method adds data points using the `DataBindCrossTable` method, it sets up
Ajax event handling with the following steps:

+   1. Subscribes to the `Chart1_Click` event handler method.
2. Sets the postback values of each series sending the series name and index.
3. Sets the Chart's `onClick` event to a postback using the `_getCoord` JavaScript function in its arguments.

+   4. Injects the `_getCoord` JavaScript function into the scripts of the page.

As a result of this setup

If a data point was clicked, `PostBackMessage` contains the series name and the data point
number. If the other chart element was clicked, `PostBackMessage` handles its coordinates.
In this case, the `HitTest` method tells which chart element was hit.

At the end, the chart is updated at the server side and the chart control encapsulated
within the `UpdatePanel` is set back asynchronously. At the browser, the image representing
the chart is updated, while the rest of the page (that is, the rest of the HTML document)
remains.

> When you run the sample, open the source code of the page. You can see the
chart's onClick event (in the <img> tag representing the chart), the _getCoord
function, and the _doPostBack calls of <area> tags with the appropriate
postback values.

# Triggering Chart Events

By default, any postback control inside an `UpdatePanel` causes an asynchronous postback
and refreshes the panel. However, you can also configure other controls on the page to
refresh an `UpdatePanel` control.

control is raised) This mechanism is very useful for charts. Clicking a data point or a label in a `Chart` control
can triggering other parts of the page — for example, it can refresh a table telling you
out the data point you clicked.

The `AjaxTriggerSample` page in the `PetShopCharts` project utilizes this mechanism to display two
related charts. The first stacked column chart shows details about 2009's sales statistics, where
data is organized into regions. When you click any of the data points in this chart, the
second chart is updated asynchronously by a trigger to show detail drill-downs. Figure 16-16
shows these charts in action.