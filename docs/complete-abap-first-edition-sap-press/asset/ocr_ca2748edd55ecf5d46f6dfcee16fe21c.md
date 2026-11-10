+   - You shouldn't put BAPIs belonging to different business object types in the same function group.
+   - The function module should be RFC-enabled.
+   - The function module should have a return parameter of type `BAPIPRET2`.
+   - Even though underscores aren't allowed for parameter names in BOR, you can separate each word in the parameter name using the underscore in the function module. For example, you can name the parameter `FirstName` in BOR as `FIRST_NAME` in the function module.
+   - The extension structures `ExtensionIn` and `ExtensionOut` should be of type `BAPIPAREX`. These parameters can be named `EXTENSION_IN` and `EXTENSION_OUT` in the function module.
+   - The function module shouldn't raise any exceptions; instead, the error message should be captured in the `RETURN` structure. The error message should be easily understandable.
+   - The function module shouldn't generate any screen output or display any dialog boxes.
+   - The function module shouldn't terminate the program. Any errors should be sent to the caller with the appropriate message type in the `RETURN` structure.
+   - No `COMMIT WORK` statement should be executed in the BAPI. This allows for calling multiple BAPIs in one LUW.
+   - Wherever possible, every BAPI should execute its own authorization checks.
+   - Individual parameters of the function module interface should be referred to the components of the BAPI structure.

# Defining the Business Object Type in BOR

Once the function module is developed, the BAPI is defined as a method of the business object type. SAP provides a wizard that can add the function module as an API method to the business object type. Using BOR, you can define your own business object types or create a subtype for an existing business object type.

To add the BAPI as a method to the business object type, proceed with the following steps:

+   1. Open an existing business object type or create a new business object type as per your requirements via Transaction SWO1.