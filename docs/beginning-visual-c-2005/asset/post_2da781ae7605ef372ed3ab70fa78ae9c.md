
## Class Inheritance and Virtual Functions

The for each loop iterates over each element in the things array so in the loop body you call the delegate with an element from the array as the first argument. This causes the Sum() function to be called for the thing object with an argument of 3. Thus this loop produces the first five output lines.

```
ubh += gcnew UBHandler(&ThisClass::Product); // Add a function to the delegate
```

This statement creates a new UBHandler delegate that points to the Product() function and combines this with the existing delegate referenced by ubh. The result is another delegate that has pointers to both the Sum() and Product() functions in its invocation list.

The last loop calls the ubh delegate for each element in the things array with a argument value 2. The result will be that both Sum() and Product() will be called for each ThisClass object with the argument value 2, so the loop produces the next ten lines of output.

Although you have used unbound delegates in a very simple way, here they provide immense flexibility in your programs. You could pass an unbound delegate as an argument to a function, for example, to enable the same function to call different combinations of instance functions at different times so the delegate becomes a kind of function selector. The sequence in which functions are called by a delegate is the sequence that they appear in the invocation list so a delegate provides you with the means of controlling the sequence in which functions are called.

## Creating Events

As I said earlier, the signaling of an event involves a delegate and the delegate contains pointers to the functions that are to be called when the event occurs. Most of the events you work with in your programs are events associated with controls such as buttons or menu items and these events arise from user interactions with your program, but you can also define and trigger events in your own program code.

An event is a member of a reference class that you define using the event keyword and a delegate class name:

```
public delegate void DoorHandler(String^ str);

// Class with an event member
public ref class Door
{
public:
// An event that will call functions associated
// with an DoorHandler delegate object
event DoorHandler^ Knock;

// Function to trigger events
void TriggerEvents()
{
Knock("Fred");
Knock("Jane");
}
};
```

## Chapter 9

The Door class has an event member with the name Knock that corresponds to a delegate of type DoorHandler. Knock is an instance member of the class, but you can specify an event as a static class member using the static keyword. You can also declare an event to be virtual. When a Knock event is triggered, it can call functions with the parameter list and return type that are specified by the DoorHandler delegate.

The Door class also has a public function, TriggerEvents() that triggers two Knock events, each with different arguments. The arguments are passed to the functions that have been registered to receive notification of the Knock event. As you see, triggering an event is essentially the same as calling a delegate.

You could define a class that might handle Knock events like this:

```
public ref class AnswerDoor
{
public:
    void ImIn(String^ name)
    {
        Console::WriteLine(L"Come in {0}, it's open.",name);
    }

    void ImOut(String^ name)
    {
        Console::WriteLine(L"Go away {0}, I'm out.",name);
    }
};
```

The AnswerDoor class has two public function members that potentially could handle a Knock event because they both have the parameter list and return type identified in the declaration of the DoorHandler delegate.

Before you can register functions that are to receive notifications of Knock events, you need to create a Door object. You can create a Door object like this:

```
Door^ door = gcnew Door;
```

Now you can register a function to receive notification of the Knock event in the door object like this:

```
AnswerDoor^ answer = gcnew AnswerDoor;
door->Knock += gcnew DoorHandler(answer, &AnswerDoor::ImIn);
```

The first statement creates an object of type AnswerDoor — you need this because the ImIn() and ImOut() functions are not static class members. You then add an instance of the DoorHandler delegate type to the Knock member of door. This exactly parallels the process of adding function pointers to a delegate and you could add further handler functions to be called when a Knock event is triggered in the same way. We can see it operating in an example.

## Class Inheritance and Virtual Functions

This example uses the classes from the preceding section to define, trigger, and handle events:

```
```cpp
// Ex9_19.cpp : main project file.
// Defining, triggering and handling events.
#include "stdafx.h"

using namespace System;

public delegate void DoorHandler(String^ str);
```
```

```
```cpp
public ref class Door
{
public:
	// An event that will call functions associated
	// with an DoorHandler delegate object
	event DoorHandler^ Knock;

	// Function to trigger events
	void TriggerEvents()
	{
		Knock(L"Fred");
		Knock(L"Jane");
	}
};
```
```

