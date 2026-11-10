In Listing 13.3, we created program ZPROGRAM2 where we use the GET PARAMETER ID statement to read the value from SAP memory using the same memory ID assigned in Listing 13.2.

Once the GET PARAMETER ID statement is executed, the value stored in the "MAT" memory ID will be transferred to the v_matnr field irrespective of whether the ZPROGRAM2 program is running in the same session as the ZPROGRAM1 program or in a different session.

```
REPORT ZPROGRAM2.
DATA v_matnr TYPE matnr.
START-OF-SELECTION.
GET PARAMETER ID 'MAT' FIELD v_matnr.
```

**Listing 13-3** Reading Value from SAP Memory

Now that you have an understanding of memory organization, let’s shift our attention to how list screens are processed by programs.

# 13.4  List Events

You’ve seen that executable programs, module pools, and function groups are the three types of programs that can contain screens. List screens are typically used with executable programs to generate report output.

List screens aren't created manually; they’re automatically generated using the WRITE, SKIP, or ULINE statement. In executable programs, the list screen is presented automatically at the end of program execution. In module pool programs, the LEAVE TO LIST-PROCESSING statement will present the generated list.

Unlike selection screens and general screens that consist of named screen elements (e.g., input fields, radio buttons, checkboxes, etc.) and data exchanged with ABAP programs with identically named fields, list screens provide a freely definable area to output data.

The runtime environment triggers list events when a list screen is processed. *List events* allow you to prepare a list and react to user actions on the screen.

The following are the different types of list events:

+   - TOP-OF-PAGE
+   - END-OF-PAGE