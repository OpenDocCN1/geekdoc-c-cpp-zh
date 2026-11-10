![](bbox=[0.142, 0.103, 0.506, 0.279])

Figure 20.34 Creating Filter

+   5. Setting a filter adds the field to the parameter interface. The calling program needs to supply this filter value to call the BAdI. The CREATE FILTER screen (see Figure 20.35) allows you to define the filter field. In this example, set the plant number as the filter.

You can provide the BAdI FILTER name, FILTER TYPE, and DESCRIPTION. For the FILTER TYPE, you can select any elementary type, such as character, numeric, string, packed, and so on, using the F4 help for the field. The CONSTANT FILTER VALUE checkbox forces the program to pass a constant during the call.

![](bbox=[0.142, 0.521, 0.646, 0.741])

Figure 20.35 Create Filter

+   6. Because the filter value is passed by the program, it's always a good practice to validate the value being passed in order to avoid any runtime errors. Under FILTER VALUE CHECK FOR BAdI IMPLEMENTATIONS, there are three options: