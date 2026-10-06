# Chapter 5: Introducing Logical Database Design (Relational Model) 133

using TEMP_ for temporary objects or IDX_for tablespaces that have only indexes in them. The prefix can be permanent or temporary for DDL generation.

You can add the prefix to the object name manually when creating the object or changing its properties. For example, instead of naming ADDRESS, you can use CUST_ADDRESS. You can also do it automatically using the utility Data Modeler. You can do it for tables, views, foreign key constraints, primary and unique key constraints, and indices that are in a relational model or in a specific suburb. In the Browser pane, go to the relational model wanted, right-click, and choose Change Object Names Prefix. You might have your objects divided into subviews exactly based on the criteria you are using for the prefix naming. In that case, select the subview from the Browser pane, right-click, and choose Change Object Names Prefix. Or you might have the classification type attached to the object, which allows you to change the prefix for all of that classification type, as described in Chapter 8. Depending on your needs, any of these can be used, and they all lead to the Change Object Names Prefix dialog, as shown in Figure 5-30.

In the Change Object Names Prefix dialog, you can select Prefix Replacement or Add Classification Prefix. Add Classification Prefix is explained in Chapter 8. Now you will see what you can do with Prefix Replacement. If you select Prefix Replacement, you can replace an existing prefix or add a new one. If you want to replace an existing prefix, just set the current prefix to Current Prefix and the new prefix to New Prefix. You can spell the prefix either with the _ or sign

![](bbox=[0.297, 0.574, 0.703, 0.819])

FIGURE 5-30. Change Object Names Prefix dialog