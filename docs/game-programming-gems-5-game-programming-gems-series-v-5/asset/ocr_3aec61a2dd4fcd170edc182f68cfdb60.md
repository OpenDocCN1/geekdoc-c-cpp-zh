Let us look at the message-handling method:

```
EMMessageResult CCmpHealth::HandleMessage(
    const CMessage &message)
{
    int newHealth;
    switch(Message.mType)
    {
    case MT_TAKE_DAMAGE:
        newHealth = mHealth -
            reinterpret_cast<int>(Message.mpData);
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

# Conclusion

We have seen that static inheritance hierarchies do not stand up to the challenges of a modern game. This article has presented a strong alternative in the form of a component-based system. This system is flexible enough to cope with frequent changes of requirements. The game designers get the power to create and modify objects without programmer intervention. This leads to quicker turnaround time for testing a design change, which leads to more design iterations, which tends to lead to better games.

The programmers no longer have to spend their time refactoring the system every time the design changes but rather move the game forward by implementing the functionality called for in the design.