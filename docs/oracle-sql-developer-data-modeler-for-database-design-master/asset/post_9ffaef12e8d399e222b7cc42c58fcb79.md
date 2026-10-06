
## 44 Oracle SQL Developer Dataameler for Database Design Mastery

![](img/431f8ac8f273fa89a28377c500ed60d7_70_0.png)

**FIGURE 3-1.** The toolbar and the bubble help for New Entity created based on this entity. If you define the Synonym To Display setting for an entity, that is the name used in diagrams for the entity, not the Name setting. If this entity is a subentity, you can select the supertype for the list Super Type. You can learn more about subtypes and superstypes in Chapter 4.

If you already know some attributes, you can add them to your design on the Attributes tab in the Entities Properties dialog, as shown in Figure 3-3. You can add an attribute at the end of the list by clicking the green plus sign. If you want to add an attribute before the selected attribute, hold the SHIFT key and click the green plus sign. If you want to add an attribute after the selected attribute, hold the CTRL key and click the green plus sign. If your attributes are in the wrong order, select the one you want to move and click the blue arrow up or down depending on which direction you want to move the attribute. If you want to modify the attribute properties, select the attribute in the list and click the Properties icon (the pencil icon) shown in Figure 3-3. For an attribute, you must define the name, and you can

## Chapter 3: Introducing Requirements Analysis 45

![](img/431f8ac8f273fa89a28377c500ed60d7_71_0.png)

FIGURE 3-2. General properties for an entity

define the data type: Domain, Logical, or Structured. If you have defined your own user data types of collection or distinct, those can be selected for a data type as well. There are always predefined data types for structured data types in Data Modeler; therefore, that data type is available even though you have not defined any. Depending on which one you select, the Type list will show you the available types for that category. If you want to see only the preferred list (defined in Preferences, as covered in Chapter 2), select Preferred. You can decide whether this attribute is the primary key by selecting Primary UID, and you can also define the attribute as mandatory by selecting Mandatory.

You can write three kinds of descriptions about an attribute: comments, comments in the relational database management system (RDBMS), and notes. Comments in the RDBMS are documentation that can be taken all the way to the database to describe an attribute that will be engineered as a column in a database. In the RDBMS field, you should enter a description that will help people use your database correctly. This text appears in the database and is the only description people not using Data Modeler or its reports can see.

## 46 Oracle SQL Developer Data Modeler for Database Mastery

![](img/431f8ac8f273fa89a28377c500ed60d7_72_0.png)

FIGURE 3-3. Properties for an attribute

> TIP
> Use Comments in RDBMS to describe how to use the database for users who do not have access to Data Modeler or its reports. Use Comments for formal documentation, and use Notes for informal documentation.

The Comments field is a description of this attribute, and people using Data Modeler can read it. It could be the official description that other users will see. Notes are usually informal notes and typically written during a planning session. Probably during the requirements analysis, the Notes field would be the best place to make notes. Afterward, you can use the descriptions in Notes and edit them to be more formal to be inserted into the Comments or Comments In RDBMS field.

## Chapter 3: Introducing Requirements Analysis 47

> TIP
> You can document everything you hear in modeling sessions and meetings and put them in Notes and afterward edit copy/move the descriptions you like from Notes to Comments in RDBMS or to Comments.

If you have any information about the volumes or growth rates of an entity, you can add that information on the Volume Properties. This information is only for documenting purposes; it will not be used for estimating space needed for the database (except DB2). Even though this information might not be used automatically, it is important information for the database design.

Every object in Data Modeler has a summary. The Summary tab tells not only the object ID used in XML files but also the creator and creation time of this object and who changed it the last time and what was. Figure 3-4 shows the Summary tab for an entity.

![](img/431f8ac8f273fa89a28377c500ed60d7_73_0.png)

**Figure 3-4.** Summary properties

## 48 Oracle Developer Data Modeler for Database Design Mastery

Relationships also have properties, which can be changed when more knowledge about the relationship becomes available. You can see and edit the properties by selecting the relationship in the Browser pane, right-clicking and selecting Properties, or by double-clicking the relationship on the logical model canvas. Figure 3-5 shows the general relationship properties. You can define a name for a relationship; otherwise, the default name is used. Using the default name is not best when you have many relationships similar to each other you need to know which is or when you have a many-to-many relationship that will be engineered to a new table with the name of the relationship. If you want to add a description for the role in the role, select the Name. This text appears in the database and is the only description people not using Data Modeler or its reports can see.

There is one more concept I like to point out: subviews. If you have many entities, it can be difficult to model. Subviews are subsets of the whole picture called subviews, which can be shown in Figure 3-6.

![](img/431f8ac8f273fa89a28377c500ed60d7_74_0.png)

## Chapter 3: Introducing Requirements Analysis 49

![](img/431f8ac8f273fa89a28377c500ed60d7_75_0.png)

relationships. You can create a subview in one of these ways:

- Go to the Browser pane, select SubView, right-clicking and select New SubView.
- Right-click the logical model canvas and select New SubView.
- Select the objects you want while holding the CTRL key, right-click, and select SubView From Selected.
- Select the central entity in the diagram, right-click, and select SubView From Selected.

FIGURE 3-6. Selecting objects to a subview

You can add objects to your subview by right-clicking the canvas and selecting Objects/Remove Object. You can read more about subviews in Chapter 4.

## Gathering Requirements for the Process Model

During the requirements analysis, the database designer might want to document the data processes. You can do that by right-clicking Data Diagrams under Process Model in the Browser pane and selecting New Data Flow Diagram. The processes are the functional side of the data, which more or less consist of data flows to design how the data flows through the system, and transformation packages, which can be used for data warehouse purposes to extract, transform, and load (ETL). Data Modeler supports all the elements needed for process modeling:

- processes
- composite processes with unlimited levels of decomposition
- transformation tasks
- triggering events
- information stores
- external agents
- external data elements
- source-target mapping for data elements
- create, read, update, delete (CRUD) dependencies between primitive process and data elements

## Introducing Data Flow Diagrams

![](img/431f8ac8f273fa89a28377c500ed60d7_76_0.png)

A data flow diagram is a formal, structured notation that models a functional process. A data flow diagram consists of processes, information stores, external agents, and data flows. A process is an activity or function that is performed. In an ideal case, each process should include only one activity. The difference between a primitive and a composite process is that a primitive process is a single process, while a composite process consists of several processes. An information store is a collection of data that is permanently stored. An external agent is an external effector: a role, organization, or system that is external to the system but interacts with it. A data flow shows how information flows in the process. An event triggers the execution of a process. A note can be used in the diagram to show important information in textual format. Figure 3-8 shows example of a data flow diagram.

![](img/431f8ac8f273fa89a28377c500ed60d7_77_0.png)

Figure 3-8. Data flow diagram
