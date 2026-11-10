
### 20.9.1 Explicit Enhancements

Explicit enhancements are similar to all the other types of enhancements, such as customer exits and BAdIs, in that they're provided explicitly in the code. If an enhancement isn't provided explicitly by SAP, you can't add your custom code.

There are two types of explicit enhancement points:

- **Static explicit enhancement points**  
  *Static enhancement points* are introduced by the `ENHANCEMENT-POINT` statement and end with the `STATIC` keyword, as shown in Figure 20.51. Static enhancement points aren't controlled by the Switch Framework.

- **Dynamic explicit enhancement points**  
  *Dynamic enhancement points* don't include the `STATIC` keyword at the end. Dynamic enhancement points are controlled by the Switch Framework.

We use static enhancement points to add data declarations and dynamic enhancement points to write program logic. The enhancements are implemented between `ENHANCEMENT` and `ENDENHANCEMENT` statements, with each enhancement assigned a number that's unique within the program.

![](img/5f2e77efd858ed75fdad8c2a2aa83c8f_960_0.png)

If you see the `ENHANCEMENT-POINT` statement in a standard SAP program, then you can add your source code plugin at that point in the source code. Implementing an enhancement is pretty straightforward.

Proceed as follows:

- 1. Open the standard SAP program that you want to enhance in display mode. Click on the seashell icon in the application toolbar, as shown in Figure 20.52. This will enable the program to change or implement enhancements.

  ![](img/5f2e77efd858ed75fdad8c2a2aa83c8f_961_0.png)

- 2. Right-click the enhancement point and select Enhancements • Create Implementation from the context menu. This will open the Select or Create Enhancement Implementation window (see Figure 20.53). Here, you can select any existing enhancement implementation or click the Create button to create a new implementation.

  ![](img/5f2e77efd858ed75fdad8c2a2aa83c8f_961_1.png)

- 3. If you click the CREATE button to create a new implementation, the system will present the CREATE ENHANCEMENT IMPLEMENTATION window, in which you can enter an Enhancement Implementation name and Short Text description for your implementation, as shown in Figure 20.54. Save the enhancement implementation to your customer package. The new enhancement implementation now will appear in the list shown in Figure 20.53. Double-click the enhancement implementation name to select it.

  ![](img/5f2e77efd858ed75fdad8c2a2aa83c8f_962_0.png)

  **Figure 20.54** Creating New Implementation

- 4. This will create an ENHANCEMENT ENDENHANCEMENT section in the code in which you can add your custom code, as shown in Figure 20.55.

  ![](img/5f2e77efd858ed75fdad8c2a2aa83c8f_962_1.png)

  **Figure 20.55** Enhancement Section

- 5. Once you add custom code, click on the ACTIVATE ENHANCEMENTS button in the application toolbar.

### 20.9.2 Implicit Enhancements

Unlike explicit enhancements that are provided in programs by SAP, implicit enhancements are available by default in the program. They are available at the beginning and end of a procedure (i.e., in subroutines, function modules, and methods), at the end of a structure definition, and at the end of an executable program.

To show implicit enhancements, follow the menu path EDIT • ENHANCEMENT OPERATIONS • SHOW IMPLICIT ENHANCEMENT OPERATIONS from ABAP Editor, Function Builder, or Class Builder.

This will show a comment line under the SOURCE CODE tab that indicates where you can create the implementation, as shown in Figure 20.56.

![](img/5f2e77efd858ed75fdad8c2a2aa83c8f_963_0.png)

Figure 20.56 Implicit Enhancement Point

Even though you have more flexibility with implicit enhancement points, you still can't use them to, for example, add code in the middle of a procedure.

Implementing implicit enhancements is similar to explicit enhancements, in that you create an enhancement implementation. We recommend keeping all related enhancements in the same implementation so that they can be switched on or off together. When you switch off an enhancement implementation, it won't be compiled.

Let's walk through how to enhance a function module interface to add custom parameters:

- 1. Open the function module you want to enhance and navigate to the **Import**, **Export**, **Changing**, or **Tables** tab, depending on which tab you want to add the custom parameter to. For this example, go to the **Export** tab. The process is the same for other parameters.