```
```cpp
public ref class AnswerDoor
{
public:
	void ImIn(String^ name)
	{
		Console::WriteLine(L"Come in {0}, it's open.",name);
	}

	void ImOut(String^ name)
	{
		Console::WriteLine(L"Go away {0}, I'm out.",name);
	}
};
```
```

```
```cpp
int main(array<System::String ^> ^args)
{
	Door^ door = gcnew Door;
	AnswerDoor^ answer = gcnew AnswerDoor;

	// Add handler for Knock event member of door
	door->Knock += gcnew DoorHandler(answer, &AnswerDoor::ImIn);
	door->TriggerEvents();  // Trigger Knock events

	// Change the way a knock is dealt with
}
```
```

```
door->Knock -= gcnew DoorHandler(answer, &AnswerDoor::ImIn);
door->Knock += gcnew DoorHandler(answer, &AnswerDoor::ImOut);
door->TriggerEvents();            // Trigger Knock events
return 0;
}
```

Executing this example results in the following output:

```
Come in Fred, it's open.
Come in Jane, it's open.
Go away Fred, I'm out.
Go away Jane, I'm out.
Press any key to continue . . .
```

## How It Works

You first create two objects in main():

```
Door^ door = gcnew Door;
AnswerDoor^ answer = gcnew AnswerDoor;
```

The door object has an event member, Knock, and the answer object has member functions that can be registered to be called for Knock events.

The next statement registers the ImIn() member of the answer object to receive notification of Knock events for the door object:

```
door->Knock += gcnew DoorHandler(answer, &AnswerDoor::ImIn);
```

If it made sense to do so, you could register other functions to be called when a Knock event is triggered.

The next statement calls the TriggerEvents() member of the door object:

```
door->TriggerEvents();            // Trigger Knock events
```

This results in two Knock events, one with the argument "Fred" and the other with the argument "Jane". The result is that the ImIn() function is called once for each event, which produces the first two lines of output.

Of course, you might want to respond differently to an event at different times, depending on the circumstances, and this is what the next three statements in main() demonstrate:

```
door->Knock -= gcnew DoorHandler(answer, &AnswerDoor::ImIn);
door->Knock += gcnew DoorHandler(answer, &AnswerDoor::ImOut);
door->TriggerEvents();            // Trigger Knock events
```

The first statement removes the pointer to the ImIn() function from the event and the second statement registers the ImOut() function for the answer object to receive event notifications. When the Knock events are triggered by the third statement, the ImOut() function is called so the results are a little different.

## Destructors and Finalizers in Reference Classes

You can define a destructor for a reference class in the same way as you define a constructor for a native C++ class. The destructor for a reference class is called when the handle goes out of scope or the object is part of another object that is being destroyed. You can also apply the delete operator to a handle for a reference class object and that results in the destructor being called. The primary reason for implementing a destructor for a native C++ class is to deal with data members allocated on the heap, but obviously that doesn’t apply to reference classes so there is less need to define a destructor in a ref class. You might do this when objects of the class are using other resources that are not managed by the garbage collector, such as files that need to be closed in an orderly fashion when an object is destroyed. You can also clean up such resources in another kind of class member called a finalizer.

A finalizer is a special kind of function member of a reference class that is called automatically by the garbage collector when destroying an object. Note that the finalizer is not called for a class object if the destructor was called explicitly or was called as a result of applying the delete operator to the object. In a derived class, finalizers are called in the same sequence as destructor calls would be, so the finalizer for the basest class is called first, followed by the finalizers for successive classes in the hierarchy with the finalizer for the most derived class being called last.

You define a finalizer in a class like this:

```
public ref class MyClass
{
    // Finalizer definition
    !MyClass()
    {
        // Code to clean-up when an object is destroyed...
    }

    // Rest of the class definition...
};
```

You define a finalizer function in a class in a similar way to a destructor, but with ! instead of the ~ that you use preceding the class name for a destructor. Similar to a destructor, you must not supply a return type for a finalizer, and the access specifier for a finalizer will be ignored. You can see how destructors and finalizers operate with a little example.

## Try It Out Finalizers and Destructors

This example shows when destructors and finalizers get called in an application:

```
// Ex9_20.cpp : main project file.
// Finalizers and destructors

#include "stdafx.h"

using namespace System;

ref class MyClass
{
public:
```
