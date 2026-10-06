# 4 Class and Object

| Line |
| - len : double |
| + Line(xp1 : Point, xp2 : Point) |
| + Line( Line &) |
| + GetLen() : double |

![](bbox=[0.155, 0.185, 0.871, 0.563])

| Point |
| - X : int |
| - Y : int |
| + Point(xx : int = 0, yy : int = 0) |
| + Point(p : Point &) |
| + GetX() : int |
| + GetY() : int |

Fig. 4.9: Relations between class Line and class Point.

Fig. 4.10: Generalization relation.

# 3. Comments

To represent classes, objects, and relations among them in a more lively fashion, UML uses some auxiliary symbols besides the basic symbols introduced above. Here we introduce comments.

Comments in UML are an important kind of symbol, and can exist independently. Comments are attached on elements or element sets for description or annotation. By commenting, we can add information like description and comment on the model. In UML, comments are represented as rectangles with angled folds and are linked to other elements of UML using a dashed line.

Example 4.6: Description of class Line and class Point with comments (see Figure 4.11).