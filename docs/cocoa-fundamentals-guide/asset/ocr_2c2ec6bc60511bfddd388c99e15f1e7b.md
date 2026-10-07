# Controls, Cells, and Menu Items

Most controls in AppKit inherit from the NSControl class. Although a control has the initial responsibility for sending an action message to its target, it carries the information needed to send the message. This, it usually relies on its cell or cells.

A control always has one or more cells—objects that inherit from NSCell—associated with it. Why is there this association? A control is a relatively "heavy" object that inherits all the combined instance variables of its ancestors, which include the NSView and NSResponder classes. Because cells are expensive, they are used to subdivide the real estate of a control into various functional areas. Cells are lightweight objects that can be used to overlay all or part of the control. It's not only a division of area, but a division of cells: cells handle the drawing that controls would otherwise have to do, and cells hold the data that controls them (instance variables for target and action). Figure 5-3 (page 184) depicts the control-cell architecture.

Abstract classes, NSControl and NSCell both implicitly handle the setting of the target and action instances. By default, NSControl simply sets the information in its associated cell, if one exists. NSControl itself supports, by default, one-to-one mapping between itself and subclasses of NSControl such as Matrix support multiple cells.) In its implementation, NSCell simply raises an exception. You must go one step further down the inheritance chain to find the cell that implements the setting of target and action: NSActionCell.

Objects derived from NSActionCell provide target and action values to their controls so they can compose and send an action message to the proper receiver. An NSActionCell object handles mouse (cursor) tracking by highlighting its area and assisting its control in sending action messages to the specified target. In most cases, the responsibility for an NSControl object's appearance and behavior is given to a corresponding NSActionCell object (NSMatrix, and its subclass NSForm, are subclasses of NSControl that do not follow this.)

**Figure 5-3** How the target-action mechanism works in the control-cell architecture

![](bbox=[0.181, 0.584, 0.819, 0.833])