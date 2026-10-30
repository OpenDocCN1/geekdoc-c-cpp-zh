+   - **Functions** execute the statements within them and return a value, such as the result of a calculation.
+   - **Module:** Procedures are stored in *modules*. If statements are like sentences and procedures are like paragraphs, then modules are the chapters or documents of the VBA language. A module consists of one or more procedures and other elements combined as a single entity within the application.
+   - **Variable:** Variables are nothing more than a little piece of the computer’s memory that you reserve for your application and that you name so you can refer to it later. You temporarily store data in variables until your application needs them. In virtually all VBA programs, you create and use variables to hold values such as customer names, dates, and numeric values manipulated by the VBA code.

VBA is appropriately defined as a *language*. And just as with any human language, VBA consists of a number of words, sentences, and paragraphs, all arranged in a specific fashion. Each VBA sentence is a *statement*. Statements are aggregated as *procedures*, and procedures live within *modules*. A *function* is a specific type of procedure—one that returns a value when it’s run. For example, `Now()` is a built-in VBA function that returns the current date and time, down to the second. You use the `Now()` function in your application whenever you need to capture the current date and time, such as when assigning a timestamp value to a record.

# Starting with VBA Code Basics

Each statement in a procedure is an instruction you want Access to perform.

There are an infinite number of different VBA programming statements that could appear in an Access application. Generally, however, VBA statements are fairly easy to read and understand. Most often, you’ll be able to understand the purpose of a VBA statement based on the keywords (such as `DoCmd.OpenForm`) and references to database objects in the statement.

Each VBA statement is an instruction that is processed and executed by the VBA language engine built into Access. Here’s an example of a typical VBA statement that opens a form:

```
DoCmd.OpenForm "frmMyForm", acNormal
```

Notice that this statement consists of an action (`OpenForm`) and a noun (`frmMyForm`). Most VBA statements follow a similar pattern of action and a reference either to the object performing the action or to the object that’s the target of the action.

`DoCmd` is a built-in Access object that performs numerous tasks for you. Think of `DoCmd` as a little robot that can perform many different jobs. The `OpenForm` that follows `DoCmd` is the task you want `DoCmd` to run, and `frmMyForm` is the name of the form to open. Finally, `acNormal` is a modifier that tells `DoCmd` that you want the form opened in its “normal” view. The implication is that there are other view modes that may be applied to opening a form; these modes include Design (`acDesign`) or Datasheet (`acFormDS`) view, and Print Preview (`acPreview`, when applied to reports).