![](bbox=[0.08, 0.12, 0.88, 0.62])

Figure 5.107. The layout of the form

+   3. The user will enter the web address inside the TextBox and click the Button next to it for navigating to this address. Therefore, let's set the Name of the TextBox as addressTextBox, Name of the Button next to it as goButton and the Text property of this Button as Go.
+   4. Similarly, the middle Buttons will function as the navigation buttons of Back, Forward and Go Home operations. Therefore, we can set their Names as goBackButton, goForwardButton and goHomeButton. Their Texts will be Back, Forward and Home. We can also set the Name of the WebBrowser as smallWebBrowser. After these changes, the form will look as shown in Figure 5.108.
+   5. Double-click the Go button to create its default event handler goButton_Click(...). We will write the following code inside this method which will take the Text property of the addressTextBox and pass it to the Navigate() method of the WebBrowser so that the web