
## FIGURE 30.11

Set the Show Add-in User Interface Errors property to see Ribbon errors.

![](img/1e45673ab6eca9d20e67635ff5b9b318_1012_0.png)

## Creating a Custom Ribbon

Creating Access Ribbons is, at minimum, a five-step process. Each of these steps is described in detail in the following sections. Later you'll see more examples of these steps.

### Step 1: Design the Ribbon and build the XML

As with most database objects, the first step to creating a new Access Ribbon is to design it carefully. If you're converting an existing toolbar or menu to an Access Ribbon, you have a pretty good idea of the controls and other items to add to the Ribbon.

The XML document you create for your Ribbon mirrors the design you've laid out. Perhaps the most challenging aspect of composing the Ribbons XML is visualizing how the Ribbon will look, based on the XML behind it. There are no visual cues in a Ribbon XML document

that hint at the Ribbon’s appearance when rendered in Access. Experience will be your best guide as you work with Ribbon customization, and sometimes trial and error is the only way to achieve a desired objective.

As a final point, Access is extremely fussy about the XML used to compose Ribbons. There is no “parser” in Access that validates the XML as a Ribbon is rendered. If an error exists in the XML document, Access refuses to render the Ribbon, or the Ribbon will be missing elements defined in the XML. This is one reason that using a good XML editor to compose your XML is important. Most often, the only way you know that an error exists in your Ribbon XML code is that Access loads the default Ribbon instead of your custom Ribbon.

Inevitably, Ribbon development in Access requires a number of back-and-forth cycles in which you modify the XML, transfer it to Access, and view the results. You have no way of really knowing how well your XML will work as a Ribbon specification until Access renders the Ribbon on the screen.

“The Basic Ribbon XML” section later in this chapter describes the fundamental XML statements required by Access Ribbons.

For this example, we’ll create a new tab on the default Ribbon. The new tab will be named “Messages” and will contain one control that opens a form. First, design a form with one Label control on it containing a message to be displayed. Figure 30.12 shows the form frmMessage, which can be found in the Chapter30.accdb database.

## FIGURE 30.12

A simple form that displays a message.

![](img/1e45673ab6eca9d20e67635ff5b9b318_1013_0.png)

To create the XML that will define the new Ribbon elements, open your favorite XML editor. The examples in this chapter use the XML Notepad application, available for free from Microsoft.com (www.microsoft.com/en-us/download/details.aspx?id=7973). Figure 30.13 shows the XML in XML Notepad.

## FIGURE 30.13

XML Notepad can be used to write XML.

![](img/1e45673ab6eca9d20e67635ff5b9b318_1014_0.png)

In XML Notepad, you can choose Source from the View menu to see the XML that is generated. Here’s the XML for Message.xml:

```
```xml
<?xml version="1.0" encoding="utf-8"?>
<customUI xmlns="http://schemas.microsoft.com/office/2009/07
    /customui" onLoad="onRibbonLoad">
  <ribbon startFromScratch="false">
    <tabs>
      <tab id="ch30_t_Messages" label="Messages">
        <group id="ch30_g_Messages" label="Show">
          <button id="ch30_b_Message" label="Show Message"
            imageMso="GroupLayout" size="large"
            onAction="ShowMessage" />
        </group>
      </tab>
    </tabs>
  </ribbon>
</customUI>
```
```

## ### 1.2 认识三角形（2）

1. 如图，在△ABC中，D为BC上一点，∠1=∠2，∠3=∠4，∠BAC=63°，求∠DAC的度数。

![](img/1e45673ab6eca9d20e67635ff5b9b318_1016_0.png)

2. 如图，在△ABC中，∠ABC=∠C，BD⊥AC，∠ABD=30°，求∠C的度数。

![](img/1e45673ab6eca9d20e67635ff5b9b318_1016_1.png)

3. 如图，在△ABC中，∠A=40°，∠B=72°，CE平分∠ACB，CD⊥AB于D，DF⊥CE，求∠CDF的度数。

## Part VII: Advanced Access Programming Techniques

## FIGURE 30.16

Specifying the new custom Ribbon in the Current Database options dialog box.

![](img/1e45673ab6eca9d20e67635ff5b9b318_1019_0.png)

When you close the Access Options dialog box after selecting a new Ribbon Name, Access displays a message that you must close and reopen the database for the changes to take effect. Figure 30.17 shows the message displayed.

## FIGURE 30.17

Changes to the Ribbon Name property require a restart of the application.

![](img/1e45673ab6eca9d20e67635ff5b9b318_1019_1.png)

## FIGURE 30.18

The XML produces new Ribbon elements that open a form.

![](img/1e45673ab6eca9d20e67635ff5b9b318_1020_0.png)

Once Access is restarted, the new tab shows on the default Ribbon. Figure 30.18 shows the new tab, the Show group on that tab, the lone Show Message button, and the form that is opened when the button is clicked.

## The Basic Ribbon XML

Take a closer look at the basic XML required by Ribbons. The following XML represents a prototype Ribbon. (Line numbers have been added to make the discussion following this XML easier to understand.)

```
```xml
<?xml version="1.0" encoding="utf-8"?>
<!-- This is a comment in the ribbon's XML -->
<customUI xmlns="http://schemas.microsoft.com/office
    /2009/07/customui" onLoad="onRibbonLoad">
<ribbon startFromScratch="true">
    <tabs>
        <tab id="tab1" ...
```

```
```xml
7       <group id="group1" ... >
8           ... Controls go here ...
9       </group>
10      </tab>
11  <tab id="tab2" ...
12      <group id="group2" ... >
13          ... Controls go here ...
14      </group>
15      ... Repeat Groups ...
16  </tab>
17  ... Repeat Tabs ...
18  </tabs>
19 </ribbon>
20 </customUI>
```
```

The first statement (`<?xml version="1.0" encoding="utf-8"?>`) is not required by and does not affect Access Ribbons. It’s completely your choice whether to keep this line or not in the USysRibbons table. Well-formed XML includes the version line, and it helps other programs to render the file, so it’s a good practice to include it. Line 2 shows how to add a comment to a Ribbon’s XML code. The `<!--` and `-->` are standard commenting tags for XML documents.

Line 3 (beginning with `<customUI ...>`) specifies an XML namespace (xmlns), an XML document that predefines acceptable tags for the XML statements that follow. The Office namespace defines the Office Ribbon constructs, such as tabs, groups, controls, and so on. Every Ribbon defined in the RibbonXML field in USysRibbons must start with this statement, so be sure it’s included.

The statement in line 4 is rather important. The `startFromScratch` directive determines whether you’re building an entire Ribbon from scratch or modifying the default Ribbon by adding or taking things away. Depending on your situation, the majority of your custom Ribbons may be built from scratch because the default Ribbon knows nothing about the forms, reports, and other objects and operations in your database. Also, the default Ribbon contains commands that may be dangerous to your application’s integrity. For instance, a user could open a form, report, or table in Design view and make changes without your being aware of it. Removing these commands from the user interface is a first line of defense for your applications.

When `startFromScratch` is set to false, your custom Ribbon definition is added to the default Ribbon to the right of the built-in tabs. Because Access includes only five tabs by default, you may have enough room for your additional tabs without overcrowding the Ribbon. When `startFromScratch` is set to true, none of the default tabs, groups, or controls is shown on the Ribbon. Only what you include in the XML will be displayed.

Most of the tags in an XML file have a corresponding closing tag that defines the end of the section that relates to that tag. All the statements between the opening and closing tags are children of that tag. Lines 19 and 20 are the closing tags for the Ribbon and CustomUI elements, respectively.
