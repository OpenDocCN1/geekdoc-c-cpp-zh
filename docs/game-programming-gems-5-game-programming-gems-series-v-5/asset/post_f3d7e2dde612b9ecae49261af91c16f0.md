
to the render component asking the Entity component for the object's world position. Any of the code in the game that has access to the object manager can query for an interface belonging to a particular object. All that is needed is the object ID.

The second means of communication between components comes in the form of messages. This is useful for the situation where a component has something to say, but does not quite know to whom to say it. A message can be sent to an object or to all objects. In the case of the collectable component telling the object it belongs to that it is picked up and wants to be hidden, it would post a message to all the components in the object to say that it would like to be hidden. Each component type will tell the object manager at initialization time which messages it is interested in receiving.

## Extending Our Object

So what to do if we want to be able to bend the spoon? At the moment, our spoon object is rigid and does not bend easily. The solution is simple enough: we add an animation component to the object.

Now, we have not really talked about how objects are defined. That bit seemed easy in the traditional system: the object was defined by where it was in the inheritance tree and by the methods it exposed to the rest of the world. We could still make a class for each object type and use aggregation so that each object class is built up from a bunch of has-a relationships rather than the is-a relationships of old. This brings us one step closer to what we want, but it still means that objects are set up in code, and that means we need to compile every time we change the structure of an object.

What we would really like to have is the whole process of creating objects be completely data driven. That way, designers can play around with existing objects and even create new object types without any programmer input. The system has everything that is needed to make this happen. We simply need to derive file formats for specifying components and objects and provide the designers with the tools they will need.

## Creating the System

Now that we have a reasonable idea of what we want, we can go ahead and create the system. The companion CD-ROM has all the code for a component-based object management system, including a few different components and messages to get started using it. It is not a complete system, and there is not really any way that it can be considering that all games are different, but it should be easy enough to extend the system to make it work for a wide range of games.

![](img/672fe9a2d008ba627b1991e15d70f43e_71_0.png)

## The Component Interface

The first class that we are going to have a look at is the component interface. This is the class from which all other component interfaces and components derive. It looks like this:

```cpp
class IComponent
{
public:
    IComponent();
    virtual ~IComponent() = 0;
    virtual bool Init(CParameterNode &) = 0;
    virtual void Deinit(void) = 0;
    virtual EMessageResult HandleMessage(const CMessage &);
    virtual EComponentTypeId GetComponentTypeId(void) = 0;

    CObjectId GetObjectId(void) const;
    ICmpEntity *GetEntity() const;

private:
    void SetObjectId(CObjectId oid);
    friend CObjectManager;
    CObjectId mObjectId;
};
```

So now we know what it looks like, but what does it do? Let us have a look at each of the declarations in turn. First we have the constructor and destructor. They do not really do much other than the virtual destructor signaling that this class is meant to be derived from and not instantiated. After that, it gets a bit more interesting. The next two declarations:

```cpp
virtual bool Init(CParameterNode &) = 0;
```

and

```cpp
virtual void Deinit(void) = 0;
```

are called on each component at initialization and de-initialization time, respectively. The one parameter to the Init() method is a reference to a CParameterNode object. CParameterNode is a node in a tree of component data. Think of it as a node in the XML datafile that lets us read data from it and its children without having to do all the parsing that reading XML would normally entail. The Init() method of each component then asks for the data it wants from this parameter node and initializes the component appropriately. The Deinit() method is responsible for cleaning up after the component, making sure to free any memory and release any handles that the component owns.

The next declaration:

```cpp
virtual EMessageResult HandleMessage(const CMessage &);
```

is not declared pure virtual. Component classes do not have to override it if they do not want to. Its return value is of the enumerated type EMessageResult that looks like this:

```cpp
enum EMessageResult
{
    MR_FALSE,
    MR_TRUE,
    MR_IGNORED,
    MR_ERROR
};
```

where MR_FALSE, MR_TRUE, and MR_ERROR all indicate that the message was handled. MR_IGNORED means that no attempt was made at handling the message. The implementation of HandleMessage() in IComponent simply returns MR_IGNORED without taking any further action.

The next declaration:

```cpp
virtual EComponentTypeId GetComponentTypeId(void) = 0;
```

returns a value of the enumerated type EComponentTypeId. There is a one-to-one relation between the entries in the enum and instantiable component classes.

Then we have:

```cpp
CObjectId GetObjectId(void) const;
```

GetObjectId() is a nonvirtual member function, and we added the member variable mObjectId. In a perfect world, we would not have this member variable, and GetObjectId() would be pure virtual to make the IComponent class a proper interface. In the real world, however, it makes a lot of sense to have mObjectId as a member variable of the IComponent class and to give the object manager access to change it through the two remaining declarations in the private section:

```cpp
void SetObjectId(CObjectId oId);
friend CObjectManager;
```

If we did not allow this, every component class would have to contain the same code to set up the object ID, and we would be introducing plenty of scope for error.

Finally we have the public method:

```cpp
ICmpEntity *GetEntity() const;
```

This is another situation where being practical is of greater importance than making it look pretty. In our system, we have decided that all objects have to contain a component that implements the ICmpEntity interface, so we add GetEntity() here to facilitate the lookup of this component from any other component that belongs to the same object. The ICmpEntity class can be seen on the companion CD-ROM.

## The Object Manager

The heart of the system is the object manager. The `CObjectManager` class is a bit too large for us to go through it method by method here, so we are going to focus on the core features. Refer to the code on the companion CD-ROM for the `CObjectManager` declaration and implementation.

The most important feature of the object manager is the database. It is implemented as a separate struct to hide the implementation details from users. We are going to have a little peek at it here though. Here it is:

```cpp
struct SObjectManagerDB
{
    // Static component type data
    SComponentTypeInfo mComponentTypeInfo[NUM_COMPONENT_TYPE_IDS];

    std::set<EComponentTypeId> mInterfaceTypeToComponentTypes[NUM_INTERFACE_TYPE_IDS];

    // Dynamic component data
    std::map<CObjectId, IComponent*> mComponentTypeToComponentMap[NUM_COMPONENT_TYPE_IDS];

    // Message data
    std::set<EComponentTypeId> mMessageTypeToComponentTypes[NUM_MESSAGE_TYPE_IDS];
};
```

All the members of `SObjectManagerDB` are plain old arrays of more complex data types. They can all be thought of as two-dimensional arrays where one dimension is known at compile time because we know the number of component, interface, and message types.

The first two data members of this struct are set up at system initialization time and will not change while the game is running. Each component type calls `CObjectManager::RegisterComponentType()`, which sets up the data in these two arrays. `SComponentTypeInfo` contains data that we need to create components. It looks like this:

```cpp
struct ComponentTypeInfo
{
    ComponentCreationMethod mCreationMethod;
    ComponentDestructionMethod mDestructionMethod;
    CHash mTypeHash;
};
```

The creation and destruction method members are function pointer typedefs:

```cpp
typedef IComponent* (*ComponentCreationMethod)(void);
typedef bool (*ComponentDestructionMethod)(IComponent *);
```

We are going to create functions with these signatures as static member functions of each component class. They are responsible for creating and destroying components,
