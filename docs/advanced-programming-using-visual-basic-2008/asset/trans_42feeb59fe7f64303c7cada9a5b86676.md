

## WcfDataService

```
'Project        Ch09HandsOn
'Programmer     Bradley/Mills paugh
'Date           June 2009
'Class          IDataService
'Description    Main form allows user to select report to display.

<ServiceContract()>
Public Interface IDataService

    <OperationContract()>
    Function GetData() As PubsDataSet

End Interface
```

```
'Project        Ch09HandsOn
'Programmer     Bradley/Mills paugh
'Date           June 2009
'Class          DataService
'Description    Retrieves the data.

Public Class DataService
    Implements IDataService

    Public Sub New()
    End Sub

    Public Function GetData() As PubsDataSet _
        Implements IDataService.GetData
        ' Fill the dataset.
        Dim APubsDataSet As New PubsDataSet
        Dim TitlesTableAdapter As New _
        PubsDataSetTableAdapters.titlesTableAdapter
        TitlesTableAdapter.Fill(APubsDataSet.titles)

        Return APubsDataSet
    End Function
End Class
```

## Summary

- 1. Crystal Reports is a tool for producing reports from database files.
- 2. You add a Crystal Reports report designer to a project, use the Report Wizard to design the report, add a CrystalReportViewer control to a form, and assign the viewer's ReportSource property to the report.
- 3. You can select the data for a report from SQL Server or from a dataset defined in the project.
- 4. The Field Explorer holds elements that can be added to a report.
- 5. The report designer is organized into bands, called the Report Header, Page Header, Group Header, Details, Group Footer, Page Footer, and Report Footer.

## Case Studies

### Claytor's Cottages

Modify the Guests page of the Claytor's Cottages case study project. Add a button or a menu item to display a report that shows the guest information.

### Christian's Car Rentals

Modify the Customers page of your Christian's Car Rentals case study project. Add a button or a menu item to display a report that shows the customer information.

## Collections

At the completion of this chapter, you will be able to:

- 1. Declare and reference collections.
- 2. Determine the proper collection type for a specific situation.
- 3. Understand various data structures.
- 4. Create a collection of objects and add and remove items in the collection.
- 5. Add objects to the Items collection of a list box, control the display, and retrieve selected objects.
- 6. Understand generics and be able to create generic procedures.
- 7. Create a generic collection of objects.

Throughout your programming, you have used a series of collections. List boxes have a collection of items. Tables have a collection of rows and of columns and datasets have collections of tables. In this chapter, you will examine various types of collections such as stacks, queues, dictionaries, hash tables, sorted lists, and array lists. A collection may consist of a group of individual data items or a collection of objects (remember that a data item is an object).

You will find that programmers and programming documentation often use the words collection, list, and data structure interchangeably. For most of the references in this chapter, you can substitute one term for another.

With generics, you create a strongly typed object, such as a procedure or a class, but the type is not defined until the object is instantiated or the procedure called. You will code a generic procedure and create a generic collection class.

## Referencing Collection Items

You have referenced some of the built-in collections of VB all along. You can refer to the individual elements of most collections by either a key (a string value) or an index (the numeric position). For example, to reference an individual table in the Tables collection of a DataSet object:

```
' The Stores table.
PubsDataSet.Tables("Stores")
```

or

```
' Also refers to the Stores table, assuming that it is the first table.
PubsDataSet.Tables(0)
```

or

```
' Also refers to the Stores table by using the bang notation.
PubsDataSet.Tables!Stores
```

## System.Collections Namespace

A collection is a group of objects. The System.Collections namespace provides classes for several different types of collections. When you need to create a collection, you should be aware of the different types available and the strengths and weaknesses of each type. You may need to inherit from a list class or simply select the type of collection that is best for a specific situation. An understanding of the types of collections can make the task easier and the program more efficient.

example, when you refer to a stack of dishes at the end of the buffet line, it is a collection of dishes in which the last one in the stack should be the first one removed. And hopefully the first person in the queue (in line) is the first one served.

Several types of collections are of the dictionary type. A dictionary consists of a key and value pair, similar to a word and its corresponding definition in a language dictionary. Two types of dictionary lists are the Hashtable and the SortedList.

| Collection class | Purpose |
|---|---|
| ArrayList | A collection that is similar to an array. The size of the list is dynamically increased to accommodate the elements added. Provides some useful methods, such as Contains, Insert, RemoveAt, and Sort. |
| BitArray | A collection that holds Boolean values. |
| CollectionBase | The parent class for creating strongly typed collections. An abstract class used only for inheritance. |
| DictionaryBase | The parent class for creating dictionary-type collections with pairs of keys and values. An abstract class, used only for inheritance. |
| Hashtable | A dictionary-type collection of keys and values. Sorted by the keys, which are hash codes of the values. |
| Queue | An unsorted collection in which the first element in is the first out (FIFO). |
| SortedList | A dictionary-type collection of keys and values sorted by the keys. Keys may be based on hash codes or other values. |
| Stack | An unsorted collection in which the last element in is the first element out (LIFO). |

Because all of the collection classes inherit from the same base, they share many properties and methods. A good example is the Count property, which contains the number of elements in the list.

The following examples are based on a program in which an array of strings is used to add and remove items from the different types of collections. Figure 10.1

![](img/e2635c7dd07a6ad20d386d5f4f3c5310_456_0.png)

Figure 10.1
The form used for the collection examples, Ch10Lists. The user can choose to create a stack, queue, sorted list, or hash table and add and remove items in the collections.

shows the program with the original list, which is loaded from the LanguageString array with this definition:

```
Private LanguageString As String() = {"English", "Spanish", "Chinese", _
    "Italian", "German", "French", "Tagalog"}
```

Each of the collections is declared at the class level:

```
Private ASortedList As SortedList
Private AHashtable As Hashtable
Private AStack As Stack
Private AQueue As Queue
```

## Using Stacks

The Stack class provides an unsorted list in which the last item added is the first one removed. The terms *push* and *pop* are used to refer to adding and deleting from a stack. Use the **Push method** to add an item to the list and a **Pop method** to remove an item.

```
' Add an item to the stack.
AStack.Push(ItemString)
```

The Pop method removes the last item from the list. If you want to look at the last item without removing it, use the Peek method.

```
' View the last item without removing it.
ItemString = AStack.Peek()

' Remove the last item from the list.
AStack.Pop()
```

Because stacks are unsorted, they are not the best type of list if you must perform searches. Items in a stack appear in the reverse order of entry. Figure 10.2 shows the example program with the elements added to a stack.

![](img/e2635c7dd07a6ad20d386d5f4f3c5310_457_0.png)

> The elements in a stack appear in reverse order from original entry.

## Using Queues

The Queue class provides an unsorted list of items in which the first item added to the list is the first one to be removed. You use the **Enqueue method** to add items to the queue and the **Dequeue method** to remove items.

