Our input to the ComputeValueFrom function is a vector of nodes, defined by NodeVec on line [1]. This corresponds to the input RPN expression, `5 3 4 + *` in Figure 6.19, but the elements are node objects from the TNode hierarchy (Section 6.6.4). The returned value will be represented by the LeafValType whose alias is defined on line [4].

If there are any nodes in the input `node_vec`, the auxiliary stack `auxStack` holding LeafValType objects is created on line [21]. Then the nodes from `node_vec` are processed from left to right in the range loop that starts on line [25], as shown in Figure 6.19. But the problem is as follows: although all elements of `node_vec` are smart pointers to the TNode base class, the actual pointers are to different objects from the TNode hierarchy. For example, with our simple expression, we will have three LeafValTypes followed by one PlusOperator and one MultOperator. We need to process them differently, as described in the previous RPN processing algorithm, but we have only TNode pointers. So, we have to figure out how, at runtime, to differentiate one TNode pointer to LeafValType from the other TNode pointer to PlusOperator, for instance. In C++, the RTTI mechanism comes to the rescue, as we mentioned in Section 3.19.1 when we discussed GROUP 2 of the C++ operators. The two RTTI constructions are the `typeid` and `dynamic_cast` operators. `typeid` allows us to check the type of an object referred to with a pointer or a reference, even if that pointer or reference is to the base class from which the class of an object of interest was derived. On the other hand, at runtime, `dynamic_cast` will try to do a checked conversion of a pointer or a reference to the requested type. If the converted types are up, down, or sideways along the inheritance hierarchy, then the conversion will succeed. Otherwise, if `dynamic_cast<a_pointer>` is attempted, a `nullptr` will be returned. In the case of `dynamic_cast<a_reference>`, a `std::bad_cast` exception is thrown. We will use these features in our code. First, to distinguish the LeafValType objects, line [29] verifies the `typeid` of an object held by node, using the `typeid` of NumberLeafNode. If they agree, then the value of the object is pushed onto the `auxStack`. Concretely, on line [32] node is cast to the pointer to the NumberLeafNode object, from which the value is read and pushed onto the stack. But how is this done? Because node is a `std::unique_ptr`, it is not compatible with the NumberLeafNode class. However, it has an overloaded cast operator built in to a pointer of the held class. As a result, `std::unique_ptr` can be used in all code requiring a pointer or reference to the held object. Hence, GetValue can be called through the node cast to the NumberLeafNode object.

```
```cpp
using NodeVec = ExpressionTreeBuilderInterpreter::NodeStack::DataContainer;

using LeafValType = double;

// Computes value of the stack
LeafValType ComputeValueFrom( const NodeVec & node_vec )
{
    auto retVal { 0.0 };

    const auto kNumOfElements = node_vec.size();
    if ( kNumOfElements == 0 )
```
```

# Listing 6.29 Function to compute the value of an expression directly from its RPN representation stored in the stack (in *Parser, NodeStackConverters.cpp*).