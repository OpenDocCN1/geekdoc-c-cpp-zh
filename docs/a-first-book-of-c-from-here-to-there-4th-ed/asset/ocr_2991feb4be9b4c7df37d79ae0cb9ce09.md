make this explanation more meaningful, think of a computer program that must track the number of parts in inventory. The required output for this program is a description of all parts carried in inventory and the number of units of each item in stock; the given inputs are the initial inventory quantity of each part, the number of items sold, the number of items returned, and the number of items purchased.

For these specifications, a designer could initially organize the program’s requirements into the three sections shown in Figure 1.14. This figure is referred to as both a top-level structure diagram and a first-level structure diagram because it represents the first overall structure of the program the designer has selected.

![](bbox=[0.25, 0.39, 0.78, 0.58])

Figure 1.14 A first-level structure diagram

After an initial structure is developed, it’s refined until the tasks in the boxes are completely defined. For example, the data entry and report modules shown in Figure 1.14 would be refined further. The data entry module certainly must include provisions for entering data. Because planning for contingencies and human error is the system designer’s responsibility, provisions must also be made for changing incorrect data after an entry is made and for deleting previous entries. Similar subdivisions for the report module can be made. Figure 1.15 is a second-level structure diagram for an inventory-tracking system that includes these further refinements.

![](bbox=[0.2, 0.8, 0.85, 0.95])

Figure 1.15 A second-level structure diagram with refinements