This section looked at the different list events used for list screens. In the next section, we'll look at two different kinds of lists.

# 13.5 Basic Lists and Detail Lists

When the list screen is displayed, the list processor has control over the program. The initial list screen is called the *basic list*, and the user actions on the basic list can create additional lists if any output statements are executed. These additional lists are called *detail lists* (or *secondary lists*).

One basic list can have up to nineteen detail lists. For example, if we use a `WRITE` statement under the `AT LINE-SELECTION` event, it creates a detail list when the user double-clicks the displayed list. When a detail list is created, it temporarily replaces the previous list on the container screen. The basic list and detail lists form a *list system*, which can have up to twenty levels. This list system allows you to create drilldown reports in which header data is shown on the basic list and the user can click the displayed header record to see the item data of the record.

Drilldown reports are also useful to divide program output into multiple levels and allow the user to navigate between different levels. For example, if we print salary details of all employees in the report output, the user can click on the employee ID to see more information about a particular employee. After checking the employee details, the user can click the `BACK` button to return to the main list. This allows us to break the report output into multiple levels without having to display all the information in one screen.

The code in *Listing 13.8* shows the basic information about the flights from table `SFLIGHT` on a basic list. When the user double-clicks a record in the basic list, a secondary list is generated that shows the flight schedule from table `SPFLI`.

```
REPORT zdemo_classical_lists NO STANDARD PAGE HEADING.

TYPES: BEGIN OF ty_sflight,
         carrid TYPE s_carr_id,
         connid TYPE s_conn_id,
         fldate TYPE s_date,
       END OF ty_sflight.

DATA : it_sflight TYPE STANDARD TABLE OF ty_sflight,
       wa_sflight TYPE ty_sflight.
PARAMETERS p_carrid TYPE SPFLI-carrid.
```