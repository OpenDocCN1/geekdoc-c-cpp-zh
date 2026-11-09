When the compiler compiles this code, the result is a type that has a number of fields and methods defined in it. You can easily see this by using the IL Disassembler tool (ILdasm.exe) provided with the .NET Framework SDK to examine the resulting managed module, which is shown in Figure 1-7.

![](bbox=[0.147, 0.16, 0.629, 0.403])

**FIGURE 1-7** ILDasm showing *Test* type's fields and methods (obtained from metadata)

Table 1-4 shows how the programming language constructs got mapped to the equivalent CLR fields and methods:

# ### TABLE 1-4 Test Type's Fields and Methods (Obtained from Metadata)

| **Type Member** | **Member Type** | **Equivalent Programming Language Construct** |
| --- | --- | --- |
| `AnEvent` | Field | Event; the name of the field is `AnEvent` and its type is `System.EventHandler`. |
| `.ctor` | Method | Constructor. |
| `Finalize` | Method | Finalizer. |
| `add_AnEvent` | Method | Event add accessor method. |
| `get_AProperty` | Method | Property get accessor method. |
| `get_Item` | Method | Indexer get accessor method. |
| `op_Addition` | Method | + operator. |
| `op_Equality` | Method | == operator. |
| `op_Inequality` | Method | != operator. |
| `remove_AnEvent` | Method | Event remove accessor method. |
| `set_AProperty` | Method | Property set accessor method. |
| `set_Item` | Method | Indexer set accessor method. |

The additional nodes under the *Test* type that aren't mentioned in Table 1-4---`.class`, `.custom`, `AnEvent`, `AProperty`, and `Item`---identify additional metadata about the type. These nodes don't map to fields or methods; they just offer some additional information