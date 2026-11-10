accessed from external sessions. To exchange data between programs running in different main sessions of the user session, we use SAP memory.

*Figure 13.4* shows the memory organization of ABAP programs.

![](bbox=[0.14, 0.193, 0.8, 0.437])

**Figure 13.4** *Memory Organization of ABAP Programs*

All the main sessions are linked to SAP memory in the user session. Programs running in the internal session can access the SAP memory of the user session. This allows you to exchange data between programs running in different windows of SAP GUI (different main sessions) for the user session. For example, one program running in main session 1 can store data in SAP memory, and another program running in main session 2 can read the data stored by the program running in main session 1. Data can be stored in SAP memory using the `SET PARAMETER ID` statement and accessed using the `GET PARAMETER ID` statement. Input fields of the screen can be linked to SAP memory to establish default values.

In Listing 13.2, we created a `ZPROGRAM1` program in which we use the `SET PARAMETER ID` statement to save the value of the `v_matnr` field in SAP memory and assigning the value `"MAT"` as the memory ID. Once this value is stored in SAP memory, any program running in the user session can access this value by referring to the memory ID `"MAT"`.

```
```abap
REPORT ZPROGRAM1.
DATA v_matnr TYPE matnr VALUE '100'.
START-OF-SELECTION.
SET PARAMETER ID 'MAT' FIELD v_matnr.
```
```

**Listing 13.2** *Storing Value in SAP Memory*