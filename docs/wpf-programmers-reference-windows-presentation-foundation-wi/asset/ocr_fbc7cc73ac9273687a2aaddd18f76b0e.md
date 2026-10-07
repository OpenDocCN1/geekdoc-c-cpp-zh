# # H Path Mini-Language

This appendix summarizes the Path mini-language (or markup syntax) that you can use to concisely define the lines and curves drawn by Path objects. Place mini-language commands in the Path control's Data property.

Table H-1 Path mini-language's commands. Uppercase versions use absolute coordinates, while lowercase versions use points relative to the previous points.

**TABLE H-1**: Path Mini-Language

| COMMAND | MEANING |
| --- | --- |
| F0 | Use Odd/Even fill rule. (See Figure H-1.) |
| F1 | Use Non-Zero fill rule. (See Figure H-1.) |
| M or | Move to the following point. |
| L or | Draw lines to the following points. |
| H h | Draw a horizontal line to the given X coordinate. |
| V or | Draw a vertical line to the given Y coordinate. |
| C or c | Draw a cubic Bézier curve. This command takes three points as parameters: two control points and an endpoint. The curve starts at the current point moving toward the first control point and ends at the endpoint moving away from the second control point. (See Figure H-2.) |
| S or | Draw a smooth Bézier curve. This command takes two points as parameters: a control point and an endpoint. The curve defines an initial control point by reflecting the control point from the previous s command. It then draws a cubic Bézier curve using the newly defined control point and the two parameter points. This makes the second curve smoothly join with the previous one. (See Figure H-2.) |

*continues*