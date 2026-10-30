
## FIGURE 21.39

The New Row Or Col property forces Access to start a column before or after a section.

![](img/1e45673ab6eca9d20e67635ff5b9b318_741_0.png)

Keep in mind that the measurement units you see on the Page Setup tab of the Ribbon are determined by the Windows international settings. For example, in Germany or Japan where the metric system is used, the units of measure will be centimeters instead of inches.

Also, you must allow for the margin widths set in the Margins gallery, accessed from the Page Setup tab of the Ribbon (see Figure 21.40).

For example, if you specify a Column Size Width of 3.5" and the left margin is set to 1", this means the right edge of the column will actually fall 4½ inches from the left physical edge of the paper, or more than halfway across an 8-x-11-inch sheet of paper printed in portrait mode. These settings will not allow two columns, each 3½ inches wide, to print on a standard letter-size sheet of paper. In this case, you might consider reducing the left and right margins until the 3½-inch columns fit properly. (Don't worry about setting the margins too small to work with your printer. Unless you're working with a nonstandard printer, Windows is pretty smart about knowing the printable area available with your printer and won't allow you to set margins too small.)

## FIGURE 21.40

All report page settings must consider the margin widths.

![](img/1e45673ab6eca9d20e67635ff5b9b318_742_0.png)

## Exploiting two-pass report processing

In Chapter 20, we mention that Access uses a two-pass approach when formatting and printing reports. We’ll now explore what this capability means to you and how you can exploit both passes in your applications.

The main advantage of two-pass reporting is that your reports can include expressions that rely on information available anywhere in the report. For example, placing a control with the Sum() function in a header or footer means that Access will use the first pass to accumulate the data required by the function, and then use the second pass to process the values in that section before printing them.

Another obvious example is putting an unbound text box in the footer of a report containing the following expression:

```
="Page " & [Page] & " of " & [Pages]
```

The built-in Pages variable (which contains the total number of pages in the report) isn’t determined until Access has completed the first pass through the report. On the second pass, Access has a valid number to use in place of the Pages variable.

The biggest advantage of two-pass reporting is that you’re free to use aggregate functions that depend on the report’s underlying record source. Group headers and footers can include information that can’t be known until the entire record source is processed.

## Part V: Working with Access Forms and Reports

There are many situations where aggregate information provides valuable insight into data analysis. Consider a report that must contain each salesperson’s performance over the last year measured against the total sales for the sales organization, or a region’s sales figures against sales for the entire sales area. A bookstore might want to know what portion of its inventory is devoted to each book category.

Figure 21.41 shows such a report. The Number of Customers, Total Sales, and Average Purchase information at the top of this report (rptSummary) are all part of the report header. In a one-pass report writer, the data needed to perform these calculations would not appear until the bottom of the page, after all the records have been processed and laid out.

## FIGURE 21.41

The summary information is part of the report’s header.

![](img/1e45673ab6eca9d20e67635ff5b9b318_743_0.png)

A glance at rptSummary in Design view (see Figure 21.42) reveals that the text boxes in the report header are populated with data derived from these mathematical expressions:

```
Number of Customers: =Count([CompanyName])
Total Sales: =Format(Sum([Purchases]),"Currency")
Average Purchase: =Format(Sum([Purchases]) / Count([CompanyName]), "Currency")
```

## FIGURE 21.42

rptSummary in Design view.

![](img/1e45673ab6eca9d20e67635ff5b9b318_744_0.png)

The Count() and Sum() functions both require information that isn't available until the entire report has been processed in the first pass. As long as Access can find the arguments provided to these functions (CompanyName and Purchases) in the underlying recordset, the calculations proceed without any action by the user.

## Assigning unique names to controls

If you use the Report Wizard or drag fields from the Field List when designing your reports, Access assigns the new text boxes the same names as the fields in the recordset underlying the report. For example, if you drag a field named Discount from the Field List, both the Name and Control Source properties of the text box are set to Discount.

If another control on the report references the text box, or if you change the Control Source of the text box to a calculated field, such as:

```
=IIF([Discount]=0,"N/A",[Discount])
```

you'll see #Error when you view the report. This happens because Access can't distinguish between the control named Discount and the field in the underlying recordset named Discount.

You must change the Name property of the control to something like txtDiscount so that Access can tell the difference between the control's name and the underlying field.

## Part VI

## Microsoft Access
Programming Fundamentals

Part VI introduces macro programming and explains the art and science of Visual Basic for Applications (VBA).

Long maligned as weaker or inferior to VBA, macros were often relegated to second-class citizenship in many Access developer tool-kits. However, as you’ll read later in this chapter, Microsoft introduced embedded macros, an efficient technique for automating many tasks in forms and reports. Chapter 23 takes a look at data macros, which enable you to perform important data-management tasks at the table level.

Starting with Chapter 24, Part VI turns your attention to automation with VBA. VBA provides functionality that goes far beyond simply opening forms and reports and controlling the user interface.

## IN THIS PART

- Chapter 22
  - Using Access Macros
- Chapter 23
  - Using Access Data Macros
- Chapter 24
  - Getting Started with Access VBA
- Chapter 25
  - Mastering VBA Data Types and Procedures
- Chapter 26
  - Understanding the Access Event Model
- Chapter 27
  - Debugging Your Access Applications

## ## 1. 引言

在当今快速发展的科技时代，人工智能（AI）已成为推动社会进步的关键力量。从智能助手到自动驾驶，AI 技术正深刻改变着我们的生活方式和工作模式。

本文旨在探讨 AI 技术在不同领域的应用现状及其未来发展趋势，为相关研究者和从业者提供参考。

## ## 2. AI 的主要应用领域

- 医疗健康：辅助诊断、药物研发
- 交通运输：自动驾驶、智能调度
- 金融服务：风险评估、智能投顾
- 教育培训：个性化学习、智能评估

## ## 3. 未来发展趋势

随着算力的提升和数据量的增长，AI 模型将变得更加复杂和智能。多模态学习、联邦学习等新兴技术有望解决当前 AI 面临的诸多挑战。

> > AI 的未来不仅在于技术的突破，更在于如何负责任地应用这些技术，确保其造福全人类。

综上所述，AI 技术正处于快速发展期，其应用前景广阔，但同时也伴随着伦理、安全等方面的挑战，需要社会各界共同努力。

Building macros consists of selecting actions from a drop-down list and then filling in the action’s arguments (values that provide information to the action). Macros let you choose actions without writing a single line of VBA code. The macro actions are a subset of commands VBA provides. Most people find it easier to build a macro than to write VBA code. If you’re not familiar with VBA, building macros is a great stepping-stone to learning some of the commands available to you while providing added value to your Access applications.

Suppose you want to build a main form with buttons that open the other forms in your application. You can add a button to the form, build a macro that opens another form in your application, and then assign this macro to the button’s Click event. The macro can be a stand-alone item that appears in the Navigation pane, or it can be an embedded object that is part of the event itself (see the “Embedded Macros” section, later in this chapter).

## Creating a macro

A simple way to demonstrate how to create macros is to build one that displays a message box that says “Hello World!” To create a new stand-alone macro, click the Macro button on the Macros & Code group on the Create tab of the Ribbon (shown in Figure 22.1).

## FIGURE 22.1
Use the Macro button on the Create tab to build a new stand-alone macro.

![](img/1e45673ab6eca9d20e67635ff5b9b318_749_0.png)

Clicking the Macro button opens the macro builder (shown in Figure 22.2). Initially, the macro builder is almost featureless. The only thing in the Macro Builder is a drop-down list of macro actions.

To the right of the Macro Builder you may see the Action Catalog. There are dozens of different macro actions, and knowing which action to use for a particular task can be an issue. The Action Catalog provides a tree view of all available macro actions and helps you know which action is needed to perform a particular task.

Select MessageBox from the drop-down list in the macro builder. The macro builder changes to display an area where you input the arguments (Message, Beep, Type, and Title) associated with the MessageBox action.

Set the arguments as follows:

- Message: Hello World!
- Beep: No
- Type: None
- Title: A Simple Macro
