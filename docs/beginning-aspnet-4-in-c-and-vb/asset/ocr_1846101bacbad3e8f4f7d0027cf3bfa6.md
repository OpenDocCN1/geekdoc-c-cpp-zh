```
public interface IOperationContract: IContract
{
    string Name { get; }
    int NumberOperands { get; }
}
```

code snippet CalcContract/ICalculatorContract.cs

# Calculator Add-In View

The add-in view redefines the contract as it is seen by the add-in. The contract defined the interfaces ICalculatorContract and IOperationContract. For this, the add-in view defines the abstract class Calculator and the concrete class Operation.

With Operation, a specific implementation is not required by every add-in. Instead, the class is already implemented with the add-in view assembly. This class describes an operation for mathematical calculations with the Name and NumberOperands properties.

The abstract class Calculator defines the methods that need to be implemented by the add-ins. While the contract defines parameters and return types that need to be passed across appdomain and process boundaries, that's not the case with the add-in view. Here, you can use types, which make it easy to write add-ins for the add-in developer. The GetOperations() method returns IList<Operation> instead of IList<OperationContract>, as you've seen with the contract assembly.

The AddInBase attribute identifies the class as an add-in view for the store.

```
using System.AddIn.Pipeline;
using System.Collections.Generic;
namespace Wrox.ProcCSharp.MAF
{
    [AddInBase]
    public abstract class Calculator
    {
        public abstract IList<Operation> GetOperations();
        public abstract double Operate(Operation operation, double[] operand);
    }
    public class Operation
    {
        public string Name { get; set; }
        public int NumberOperands { get; set; }
    }
}
```

code snippet CalcView/CalculatorView.cs

# Calculator Add-In Adapter

The add-in adapter maps the contract to the add-in view. This assembly has references to both the contract and the add-in view assemblies. The implementation of the adapter needs to map the method IListContract<IOperationContract> GetOperations() from the contract to the view method IList<Operation> GetOperations(). The assembly includes the classes OperationViewToContractAddInAdapter and CalculatorViewToContractAddInAdapter. These classes implement the interfaces IOperationContract and ICalculatorContract. The methods of the base interface IContract can be implemented by deriving it from the base class ContractBase. This class offers a default implementation. OperationViewToContractAddInAdapter implements the other members of the IOperationContract interface and just forwards the calls to the Operation view that is assigned in the constructor.