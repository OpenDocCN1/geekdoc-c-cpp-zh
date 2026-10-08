# Chapter 19 Custom Linked Data Structures

```
// create data to store in List
bool aBoolean = true;
char aCharacter = '\$';
int aInteger = 34567;
string aString = "hello";
```

```
// use List insert methods
list.InsertFront(aBoolean);
list.Display();
list.InsertAtFront(aCharacter);
list.Display();
list.InsertAtBack(aInteger);
list.Display();
list.InsertAtBack(aString);
list.Display();
```

```
// remove data from list and display after removal
{
object removedObject = list.RemoveFront();
Console.WriteLine($"{removedObject} removed$");
list.Display();
```

```
removedObject = list.RemoveFront();
Console.WriteLine($"{removedObject} removed$");
list.Display();
```

```
removedObject = list.RemoveBack();
Console.WriteLine($"{removedObject} removed$");
list.Display();
```

```
removedObject = list.RemoveBack();
Console.WriteLine($"{removedObject} removed$");
list.Display();
```

```
catch (EmptyListException emptyListException) {
Console.Error.WriteLine($"\n{emptyListException}");
}
```

```
The list is: True
The list is: $ True
The list is: $ True 34567
The list is: $ True 34567 hello
removed
The list is: True 34567 hello
```

Fig. 19.5 Testing class List. (Part 2 of 3.)