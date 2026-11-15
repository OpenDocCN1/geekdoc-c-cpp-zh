Obviously, the difference in terms of readability is tremendous because in the second snippet, the cases are self-documenting to some degree. However, the performance at runtime is identical. To achieve this, the second snippet uses enum values in each case statement.

An enum is a type that the developer can define. The key characteristic of an enum is that it identifies a compile-time-defined set of possible values, each value referred to by name, making the code easier to read. You define an enum using a style similar to that for a class, as Listing 8.10 shows.

# LISTING 8.10: Defining an Enum

```
enum ConnectionState
{
    Disconnected,
    Connecting,
    Connected,
    Disconnecting
}
```

> **NOTE**
> 
> An enum is helpful even for Boolean parameters. For example, a method call such as SetState(true) is less readable than SetState(DeviceState.On).

You refer to an enum value by prefixing it with the enum name; to refer to the Connected value, for example, you use ConnectionState.Connected. You should not use the enum names within the enum value name, to avoid the redundancy of something such as ConnectionState.ConnectionStateConnected. By convention, the enum name itself should be singular, unless the enums are bit flags (discussed shortly).

By default, the first enum value is 0 (technically, it is 0 implicitly converted to the underlying enum type), and each subsequent entry increases by one. However, you can assign explicit values to enums, as shown in Listing 8.11.