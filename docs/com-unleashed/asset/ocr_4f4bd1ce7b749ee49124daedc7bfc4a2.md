# # Summary

Monikers provide a way to access a COM object with a name. This can be a real benefit to developers. Monikers also give COM objects a way to initialize with an initialization string, simplifying code and instantiations.

In this chapter you learned about the different moniker types and how to use them. You also learned about the all-important topic of the Running Object Table.

How many times have you implemented map containers that identify distinct object instances of the same class by name? I know I’ve done it at least a hundred times. Monikers and the Running Object Table are COM’s implementation of the map container for COM objects. I’ve already run across a few instances where the Running Object Table looked very tempting. Unfortunately, due to the complexity of programming using monikers and the Running Object Table, you may have yet to implement anything beyond the trivial. I’m hoping that this chapter provided you with the fuel you need to use monikers in your applications.