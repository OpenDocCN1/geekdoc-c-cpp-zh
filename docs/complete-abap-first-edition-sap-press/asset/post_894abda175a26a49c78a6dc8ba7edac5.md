
**Billing Document Header Data**

| BILLING DOCUMENT | PAYER | NET VALUE | BILLING DATE |
|---|---|---|---|
| 90039748 | 300760 | 2,500.00 | 24.04.2015 |
| 90039749 | 300760 | 24,148.00 | 24.04.2015 |
| 90039750 | 300760 | 24,148.00 | 24.04.2015 |
| 90039751 | 300760 | 24,148.00 | 24.04.2015 |
| 90039752 | 300760 | 24,148.00 | 24.04.2015 |
| 90039753 | 300760 | 24,148.00 | 24.04.2015 |
| 90039754 | 301111 | 31,822.00 | 24.04.2015 |
| 90039755 | 301111 | 31,822.00 | 24.04.2015 |
| 90039756 | 301111 | 31,822.00 | 24.04.2015 |
| 90039757 | 301111 | 31,822.00 | 24.04.2015 |
| 90039758 | 301111 | 31,822.00 | 24.04.2015 |

**Figure 13.10 Basic List for Code in Listing 13.9**

**Billing Document Item Data**

| ITEM | DESCRIPTION | BILLED QUANTITY | SU | NET VALUE | MATERIAL | TAX AMOUNT |
|---|---|---|---|---|---|---|
| 000010 | Bicycle Components | 1,000 | EA | 1,300.00 | BIO COMP001 | 0.00 |
| 000020 | Micro Manipulators | 1,000 | EA | 2,550.00 | MIC ANT001 | 0.00 |
| 000030 | Bicycle Components | 1,000 | EA | 1,258.00 | BIO COMP001 | 0.00 |
| 000040 | Thermocyclers | 1,000 | EA | 3,027.00 | THER CYC03 | 0.00 |
| 000050 | Photometers | 1,000 | EA | 1,779.00 | PHOT MET02 | 0.00 |
| 000060 | CD2 Inactivators | 1,000 | EA | 3,459.00 | CD2 INACT02 | 0.00 |
| 000070 | Shakers | 1,000 | EA | 2,246.00 | SHAK 003 | 0.00 |
| 000080 | Easyplot | 1,000 | EA | 201.00 | EAS PET003 | 0.00 |
| 000090 | Photometers | 1,000 | EA | 1,740.00 | PHOT MET02 | 0.00 |
| 000100 | CD2 Inactivators | 1,000 | EA | 3,779.00 | CD2 INACT02 | 0.00 |
| 000110 | Shakers | 1,000 | EA | 2,300.00 | SHAK 003 | 0.00 |
| 000120 | Easyplot | 1,000 | EA | 200.00 | EAS PET003 | 0.00 |

**Figure 13.11 Detail List for Code in Listing 13.9**

### 13.7.2 READ LINE

Similar to the `HIDE` statement, the `READ LINE` or `READ CURRENT LINE` statement can be used to capture the value when the user double-clicks a record. Using the `READ LINE` statement, you can read any line by supplying the row number. You can use the `GET CURSOR` statement to dynamically identify the row on which the user double-clicked and use that row number with the `READ LINE` statement to get the field value, as shown in Listing 13.10. To read the line in succession, use the `READ CURRENT LINE` statement.

```abap
DATA row TYPE sy-index.
GET CURSOR LINE row.
READ LINE row FIELD VALUE wa_vbrk-vbeln.
READ CURRENT LINE FIELD VALUE wa_vbrk-vbeln.
```

**Listing 13.10** Using READ LINE and READ CURRENT LINE

In Listing 13.10, we are defining a row variable of type `sy-index` to identify the cursor position. The `GET CURSOR` statement fills the variable `row` with the line number in the list of the current cursor position. The `READ LINE` statement reads the field value of the supplied row number, and the `READ CURRENT LINE` statement automatically reads the line where the cursor is currently positioned.

### 13.7.3 GET CURSOR

To retrieve information about the cursor position, we can use the `GET CURSOR` statement to determine the current row and current field, as shown in Listing 13.11.

```text
*Using GET CURSOR to fetch row number
DATA row TYPE sy-index.
GET CURSOR LINE row.
*Using GET CURSOR to fetch column (field) name
DATA field TYPE string.
GET CURSOR FIELD field.
```

**Listing 13.11** Using GET CURSOR

### 13.7.4 DESCRIBE LIST

The `DESCRIBE LIST` statement provides information about the attributes of the list levels. Using this statement, we can retrieve information such as the number of lines or number of pages of a list, get the page number of a particular line number, or get the properties of the particular page. Refer to the keyword documentation to see all the possible additions that can be used with this statement.

