
### 15.2.2 Reacting to User Actions

When we provide additional function codes using a custom SAP GUI status, we need to handle the related functionality in the program. For example, if we add a PDF button to allow a user to download the output as a PDF, then we need to write code in the program to download the output as a PDF. This requires identifying the user action on the screen and writing the respective logic.

To achieve this, we need to pass the subroutine name to the I_CALLBACK_USER_COMMAND parameter. This subroutine should be maintained in the program with two formal parameters, one of type SY-UCOMM and another of type SLIS_SELFIELD, as shown:

```abap
FORM user_command USING r_ucomm LIKE sy-ucomm
                       rs_selfield TYPE slis_selfield.
ENDFORM.
```

When this subroutine is called from the ALV function module (refer back to Figure 15.8), it will pass these parameters to the calling program. Here, R_UCOMM will contain the function code, and RS_SELFIELD will contain information about the output table, the current row, the user selected, and so on.

Listing 15.9 shows sample code to identify if the user has selected the PDF icon we created previously. Multiple user actions can be evaluated within the subroutine using the CASE statement. The standard function code '&IC1' is passed to the R_UCOMM formal parameter if the user double-clicks the row. The RS_SELFIELD-FIELDNAME and RS_SELFIELD-VALUE fields will contain the column name in which the user double-clicked the displayed output and the value in the cell, respectively.

```abap
FORM user_command USING r_ucomm LIKE sy-ucomm
                       rs_selfield TYPE slis_selfield.

CASE r_ucomm.
  WHEN 'PDF'.
*write appropriate logic.
  WHEN '&IC1'.
*write appropriate logic.
ENDCASE.
ENDFORM.
```

**Listing 15.9** Identifying User Action

### 15.2.3 Printing TOP-OF-PAGE

To print the TOP-OF-PAGE information, we can pass the subroutine name to the `I_CALLBACK_TOP_OF_PAGE` parameter. Within this subroutine, the `REUSE_ALV_COMMENTARY_WRITE` function module is called to print TOP-OF-PAGE, as shown in Listing 15.10.

Refer to the function module documentation for the `REUSE_ALV_COMMENTARY_WRITE` function module to learn more about the parameter interface.

```abap
FORM top_of_page.
  DATA: lt_cw TYPE slis_t_listheader,
        lw_cw TYPE slis_listheader.
  lw_cw-typ = 'H'.
  lw_cw-info = 'Flight Information'.
  APPEND lw_cw TO lt_cw.

  lw_cw-typ = 'S'.
  lw_cw-key = 'P_CARRID'.
  lw_cw-info = 'Selection criteria'.
  APPEND lw_cw TO lt_cw.
  CALL FUNCTION 'REUSE_ALV_COMMENTARY_WRITE'
    EXPORTING
      i_t_list_commentary = lt_cw.
ENDFORM.
```

**Listing 15.10** Printing TOP-OF-PAGE

**ALV** function modules support various other events, such as `USER_COMMAND`, `TOP_OF_COVERPAGE`, `END_OF_COVERPAGE`, and so on, depending on the type of list generated. These events allow you to provide additional information to ALV when the report is running. The `REUSE_ALV_EVENTS_GET` function module can be used to get the supported events for the list, and the subroutine names can be passed for different events using the `IT_EVENTS` parameter.

## 15.3 ALV Reports Using the Control Framework

As discussed in Chapter 12, the Control Framework shows the grid display in a custom control. The `CL_GUI_ALV_GRID` control class is used to display the ALV output in a custom container. The `CL_GUI_ALV_GRID` class is the classic (old) variant used to work with the Control Framework. We recommend using the modern variant class, `CL_SALV_TABLE`, for new developments. We’ll provide more details about the `CL_SALV_TABLE` class in Section 15.4.

Similar to the picture control example from Chapter 12, working with the ALV grid control is pretty straightforward. In this section, you’ll learn how to use the ALV grid control via the `CL_GUI_ALV_GRID` control class.

To begin, we first need to define a screen for the program and create a custom container on the screen. In the PBO module of the screen, we instantiate the container object that is referenced to the `CL_GUI_CUSTOM_CONTAINER` class. The custom container name is passed to the constructor during instantiation.

Once the container object is instantiated, we instantiate the ALV grid object that’s referenced to the `CL_GUI_ALV_GRID` class. The parent container object is passed to the constructor of this class.

