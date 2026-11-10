![](bbox=[0.145, 0.093, 0.616, 0.248])

**Figure 2.12** Package Builder Initial Screen

3. After clicking the CREATE button, a dialog box will appear. In the CREATE PACKAGE dialog box, maintain the attributes of the package, as shown in Figure 2.13, and click OK. Only the SHORT DESCRIPTION field is mandatory.

The following are the important attributes:

+   - PACKAGE: Provide the name of the package.
+   - SHORT DESCRIPTION: Provide a short description for your package.
+   - APPLICATION COMPONENT: Use the [F4] help to select the appropriate application component based on the development objects that will be saved in this package.
+   - SOFTWARE COMPONENT: This is selected as HOME for customer packages.
+   - TRANSPORT LAYER: Select the transport layer based on the target system for the objects. You may have to consult your manager or SAP Basis administrator to select the correct transport layer.
+   - SUPERPACKAGE: Packages can be nested, so you can embed one package into another in a package hierarchy. This allows for better modularization. Provide the name of the superpackage in this field if you want to nest the current package as a subpackage in an existing package.
+   - PACKAGE TYPE: Select the package type that you wish to create. You can create the package as a STRUCTURE PACKAGE, MAIN PACKAGE, or DEVELOPMENT PACKAGE:
+     - STRUCTURE PACKAGE: This forms the top level in the package hierarchy. You can add main packages to a structure package.
+     - MAIN PACKAGE: A main package acts as a container for development objects that are semantically linked. A main package contains subpackages (of