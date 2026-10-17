![](bbox=[0.282, 0.179, 0.714, 0.402])

# CREATING AND EDITING SNIPPETS

To create a snippet, drag the desired “template” code into the snippet library. The snippet will be added to the list of available snippets. To edit the snippet, select it in the library. When the pop-up window appears, click the Edit button in the lower-left corner. The pop-up will reveal editing controls (Figure 7.10).

You can set the title and description that appear in the library list, and the platform and language the snippet targets. You can also set a completion shortcut to use when editing code. Finally, you can edit the snippet itself. When you’re finished editing, click Edit or Done.

An example of a useful snippet is a ready-to-go set of the three primary NSTableViewDataSource protocol methods. When using this protocol to populate an NSTableView programmatically, the quickest way to get up and running used to be to copy the method signatures from the documentation and then insert the brackets, the if conditionals for determining the table being operated on, and so on. Now you need to define this only once, format it as you want, and then save it as a snippet for reuse in any future projects and workspaces.

You can also insert placeholder tokens that are the parts of the snippet (such as arguments) that must be filled in to complete the code. For example, to add a placeholder for an NSNumber argument, you would type <#NSNumber#> where the argument belongs. When the snippet is used, the text that appears between the hash marks is what will appear in the snippet. The token’s text should serve as a helpful prompt regarding what should be filled in when using the snippet.