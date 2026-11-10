of the parameters field or the line of `SELECT-OPTIONS` is transferred to the ABAP program. This event is used to validate the field input. If an error or warning message is shown, the field will be automatically input-enabled. For example:

```
PARAMETERS p_matnr TYPE matnr.
AT SELECTION-SCREEN ON p_matnr.
```

# AT SELECTION-SCREEN ON END OF <sel>

This event is triggered when the selection table of the `SELECT-OPTIONS` field is fully passed to the ABAP program after the user action on the multiple selection window. This event allows you to validate all the entries of the selection table. For example:

```
SELECT-OPTIONS s_matnr FOR v_matnr.
AT SELECTION-SCREEN ON END OF s_matnr.
```

# AT SELECTION-SCREEN ON BLOCK

You can organize the selection screen fields into multiple blocks. This event is triggered when the data of all the fields of the block is transferred to the program. If an error or warning message is raised in this event, all the fields in the block will be input-enabled. For example:

```
SELECTION-SCREEN BEGIN OF BLOCK b1.
PARAMETERS : p_matnr TYPE matnr,
             p_spras TYPE spras.
SELECTION-SCREEN END OF BLOCK.
AT SELECTION-SCREEN ON BLOCK b1.
```

# AT SELECTION-SCREEN ON RADIO BUTTON GROUP

This event is triggered when all the fields of a radio button group are passed to the ABAP program. If an error or warning message is raised in this event, all the fields in the radio button group will be input-enabled. The individual radio button fields are not passed to the ABAP program independently, so they don't trigger `AT SELECTION-SCREEN ON` field event. For example:

```
PARAMETERS : p_day RADIOBUTTON GROUP rb1,
             p_month RADIOBUTTON GROUP rb1,
             p_year RADIOBUTTON GROUP rb1.

AT SELECTION-SCREEN ON RADIOBUTTON GROUP rb1.
```

# AT SELECTION-SCREEN

This is a standard selection screen event and is triggered after all the selection screen events are executed. This event can be used to validate user inputs. If an error or warning message is raised in this event, all the fields of the selection