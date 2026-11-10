![](bbox=[0.148, 0.103, 0.573, 0.326])

Figure 18.32  Form Interface

Similarly, we’ve defined a `ZBILL_T_ITEM` table type in ABAP Data Dictionary, the line type for which has the components `VBELN`, `POSNR`, `ARKTX`, and `NETWR` for item data. In the form interface, we’ve defined a `im_header` structure, which is of type `zbll_header`, and an internal table `im_item`, which is of type `zbll_t_item` (see Figure 18.32).

![](bbox=[0.148, 0.497, 0.858, 0.684])

Figure 18.33  Header Structure

# Global Definitions

Global variables and constants for the form are defined in GLOBAL DEFINITIONS. This section consists of multiple tabs to define objects such as variables, constants, field symbols, data types, and currency and quantity fields under their respective tabs. You can also maintain the initialization code under the INITIALIZATION tab to initialize the form fields. The FORM ROUTINES tab allows you to maintain subroutines that can be called from within the form. The definitions in this