The `SET_TABLE_FOR_FIRST_DISPLAY` method of the `CL_GUI_ALV_GRID` class is called to pass the output data that should be displayed in the grid control. The parameter interface of this method is similar to the ALV function modules we discussed in the previous section.

Listing 15.11 shows the sample code to load the custom ALV grid control.

```abap
REPORT zdemo_alv_grid.
TABLES sflight.
DATA: it_sflight TYPE STANDARD TABLE OF sflight.
DATA: g_container TYPE REF TO cl_gui_custom_container,
      g_grid      TYPE REF TO cl_gui_alv_grid.

START-OF-SELECTION.
  CALL SCREEN 100.
*&---------------------------------------------------------------------*
*&      Module PBO OUTPUT
*&---------------------------------------------------------------------*
MODULE pbo OUTPUT.
  IF g_grid IS NOT BOUND.
    CREATE OBJECT g_container
      EXPORTING
        container_name = 'CUSTOM'.

    CREATE OBJECT g_grid
      EXPORTING
        i_parent = g_container.
  ENDIF.

ENDMODULE.
*&---------------------------------------------------------------------*
*&      Module PAI INPUT
*&---------------------------------------------------------------------*
MODULE pai INPUT.
  SELECT * FROM sflight INTO TABLE it_sflight WHERE carrid EQ sflight-carrid.

  CALL METHOD g_grid->set_table_for_first_display
    EXPORTING
      i_structure_name = 'SFLIGHT'
    CHANGING
      it_outtab        = it_sflight
    EXCEPTIONS
      invalid_parameter_combination = 1
      program_error                 = 2
      too_many_lines                = 3
      others                        = 4
      .
  IF sy-subrc <> 0.
* Implement suitable error handling here
  ENDIF.
ENDMODULE.
```

**Listing 15.11** Working with ALV Grid Custom Control

In Listing 15.11, we defined two reference objects, `G_CONTAINER` and `G_GRID`, referring to `CL_GUI_CUSTOM_CONTAINER` and `CL_GUI_ALV_GRID`, respectively. A screen with screen number 100 is defined for the program, with one input field, `SFLIGHT-CARRID`, and a custom container named `'CUST'`.

The `G_CONTAINER` reference object is instantiated by passing the custom container name. The reference object `G_GRID` is instantiated by passing the `G_CONTAINER` object as the parent container. We're ensuring the grid object is instantiated only once by using the `IF` condition `IF g_grid IS NOT BOUND`. The `IF` statement ensures that the grid object isn't instantiated each time the PBO module is called.

In the PAI module, the data from table `SFLIGHT` is selected into internal table `IT_SFLIGHT` and passed to the `SET_TABLE_FOR_FIRST_DISPLAY` method of the `G_GRID` reference object. The user can input the airline code and press `Enter` to see the details in the grid, as shown in Figure 15.14.

The `CL_GUI_ALV_GRID` class provides various methods that help you to work with the ALV grid. The class also triggers various events that can be handled by maintaining suitable event handler methods in the program. To learn more about each method of the class, visit https://help.sap.com/saphelp_erp60_sp/helpdata/en/22/a3f5ecd2fe11d2b467006094192fe3/content.htm.

![](img/5f2e77efd858ed75fdad8c2a2aa83c8f_652_0.png)

Figure 15.14 ALV Grid Control

## 15.4 ALV Object Model

With the 2004 SAP NetWeaver release, SAP introduced the ALV object model, which simplifies ALV generation via the `CL_SALV` family of classes. As you've seen in previous sections, we had to pass a lot of parameters to ALV and manually build the field catalog.

ALV function modules use procedural programming, which may not always suit you if you try to implement your programs in a completely object-oriented way. The `CL_GUI_ALV_GRID` custom controller class does provide object-oriented implementation, but you still need to create your own screens, pass various parameters, and build the field catalog manually.

The ALV object model provides a purely object-oriented implementation of ALV and simplifies creating ALV reports. The ALV object model supports three types of display: tabular display, hierarchical display, and the tree model.

The tabular display shows the output in a two-dimensional grid format; the hierarchical display shows the output in a hierarchical sequence, such as showing header and item data; and the tree model shows the output as a tree structure with parent and child nodes.

Table 15.2 lists the classes of the ALV object model for each type of display.
