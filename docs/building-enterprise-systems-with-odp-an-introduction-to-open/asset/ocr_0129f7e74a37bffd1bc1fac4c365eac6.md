sential system properties, such as resource consumption, fault tolerance or persistence. These groupings (illustrated in a much simplified configuration in figure 5.1), include such elements as nodes and, within them, sets of clusters, with cluster managers, sets of capsules, with capsule managers, and a nucleus.

These concepts are used to define the logical structure of the node. These days, there are many complete packages of infrastructure support available, but it is still important to have a common functional architecture for the infrastructure to support interoperability and interworking between these products, or to extend it to new technologies as they appear.

It is important to understand the kinds of functionality required to support provision of distribution transparencies, the basic mechanisms needed to achieve those functionalities, and how they can be structured and assigned to the architectural elements of the engineering viewpoint. This provides a reference architecture, against which existing distributed processing systems can be compared and evaluated, or with which tomorrow's systems can be designed. Using it helps technical architects specify or select required infrastructure characteristics.

The first two concepts make the distinction between provision and use of resources, as follows:

+   - A **node** represents a physical object that has computing, communication and storage capabilities, and generally has connections to other nodes. A node will therefore have one or more network addresses, and the elements deployed on the node can become network accessible. Your laptop, your office PC, your mobile phone and your organization's server machines are all nodes. However, this is a slight simplification because a node does not actually have to be a separate, physically tangible object; a virtualization of such a resource (see section 9.1) can also be considered to be a node.

+   - An **engineering object** is any object of interest in this viewpoint. These objects support computational requirements, distribution transparencies or infrastructural aspects of the system. We distinguish here between BEOs, which represent computational objects, and other engineering objects, whose aim is to provide basic engineering functions, such as managers, interceptors and directories.

The engineering viewpoint language also defines three other concepts that describe the principal controlling elements involved in any engineering specification:

+   - A **nucleus** represents the basic mechanisms needed to make a node function at the lowest level, typically representing an operating system kernel that manages and allocates processing capabilities, communication capabilities and storage capabilities. Fair scheduling and accurate