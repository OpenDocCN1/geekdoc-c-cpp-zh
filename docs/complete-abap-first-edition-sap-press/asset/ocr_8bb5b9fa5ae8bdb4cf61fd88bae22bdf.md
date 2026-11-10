automatically highlighting the field with an error by disabling all the other fields on the screen and enabling only the field with the error.

In Listing 14.3, we defined two selection screen fields, `p_matnr` and `p_spras`. When we use the `AT SELECTION-SCREEN ON` field event to independently validate the fields, the system will automatically highlight the field in error by input-enabling the error field and making the remaining fields on the selection screen input-disabled.

```
PARAMETERS : p_matnr TYPE matnr.
             p_spras TYPE spras.
AT SELECTION-SCREEN ON p_matnr.
*Validate p_matnr input field
AT SELECTION-SCREEN ON p_spras.
*Validate p_spras input field.
```

**Listing 14.3** Validating Input Fields Independently

If a group of fields should be validated together, it's recommended to group the fields into a block (using `SELECTION-SCREEN BEGIN OF BLOCK`) and use the `AT SELECTION-SCREEN ON BLOCK` event. This allows you to automatically highlight the fields of the block by disabling all the other fields on the screen and enabling only the fields of the block.

In Listing 14.4, we grouped the `p_matnr` and `p_spras` fields into block `b1`. When we use the `AT SELECTION-SCREEN ON BLOCK b1` event to validate the input fields, both `p_matnr` and `p_spras` will be input-enabled together when an error message is raised in the event.

```
SELECTION-SCREEN BEGIN OF BLOCK b1.
PARAMETERS : p_matnr TYPE matnr.
             p_spras TYPE spras.
SELECTION-SCREEN END OF BLOCK.
SELECTION-SCREEN BEGIN OF BLOCK b2.
PARAMETERS : p_werks TYPE werks_d.
SELECTION-SCREEN END OF BLOCK.

AT SELECTION-SCREEN ON BLOCK b1.
*Validate p_matnr and p_spras input fields together
```

**Listing 14.4** Validating Input Fields as Related Group

Similarly, when validating radio buttons, use the `AT SELECTION-SCREEN ON RADIO BUTTON GROUP` event to ensure all the radio buttons are enabled when an error message is shown. For example, in Listing 14.5, if an invalid radio button option