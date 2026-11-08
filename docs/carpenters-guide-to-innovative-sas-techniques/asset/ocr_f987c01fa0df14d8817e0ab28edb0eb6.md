The metadata shown here contains the data set name and the check information associated with

| 13.5.2 Metadata Driven Field Checks |  |  |  |  |  |
|---|---|---|---|---|---|
| Obs | dsn | var | chkrating | chktype | chktext |
| 1 | demog | subject | 1 | notmiss |  |
| 2 | demog | RACE | 2 | list | ('1','2','3','4','5','6') |
| 3 | conmed | medstdt_ | 4 | datefmt | mmddyy10. |
| 4 | lab_chemistry | potassium | 2 | maximum | 6.7 |

that check. If the metadata is designed to contain sufficient information, it can easily be expanded to accommodate any number of checks on any number of data sets, and multiple checks can be performed on any given variable. The number of checks and the kinds of checks are only limited by the programmer’s imagination.

In the examples in Section 2.3.3 a data validation and error reporting macro was developed that utilized metadata to perform simple data checks. We can expand on that macro by making use of the type of metadata shown here. In this example the checks are performed across all data sets, and the checks themselves are constructed from the information in the metadata.

Any number of different types of checks is possible; shown here are just a few to give you an idea of the possibilities (variable CHKTYPE in the metadata):

+   - **notmiss** — the variable may not contain missing values.
+   - **list** — the value must be in the list of values in CHKTXT.
+   - **datefmt** — the formatted value of the variable (using the format in CHKTXT) must not be missing.
+   - **maximum** — the value must be less than or equal to the value in CHKTXT.

Using this approach any number of checks can be performed against a given variable or data set. Adding and changing checks does not require coding changes, unless a brand new check is introduced. Here a slight coding modification would be required if we wanted to introduce a check for minimum values.