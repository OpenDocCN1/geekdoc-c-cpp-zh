4. Next, select the entire row for the Id by clicking in the margin on the left (identified by the black arrow in Figure 12-19) and then on the Table Designer toolbar, visible in Figure 12-20, click the second button from the left (with the yellow low key on it) to turn the Id column into a primary key.

![](bbox=[0.52, 0.2, 0.9, 0.38])

FIGURE 12-20

5. Below the table definition you see the Column Properties, a panel that looks similar to the Properties Grid in VS. With the Id column still selected, scroll down a bit on the Column Properties grid until you see Identity Specification. Expand the item and then set (Is Identity) to Yes, as shown in Figure 12-21.

![](bbox=[0.13, 0.58, 0.8, 0.75])

FIGURE 12-21

6. Press Ctrl+S to save your changes. A dialog box pops up that enables you to provide a name for the table. Type Genre as the name and click OK to apply your changes. Then press Ctrl+F4 to close the table designer.

7. Create another table by following steps 2 and 3, but this time create a table with the following specifications to hold the CD and concert reviews for the Planet Wrox website.

| COLUMN NAME | DATA TYPE | ALLOW NULLS | DESCRIPTION |
|---|---|---|---|
| Id | int | No | The primary key and identity of the table. |
| Title | nvarchar (200) | No | Contains the title of the review. |
| Summary | nvarchar (max) | No | Contains a short summary or teaser text for the review. |
| Body | nvarchar (max) | Yes | Contains the full body text of the review. |