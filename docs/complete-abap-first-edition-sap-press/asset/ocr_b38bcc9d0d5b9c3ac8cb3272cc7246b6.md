filter criterion. The custom logic is maintained in each respective implementa-tion. This way when a particular plant needs a change in logic, only the logic in the respective implementation needs to be changed. Similarly, if the plant no lon-ger needs the specific logic to be executed, you can simply deactivate the imple-mentation.

In this section, we'll create a new BAdI and understand the process to define and implement the BAdI. There are two transactions available to work with BAdIs: Transaction SE18 is used to define the BAdI (and to search for existing BAdIs), and Transaction SE19 is used to implement the BAdI.

To determine all the classic BAdIs that are called in a standard SAP application, you can set a breakpoint in the get_instance method of the cl_exithandler class and run the application. The breakpoint is triggered each time a classic BAdI is called in the application. New BAdIs are instantiated differently, so they don't trigger this method.

# 20.8.2 Defining a BAdI

There are three steps involved in defining a BAdI:

+   1. Create an enhancement spot.
+   2. Create the BAdI definition.
+   3. Create the BAdI interface.

In the following sections, we'll walk through each of these steps.

# Creating Enhancement Spot

Enhancement spots act as wrappers for BAdI definitions. One enhancement spot can have multiple BAdI definitions.

To create an enhancement spot, proceed with the following steps:

+   1. Go to Transaction SE18 (BAdI Builder), and select the ENHANCEMENT SPOT radio button. Provide a name for the enhancement spot and click CREATE (see Figure 20.29).
+      Alternatively, you can open the package in Object Navigator (Transaction SE80). Right-click the package and select CREATE • ENHANCEMENT • ENHANCEMENT SPOT.