Listing 13.12 uses the `DESCRIBE LIST` statement to identify the last page and then read the number of lines on the last page. In this example, the `last_page` field will contain the total number of pages generated. Using this value, we read the number of lines on the last page. The `lines` field will contain the number of lines in the last page.

```abap
DATA: last_page TYPE I.
      lines     TYPE I.
AT LINE-SELECTION.
DESCRIBE LIST NUMBER OF PAGES last_page.
DESCRIBE LIST PAGE last_page LINES lines.
```

**Listing 13.12** Using DESCRIBE LIST Statement

### 13.8 Practice

Learning is all about putting theory into practice. The following practice examples should help you explore classical lists (list screens):

- 1. An `END-OF-PAGE` event is triggered when the page is filled. For example, if you have set the line count as `10 (2)`, it means the total number of lines per page is ten, out of which two lines are reserved for the footer. Therefore, the system will trigger the `END-OF-PAGE` event after printing eight lines on the page. However, if the page isn't filled, the `END-OF-PAGE` event isn't triggered. For example, if you've set the line count as `10 (2)` but only six lines are printed in the output, then `END-OF-PAGE` isn't triggered.

  The code in Listing 13.13 doesn't trigger the `END-OF-PAGE` event. For this practice example, modify the code (without printing extra lines) in such a way as to trigger the `END-OF-PAGE` event even if the page isn't filled.

```abap
REPORT ZDEMO_LIST_LINE_COUNT LINE-COUNT 12(2).
START-OF-SELECTION.
DO 6 TIMES.
  WRITE : / 'Demo on end-of-page'.
ENDDO.
END-OF-SELECTION.
WRITE 'END-OF-PAGE event is executed'.
```

**Listing 13.13** Code for Exercise 1

**Hints**

- Find out how many lines are printed and calculate the difference by checking a system field that gives the line count. Use the `SKIP` statement to print blank lines.
- Explore the `RESERVE` keyword.

- 2. Create a basic list and multiple detail lists. For example, when you double-click a line in the basic list, it should open a detail list (use the `WRITE` statement in the `AT LINE-SELECTION` event to print some dummy data). When you double-click a line in the detail list, it should open a new detail list. Double-clicking a line in this list should open further detail lists. For example, say you've opened five detail lists. When you click the Back button on the fifth detail list, it will take you to the fourth detail list. Clicking the Back button on the fourth detail list will take you to the third detail list and so on, until you reach the basic list.

  For this exercise, find out how you can reach the basic list directly when you click on any detail list in the system.

  **Hint**

  Explore the `sy-lsind` system field.

- 3. Discover how to print icons on the list screen. We can print different icons to display the status of a record when displaying records in the output. Figure 13.12 shows a green light icon in the first column of the record to signify that the record is processed successfully. For this exercise, find out how to print icons as shown in Figure 13.12.

  ![](img/5f2e77efd858ed75fdad8c2a2aa83c8f_598_0.png)

  **Figure 13.12** Icon Displayed in Output

  **HINT**

  Explore all the additions for the `WRITE` statement.

### 13.9 Summary

In this chapter, we discussed the various program types in ABAP, which processing blocks they support, and how program types determine program execution flow. We also discussed different ways to execute programs, both internally in the program code and through SAP GUI and covered how understanding memory management is vital to determining how data is exchanged between programs. We looked at how programs run in an internal session and what happens behind the scenes when different programs are called internally.

In addition, we discussed various list events and explored when the events are called and their purposes. You also learned how different events are used to create interactive reports.

In the next chapter, we'll discuss another type of screen in ABAP: the selection screen.

*Selection screens allow users to select what information they see in a specific application. This chapter discusses how to design events that occur in a selection screen.*

## 14 Selection Screens

*Selection screens* are special screens created by using specific ABAP statements. Unlike dialog screens, which are created in Screen Painter, selection screens are auto-generated and don't require manual design. Selection screens are used when a user can provide the selection criteria to restrict the data processed by a program.

In this chapter, we'll look at the features of selection screens. We'll start by discussing how to define selection screens in Section 14.1. When the selection screen is processed, the ABAP runtime environment triggers different selection screen events that allow us to prepare and process input fields on the selection screen. We'll explore the selection screen events in Section 14.2 and how these events can be used for validating user input in Section 14.3. A selection screen can contain many input fields to restrict the data being processed by the program.

Often, users run a report frequently with same set of inputs. For example, a user may input same selection criteria to check daily stock movements for a particular plant each time he runs the report. To avoid having to repeatedly input the same selection criteria each time the report is run, we can create a selection screen variant to save the selection criteria. We'll discuss how to create and use selection screen variants in Section 14.4.

Reports can be executed online by the user through an SAP GUI screen or they can be scheduled to execute in the background. Background execution of a program is useful if the program is processing huge amounts of data and takes a long time to complete execution. Sometimes, a user may also want to run a report at a fixed time of day at regular intervals. We'll discuss how to execute programs in the background in Section 14.5.
