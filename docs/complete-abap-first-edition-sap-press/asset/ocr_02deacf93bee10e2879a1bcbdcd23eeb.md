that you can only make program changes, as opposed to customer exits and BAdIs that support screen and GUI enhancements.

BTEs are implemented using function modules, unlike BAdIs, which use ABAP Objects. BTEs preceded BAdIs and are an older enhancement technique, but we’re covering them here for the sake of completeness.

BTEs work on the principle that the system triggers an event for which a suitable function module is maintained to execute custom code. SAP provides sample function modules for all events (called *samples*), and we can copy these sample function modules and write our custom code. The interface of these function modules shouldn’t be changed.

There are two types of interfaces available:

+   - **Publish and subscribe interfaces**  
+     These interfaces allow you to interrupt standard SAP application flow to carry out additional work outside of the application. These interfaces don’t export any data back to the application, so you can’t use them to modify the application data. They import certain application data, which can be used to perform additional steps external to the application. For example, when creating a vendor, you may want to update certain custom tables with additional data using the vendor number.
+   - **Process interfaces**  
+     These interfaces allow you to interrupt the standard SAP application and modify its data. They allow you to change how a standard SAP application behaves and influence the application data, and they implement importing and changing parameters, which can be used to modify the application data.

Let’s use a vendor master record as an example to explain how BTEs are implemented. For this example, we want to execute some custom code when a vendor master record is saved via Transaction FK02.

# 20.10.1 Implementing a BTE

BTEs are implemented using Transaction FIBF. Most of the configurations are carried out by functional consultants; as ABAP developers, our role is limited to creating the function module and adding custom code.