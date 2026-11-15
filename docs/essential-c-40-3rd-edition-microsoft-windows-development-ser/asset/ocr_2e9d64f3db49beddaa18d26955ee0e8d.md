to support the invocation of the dynamic getter and setter properties. Furthermore, the implementations are straightforward. First, they examine the contained XElement, looking for an element with the same name as the binder.Name—the name of the member invoked. If a corresponding XML element exists, then the value is retrieved (or set). The return value is set to true if the element exists and false if it doesn't. Automatically, a return value of false will cause the runtime to throw a Microsoft.CSharp.RuntimeBinder.RuntimeBinderException at the call site of the dynamic member invocation.

System.Dynamic.DynamicObject supports additional virtual methods if additional dynamic invocations are required. Listing 17.33 shows the list of all the overridable members.

# Listing 17.33: Overridable Members on System.Dynamic.DynamicObject

```
using System.Dynamic;

public class DynamicObject : IDynamicMetaObjectProvider
{
    protected DynamicObject();

    public virtual IEnumerable<string> GetDynamicMemberNames();
    public virtual DynamicMetaObject GetMetaObject(
        Expression parameter);
    public virtual bool TryBinaryOperation(
        BinaryOperationBinder binder, object arg,
        out object result);
    public virtual bool TryConvert(
        ConvertBinder binder, out object result);
    public virtual bool TryCreateInstance(
        CreateInstanceBinder binder, object[] args,
        out object result);
    public virtual bool TryDeleteIndex(
        DeleteIndexBinder binder, object[] indexes);
    public virtual bool TryDeleteMember(
        DeleteMemberBinder binder);
    public virtual bool TryGetIndex(
        GetIndexBinder binder, object[] indexes,
        out object result);
    public virtual bool TryGetMember(
        GetMemberBinder binder, out object result);
    public virtual bool TryInvoke(
        InvokeBinder binder, object[] args,
        out object result);
    public virtual bool TryInvokeMember(
```