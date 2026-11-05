your code while you’re typing code or building your project. This is where Code Contracts become interesting and add the most value for me.

![](bbox=[0.153, 0.137, 0.848, 0.655])

*Figure 5: Code Contracts Property Page*

# Static checking

If you enable static checking, it is advisable to keep the **Check in background** option selected in the Properties page. This is because analysis can take some time to perform. Another advisable option is to select the parallel build option in Visual Studio. From the **Tools** menu in Visual Studio, select **Options**. In the tree-view on the left of the Options screen (Figure 6), expand the **Projects and Solutions** node. You will notice a node called **Build and Run**. Select that, and you will see the option to enable parallel builds.

Any value greater than **1** will enable the parallel builds option in Visual Studio. The default value on my machine is **8**. Entering the value **1** in this text box will effectively switch off parallel builds in Visual Studio. By enabling parallel builds in Visual Studio, you enable Code Contracts to