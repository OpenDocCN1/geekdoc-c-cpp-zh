# 14.6 Displaying and Hiding Screen Elements Dynamically

You've seen that selection screen fields can be hidden manually by using a variant, but if you want to dynamically display or hide selection screen fields, you can handle that task programmatically in the code. For example, say you want to show certain fields to the user or hide fields based on user authorization; you can address this programmatically.

To manipulate the selection screen fields programmatically, use the `AT SELECTION-SCREEN OUTPUT` event. Because this event is called in the PBO event of the selection screen, we can change the field attributes before the selection screen is displayed to the user.

All the screen fields and their attributes are transferred through a special table called `SCREEN`. We can loop this table to access individual screen field attributes and manipulate them accordingly.

Figure 14.20 shows the components of the screen structure.

![](bbox=[0.148, 0.463, 0.857, 0.823])

**Figure 14.20** Components of Screen Structure