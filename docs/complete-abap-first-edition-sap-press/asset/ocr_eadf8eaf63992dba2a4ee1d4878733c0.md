Table 14.1 describes the components of the screen structure and provides their possible values (as shown in Figure 14.20).

| Field Name | Possible Values | Meaning |
|---|---|---|
| NAME | Name of screen element | Name of the screen field |
| GROUP1 to GROUP4 | 1d1 to 1d4 | Modification group to apply common settings to related fields that belong to the same group |
| REQUIRED | 0, 1, 2 | Mandatory or recommended field |
| INPUT | 0, 1 | Input-ready field |
| OUTPUT | 0, 1 | Read-only/display field |
| INTENSIFIED | 0, 1 | Highlighted field |
| INVISIBLE | 0, 1 | Invisible element |
| LENGTH | Visible length of field | Field length |
| ACTIVE | 0, 1 | Active field |
| DISPLAY_3D | 0, 1 | Display frame |
| VALUE_HELP | 0, 1, 2 | Input help button |
| REQUEST | 0, 1 | Input exists |
| VALUES_IN_COMBO | 0, 1 | Dropdown list box |

**Table 14.1** Screen Structure Components

As discussed in Chapter 12, we can use the `LOOP AT SCREEN` statement to access all the screen fields one at a time and modify their attributes. Listing 14.6 shows an example of how to modify the screen fields using the screen structure. In this example, we’re looping the screen structure to disable input for the `p_matnr` and `p_spras` fields.

```
PARAMETERS : p_kunnr TYPE kunnr,
            p_matnr TYPE matnr,
            p_spras TYPE spras.

DATA wa_screen TYPE screen.
AT SELECTION-SCREEN OUTPUT.
  LOOP AT SCREEN INTO wa_screen.
    IF wa_screen-name EQ 'P_MATNR'.
      wa_screen-input = abap_false.
    ENDIF.
    IF wa_screen-name EQ 'P_SPRAS'.
```