# soapAction Names

The soapAction name is nearly identical to the fully qualified operation name as described earlier, with the major version number appended to the interface name. An idealized structure for soapAction names has the form

```
<functionalContext><abstractService><interfaceName+major>
<operationName>
```

Expanding the functional context, you have:

```
<enterpriseID><lineOfBusiness><functionalArea><abstractService>
<interfaceName+major><operationName>
```

This approach provides the maximum flexibility in defining endpoints. Using this approach, all requests for all operations could be sent to a single endpoint (location) without ambiguity: The soapAction uniquely identifies the required operation.

# Best Practice: SOAP Action Names

The SOAP action name should be the fully qualified operation name with the major version number appended to the interface name.

# Schema Types Specific to an Interface and an Operation

As mentioned in the previous section, schema types are often created that are dedicated to a single operation. The ideal structure for an operation-specific message type name would be

```
<enterpriseID><lineOfBusiness><functionalArea><abstractService>
<interfaceName><operationName><typeName>
```

This leads to idealized names like

```
com.nouveau.insurance.finance.paymentManager.claimPayment.
payClaim.Request
com.nouveau.insurance.finance.paymentManager.claimPayment.
payClaim.Response
```

In reducing this idealized structure to an implementation you encounter a limitation of the schema definition language: It does not support hierarchical names within the namespace. Specifically, the Request and Response cannot be scoped within the payClaim operation