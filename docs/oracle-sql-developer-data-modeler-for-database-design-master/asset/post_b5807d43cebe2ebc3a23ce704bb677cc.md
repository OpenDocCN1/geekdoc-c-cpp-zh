
# Chapter 4: Introducing Conceptual Database Design (Logical Model) 59

defined with word types and their compulsions in the pattern. The word types supported by Data Modeler are Prime, Class, Modifier, and Qualifier, as defined in Chapter 2. A defined structure for an attribute could be, for instance, one optional mandatory word, one optional modifier, and one mandatory class word. Examples of this structure are "Temporary Company Delivery Address" or "Company Address." You can create a structure for an object name by clicking the green plus sign on the Design Properties Settings | Naming Standard for that object and selecting the word type from the list. Then you either select Mandatory to define this pattern as required or disable it as optional. You can add as many word types as you need for the pattern. You can remove word types from the pattern by clicking the red X button.

These naming standards will be checked against defined glossaries when you apply design rules, and any violations will be reported as warnings. You can use this functionality to make sure all words used in your design are defined in your glossary, and you can define one or more glossaries as validation glossaries on the Settings of the Design Properties dialog, as explained in Chapter 2. If you define more than one glossary, a name is considered to be valid if it is validated using any of the defined glossaries. You can use different glossaries, for instance, to represent areas of interest. One glossary could be for the marketing department, another for sales, and the third one for financials. Finally, you can share the design-level properties with other users, as described in Chapter 2.

> NOTE
Using glossaries for validation may cause problems if you have the same word in two glossaries.

![](img/431f8ac8f273fa89a28377c500ed60d7_85_0.png)

There are also properties that apply to the logical model level. Select Logical Model in the Browser pane, right-click, and choose Properties | Naming Options. You can specify the maximum length of a name and the character case (upper, lower, mixed). You can also select a set from the Valid Characters list or specify yours own or select All characters to be valid. You can set these settings for entities, attributes, and views. See Figure 4-1 for more details. If you try to create something that violates your naming options, you will get an error message immediately. For instance, if the Naming Options properties define that an entity name must be all uppercase but the designer creates an entity name with lowercase, an error message is given. If an element has been created before changing the naming options, it will be checked when the design rules are applied, and any violations by the Naming Options properties will be reported as errors. In Data Modeler version 4.0.2, the Naming Options settings cannot be shared with other users, but there are plans for future releases to provide this functionality.

# 60 Oracle SQL Developer Data Modeler for Database Design Mastery

![](img/431f8ac8f273fa89a28377c500ed60d7_86_0.png)

Figure 4-1. Naming options for a logical model

In addition to properties, you can set some preferences that affect the logical model. Choose the Tools | Preferences menu to open the Preferences dialog. You can make your design work easier and more comfortable by setting the preferences for the logical model the way you want Data Modeler to work. In Chapter 2 already saw how to define the notation used and how to define the preferred types, among others. In the Preferences dialog, select Data Modeler | Logical to see the settings for the logical model, as shown in Figure 4-2. By setting these preferences, you can define what the defaults will be when a new entity or a relationship to a relational model. You can change these defaults at any time to effect on new elements, and they can be changed in your logical model individually if wanted. You can define the source and target to be optional or mandatory (Source Optional, Target Optional). The source is where the relationship starts, and the target is where it enters. For instance, a Customer could be the source, and an Order be the target. A Customer might have many Orders (Source Optional, which means the relationship line on the source side is optional; a Customer can exist without an Order), but an Order must be by a Customer (Target Mandatory, which means the relationship line on the target side must be mandatory; an Order cannot exist without a Customer). In other words, if is a Customer, there is no need to have an Order, but if there is an Order, there must be a Customer. You can tell Data Modeler to define the first unique identifier as the primary key by selecting Use Set First Unique Key As Primary Key. There might be several unique keys in one entity, which helps the tool and the designer set one of them as the primary

# Chapter 4: Introducing Conceptual Database Design (Logical Model) 61

![](img/431f8ac8f273fa89a28377c500ed60d7_87_0.png)

FIGURE 4-2. Preferences for a logical model

key. I don't recommend this functionality since I want to define my own primary keys and be sure the right unique key will be selected, the first one. Another problem is that a unique key can have nulls, but a primary key cannot. So, if the first unique key is set as the primary key, all its attributes must have nulls allowed. It is not common to have several unique keys in one entity anyway. To see the preferences for a logical model for forward engineering and the preferences for the relational model, see Chapter 5.

> NOTE
Changing some preferences will affect only the elements created after the change.

62 Oracle SQL Developer Data Modeler for Database Design Mastery

## Introducing the Logical Model

When designing the database, it is valuable to start the design work as soon as possible in the project because when turning the requirements into a formal form, the designer may realize there are many questions that have not been asked. In fact, there are many ways of modeling techniques. You can't always say one way is better than another, but sometimes you can. The theory of logic will give you guidance in finding and choosing one definition over another. The relational theory helps when implementing the requirement in an ER model in the right way. For instance, an end user might simply say, "A customer must place an order." With that, the user might think that this statement defines a customer (that is, to be a customer at all, must place an order). In other words, the end user might think they have defined the concept of a customer. A person trained in logic realizes that that is not the case; there are many possible formal interpretations. The important task is to find out which of them is the one intended before modeling any solution. To clarify, the definition of a customer in the example could be any of the following:

- Every customer places at least one order.
- At least one customer places at least one order.
- There's at least one order that every customer places.
- Each customer places exactly one order.
- There's exactly one order that every customer places.

Or it could mean something.
In this case, it would be quite easy to find the right definition because a customer is a familiar concept to most people, but you will face the same kind of assertions about concepts you are not familiar with, and you still must be prepared to ask the right questions to be able to make the right decisions when modeling. You can find more information about logic and relational theory from several books on the topic, for instance written by C.J. Date.
It is important to be consistent on how you model, at least in one model. It is much easier to read and understand the model if the solution for the problem is always the same. C.J. Date says, "You can be consistent or you can be inconsistent, but never switching the time between the two." It is also important to understand that the goal is to model the target, not the whole world. One reason to have a clear and simple model is that this model will be your best tool when talking with end users. You might be surprised how well they can read and understand it.
