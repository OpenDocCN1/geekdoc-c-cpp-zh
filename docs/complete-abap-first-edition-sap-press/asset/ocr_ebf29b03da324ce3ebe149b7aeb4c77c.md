Under the SCREEN AREAS section, note that information about the CALLING SCREEN and CALLED SCREEN with the respective program names and screen numbers is listed. To add custom fields, you edit the screen of the called screen. For example, in Figure 20.26, we're adding custom fields to screen 0101 of program SAPLXM06 to add extra fields to a PO header. The same fields should be added to the CI include of the purchase order header table. In this case, we'd add the fields to CI_EKKODB.

![](bbox=[0.142, 0.264, 0.772, 0.633])

**Figure 20.26** Components of Enhancement MM06E005

# 20.7.4 Menu Exits

*Menu exits enable you to add custom function codes to standard SAP applications. This allows you to provide additional functionality when the function code is selected. Customer function codes are named +CUS.*

For example, if you look at the GUI status for ABAP Editor (from ABAP Editor, follow the menu path SYSTEM • STATUS and double-click the GUI STATUS field), you'll see that a customer function code exists under the UTILITIES menu, as shown in Figure 20.27. When we implement the enhancement and activate it, the menu option will be added to ABAP Editor.