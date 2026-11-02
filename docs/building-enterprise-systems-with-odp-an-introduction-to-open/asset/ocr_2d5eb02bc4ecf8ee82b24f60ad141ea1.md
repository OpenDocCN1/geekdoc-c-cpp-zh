specification, since it can reference the existing solutions and merely state how they are combined to meet the infrastructure needs of the system.

The technology viewpoint is concerned with managing real-world constraints, such as restrictions on the hardware available to implement the system within budget, or the existing application platforms on which the applications must run. The designer never really has the luxury of starting with a green field, and this viewpoint brings together information about the existing environment, current procurement policies and configuration issues. It is concerned with selection of ubiquitous standards to be used in the system, and the allocation and configuration of real resources. It represents the hardware and software components of the implemented system, and the communication technology that provides links between these components. Bringing all these factors together, it expresses how the specifications for an ODP system are to be implemented.

This viewpoint also has an important role in the management of testing conformance to the overall specification because it specifies the information required from implementers to support this testing.

# 1.2.3 Viewpoint Languages

We can think of any mechanism for conveying ideas as being a language, be it written, drawn or spoken. The communication can be between people, between machines, or understood by both.

Thus, we can speak of the set of concepts, conventions and constraints expressed in a particular viewpoint as forming a viewpoint language. The rules of interpretation for such a language can, in a particular instance, be seen as representing a viewpoint virtual machine. We can think of the supporting tools as parsing the language's grammar and checking its semantic rules, or as implementing the equivalent virtual machine; these are just two sides of the same coin.

From an architectural point of view, we need not be concerned with the physical representation of this language as marks on paper or encoded in messages. An abstract language can be represented by a number of different concrete notations, suited to use in different situations. Many tools, for example, can work with either a graphical or a textual notation, and store designs in a third, machine-oriented format, such as a dialect of XML. These are all different notations expressing the same abstract language.

Thus for each of the five viewpoints being considered here, we have a corresponding viewpoint language. We talk about the viewpoint when we wish to stress the perception of the stakeholder concerned, and about the language when we want to emphasize the way the ideas are communicated, but the two aspects are intimately coupled; one cannot express the ideas without using the language.

Because the different viewpoints stress different aspects of the design, and do so using different techniques, the stakeholders will each be most comfort-