- 2. Click on the **Enhance** icon (see Figure 20.57) in the toolbar. The system will prompt you to create an enhancement implementation. Create an enhancement implementation as explained in Section 20.9.1.

  ![](img/5f2e77efd858ed75fdad8c2a2aa83c8f_963_1.png)

  Figure 20.57 Create Enhancement

- 3. Add the custom field to the interface, as shown in **Figure 20.58**. If you're adding import, changing, or tables parameters, make sure to check the OPTIONAL checkbox to ensure that your enhancement won't break the existing programs calling this function module.

  As you can see in **Figure 20.58**, the existing parameters of the function module are input-disabled. You can also see the enhancement implementation name in the **ENHANCEMENT IMPLEMENTATION** column.

  ![](img/5f2e77efd858ed75fdad8c2a2aa83c8f_964_0.png)

  Figure 20.58 Adding Custom Parameter to Export Tab

- 4. The parameter added to the interface should be filled in the source code of the function module. Navigate to the SOURCE CODE tab. If you don't see a suitable explicit enhancement point in the code, you can use the implicit enhancement point to update the parameter, as explained in the following steps.

- 5. Use the menu path EDIT • ENHANCEMENT OPERATIONS • SHOW IMPLICIT ENHANCEMENT OPERATIONS to display the implicit enhancement points.

- 6. Select the implicit enhancement point and follow the menu path EDIT • ENHANCEMENT OPERATIONS • CREATE IMPLEMENTATION, as shown in **Figure 20.59**.

  ![](img/5f2e77efd858ed75fdad8c2a2aa83c8f_964_1.png)

  Figure 20.59 Creating Implementation

- 7. You'll see a dialog box to choose the enhancement mode (see Figure 20.60). Choose the Declaration button if you want to add data declarations (static enhancement), and choose the Code button if you want to add program logic (dynamic enhancement). For this example, select the Code button.

  ![](img/5f2e77efd858ed75fdad8c2a2aa83c8f_965_0.png)

  Figure 20.60 Enhancement Mode

- 8. Choose an existing implementation if the code you're adding is related to another enhancement; otherwise, create a new enhancement implementation. Add the program logic between `ENHANCEMENT` and `ENDENHANCEMENT`, as shown in Figure 20.61. Within the source code of the function module, you have access to both the existing parameters and the new parameter that you added. You can also access the global data objects of the function group, but use caution when changing global data of the function group.

  ![](img/5f2e77efd858ed75fdad8c2a2aa83c8f_965_1.png)

  Figure 20.61 Implementing Enhancement

The steps to enhance a method are similar to the steps to enhance a function module. You can also enhance a class to add new methods. The bonus is that these new methods can also access the private components of a class.

## 20.10 Business Transaction Events

*Business transaction events* (BTEs) are a type of enhancement specifically available for the SAP ERP Financial Accounting component. BTEs are similar to user exits in that you can only make program changes, as opposed to customer exits and BAdIs that support screen and GUI enhancements.

BTEs are implemented using function modules, unlike BAdIs, which use ABAP Objects. BTEs preceded BAdIs and are an older enhancement technique, but we’re covering them here for the sake of completeness.

BTEs work on the principle that the system triggers an event for which a suitable function module is maintained to execute custom code. SAP provides sample function modules for all events (called *samples*), and we can copy these sample function modules and write our custom code. The interface of these function modules shouldn’t be changed.

There are two types of interfaces available:

- **Publish and subscribe interfaces**  
  These interfaces allow you to interrupt standard SAP application flow to carry out additional work outside of the application. These interfaces don’t export any data back to the application, so you can’t use them to modify the application data. They import certain application data, which can be used to perform additional steps external to the application. For example, when creating a vendor, you may want to update certain custom tables with additional data using the vendor number.

- **Process interfaces**  
  These interfaces allow you to interrupt the standard SAP application and modify its data. They allow you to change how a standard SAP application behaves and influence the application data, and they implement importing and changing parameters, which can be used to modify the application data.

Let’s use a vendor master record as an example to explain how BTEs are implemented. For this example, we want to execute some custom code when a vendor master record is saved via Transaction FK02.

### 20.10.1 Implementing a BTE

BTEs are implemented using Transaction FIBF. Most of the configurations are carried out by functional consultants; as ABAP developers, our role is limited to creating the function module and adding custom code.
