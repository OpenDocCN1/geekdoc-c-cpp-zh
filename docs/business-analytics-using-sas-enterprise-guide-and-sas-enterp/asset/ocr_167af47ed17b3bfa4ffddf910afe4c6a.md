# Output 8.4: View Subtree Assessment Plot

![](bbox=[0.115, 0.145, 0.557, 0.503])

If the error begins to increase, you should limit the number of leaves or prune the tree. For more information on pruning decision trees, see *Decision Trees for Analytics Using SAS® Enterprise Miner*, by Barry de Ville and Padraic Neville (2013).

# Node Characteristics

Three dimensions of the tree output help you visually interpret the results:

+   - *Shading*: When the shading is darker, the percentage of the target group MULTI_SUBS > 1 is higher.
+   - *Line Width*: The width or thickness of the connecting lines represents the volume of records going to the node.
+   - *Node Values*: Each node displays values for the records for both the model and validation data subsets within that node.
+     - *Node Id*: This simple identifier makes it easy to identify the exact node.
+     - *Percentage*: The percentage of the target variable represents DMR customers who have more than one subscription.
+     - *Count*: The count is the number of DMR customers in that node.