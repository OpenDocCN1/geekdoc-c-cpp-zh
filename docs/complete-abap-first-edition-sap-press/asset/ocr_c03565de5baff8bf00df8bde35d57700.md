+   6. To print payer details, open the SAP script editor for the payer window and maintain the text as shown in Figure 18.16. Here, you're printing the data from the `wa_kna1` data object of the driver program.

![](bbox=[0.142, 0.18, 0.479, 0.338])

**Figure 18.16** Payer Window

+   7. Print the item details of the document in the main window (window of type `MAIN`). A main window is divided into three areas: the `TOP`, `BODY`, and `BOTTOM` areas. When the `MAIN` window is called in the driver program, the composer automatically takes care of printing the text in the top area above the body. Once the body contents are outputted, the composer will print the text in the bottom area.

The top area and bottom area are triggered by the text in the body. If the body is empty, then the text in the top and bottom areas will not be printed. The composer will remember the contents of the top and bottom areas and will print them on all pages. Among other things, you can use the top area to print column headings and the bottom area to print subtotals. The top and bottom areas are specified in the form using the `/;TOP...ENDTOP` and `/;BOTTOM...END BOTTOM` control commands, as shown in Figure 18.17.

![](bbox=[0.142, 0.684, 0.741, 0.863])

**Figure 18.17** Main Window