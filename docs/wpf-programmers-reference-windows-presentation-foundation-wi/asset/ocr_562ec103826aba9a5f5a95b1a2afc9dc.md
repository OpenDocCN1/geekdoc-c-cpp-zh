Finally, the code uses the XpsDocumentWriter's Write method to write the document's paginator into the print queue.

Figure 17-6 shows the PrintFlowDocument program running in TwoPage, so it displays two pages of the FlowDocument's contents.

![](bbox=[0.095, 0.187, 0.659, 0.0050030000000000005])

FIGURE 17-6

The program displays its FlowDocument inside a FlowDocumentReader. Note that the format of the program's printout depends on the reader's mode when you make the printout. Figures 17-7 through 17-9 show the results when the reader is in Page mode, TwoPage mode, and Scroll mode, respectively.

Figures 17-7 and 17-8 look a lot like previous versions, although the printed results are smaller than they appear in the figures. The figures make it look like each page is fully full, but when printed, the results occupy only the upper third of the printed page.

![](bbox=[0.095, 0.703, 0.501, 0.918])

FIGURE 17-7

![](bbox=[0.515, 0.703, 0.859, 0.918])

FIGURE 17-8