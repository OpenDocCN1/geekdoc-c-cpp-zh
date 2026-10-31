```
/finance/paymentManager/claimPayment/wsdl/claimPayment.wsdl
```

the third part, is called the path. It represents a name hierarchy local to the machine designated by the Internet domain name. The path name hierarchy is read left to right.

What makes the use of two different name hierarchies and their differences in right-to-left and left-to-right reading unambiguous is the use of two different field separators. The Internet domain namespace fields are separated by a period (.), while the local namespace fields are separated by a forward slash (/). The occurrence of the first slash to the right of the Internet domain name is the clue that you have switched naming hierarchies.

If you wanted to make this namespace uniform, reading entirely left to right, you would have to switch the order of the Internet namespace elements:

```
com.nouveau.insurance.finance.paymentManager.claimPayment.wsdl.claimPayment.wsdl
```

This is, of course, the kind of structure used for naming Java classes.

# Best Practice: General-to-Specific Structure

When the structure of names is not already constrained, establish a uniform left-to-right, general-to-specific hierarchical structure for names following the pattern

```
<functionalContext><abstractService><abstractInterface>
```

When the structure of names is partially constrained (e.g., URLs and URIs), apply this principle to the lower-level structure of the names (i.e., the path in the URL or URI).

# Employ Hierarchical Naming Authorities

Names, to be useful, must be unique. Uniqueness requires that some authority keep track of which names have been assigned so that newly issued names can be assured to be different. Unfortunately, having a single authority to keep track of all names is impractical, particularly for names with global scope.

The systems that have evolved (in numerous places) to address this issue involve the use of hierarchical authorities. This strategy involves two elements. The first is a standardized syntactic structure for defining names as sequences of fields. The Internet domain name structure (e.g., insurance.nouveau.com) is one example.