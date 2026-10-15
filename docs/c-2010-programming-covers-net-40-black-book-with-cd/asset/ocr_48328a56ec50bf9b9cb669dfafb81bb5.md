# Chapter 19: Working with Windows Communication Foundation

**NOTE**

The client session has one service instance per proxy. If the client creates another proxy to the same or different endpoint, the second proxy is associated with a new instance and session.

The service instance can maintain its state because it remains in the memory throughout a session. The following code snippet shows how to configure a per-session instancing service:

```
```csharp
[AttributeUsage(AttributeTargets.Interface|AttributeTargets.Class, Inherited=false)]
public sealed class ServiceContractAttribute : Attribute
{
    public bool Session
    {
        get;
        set;
    }
    // More members
}
```
```

While configuring a per-session instancing service, you can use the Session property to support sessions in your services. By default, the value of the Session property is set to false. If you want the service to support sessions, set the value of Session property to true, as shown in the following code snippet:

```
```csharp
[ServiceContract(Session=true)]
Interface IMyServiceMode
{
    ...
    ...
}
```
```

You can keep a service instance alive throughout the session by setting the InstanceContextMode property of the ServiceBehaviorAttribute attribute to InstanceContextMode.PerSession, as shown in the following code snippet:

```
```csharp
[ServiceBehavior(InstanceContextMode=InstanceContextMode.PerSession)]
class MYWCFService: IMyServiceMode
{
    ...
    ...
}
```
```

# Sharable Instancing Service

When you work with WCF, you may want to pass the current state of your session to another client. You can achieve this by using a sharable instancing service. Unlike a per-session instancing service, a sharable instancing service consists of one addition aspect, unique ID. When the first client creates a session with a sharable instancing service, it passes an ID of the instance to the second client. The second client creates an independent session but shares the same instance.

To configure a sharable instancing service, set the InstanceContextMode property of the ServiceBehaviorAttribute attribute to InstanceContextMode.Sharable, as shown in the following code snippet:

```
```csharp
[ServiceBehavior(InstanceContextMode=InstanceContextMode.Sharable)]
class MyWCFService: IMyServiceMode
{
    ...
    ...
}
```
```