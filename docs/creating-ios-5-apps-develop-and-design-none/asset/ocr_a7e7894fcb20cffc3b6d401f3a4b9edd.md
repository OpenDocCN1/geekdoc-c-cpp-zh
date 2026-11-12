![](bbox=[0.09, 0.13, 0.73, 0.46])

# ### FIGURE 6.2 Setting the document type

With the application icon and Health Beat target still selected, click the Info tab. Now, click the Add icon and select Add Document Type from the pop-up menu. This will create a single untitled document type. Expand the document type and make the following changes. Enter **Health Beat History** in the Name field. Enter `com.freelancemadscience.hhistory` in the Types field. Next, expand "Additional document type properties," add a `CFBundleTypeExtensions` key, and set its Type to **Array**. Next, add an `LSHandlerRank` key and set its Value to **Owner**. Finally, expand `CFBundleTypeExtensions` and add a single string sub-item named `hhistory`.

We don't need to worry about creating document icons. iOS will automatically create our icons based on our application icons (see Chapter 9). If you want additional information on creating document-specific icons, check out the section "Custom Icon and Image Creation Guidelines" in Apple's iOS Human Interface Guidelines.

The entry should now match **Figure 6.2**.

Since we've defined a custom document type, we must now export it. Click the Add button again and select **Add Exported UTI**. Then expand the untitled UTI. Type **Health Beat History** in the Description field and `com.freelancemadscience.hhistory` in the Identifier field. Now expand "Additional exported UTI properties," add a `UTTypeTagSpecification` key, and set its Type to **Dictionary**. Expand the dictionary, add a `public.filename-extension` sub-key, and set its Type to **Array**. Finally, expand the array and add a single item to it. Set this item's Value to `hhistory`. The exported UTI should now match **Figure 6.3**.