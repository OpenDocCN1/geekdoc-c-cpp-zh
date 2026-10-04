Information flow control (IFC) is a technique to assert the security of a given program with respect to a given security policy. The classical security policy noninterference requires that public output of a program may not be influenced from secret input. This book leverages a technique called program slicing, which is closely connected to IFC and offers many dimensions for improving analysis precision. It presents a precise model for object-oriented programs in a classic data structure for slicing and extends the slicing algorithms to allow for precise IFC and to provide a method to downgrade secret information, if necessary. Path conditions provide further insight into how one statement influences another. They may lead to conditions for illicit information flow, or may provide evidence that an assumed flow is impossible.

An evaluation shows that these techniques scale well to the security kernels which we have in mind, while the burden for specifying the security policy is very low. But most importantly, our security analysis can certify programs written in a realistic programming language, namely full Java bytecode.

![](bbox=[0.568, 0.856, 0.83, 0.953])

ISBN: 978-3-86644-398-3

www.uvka.de