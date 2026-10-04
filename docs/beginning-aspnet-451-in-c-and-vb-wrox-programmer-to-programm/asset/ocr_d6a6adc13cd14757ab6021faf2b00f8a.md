5. Request Default.aspx in your browser by right-clicking it and choosing View in Browser. You now will see the web page with images from the DarkGrey theme, shown in Figure 6-18, that displays the page in Apple’s Safari.

![](bbox=[0.166, 0.173, 0.712, 0.473])

FIGURE 6-18

6. Go back to VS, open the Web.config file, and switch the two theme attributes of the <pages> element from DarkGrey to Monochrome. Open Default.aspx in your browser and you will see the page with the new theme and images as shown in Figure 6-19 that displays the page in Google Chrome. If you still see the old page, press Ctrl+F5 to cause a hard refresh. If you find that the page in the browser is showing a combination of the two themes, go back to VS, open Web.config, and merge the StyleSheet attribute from the <pages> element.

![](bbox=[0.166, 0.653, 0.712, 0.933])

FIGURE 6-19