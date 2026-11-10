
filter criterion. The custom logic is maintained in each respective implementation. This way when a particular plant needs a change in logic, only the logic in the respective implementation needs to be changed. Similarly, if the plant no longer needs the specific logic to be executed, you can simply deactivate the implementation.

In this section, we'll create a new BAdI and understand the process to define and implement the BAdI. There are two transactions available to work with BAdIs: Transaction SE18 is used to define the BAdI (and to search for existing BAdIs), and Transaction SE19 is used to implement the BAdI.

To determine all the classic BAdIs that are called in a standard SAP application, you can set a breakpoint in the get_instance method of the cl_exithandler class and run the application. The breakpoint is triggered each time a classic BAdI is called in the application. New BAdIs are instantiated differently, so they don't trigger this method.

## 20.8.2 Defining a BAdI

There are three steps involved in defining a BAdI:

- 1. Create an enhancement spot.
- 2. Create the BAdI definition.
- 3. Create the BAdI interface.

In the following sections, we'll walk through each of these steps.

### Creating Enhancement Spot

Enhancement spots act as wrappers for BAdI definitions. One enhancement spot can have multiple BAdI definitions.

To create an enhancement spot, proceed with the following steps:

- 1. Go to Transaction SE18 (BAdI Builder), and select the ENHANCEMENT SPOT radio button. Provide a name for the enhancement spot and click CREATE (see Figure 20.29).
  - Alternatively, you can open the package in Object Navigator (Transaction SE80). Right-click the package and select CREATE • ENHANCEMENT • ENHANCEMENT SPOT.

![](img/5f2e77efd858ed75fdad8c2a2aa83c8f_948_0.png)

Figure 20.29  BAdI Builder: Initial Screen

- 2. On the CREATE ENHANCEMENT SPOT screen, as shown in Figure 20.30, provide a short description. In the TECHNOLOGY dropdown box, select BAdI DEFINITION. In the COMPOSITE ENHANCEMENT SPOT field, you can enter the composite enhancement spot name, which simply groups the related enhancement spots. Enhancement spots grouped into a composite enhancement spot are displayed in a tree structure, allowing you to check dependencies and change all related enhancement spots together. This only has a semantic meaning and is similar to grouping related objects into a package.

- 3. Click the green checkmark (OK) to continue.

![](img/5f2e77efd858ed75fdad8c2a2aa83c8f_948_1.png)

Figure 20.30  Create Enhancement Spot

### Creating a BAdI Definition

Once you click the green checkmark on the CREATE ENHANCEMENT SPOT screen shown in Figure 20.30, the system will take you to the ENHANCEMENT SPOT CHANGE screen, which contains four tabs.

From here, proceed with the following steps:

- 1. Under the ENH. SPOT ELEMENT DEFINITION tab, as shown in Figure 20.31, click the CREATE BAdI button.

![](img/5f2e77efd858ed75fdad8c2a2aa83c8f_949_0.png)

Figure 20.31  Create BAdI

- 2. This will open a dialog box in which you can provide the NAME for the BAdI definition and a SHORT DESCRIPTION. Click the green checkmark to continue (see Figure 20.32).

![](img/5f2e77efd858ed75fdad8c2a2aa83c8f_949_1.png)

Figure 20.32  Create BAdI Definition

- 3. On the BAdI definition page, as shown in Figure 20.33, you'll see the BAdI definition with its subobjects in a tree structure. Once the BAdI is selected, you can set certain attributes. Within the ENH. SPOT ELEMENT DEFINITION tab, implement the following changes:
  - In the Usability section, you can select or deselect the MULTIPLE USE checkbox, depending on whether you want to allow multiple implementations for this BAdI to be called or if only a single implementation can be active at any given point in time. As previously mentioned, multiple implementations are useful when you want to provide different logic for different countries, company codes, plants, and so on. The LIMITED FILTER USE checkbox allows you to set a filter criterion for BAdI implementation. You'll learn more about implementing filters in the next subsection. Selecting the AMDP BAdI checkbox creates a special BAdI for ABAP Managed Database Procedures (AMDP). AMDP is a framework which currently supports database procedures and functions from the SAP HANA database.
  - In the **Instance Creation Mode** section, you can select the following:
    - **Newly Creating Instantiation:** Select this if you don't want the BAdI to buffer the data when it's called multiple times by the program.
    - **Reusing Instantiation:** Select this if you're fine with reusing data when the BAdI is called multiple times by the program. This option is useful if you're selecting data from the database and want to avoid database access each time the BAdI is called in the program. This implements a singleton pattern in which only one instance exists.
    - **Context-Specific Instantiation:** Selecting this option allows you to specify a context while calling the BAdI; the context controls the BAdI instantiation. If the BAdI is called with the same context, the same BAdI instance is reused; otherwise, a new instance is created. To specify the context, the context class must implement the `IF_BADI_CONTEXT` interface.
  - The **Fallback Class** option allows you to implement a fallback class. A *fallback class* is the default class called if no implementation is active. The fallback class is also called for multiple-use BAdIs with filter criteria when none of the implementations satisfy the filter criteria.

![](img/5f2e77efd858ed75fdad8c2a2aa83c8f_950_0.png)

- 4. You can define a filter for the BAdI by right-clicking on the BAdI definition name and selecting **CREATE FILTER** from the context menu (see **Figure 20.34**).

![](img/5f2e77efd858ed75fdad8c2a2aa83c8f_951_0.png)

Figure 20.34  Creating Filter

- 5. Setting a filter adds the field to the parameter interface. The calling program needs to supply this filter value to call the BAdI. The CREATE FILTER screen (see Figure 20.35) allows you to define the filter field. In this example, set the plant number as the filter. You can provide the BAdI FILTER name, FILTER TYPE, and DESCRIPTION. For the FILTER TYPE, you can select any elementary type, such as character, numeric, string, packed, and so on, using the F4 help for the field. The CONSTANT FILTER VALUE checkbox forces the program to pass a constant during the call.

![](img/5f2e77efd858ed75fdad8c2a2aa83c8f_951_1.png)

Figure 20.35  Create Filter

- 6. Because the filter value is passed by the program, it's always a good practice to validate the value being passed in order to avoid any runtime errors. Under FILTER VALUE CHECK FOR BAdI IMPLEMENTATIONS, there are three options:
  - **No Check:** This option doesn’t perform any check, and the program is free to pass any value. This can result in runtime errors if incompatible values are passed.
  - **Automatic Through Dictionary:** Selecting this option will show a field in which you can assign a data element (or domain). This allows you to check for type compatibility with the field of the calling program. For example, if the filter is set as TYPE p, then it will raise a syntax error if a field of another type is passed in the calling program. During the implementation of the BAdI, this option uses the value range defined for the domain to list the possible values. Only one of the possible values defined in the value range can be set as the filter value (see Figure 20.36).

![](img/5f2e77efd858ed75fdad8c2a2aa83c8f_952_0.png)

Figure 20.36  Assigning Data Element as Filter Check

  - **By Own Program:** This option allows you to implement your own check by creating a class, as shown in Figure 20.37. Once you provide the class name and click OK, you’ll be taken to Transaction SE24 (Class Builder), where you can implement the class.

![](img/5f2e77efd858ed75fdad8c2a2aa83c8f_952_1.png)

Figure 20.37  Filter Check by Own Program

    This class implements an `IF_FILTER_CHECK_AND_F4` interface that has four methods, as shown in Figure 20.38:

    - **SHOW_F4_ICON:** This method has a returning parameter, which you can set as `abap_true (X)` to show the F4 icon to the developer implementing the BAdI; this tells the developer that F4 help is available to select the filter value.
