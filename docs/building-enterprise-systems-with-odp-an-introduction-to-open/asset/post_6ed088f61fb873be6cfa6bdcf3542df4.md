
are known by the system.” An example of such an invariant schema is shown in figure 3.1.

*A static schema* models assertions that must be true at a single moment in time. A common use of a static schema is to specify a given state of a set of information objects, in situations of particular interest to the modeller. For instance, it might describe the final state of a successful repair order.

## 3.3 Writing Information Specifications

This section describes how to use the concepts and structuring rules of the information language to write an ODP information specification. We need to describe the process of developing the specification, and the notation to use. RM-ODP does not impose any methodology to build the information specifications, but, to illustrate the ideas, we will follow a simple process by which we specify:

- 1. The types of the information objects and the types of the relationships between information objects.
- 2. The types of the information actions that can happen during the operation of the system.
- 3. A set of dynamic schemata that describe the behaviour of the objects when the actions occur.
- 4. A set of invariant schemata that describe the constraints on the system elements.
- 5. A set of static schemata which provide instantaneous views of the system or of any of its constituent objects.

There are many possible options for representing the information language concepts, depending on the experience and skills of the information modeller; Entity-Relationship Models (ERM), Object Role Models (ORM) or UML class diagrams can all be used. In this book, we will make use of the corresponding UML4ODP profile, which provides a set of UML elements to write information specifications in UML.

### 3.3.1 Information Object Types

In the first place, we need to specify the types of the information objects that model the data being handled by our ODP system. Information objects are generally specified in terms of their types, which in UML are expressed by classes stereotyped as «IV-Object».

![](img/b3a2d21424654c9a1d0654b2dce50e07_86_0.png)

FIGURE 3.1: Invariant schema showing information object types.

Figure 3.1 shows the ODP information object types of the PhoneMob information specification. Note that the information specification captures the information handled by the system, and there is no need to represent the computerized system itself (in contrast to the enterprise viewpoint specification).

The class diagram in figure 3.1 also expresses the allowed relationships between the information object types. For example, it defines that an information object representing a service centre should be related to the information objects that represent its staff, to the set of loan handsets owned by the shop (either in stock, or given to VIP users while their phones get fixed), and to the set of repair orders for which the centre is responsible. In turn, the information objects that represent such orders are related to the information objects that represent the broken handsets, the users that took them to the shop, and the records logging the different actions that have been performed on the broken phone since the repair order was opened.

Furthermore, the model specifies constraints on the kinds of objects and the kinds of associations that can appear in a valid information object configuration for the system (in terms of the multiplicities of the association ends or specific constraints on some of the objects, for instance).

All of these elements are defined within a UML package that is stereotyped as an «IV_InvariantSchema», which represents an ODP information invariant schema.

### 3.3.2 Information Action Types

In the information viewpoint, actions are used mainly for describing events that cause state changes of information objects. Figure 3.2 shows some of the action types of the PhoneMob system.

![](img/b3a2d21424654c9a1d0654b2dce50e07_87_0.png)

*FIGURE 3.2: Invariant schema showing selected information action types.*

In the UML representation, the information actions are expressed as action types within the invariant schema package. Information action types are expressed by UML signals stereotyped «IV_Action». Attributes of the signals represent the information conveyed by the ODP interactions expressed by such signals. Thus, the instances of the classes that represent the action occurrences will be expressed by signals, sent or received by the state machines of the corresponding information objects (see next section). Internal actions are expressed as internal transitions of the state machine for the information object concerned.

### 3.3.3 Dynamic Schemata

UML state machines can be used to describe the behaviour of information objects; state changes are triggered by signals that express information actions. Thus, the state machines express dynamic schemata. Note that a signal causes changes in all the state machines that define a transition for it, reflecting the fact that an ODP interaction may cause state changes in all the objects involved in it. In other words, an ODP interaction is a piece of shared behaviour.

Figure 3.3 illustrates the state machine of the Handset information object. This diagram shows not only the effect of the actions on the corresponding information objects, but also the states in which the actions are allowed, serving as pre- and post-conditions for those actions.

![](img/b3a2d21424654c9a1d0654b2dce50e07_88_0.png)

FIGURE 3.3: State machine for the Handset information object.

### 3.3.4 Invariant Schemata as Constraints

We have seen how invariant schemata can be used to specify the information object types and their relationships, but they can also be used to express other kinds of constraints on the information handled by the system.

For example, we may need to express the fact that no handset can be referenced simultaneously by more than one repair order, or that users should have unique names in the system. These kinds of invariant have already been incorporated into the UML class diagram that describes the information object types by choosing the multiplicity of the association ends, or adding some OCL constraints to the elements (see, for example, the constraints specified for classes User or RepairOrder in figure 3.1).

Other OCL constraints can be used to specify further restrictions on the model, or to express integrity constraints. For example, we could restrict the number of repair orders currently open in a centre, in accordance with a possible enterprise policy stating such a business rule, by simply adding an OCL constraint to the ServiceCentre information object type, as in the following fragment.

```
context ServiceCentre inv:
    self.repairOrder->select(status <> MaxOrderStatus::closed)->
                         size() <= MaxOpenOrders
```

Further invariant schemata can be specified in this way, defining the integrity constraints and well-formed rules of the information model that specifies the shared data model handled by the system.

### 3.3.5 Static Schemata

Sometimes it is very useful to be able to describe instantaneous views of the information, for example at system initialization, or at any other specific moment in time that is relevant to any of the system stakeholders. This specification of the instantaneous state of the objects is precisely the one provided by static schemata, which in UML are expressed by means of object diagrams.

![](img/b3a2d21424654c9a1d0654b2dce50e07_89_0.png)

FIGURE 3.4: Current state of an example RepairOrder.

For instance, the UML package shown in figure 3.4 expresses a possible state of one repair order, in which the order has been registered, the telephone tested and found faulty, and a loan handset has been assigned and given to the user. No further actions have been done for that order so far — for example, the faulty handset has not yet been sent to the manufacturer for repair.

## 3.4 Structure of the Information Specification

All the elements that constitute the information specification of the system are gathered together within a single model, stereotyped «Information_Spec». This model contains the set of packages that express the invariant, static and dynamic schemata of the information specification, structuring them in different packages for organizational purposes. Figure 3.5 depicts the «Information_Spec» model for the PhoneMob system.

![](img/b3a2d21424654c9a1d0654b2dce50e07_90_0.png)

FIGURE 3.5: Structure of the PhoneMob information specification.

Note that in this figure there is no package for the specification of dynamic schemata. Given that they are modelled in UML as state machines associated with the corresponding object types, splitting their specification across different packages does not make much sense.
