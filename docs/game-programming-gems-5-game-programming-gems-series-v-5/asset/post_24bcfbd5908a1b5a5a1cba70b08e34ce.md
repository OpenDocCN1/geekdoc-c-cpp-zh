
respectively. The object manager only deals with pointers to components, which leaves effective management of component memory as an exercise for the reader. For the system implemented here, standard new and delete work just fine. The variable mTypeHash is used to look up the component type ID based on the hashed name string for the component.

For each interface type, we maintain a set of component types that implement it. That information is stored in the array mInterfaceTypeToComponentTypes[]. This is used in the QueryInterface() method of the object manager. To simplify things, we only allow one implementation of any interface in each object so that QueryInterface() either returns NULL if no components in the object implement that interface, or a pointer to the component in the object that does so.

During the course of the game, we will be using the mComponentTypeToComponentMap array a lot. Each element of this array is a map that maps IComponent pointers to the object IDs of the objects to which they belong. When a component is created, its object ID and address (in the form of an IComponent pointer) gets added to the map at the array index determined by its component type. The QueryInterface() method will ultimately have to look at mComponentTypeToComponentMap to see if it can match an interface via mInterfaceTypeToComponentTypes to a component pointer. Look at the code on the companion CD-ROM for details of this method.

The last member of sObjectManagerDB is mMessageTypeToComponentTypes. This keeps track of which component types subscribe to which message types. Message subscriptions tend to be set up at initialization time, although there is nothing stopping subscriptions or unsubscriptions while the game is running.

## A Sample Component

If our game involves dealing and taking damage, we are quite likely to need a health component. The requirements are quite simple:

- Keep track of the current health of the object.
- Allow querying of the current health.
- Update the current health value when the message MT_TAKE_HIT is received.
- Send the message MT_HEALTH_DEPLETED when the health reaches zero.

### The Interface Class

First we create the interface ICmpHealth. It looks like this:

```
class ICmpHealth : public IComponent
{
public:
    virtual int32 GetHealth()=0;
protected:
    static void RegisterInterface(EComponentTypeId);
};
```

The method declaration GetHealth() is the reason we create this interface in the first place. The implementation of the next method looks like this:

```
void ICmpHealth::RegisterInterface(EComponentTypeId compId)
{
    GetObjectManager().RegisterInterfaceWithComponent(
        IID_HEALTH,
        compId);
}
```

This method needs to be called from the Init() method of any component that implements this interface. The RegisterInterfaceWithComponent() function call tells the object manager that the component of type compId implements IID_HEALTH. GetObjectManager() as a global function.

### The Component Class

We call our component class CCmpHealth, and it looks like this:

```
class CCmpHealth : public ICmpHealth
{
public:
    // Static methods
    static void RegisterComponentType(void);
    static IComponent* CreateMe();
    static bool DestroyMe(IComponent *);

    // Virtual IComponent methods
    virtual bool Init(CParameterNode &);
    virtual void Deinit(void);
    virtual EMessageResult HandleMessage(const CMessage &);
    virtual EComponentTypeId GetComponentTypeId(void)
    { return CID_HEALTH; }

    // ICmpHealth methods
    virtual int32 GetHealth() { return mHealth; }

private:
    int mHealth;
};
```

First, we look at the implementation of the static methods:

```
void CCmpHealth::RegisterComponentType()
{
    ICmpHealth::RegisterInterface(CID_HEALTH);
    GetObjectManager().RegisterComponentType(
        CID_HEALTH,
        CCmpHealth::CreateMe,
        CCmpHealth::DestroyMe,
        CHash("health"));
    GetObjectManager().SubscribeToMessageType(
        CID_HEALTH,
        MT_TAKE_DAMAGE);
}
```

This is arguably the most interesting of the three. It begins by registering itself as an implementer of the IComponent interface. Then it calls RegisterComponentType() in the object manager to tell it about the CreateMe() and DestroyMe() methods, and also what name (in the form of a hash value) it would like to be known under. The last thing it does is to register the component as a recipient of the MT_TAKE_DAMAGE message.

The next two methods take care of creating and destroying the component. We simply use standard new and delete to do so.

```
IComponent *CCmpHealth::CreateMe()
{
    return new CCmpHealth;
}

bool CCmpHealth::DestroyMe(IComponent* pComponent)
{
    delete pComponent;
    return true;
}
```

This is an area that would benefit from a little more work on a tailor-made memory-management system, as we will be doing a lot of creating and destroying components. Different component types could even use different allocation schemes as long as the create and destroy methods match for each type.

Now we move on to the methods defined in IComponent. The method:

```
bool CCmpHealth::Init(CParameterNode &compNode)
{
    mHealth = compNode.GetInt("Health");
    if (CParameterNode::GetLastResult() != EPRI_OK)
        return false;

    return true;
}
```

reads the data that the component needs. compNode is the component level parameter node. The call to GetInt("Health") asks for the int value of the child node with name health. To simplify things, there is only one child layer of nodes under compNode. If the request for data fails, the CParameterNode class flags an error. That is checked for by calling GetLastResult().

The next method:

```
void CCmpHealth::Deinit(void)
{
}
```

does absolutely nothing. Our only data member is an int value, so there is not much to clean up. If the component had any memory allocated, we would have to free it here.

Let us look at the message-handling method:

```
EMessageResult CCmpHealth::HandleMessage(
    const CMessage &message)
{
    int newHealth;
    switch(message.mType)
    {
    case MT_TAKE_DAMAGE:
        newHealth = mHealth -
            reinterpret_cast<int>(message.mpData);
        if(newHealth <= 0 && mHealth > 0)
        {
            GetObjectManager().PostMessage(
                GetObjectId(), MT_HEALTH_DEPLETED);
        }
        mHealth = newHealth;
        return MR_TRUE;
    }
    return MR_ERROR;
}
```

When we receive the MT_TAKE_DAMAGE message, we know that its data field is of type int and represents how much damage we have taken. If the health went from positive to negative, our health is depleted and we need to tell the other components that make up this object about it. We do this by calling the PostMessage() method in the object manager. We have to specify the recipient object, and for that, we will use the GetObjectId() method that we have inherited from CComponent. If we would like all objects to hear about a message, we would call broadcastMessage(). Then we set the new health value and return MR_TRUE to indicate that all went well. If we did not recognize the message we received, that is an error. We use MR_IGNORED for messages to which we know we have subscribed but decide to ignore.

The last two functions are so straightforward that we have defined them inline with the declaration.

## Conclusion

We have seen that static inheritance hierarchies do not stand up to the challenges of a modern game. This article has presented a strong alternative in the form of a component-based system. This system is flexible enough to cope with frequent changes of requirements. The game designers get the power to create and modify objects without programmer intervention. This leads to quicker turnaround time for testing a design change, which leads to more design iterations, which tends to lead to better games.

The programmers no longer have to spend their time refactoring the system every time the design changes but rather move the game forward by implementing the functionality called for in the design.
