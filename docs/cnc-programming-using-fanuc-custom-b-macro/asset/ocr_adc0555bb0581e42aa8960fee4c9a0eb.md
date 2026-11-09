OOOOO
§

+   - Type #1 = 1 (or any other “harmless” macro statement, so as not to cause any unexpected machine behavior), followed by the *end of block* (EOB) character (which is a semicolon), and then press the INPUT key, on the MDI panel.

+   - Press the CYCLE START button on the MOP.

This will assign a value of 1 to the macro variable number 1. If no error message, the machine has macro programming capability with full functionality (the control manufacturers do not enable this feature with partial functionality; it will either be available or not available). To doubly sure, check the value of the defined macro variable on the offset/setting screen.

+   - Press the OFS/SET function key on the MDI panel.

+   - Press the right extension key (▶) below the display screen, if the MACRO soft key does not appear. Now press the MACRO soft key.

This will show, on a *roll-over* screen (i.e., the first line reappears after the last line, in forward scrolling), the values stored in all the macro variables (001 to 033, 100 to 199, and 500 to 999, typically), which can be viewed using the up/down arrow keys and the page up/page down keys on the MDI panel. The value stored in variable number 001 (which is the same as variable number 1) would be displayed as 00001.000 (values are stored using eight digits, with blank fields for the remaining variables (a blank field indicates an undefined variable), except perhaps those in the 500 to 999 range, which retain the previously stored values even after power OFF. These variables, which are called *permanent common variables*, can, however, be re-defined. Pressing the RESET key will clear all the variables except the permanent common variables. A parameter setting, however, can retain the values of all the variables, even after RESET operation. Different types of variables are described in detail in Chap. 3.

If the machine does not have the macro feature, it will not recognize the macro statement, and will give an error message. In such a case, the company whose control is installed on the machine (such as Fanuc, Siemens, Heidenhain, etc.) has to be contacted. They will enable this option on the machine for a charge. It is interesting to note that the electronic hardware of a particular control version is the same for all the machines on which the standard features always remain available. But the control manufacturers enable (through software coding) only those optional features for which they receive additional payment. So, do not worry if your machine is not macro-enabled, just be willing to pay for it. However, nonstandard controls usually do not have macro capability.