Not every property associated with a Field object is valid at a particular time. Some properties are set only after the field contains data or when the field is involved in an index. For example, the Value property of the Field object cannot be referenced directly from code. Instead, you set or get the value of a field only through the field's membership in a Recordset object. The On Error Resume Next statement allows this code to run, in spite of invalid properties. The errors that may occur when invalid properties are referenced by this code are ignored.

# Understanding ADO Objects

The ADO object model is shown in Figure 28.4. As you can see, the ADO object model is flatter and simpler than the DAO model and includes only a few objects. Notice that the ADO object model is not hierarchical. Each object stands alone and is not subordinate to another object in the model.

FIGURE 28.4
The ADO object model.

![](bbox=[0.22, 0.52, 0.72, 0.78])

Using ADO objects requires a reference to the ADO library. Figure 28.5 shows the References dialog box (opened by choosing Tools → References in the VBA Editor window) with the ADO library (Microsoft ActiveX Data Objects) selected. The exact version of the ADO library installed on your machine may vary, and, in fact, there may be more than one ADO library in the References dialog box. Select the highest-numbered library if you want to use the latest version available to Access. You may want to select a lower-numbered library to maintain compatibility with an existing system.