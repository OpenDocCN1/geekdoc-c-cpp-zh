# 202 Oracle Developer Data Modeler for Database Design Mastery

# Using Dynamic Properties and User-Defined Properties

You can use dynamic properties to add your own functionality to Data Modeler. Dynamic properties are name-value pairs that can be created and used during scripting. One example is the Discover Foreign Keys utility described in Chapter 10 where Data Modeler creates a dynamic property named byFKDDiscoverer and attaches to all foreign keys created automatically during the Foreign Keys process. You can create new dynamic properties on the property screen of most of the elements in Data Modeler on the Dynamic Properties tab. On that tab you define a property and a value you want to create. On the same screen you can remove dynamic properties. You can also create dynamic properties using transformation scripts and attach them to objects. Figure 8-8 shows a transformation script that adds a dynamic property called Heli to all tables and sets it to the value of True. The last row in the script, table.setDirty(true);

![](bbox=[0.133, 0.458, 0.833, 0.863])

| Name | Object | Engine | Variable |
|---|---|---|---|n| 8 | TEMPLATE_USER_QUERY_HAVE | relational | Mozilla Rhino | model |
| 9 | Copy Comments to Comments in RDBMS | relational | Mozilla Rhino | model |
| 10 | Create index on | relational | Mozilla Rhino | model |
| 11 | Create subtitle from tables in result | relational | Mozilla Rhino | model |
| 12 | Template for Data Vault Hubs and Links | relational | Mozilla Rhino | model |
| 13 | Template for Data Vault Satellites | relational | Mozilla Rhino | model |
| 14 | CreateAttachDynamicToSortTable | relational | Mozilla Rhino | model |

```
tables = model.getTableSet().toArray();
for (var t = 0; t < tables.length; t++) {
  table = tables[t];
  table.setProperty("Heli", "True");
  table.setDirty(true);
}
```

FIGURE 8-8. Custom transformation script for adding a dynamic property for a table