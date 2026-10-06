```
let ctor = ProvidedConstructor(
    parameters = [],
    InvokeCode = fun args -> @@MyProductionCode(
@@@>)

ty.AddMember(ctor)
ty.AddMember(m)

nty.AddXmlDoc("xml comment"
    ty))

do
    newT.AddMember(ctor)

do this.AddNamespace(rootNamespace, [newT])
```

> Note This code requires a reference to System.Xml and System.Xml.Linq.

The type provider gives the user a place to design his design-time logic. You can use type providers to better take advantage of the editing power of Visual Studio without getting into the details of the Visual Studio SDK.

# Using the DGML-File Type Provider

Directed Graph Markup Language (DGML) is supported in Visual Studio. DGML is used to draw a diagram representing a graph structure that contains nodes and edges. You can use DGML to represent a state machine, where the node is the state and the edge is the possible transition between states. Figure 5-8 illustrates how the DGML is shown in Visual Studio. It represents a state machine with four states: State0 to State3. The DGML file is actually an XML file. Listing 5-41 shows the content of the DGML file that is shown in Figure 5-8. The Nodes section defines all the nodes in the graph, and the Links section defines all the edges.