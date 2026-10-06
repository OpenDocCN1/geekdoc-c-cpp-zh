# 172 Oracle SQL Developer Data Modeler for Database Design Mastery

![](bbox=[0.125, 0.135, 0.831, 0.535])

**Figure 7-4.** DDL Generation Options dialog

you can select some tables and deselect others, and only the ones you have selected will be included in the DDL generation.

Below these tabs there a Design Rules button. This button enables you to run a check for the predefined design rules on the current design for any violations. It probably be wise to use this and fix any violations before generating the DDLs. If the Include Comments option is selected, the DDLs will include the comments defined in the relational model. There is also a list of supported DDL types: Regular DDL, Advanced Interactive DDL, and Advanced CL DDL. Regular DDL generates regular DDL, while Advanced Interactive DDL and Advanced DDL support interactive scripts. At the beginning of the generated DDL script (in the comments), you can see what kind of interactive support script type has and what privileges are needed for that functionality. The regular DDLs look like the example you saw earlier in this chapter when creating a table called Order.