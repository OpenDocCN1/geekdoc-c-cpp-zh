
![](img/b3a2d21424654c9a1d0654b2dce50e07_253_0.png)

FIGURE A.10: A dynamic schema for the RepairOrder information object.

## A.3 Computational Viewpoint Specifications

The overall structure of the computational viewpoint specification of the PhoneMob system is shown in figure A.11. It contains three high-level packages. One describes the software architecture of the application. The second deals with the behavioural aspects of the system. The last one contains the basic data types used in the specification (which were shown in figure 4.8). In addition, the model for the complete computational specification has some associated tag values that determine which transparencies are required for the system. In this case, the transaction and replication transparencies are needed (see the engineering specification in section A.4) together with the access and location transparencies, which are mandatory for any computational specification — and thus there is no need to specify them explicitly.

![](img/b3a2d21424654c9a1d0654b2dce50e07_253_1.png)

FIGURE A.11: The overall structure of the computational specification.

The internal packages of the computational specification were described in chapter 4; figure 4.5 showed the structure of the SoftwareArchitecture package, which was organized in four layers, and was later refined in figure 4.7. The signatures of the services provided and required by each computational interface were shown in figure 4.6. Finally, some examples of behavioural specifications of the system were shown, using sequences of interactions (figure 4.9) and flows (figure 4.10).

The rest of the computational specification of the PhoneMob system follows a very similar pattern, and hence is not included here.

## A.4 Engineering Viewpoint Specifications

The ODP engineering specifications of a system describe how the engineering objects (that correspond to the computational objects that implement the functionality of the system) are distributed to processing nodes and how they interact through channels. Both the internal structural organization of nodes (into capsules and clusters) and channels (into stubs, binders, protocol objects and interceptors) are expressed in this viewpoint.

![](img/b3a2d21424654c9a1d0654b2dce50e07_254_0.png)

FIGURE A.12: The overall structure of the engineering specification.

The overall organization of the engineering specification of the PhoneMob system is shown in figure A.12. This contains two main packages, one with the basic engineering object types and the other with the distribution structure.

Package NV-Objects describes the basic engineering objects. They correspond to the computational objects described in the computational specification. The same grouping structure is used again here, although just for packaging purposes, since it does not imply any constraints on the distribution. One package contains the ODP objects that implement either common functions (such as the Trader) or services that provide the required transparencies (such as the TransactionMgr; remember that the computational specification stated that transaction transparency was required).

![](img/b3a2d21424654c9a1d0654b2dce50e07_255_0.png)

FIGURE A.13: The distribution of engineering objects.

The distribution of the engineering objects is described by the elements of the ObjectDistribution package, which defines seven nodes and seven channels. Some of these elements are represented in figure A.13, which provides an overview of the distribution of the main system processing elements. Nodes contain capsules and clusters that represent groupings of elements for protection and migration management purposes, according to the policies and strategies defined for the system.

Finally, the engineering specification also provides the elements needed to represent the internal elements of channels, as was discussed in chapter 5, where figure 5.3 showed the architecture of one of the channels of the application. The rest of the channels follow a similar pattern.

## A.5 Technology Viewpoint Specifications

The technology specifications focus on four main issues: (1) identifying the main types of technology objects used to implement the system; (2) describing the requirements on these objects in terms of implementable standards; (3) stating the extra information for testing (IXIT) that needs to be associated with the technology objects; and (4) describing the relevant processes and activities involved in the provision, deployment, maintenance and evolution of the systems and its parts. In our example, the technology specifications are structured accordingly, with packages for each of these descriptions (see figure A.14).

The contents of these packages have already been described in chapter 6, in figures 6.1, 6.2, 6.3 and 6.4, respectively.

![](img/b3a2d21424654c9a1d0654b2dce50e07_256_0.png)

FIGURE A.14: The overall structure of the technology specification.

## A.6 Correspondences

We need to specify not only the viewpoints, but also how the elements in the individual viewpoints relate to each other. The PhoneMob system specification defines six pairwise correspondences between the viewpoints (see figure A.1). There is not room here to describe the detailed contents of all these packages; instead, we will focus on how correspondences are identified and expressed.

Chapter 7 explained that the UML4ODP standard provides checklists for identifying the correspondences that should be specified for a system. Some of them are mandatory for any ODP system specification, such as the ones that link the computational and engineering objects. Others depend on the system being specified. Examples of these optional correspondences are the ones that link enterprise and computational objects, or enterprise interactions with computational interfaces. Not every enterprise object or interaction has a corresponding element in the computational viewpoint. The Paper Document enterprise object type, for example, has no corresponding computational element.

In general, we can identify two kinds of correspondences between viewpoint elements, according to the type of relationship between them. In the first place, we have the correspondences between viewpoint elements that represent the same entity, such as a handset, from different perspectives.

Figure A.15 shows the representation of Handset objects in the enterprise, information and computational viewpoints, each one focusing on different aspects, giving rise to slight variations. It also shows the correspondences between them. Note that a handset is an object in the enterprise and information viewpoints, and a data type in the computational viewpoint. As a result, there is no representation for it in the engineering and technology viewpoints.

![](img/b3a2d21424654c9a1d0654b2dce50e07_257_0.png)

FIGURE A.15: Correspondences between different views of the same entity.

![](img/b3a2d21424654c9a1d0654b2dce50e07_258_0.png)

FIGURE A.16: Correspondences from computational to engineering objects.

Another example of this kind of correspondence is the set of relationships between engineering and computational objects. This is shown in figure A.16. Note that object names do not always coincide.

The second kind of correspondence happens when the related objects do not represent the same entity but there is still a relationship between them. A typical example is an enterprise policy that affects several information or computational elements. In this case, the purpose is twofold. Firstly, the correspondences specify how the policy constrains the related elements and, secondly, the correspondences provide the traceability mechanisms required to identify the elements that are affected by the policy and, conversely, the policies that affect an individual viewpoint element.

This kind of correspondence is also used to specify the choice of technology required to implement and deploy the engineering nodes and channels. This is illustrated in figures A.17 and A.18, where the correspondences represent

![](img/b3a2d21424654c9a1d0654b2dce50e07_258_1.png)

FIGURE A.17: Correspondences from engineering to technology objects.
