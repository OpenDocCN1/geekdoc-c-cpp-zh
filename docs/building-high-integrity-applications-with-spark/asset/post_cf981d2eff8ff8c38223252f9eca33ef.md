
confusing information flow results where inputs incorrectly appear to depend on values previously sent as outputs. Use a separate abstraction for each external variable as was done in package Serial_Port in Section 7.3.2.

Finally, we note that a variable abstraction package need not include any hidden external variables. The external entity to which our SPARK program communicates might be an API of some library, operating system, or cooperating software system.

## 8.3.3 Principles of the INFORMED Design Approach

The INFORMED technical report lists five guiding design principles.

### 1. Application-Oriented Aspects

SPARK aspects provide an expression of the behavior of the software independently of the actual code. This description is more useful if it is expressed in problem domain terms rather than in implementation terms. For example, we prefer to see the terms fuel valve rather than digital-to-analog converter #3.

### 2. Minimal Information Flow

To reason about the behavior of a system, we need to reason about the information that flows through it. Such reasoning is simplified if the information flows are minimized. Moving data from one part of the system to another increases the information flow complexity as measured by the Global and Depends aspects. Methods for minimizing information flow include

- Minimizing propagation of unnecessary details;
- Localizing and encapsulating of state information;
- Avoiding making copies of data; and
- Using an appropriate hierarchy of packages.

### 3. Clear Separation of the Essential from the Inessential

Software designers have to reconcile many, sometimes conflicting, constraints. When such conflicts arise, the designer should make the essential functionality of the system the highest priority.

For example, although it might ease the testing of a system by making certain data global, it is preferred that this inessential aspect of the design be located in the place that ensures minimal information flow. Additional code, clearly identified by comments and flow analysis as not being necessary for the essential functionality of the system, can provide access to the data at test time.

### 4. Careful Selection of the SPARK Boundary

Careful thought should be given to defining the boundary between what is in SPARK and what is not. This boundary is far more fluid with SPARK 2014 with its goal of supporting verification through a combination of proof and testing than it is with SPARK 2005.

### 5. Use Static Analysis Early

The packages making up the design should be examined as early as possible with the SPARK tools. Early use of these tools is facilitated by using abstractions, deferring implementation details, and making appropriate use of SPARK_Mode => Off. The analysis should continue as the design evolves. This constant checking of design choices provides assurance that our aims are met.

## 8.3.4 INFORMED Design Steps

The INFORMED report includes a suggested sequence of six steps for constructing a SPARK application.

- 1. Identification of the system boundary, inputs, and outputs.
- 2. Identification of the SPARK boundary within the overall system boundary.
- 3. Identification and localization of system state.
- 4. Handling of the initialization of state.
- 5. Handling of secondary requirements.
- 6. Implementing the internal behavior of components.

Design is an iterative process so there is usually considerable looping, backtracking, and feedback among the steps within the following steps.

### 1. Identification of the system boundary, inputs, and outputs

The SPARK system being designed is typically part of a larger system that has interactions with the outside world. The first step is to delineate this boundary and identify the physical inputs and outputs. These are the environmental quantities that impact or are impacted by the system’s behavior. They are described as monitored and controlled variables in the Four-Variable Model of Parnas and Madey (1995), which describes the interactions between a computer system and the environment. This model is illustrated in Figure 8.1.

![Figure 8.1. The four-variable model (adapted from Parnas and Madey, 1995).](img/d1a16034f5d1724d114fe7293dc71133_319_0.png)

### 2. Identification of the SPARK boundary

After identifying the boundary of our overall system, we give thought as to where to place the boundary of the SPARK portions of our application – that is, what parts are in SPARK and what parts are not. Selection of the boundary variable packages and boundary variable abstract packages is one way to define the SPARK boundary. The input and output values provided by the abstract state of these packages are the input data items and output data items of the Parnas model illustrated in Figure 8.1. Figure 8.2 shows the flow of information through these packages to and from the non-SPARK software and environment defined by the Parnas four-variable model. The INFORMED report gives examples of systems that contain multiple SPARK systems within an overall system.

![Figure 8.2. Boundary variable packages define the SPARK boundary.](img/d1a16034f5d1724d114fe7293dc71133_319_1.png)

The identification of the styles of verification that will be applied to each component identified at this point is a crucial part of VDD. Proof will certainly play a large role in the verification of SPARK units, and runtime assertion checking will help us verify Ada units. Units written in other languages will need to be tested. We must determine the depth of analysis required of each unit. The recommendations given in Section 8.4 provide guidance in planning the verification at the boundaries between SPARK and non-SPARK units.

### 3. Identification and localization of state

The identification of state that is required in our system and determining where to place that state information are central to meeting the INFORMED design method’s goals. As such, the report categorizes the different ways that packages can be used for the management, concealment, and communication of state.

Most nontrivial systems store values in variables and therefore have “history” or state. In the absence of state, calling an operation with a particular set of values always returns the same answer. On the other hand, the result of calling an operation that uses state may also depend on some complex history of all previous calls of that procedure. The INFORMED report emphasizes that the selection of appropriate locations for this state is probably the single most important decision that influences the amount of information flow in the system. You must decide (1) what must be stored, (2) where should it be stored, and (3) how should it be stored.

**What must be Stored?**

Some static data storage is almost always required, but the amount should be minimized as far as possible. You should avoid duplicating data by storing it in a single place and make it available to other units through “accessor functions.”

Classification of state is a crucial part of INFORMED. States may be classified into groups such as essential, inessential, input, output, and so on. The golden rule of refinement tells us to only refine concrete states as constituents of the same abstract state if they are of the same classification and initialization mode.

Integrity levels for safety (level A, B, etc.) or security (classified, unclassified, top-secret, etc.) are good candidates for state classes. The golden rule of refinement is especially important here – never refine together states that are of different integrities. If you have separation properties, such as making sure that top-secret and unclassified material are kept separate, you need to design that separation into your state hierarchy.⁵

**Where should it be Stored?**

The INFORMED report gives us several guidelines. Data stored inside the main program does not appear in its data flow or information flow dependency contracts. This has the unfortunate effect of removing all of the information describing the flow of data. Therefore, it is more appropriate to place this data within variable packages or boundary variable packages. The main program then includes the abstract states of these packages in its global and depends aspects. Of course, within the packages we will refine the abstract states into combinations of concrete state variables and abstract state variables of lower level packages with state.

**How should it be Stored?**

The INFORMED report describes a number of ways to store state:

- In a variable package at library level (global state)
- In a variable package embedded within another variable package (hierarchical state refinement)
- In a variable package that is a private child of another variable package (the preferred approach to hierarchical state refinement)
- In a variable package embedded within the main program
- As an instance of type defined in a type package
- As a concrete Ada variable

State should be localized as much as possible. It should be avoided entirely where a local variable within a subprogram will suffice. Variables declared in subprograms (other than the main program) exist only for the life of a call to that subprogram. Type packages give us extra freedom in locating items with complex state as locally as possible.

We advise that when you need only a single instance of an object with state that you use a variable package and use type packages when multiple copies are required. The use of variable packages can be extended to those situations with a small finite number of objects. For example, it might be better to encapsulate three buttons within a single control panel package rather than to define a button type package.

### 4. Handling of the initialization of state

After identifying and determining the location of states, our next consideration is on how the various states will be initialized. There are two approaches to initialize state:

- a. Initializing during program elaboration. This initialization includes the assignment of initial values accompanying variable declarations and the execution of statements in a package’s elaboration part (see Section 3.4.1).

  We discussed default initialization in Section 4.4. The use of the *Initializes* aspect provides an important piece of information to the SPARK
