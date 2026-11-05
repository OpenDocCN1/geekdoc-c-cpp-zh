Here, the declarations of X, Y, and Z are overriding property declarations. Each property declaration exactly matches the accessibility modifiers, type, and name of the corresponding inherited property. The get accessor of X and the set accessor of Y use the base keyword to access the inherited accessors. The declaration of Z overrides both abstract accessors—thus, there are no outstanding abstract function members in B, and B is permitted to be a non-abstract class. end example]

When a property is declared as an override, any overridden accessors shall be accessible to the overriding code. In addition, the declared accessibility of both the property or indexer itself, and of the accessors, shall match that of the overridden member and accessors. [Example:

```
public class B
{
    public virtual int P {
        protected set {...}
        get {...}
    }
}
public class D: B
{
    public override int P {
        protected set {...}    // Must specify protected here
        get {...}              // Must not have a modifier here
    }
}
```

end example]

# 15.8 Events

# 15.8.1 General

An event is a member that enables an object or class to provide notifications. Clients can attach executable code for events by supplying event handlers.

Events are declared using event-declarations:

```
event-declaration:
    attributesopt event-modifierSopt event type variable-declarators ;
    attributesopt event-modifierSopt event type member-name
    { event-accessor-declarations }

event-modifiers:
    event-modifier
    event-modifiers event-modifier

event-modifier:
    new
    public
    protected
    internal
    private
    static
    virtual
    sealed
    override
    abstract
    extern

event-accessor-declarations:
    add-accessor-declaration remove-accessor-declaration
    remove-accessor-declaration add-accessor-declaration
```