*Selection screens allow users to select what information they see in a specific application. This chapter discusses how to design events that occur in a selection screen.*

# 14 Selection Screens

*Selection screens* are special screens created by using specific ABAP statements. Unlike dialog screens, which are created in Screen Painter, selection screens are auto-generated and don't require manual design. Selection screens are used when a user can provide the selection criteria to restrict the data processed by a program.

In this chapter, we'll look at the features of selection screens. We'll start by discussing how to define selection screens in Section 14.1. When the selection screen is processed, the ABAP runtime environment triggers different selection screen events that allow us to prepare and process input fields on the selection screen. We'll explore the selection screen events in Section 14.2 and how these events can be used for validating user input in Section 14.3. A selection screen can contain many input fields to restrict the data being processed by the program.

Often, users run a report frequently with same set of inputs. For example, a user may input same selection criteria to check daily stock movements for a particular plant each time he runs the report. To avoid having to repeatedly input the same selection criteria each time the report is run, we can create a selection screen variant to save the selection criteria. We'll discuss how to create and use selection screen variants in Section 14.4.

Reports can be executed online by the user through an SAP GUI screen or they can be scheduled to execute in the background. Background execution of a program is useful if the program is processing huge amounts of data and takes a long time to complete execution. Sometimes, a user may also want to run a report at a fixed time of day at regular intervals. We'll discuss how to execute programs in the background in Section 14.5.