
specified in terms of its reaction when one of its buttons is pushed. Constructing a model of an elevator, however, requires selecting the attributes and behaviors that are of interest. For purposes of a simulation, for example, you might be concerned only with the elevator's current floor position and how to simulate movement between floors. Other attributes and behaviors might be left out of the model because they don't affect the aspects of the elevator you're interested in studying. In Section 10.4, you see how to create an elevator object in C++ and then simulate its movement from floor to floor.

## A Class Is a Plan

In creating C++'s objects, you must first create a structure, or plan, for a class of objects from which individual objects are created. For example, before attempting to assemble a bicycle or a backyard basketball hoop, you would want to know that all the parts are available and have a set of assembly instructions. In preparing a dinner, you might consult a recipe that specifies a list of ingredients and procedures for combining them correctly. In all these examples, even if written instructions aren't available, they have to at least exist in the mind of the builder, the chef, or whoever is in charge of the project. In C++, the plans from which objects are created and used are referred to as classes.

From a programming perspective, a class can be considered a construction plan for objects and how they can be used. This plan lists the required data items and supplies instructions for using the data. After one or more objects from this plan, or class, have been constructed, they can then be operated on only in ways defined by the class. Although many objects can be created from the same class, each different object type requires its own class, which is similar to producing many Chevrolet Camaros from one set of plans and Chevrolet Malibus from another.

To understand how a C++ class is actually constructed, a recipe is a useful analogy. The difference is that a C++ class is a recipe for assembling data rather than food items. Other than that, the relationship between a C++ class and a somewhat modified recipe is almost one to one and is extremely informative.

Take a look at the recipe shown in Figure 10.2. Most recipes contain similar types of components, but what's surprising is that almost exactly the same elements are required in constructing a C++ class. Notice that the recipe shown in this figure isn't the final spread; it merely provides a plan for creating a sardine spread. The recipe can be used many times, and each time it's used, a particular batch of sardine spread is produced.

## From Recipe to Class

Now you can make the connection between the recipe in Figure 10.2 and a C++ class. As mentioned, a class can be considered the plan or recipe from which programming objects are created. Like its recipe counterpart, a class typically contains sections for ingredients and methods.

### Recipe Name: Gary's Sardine Spread

### Ingredients:

| Measure | Contents |
|---|---|
| 1 can | Boneless and skinless sardines |
| 2 stalks | Celery |
| 1/4 medium | Red onion |
| 1 tablespoon | Mayonnaise |
| 1/4 cup | Parsley |
| dash | Olive oil |
| splash | Red wine vinegar |
| dash | Salt |
| dash | Pepper |

### Method of Preparation:

- Finely shred the sardines using two forks
- Finely dice the celery and onion and mix well with sardines
- Add olive oil and mix well
- Add mayonnaise and mix well
- Add red wine vinegar and mix well
- Finely dice the parsley and mix well
- Salt and pepper to taste

Figure 10.2 Recipe for Gary's sardine spread

In the ingredients section, instead of recipe measures such as a teaspoon or cup, C++ deals with measures for holding integers, double-precision numbers, strings, and other types of suitable data "ingredients." Besides a measure, each data item has a specific value, such as 5, and a name, such as firstIntegerNumber. Therefore, the list of data items used in a C++ class is, like the list of ingredients in a recipe, contained in a specific section. As an example, suppose you're creating a C++ program to calculate the average of two numbers. The following programming plan for determining an average shows the data elements and methods for constructing a class for this application, which will form the basis of an object-oriented solution:

```
// Class declaration section
Class Name: AverageOfTwoNumbers
// A list of data items to use (the parts list)
Type      Name
double    firstNumber
double    secondNumber
// A list of necessary methods (prototypes)
double assignValues(double, double);
double calculateAndDisplay(double, double);
// Class implementation section (the instructions)
Code for the two methods listed previously
```

Notice that this programming plan contains the same two basic sections shown in Figure 10.2: a list of ingredients (in this case, the ingredients are data items) and an assembly section containing the actual instructions, as methods, for using the ingredients listed.

There are, however, three notable differences in the ingredients section. First, the Measure column in Figure 10.2 is relabeled as Type in the programming plan. Second, the Contents column in Figure 10.2 is missing in the programming plan. The actual values, or contents, can be assigned as default method parameters or, more typically, provided as user-entered values requested by the listed methods. Finally, the class declaration section provides not only a list of data “ingredients,” but also a list of method names and data types (the prototypes). Using this basic structure, you’re ready to learn how to develop C++ classes in the next section for constructing working object-oriented programs.

## EXERCISES 10.1

- 1. (Practice) Figure 10.3 is a simplified diagram for assembling a birdhouse. Referring to this diagram, create a parts list and instructions for constructing it.

![](img/202cface8244f523c2641baa2e00d7dd_457_0.png)

Figure 10.3 Building a birdhouse

- 2. (Practice) a. List the items you need to build a staircase with five steps.
  b. Write instructions for assembling the items listed in Exercise 2a.

- 3. (Practice) a. List the ingredients you need to create 10 peanut butter and jelly sandwiches.
  b. Write instructions for assembling the items listed in Exercise 3a.

- 4. **(Practice)** Find assembly instructions from a recent item you have built (for example, a bicycle or a bookcase with one shelf). Identify the major elements in the assembly instructions that correspond to the Ingredients and Method of Preparation sections shown in Figure 10.2.

- 5. **(Practice)** Determine the data items and methods that would be useful for a class used for simulating tossing a single die. Choose your own class name and data item names.

- 6. **(Practice)** Determine the data items and methods that would be useful for a class used for calculating the floor space of a rectangular room. Choose your own class name and data item names.

## 10.2 Creating Your Own Classes

In computer terminology, the combination of data and associated operations is defined as a **class**. That is, a class defines both the types of data and the types of operations that can be performed on the data. Seen in this light, the built-in data types in C++ can also be considered classes, in that they provide types of data and operations that can be performed on the data. Because of this correspondence, C++ classes are sometimes referred to as programmer-defined data types or **abstract data types**. In a simplified form, this relationship can be described as follows:

*class = allowable data values + operational capabilities*

Before seeing how to construct your own classes, take a moment to review a list of the operational capabilities supplied with C++’s built-in data types. The reason for this review is that you have to provide some of these capabilities as part of the classes you create. Although you probably don’t think of these capabilities when you use them, the designers of C++ clearly had to when they created the C++ compiler. Table 10.1 lists the minimum set of these capabilities.

**Table 10.1** Operational Capabilities of C++’s Built-In Data Types

| Capability | Example |
|---|---|
| Define one or more variables of the class | `int a, b;` |
| Initialize a variable at definition | `int a = 5;` |
| Assign a value to a variable | `a = 10;` |
| Assign one variable’s value to another variable | `a = b;` |
| Perform mathematical operations | `a + b;` |
| Convert from one data type to another | `a = int (7.2);` |

Constructing a class is easy, and you already have all the necessary tools in variables and functions. In C++, variables provide the means of defining new data types, and functions provide the means of defining operational capabilities. Using this information, you can extend the previous definition of a class to its C++ representation:

*C++ class = data + functions*
