# Declaration Area

Each ABAP program consists of a global declaration area followed by a number of processing blocks. The objects defined in the global declaration part are visible in all processing blocks of the ABAP program. In some processing blocks (such as procedures), data declarations can be made within the processing block that are locally visible.

Listing 7.1 shows an example of global and local declarations.

```
REPORT ZC_B_EXAMPLE.
*Global declarations of the program
DATA: f1 TYPE c VALUE 'A',
      f2 TYPE c VALUE 'B'.
END-OF-SELECTION.
  PERFORM output. "Calling a subroutine
*&--------------------------------------------------------------*
*&      Form  OUTPUT
*&--------------------------------------------------------------*
FORM output.
*Local declaration that can be accessed (visible) within
*this subroutine
  DATA f3 TYPE c VALUE 'C'.
  WRITE f1.
  WRITE f2.
  WRITE f3.
ENDFORM.
```

**Listing 7.1** Local and Global Data

In Listing 7.1, we defined data objects f1 and f2 in the global declaration area of the program. The program contains a subroutine with the name OUTPUT, within which we declared the data object f3. Because the data object f3 is declared within the subroutine OUTPUT, it's local to this subroutine. In other words, the data object f3 is locally visible within the subroutine OUTPUT and can be accessed only by ABAP statements that are part of the subroutine.

You can't access this data object f3 from other processing blocks of the program. However, the global data objects f1 and f2 can be accessed by ABAP statements from any processing block of the program.

# Using Processing Blocks

Processing blocks are indivisible units that contain ABAP statements. For example, in Listing 7.1, END-OF-SELECTION is an event block, which is a type of processing