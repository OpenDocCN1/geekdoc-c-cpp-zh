# Create the CheckoutController component

+   1. In Solution Explorer, right-click the Delegates solution, point to Add, and then click New Project.

+   2. In the Add New Project dialog box, in the left pane, expand Windows, and then click the Universal node. In the middle pane, select the Class Library (Universal Windows) template. In the Name box, type CheckoutService, and then click OK.

+   3. In Solution Explorer, expand the CheckoutService project, right-click the file Class1.cs, and then click Rename. Change the name of the file to CheckoutController.cs and then press Enter. Allow Visual Studio to rename all references to Class1 as CheckoutController when prompted.

+   4. Right-click the References node in the CheckoutService project, and then click Add Reference.

+   5. In the Reference Manager – CheckoutService dialog box, in the left pane, click Solution. In the middle pane, select the DataTypes project, and then click OK.
+   The CheckoutController class will use the Order class defined in the DataTypes project.

+   6. In the Code and Text Editor window displaying the CheckoutController.cs file, add the following using directive to the list at the top of the file:

```
using DataTypes;
```

+   7. Add to the CheckoutController class a public delegate type called CheckoutDelegate, as shown in the following in bold:

Click here to view code image

```
public class CheckoutController
{
    public delegate void CheckoutDelegate(Order order);
}
```

You can use this delegate type to reference methods that take an Order parameter and that do not return a result. This just happens to match the shape of the AuditOrder and ShipOrder methods of the Auditor and Shipper classes.

+   8. Add a public delegate called CheckoutProcessing based on this delegate type, like this:

Click here to view code image

```
public class CheckoutController
{
    public delegate void CheckoutDelegate(Order order);
    public CheckoutDelegate CheckoutProcessing = null;
}
```