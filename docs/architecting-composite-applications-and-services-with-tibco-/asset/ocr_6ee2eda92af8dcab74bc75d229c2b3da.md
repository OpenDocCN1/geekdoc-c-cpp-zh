are readily readable. Two common conventions that satisfy this criterion are

+   - Non-leading capitals: Each word in a field other than the first begins with a capital letter, such as `ClaimService` (for a type) or `claimService` (for an instance). The leading capital should be determined by whether the field references a type or an instance (see previous section).
+   - All letters are capitalized, and an underscore (_) or other separator is used between words, for example, `CLAIM_SERVICE`. This convention pretty much requires that an additional term be used to distinguish types from instances (see previous section).

One convention to be avoided is the use of all capitals with no special characters allowed (e.g., no underscores). Such a convention leads to names like CLAIMSERVICE, which is not only hard to read but also may lead to ambiguities.

# Best Practice: Plan for Multi-Word Fields

Adopt a convention for capitalizing names that ensures that the resulting multi-word names are readily readable.

# Use a Distinct WSDL Namespace URI for Each Interface

To avoid naming conflicts among the messages, ports, and operations of different interfaces, each interface should have its own namespace URI. Equally important, using distinct namespace URIs makes it possible to independently version the interfaces. This will facilitate the graceful evolution of interfaces in the environment.

# Best Practice: Use a Unique WSDL Namespace URI for Each Interface

Define each interface in a separate WSDL, and use a unique namespace URI for each WSDL.