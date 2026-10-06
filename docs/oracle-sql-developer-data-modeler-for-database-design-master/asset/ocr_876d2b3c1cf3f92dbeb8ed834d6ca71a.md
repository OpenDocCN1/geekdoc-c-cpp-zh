# 192 Oracle SQL Developer Data Modeler for Database Design Mastery

```
// column even if the name of column is changed
var t_name = "table_template_Sat";nvar p_name = "ctemplateID";
template = model.getTableSet().getByName(t_name);
if(template==null) {
    tcolumns = template.getTableElements();
    tables = model.getTableSet().toArray();
    for (var t = 0; t<tables.length; t++) {
        table = tables[t];
        

// // compare name ignoring the case
        if(!table.getName().equalsIgnoreCase(t_name)) {
            if (table.getName().substring(0,3).equalsIgnoreCase("SAT")) {
                for (var i = 0; i < tcolumns.length; i++) {
                    column = tcolumns[i];
                    col = table.getElementByName(column.getName());
                    if(col==null) {
                        col = ;
                    }
                    table.getColumnProperty(p_name,column.getObjectID());
                    if(col==null) {
                        col = table.createColumn();
                    }
                    column.copy(col);
                }
            }
            // //set property after copy otherwise it'll be
            //cleared by copy
            col.setProperty(p_name,column.getObjectID());
            table.setDirty(true);
        }
    }
}
}
```

You can add these transformation scripts | Design Rules and Transformations | Transformations. Click the green plus sign, define a name for a script, and define the following: Set Object to Relational, Engine to Mozilla Rhino, and Variable to Model. Then write the code in the script editor. Save, and you are ready to run the script by clicking Apply. When writing transformation scripts, you can use dynamic properties to get a lot of possibilities for adjusting Data Modeler to your demands. I will talk more about dynamic properties later in this chapter.