With this functionality you can define preconditions, postconditions, and invariants within a method. The preconditions lists what requirements the parameters must fulfill, the postconditions define the requirements on returned data, and the invariants define the requirements of variables within the method itself.

Contract information can be compiled both into the debug and the release code. It is also possible to define a separate contract assembly, and many checks can also be made statically without running the application. You can also define contracts on interfaces that cause the implementations of the interface to fulfill the contracts. Contract tools can rewrite the assembly to inject contract checks within the code for runtime checks, check the contracts during compile time, and add contract information to the generated XML documentation.

Figure 19-1 shows the project properties for the code contracts in Visual Studio 2010. Here, you can define what level of runtime checking should be done, indicate if assert dialogs should be opened on contract failures, and configure static checking. Setting the Perform Runtime Contract Checking to Full defines the symbol CONTRACTS_FULL. Because many of the contract methods are annotated with the attribute [Conditional("*CONTRACTS_FULL*")], all runtime checks are only done with this setting.

![](bbox=[0.13, 0.51, 0.62, 0.82])

FIGURE 19-1

> To work with code contracts you can use classes that are available with .NET 4 in the namespace System.Diagnostics.Contracts. However, there's no tool included with Visual Studio 2010. You need to download an extension to Visual Studio from Microsoft DevLabs: http://msdn.microsoft.com/en-us/devlabs/dd491992.aspx. For static analysis with this tool, the Visual Studio Team System is required; for runtime analysis, Visual Studio Standard edition is enough.

Code contracts are defined with the Contract class. All contract requirements that you define in a method, no matter if they are preconditions or postconditions, must be placed at the beginning of the method. You