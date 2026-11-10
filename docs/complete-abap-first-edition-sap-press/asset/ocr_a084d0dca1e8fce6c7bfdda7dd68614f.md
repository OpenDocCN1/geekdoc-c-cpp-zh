When you create a function group or function module in the Function Builder, the main program and include programs are generated automatically (see Figure 7.12).

![](bbox=[0.142, 0.18, 0.85, 0.406])

**Figure 7.12** Function Group Includes

As shown in Figure 7.12, the main program `SAPLZCB_FG` contains nothing but the `INCLUDE` statements for the following include programs:

+   - `LZCB_FGTOP`: Contains the `FUNCTION-POOL` statement and global data declarations for the entire function group.
+   - `LZCB_FGUXX`: Contains further `INCLUDE` statements for the include programs `LfgrpU01`, `LfgrpU02`, and so on. These `INCLUDE` statements contain the actual function modules.
+   - `LfgrpF01` and `LfgrpF02`: Subroutines can be maintained in the `INCLUDE` programs `LfgrpF01`, `LfgrpF02`, and so on and can be called from all function modules of the group as internal subroutines.

All the function modules in the function group can access the data declarations made in the global data area of the function group. For this reason, you should place all function modules that use the same data in a single function group instead of creating a new function group for each function module. For example, if you have a set of function modules that all use the same internal table, you could place them in a function group containing the table definition in its global data.