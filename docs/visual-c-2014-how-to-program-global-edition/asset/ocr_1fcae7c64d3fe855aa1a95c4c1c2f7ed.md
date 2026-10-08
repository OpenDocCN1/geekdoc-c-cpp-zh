# Chapter 15 Graphical User Interfaces with Windows Forms: Part 2

| Name | Category | Price | Name | Category | Price |
| Soda | Beverage | $1.95 | Chicken Alfredo | Main Course | $13.95 |
| Tea | Beverage | $1.50 | Chicken Picatta | Main Course | $13.95 |
| Coffee | Beverage | $1.25 | Turkey Club | Main Course | $11.95 |
| Mineral Water | Beverage | $2.95 | Lobster Pie | Main Course | $19.95 |
| Juice | Beverage | $2.50 | Prime Rib | Main Course | $20.95 |
| Milk | Beverage | $1.50 | Shrimp Scampi | Main Course | $18.95 |
| Buffalo Wings | Appetizer | $5.95 | Turkey Dinner | Main Course | $13.95 |
| Buffalo Fingerers | Appetizer | $6.95 | Stuffed Chicken | Main Course | $14.95 |
| Potato Skins | Appetizer | $8.95 | Apple Pie | Dessert | $5.95 |
| Nachos | Appetizer | $8.95 | Sunday | Dessert | $3.95 |
| Mushroom Caps | Appetizer | $10.95 | Carrot Cake | Dessert | $5.95 |
| Shrimp Cocktail | Appetizer | $12.95 | Mud Pie | Dessert | $4.95 |
| Chips and Salsa | Appetizer | $6.95 | Apple Crisp | Dessert | $5.95 |
| Seafood Alfredo | Main Course | $15.95 | | |

**Fig. 15.52** Food items and prices.

**15.10 (Using TabPages)** Create an app that contains three TabPages. On the first TabPage, place a Checked1Box with six items. On the second TabPage, place six TextBoxes. On the last TabPage, place six LinkLabels. The user's selections on the first TabPage should specify which of the six LinkLabels will be displayed. To hide or display a LinkLabel's value, use its Visibl1 property. Use the second TabPage to modify the web page that is opened by the LinkLabels.

**15.11 (MDI Drawing Programs)** Create an MDI app with child windows that each have a Panel for drawing. Add menus to the MDI app that allow the user to modify the size and color of the paintbrush. When running this app, be aware that if one of the windows overlaps another, the Panel will be cleared.