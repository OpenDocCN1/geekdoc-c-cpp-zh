```
```abap
DATA : lo_sel       TYPE REF TO cl_salv_selections,
       ls_cell      TYPE salv_s_cell,
       container_2  TYPE REF TO cl_gui_container,
       lt_mara      TYPE STANDARD TABLE OF ty_mara,
       lw_mara      TYPE ty_mara.

lo_sel = mo_alv->get_selections( ).
ls_cell = lo_sel->get_current_cell( ).

LOOP AT lt_mara INTO lw_mara.
  ASSIGN COMPONENT ls_cell-columnname OF STRUCTURE lw_mara TO
    <field>.
  IF <field> IS ASSIGNED.
    IF <field> EQ ls_cell-value.
      APPEND lw_mara TO lt_mara.
    ENDIF.
  ENDIF.
ENDLOOP.
CALL METHOD splitter->get_container
  EXPORTING
    row    = 2
    column = 1
  RECEIVING
    container = container_2.

TRY.
  IF so_alv IS BOUND.
    so_alv->set_data( CHANGING t_table = lt_mara ).
  ELSE.
    CALL METHOD cl_salv_table=>factory
      EXPORTING
        list_display = if_salv_c_bool_sap=>false
        r_container  = container_2
      IMPORTING
        r_salv_table = so_alv
      CHANGING
        t_table      = lt_mara.
  ENDIF.
  CATCH cx_salv_msg .
ENDTRY.
so_alv->display( ).
ENDMETHOD.                    "on_double_click
```
```

# **Listing 16.5** Filter Functionality Using Field Symbols

In Listing 16.5, we've defined a <FIELD> field symbol as a generic type (we'll discuss typing field symbols in a moment). Within the loop, we're dynamically assigning the component of the table to the field symbol. Based on which column the user double-clicks, the LS_CELL-COLUMNAME field will have that field name.