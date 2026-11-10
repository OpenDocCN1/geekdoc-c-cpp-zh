```
```abap
gr_event_handler TYPE REF TO lcl_event_handler,
gr_event         TYPE REF TO cl_salv_events_table.
TYPES: BEGIN OF ty_mara,
         matnr TYPE mara-matnr,
         ersda TYPE ersda,
         ernam TYPE ernam,
         laeda TYPE laeda,
         mtart TYPE mtart,
       END OF ty_mara.
DATA: it_mara TYPE STANDARD TABLE OF ty_mara,
      gv_matnr TYPE matnr.
SELECT-OPTIONS: s_matnr FOR gv_matnr.

*&--------------------------------------------------------------*
*&    Class LCL_EVENT_HANDLER
*&--------------------------------------------------------------*
CLASS lcl_event_handler DEFINITION.
  PUBLIC SECTION.
    METHODS: on_double_click FOR EVENT double_click OF cl_salv_events_
table IMPORTING row column.
ENDCLASS. "LCL_EVENT_HANDLER

*--------------------------------------------------------------*
*    CLASS lcl_event_handler IMPLEMENTATION
*--------------------------------------------------------------*
CLASS lcl_event_handler IMPLEMENTATION.
  METHOD on_double_click.
    DATA: lo_sel       TYPE REF TO cl_salv_selections,
          ls_cell      TYPE salv_s_cell,
          container_2  TYPE REF TO cl_gui_container,
          lt_mara      TYPE STANDARD TABLE OF ty_mara,
          lw_mara      TYPE ty_mara.
*Get reference to the user selection.
    lo_sel = mo_alv->get_selections( ).
*Get the value of the cell
    ls_cell = lo_sel->get_current_cell( ).
*Logic to filter records
    IF ls_cell-columnname EQ 'MATNR'.
      LOOP AT it_mara INTO lw_mara WHERE matnr EQ ls_cell-value.
        APPEND lw_mara TO lt_mara.
      ENDLOOP.
    ELSEIF ls_cell-columnname EQ 'ERSDA'.
      LOOP AT it_mara INTO lw_mara WHERE ersda EQ ls_cell-value.
        APPEND lw_mara TO lt_mara.
      ENDLOOP.
    ELSEIF ls_cell-columnname EQ 'ERNAM'.
      LOOP AT it_mara INTO lw_mara WHERE ernam EQ ls_cell-value.
        APPEND lw_mara TO lt_mara.
      ENDLOOP.
```
```