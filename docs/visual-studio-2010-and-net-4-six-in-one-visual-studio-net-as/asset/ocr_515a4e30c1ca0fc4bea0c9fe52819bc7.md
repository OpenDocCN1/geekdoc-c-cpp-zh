The fourth data point adds a label to the data point. The Label property can use the same tokens as used for the AxisLabel property.

# # ADVANCED CHART MANIPULATION

By now, you've learned to create great charts with the new Chart control, and you are familiar with chart elements and most customization options. The Chart control has many properties you can use to change its visual properties and behavior, and they are generally very simple to use. The Chart's design is a great tool for you to understand the meaning and effects of these properties to specific values, because changes are immediately reflected in the design surface. You can also write simple and straightforward programs to set these properties from code.

For most cases, when you intend to use the Chart control, what you've learned is enough to encapsulate spectacular charts into your applications. However, there are some advanced features of the Chart control, so let's look at all of them.

# # Annotations

The great advantage of charts over the use of tables is that they could provide a better representation of data — especially when you deal with dozens or hundreds of numbers — and they can catch your eye in a moment, unlike tables. A few words, arrows, or other decorations can be invaluable for you focus on the essential data visualization by the chart.

Chart annotations allow you to create these small decorations. The Chart control has a collection property named Annotations, and you can add an unlimited number of Annotation instances to it.

# # Annotation Types

There are several annotation types shipped with the Chart control. They form a type hierarchy with Annotation class as a root. Table 14-9 summarizes these classes, and describe their most essential properties.

# TABLE 14-9: Annotation Types

| ANNOTATION TYPE | DESCRIPTION |
|---|---|n| Annotation | This abstract class defines properties and methods common to all annotations. By default, annotations are positioned using relative coordinates, with (0, 0) representing the top-left corner, and (100, 100) representing the bottom-right corner of the chart image. It is also possible to switch from this relative coordinate system to a system that uses axis values. With an axis coordinate system, X and Y (which represent the position of the top-left corner of an annotation) are set using X axis and Y axis values, instead of values that range from 0 to 100 |