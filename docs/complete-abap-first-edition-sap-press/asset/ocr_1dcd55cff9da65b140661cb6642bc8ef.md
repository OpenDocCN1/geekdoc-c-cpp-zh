code is shown in [Listing 10.3](#). From this template, replace `sql_view_name` with the name of the view and `data_source_name` with the name of the database table.

![](bbox=[0.052, 0.18, 0.851, 0.364])

**Figure 10.48** CDS View Editor

```
```abap
@AbapCatalog.sqlViewName: 'sql_view_name'
@AbapCatalog.compiler.compareFilter: true
@AccessControl.authorizationCheck: #CHECK
@EndUserText.label: 'Test'
define view Zcds_Demo1 as select from data_source_name {
}
```
```

**Listing 10.3** CDS View Template

+   6. You can specify database table fields within the curly braces. For example, if you want to define the `ZDEMO_V1` view for database table VBRK and list certain fields from the table, the template can be edited as shown in [Figure 10.49](#).

![](bbox=[0.142, 0.641, 0.586, 0.783])

**Figure 10.49** Editing Template to List Certain Fields from Table

+   7. To list all the fields from the table, use `*` within the curly braces, as shown in [Figure 10.50](#).