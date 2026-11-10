you change a field, through the field symbol, the field of the third row is changed immediately, because the field symbol points to the third row directly.

We don't have to copy the contents manually using the `MODIFY` statement as we did in Listing 16.2, because the `<wa>` field symbol in Listing 16.3 doesn't take a separate memory space but points to the existing memory, unlike the work area `wa` in Listing 16.2.

Once the data object is assigned to the field symbol, we can work with the field symbol just like the assigned data object and perform operations that can usually be performed on the assigned data object. Almost any data object can be assigned to a field symbol.

As you can see in Listing 16.3, there is a way to define field symbols, assign a data object to a field symbol, check if the field symbol is assigned before accessing the field symbol, and more. Before we discuss these aspects, however, let's look at how field symbols can help make programs dynamic.

# 16.1.1 Using Field Symbols to Make Programs Dynamic

For our example, we'll use a report to show some basic information about a material. In this report, we'll use the ALV object model to display the output. We'll provide functionality for the user to double-click in any cell to filter the records based on the value of the cell and show the result in a new container below the displayed output.

Most of the components of this report are static: We already know the data to be displayed in the output and the user input for the report. However, filtering the records based on user action is dynamic. Let's look at how we can achieve this in a static way and then look at how to make it dynamic.

Listing 16.4 shows the code for the report using the ALV object model. The code is long, but very straightforward. Take some time to go through the code and try it out in your system.

```
````abap
REPORT zdemo_salv_static.
CLASS lcl_event_handler DEFINITION DEFERRED.
DATA: custom_container TYPE REF TO cl_gui_custom_container,
      splitter         TYPE REF TO cl_gui_splitter_container,
      container_1      TYPE REF TO cl_gui_container,
      so_alv           TYPE REF TO cl_salv_table,
      mo_alv           TYPE REF TO cl_salv_table.
````
```