# How to work with the Item template

When you use the Web Forms Designer to create a FormView control and bind it to a data source, the Web Forms Designer automatically generates basic templates for the FormView control. For instance, the code in figure 15-13 shows a typical Item template. This template is used to display the data from the data source in ReadOnly mode.

As you can see, the Item template consists of a literal header and a label control for each field in the data source. The Text attribute of each label control uses either the Bind or Eval method for data binding. The Eval method is used for columns that can’t be modified. That’s the case for the ProductID column in the Products table, since this is the key column.

To control the format and layout of the data that’s displayed in ReadOnly mode, you can edit the Item template. To do that, it’s common to use CSS as described in chapter 5. In particular, it’s common to float the literal text to the left of the labels so the labels are left-aligned. You’ll see an example of this later in this chapter.

Note that if the data source includes Update, Delete, and Insert commands, the Item template will include command buttons that let the user edit, delete, or add new rows. Although these buttons are created as link buttons, you can easily change them to regular buttons or image buttons.