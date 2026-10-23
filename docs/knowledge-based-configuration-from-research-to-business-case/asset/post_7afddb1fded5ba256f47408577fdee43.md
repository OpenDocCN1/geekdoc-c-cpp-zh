
![](img/214a17cc1f5bbf0914497c7414128438_147_0.png)

## 10.3 Configuration Model: Structure

For separating functional characteristics and technical components of building automation systems, we divide the structure of the SmartHome model (represented by `SmartHome`) into a *feature model* (represented by `SmartHomeFeature`; see Subsection 10.3.1) and a *system model* (represented by `SmartHomeSystem`; see Subsection 10.3.2). These models allow a clear separation of functional characteristics (features) of a SmartHome from the components realizing these functionalities (see the association `realize` in Figures 10.2 and 10.3). The use of SmartHome as an aggregate with two parts, `SmartHomeFeature` and `SmartHomeSystem`, combines both aspects in the resulting configuration of one product.

Both models exploit configuration knowledge representations as introduced in Hotz et al. (2014)⁴ and beyond. In particular, the presented models cover the following feature and component-related representation aspects, which will be explained in more detail in the following sections:

- *Classes* are used for representing features and component types. For example, the sun blinds feature is represented with the class `SunBlindsFeature` and a dimmer is represented with the component type `Dimmer`.
- *Instances* represent selected or inferred features or components for a certain configuration. Instances are not represented in the configuration model but created during the configuration process.

![](img/214a17cc1f5bbf0914497c7414128438_148_0.png)

**FIGURE 10.2**

The SmartHome feature model with root feature `SmartHomeFeature` is related to the system model with root component type `SmartHomeSystem` through the association realize (i.e., a `SmartHomeSystem` realizes the `SmartHomeFeature`). Both roots are part of the overall `SmartHome` model.

- *Part-of* with multiplicity is used to express feature–subfeature relations and aggregate–part relations. For example, if sun blinds are desired as a feature for a smart room, then the user (customer) should also make a decision with respect to the (sub) feature controlling the sun blinds.
- *Specialization* is used for structuring the model with respect to common attributes. For example, a dimmer is a special control unit; consequently, it has all attributes of a control unit.
- *Attributes* are only used for components. For example, the power consumption of an electrical component is modeled by an attribute of a class. Features can typically be selected by a user and have no further attributes.
- *Requires* is used for expressing dependencies between components, features, or components and features. For example, a switchable light group requires a switch.

**FIGURE 10.3**

The SmartHome system model (Part 1; with root `SmartHomeSystem`) and its relationship to the feature model (with root `SmartHomeFeature`) through the directed association realize. One example for the realize association provides the inside sensor (`SensorInside`), which realizes the presence feature modeled in the feature model as `PresenceDetection`.

![](img/214a17cc1f5bbf0914497c7414128438_149_0.png)

- *Incompatible-with* is used for excluding features or components that cannot occur together. For example, a manual control is incompatible with a presence detection.
- *Compatible* is used for features or components that can be used together but need not. For example, a sun blind can be combined with a light group.
- *Shared class* is used for expressing common aspects of different features or components. For example, a presence detection feature can be shared by a sun blind and a light group feature, but each instance shall have its own presence detection component.
- *Connections/Associations* express relations between features or components that are of particular interest in the domain. For example, a control unit is connected with a light group that it regulates.

In the following, we introduce only features, component types, and component attributes that are used in Section 10.4 for illustrating the constraints.

### 10.3.1 A Feature Model for SmartHomes

A feature model of major functional properties of a SmartHome is depicted in Figure 10.2. This model represents possible functional properties, or combinations of features. However, the components of a SmartHome system do not allow all combinations of features; consequently, realizable combinations of features are further restricted by constraints (see Section 10.4).

Figure 10.2 presents the compositional structure that divides features into subfeatures (e.g., `ManualControl` is a subfeature of `SunBlindsFeature`). In addition to the compositional structure, a configuration model has to specify also the specialization relations between classes. In the feature model of SmartHomes represented here, the specialization hierarchy for features is flat; that is, all features are specializations of `SmartHomeFeature` (these specializations are omitted in Figure 10.2 for readability purposes).

We extend the notation used in Hotz et al. (2014)⁵ for feature models by *cardinalities* (following Czarnecki et al., 2005) and *associations* for relating the feature model to the system model shown in Figure 10.3. Cardinalities can be expressed for one feature (*Features with cardinality*) or for a feature group (*Cardinality of feature group*). A feature group is a collection of features and its cardinality specifies how many features are in the collection.

In our example, one SmartHome can have up to five rooms and, thus, the `SmartHomeFeature` can have up to five `SmartRoomFeature`s. Each room in a SmartHome has its own features. Each room might have one optional `SunBlindsFeature` and up to 15 instances of `LightGroupFeature`, which can have dedicated controls, as described in the following.

**Controlling the Sun Blinds.** As a functional property, the user can select the *controlling of the sun blinds*; *that is*, his/her preferences about when the sun blinds should be lowered or raised. The sun blinds can be controlled manually or automatically depending on some environmental circumstances (see Section 10.2) such as

- The amount of light in the room (`BrightnessDep.`)
- The presence of a person in the room (`PresenceDep.`)
- A wind factor (`WindDep.`)
- The outside temperature (`TemperatureDep.`)

All these features are optional (indicated by 0..1). However, at least one feature has to exist (indicated by Or). The control alternatives can be combined when the customer selects multiple features; for example, a manual control of the sun blinds in combination with the temperature dependent control can be in one room. All combinations are possible, but the components needed for realizing a certain combination may vary (see the Constraint `fsc-3` in Subsection 10.4.3).

**Controlling the Lights.** As a further functional property, the user can select the *controlling of the lights* in the room; that is, his/her preferences for the decision when the light should switch on or off. A `LightGroupFeature` represents this functional property. It consists of one or two features of type `ConstantLightControl`, `PresenceDependent`, or `ManualControl` (each one of these is optional). Thus, the feature group `LightGroupFeature` restricts the number of its members. A light group can be controlled automatically depending on the presence of a person (`PresenceDependent` of `LightGroupFeature`), can be controlled manually (`ManualControl` of `LightGroupFeature`), or it can be a constant light (`ConstantLightControl`) that ensures constant lighting conditions. A manual control offers two options: It can either be a switch (`SwitchableLightControl`) or a dimmer (`DimmableLightControl`). However, not all combinations are possible; see Subsection 10.4.1.

A presence dependency feature (i.e., `PresenceDep` of the `SunBlindsFeature` and `PresenceDependent` of the `LightGroupFeature`) has as mandatory feature the `PresenceDetection` feature. This models the fact that the system somehow must detect the presence of a person in a room to allow presence-dependent control. The presence dependency features are more customer-oriented (*user feature*)—they can directly be selected by customers—whereas the `PresenceDetection` feature is more system related (*system feature*)—the system should have this feature, if the customer selects a presence dependency feature. The system feature `PresenceDetection` represents the connection to the system model by having an association to the realizing component `SensorInside` (see Figure 10.3).

### 10.3.2 A System Model of SmartHomes

Figures 10.3 and 10.4 present the system model of SmartHomes in two (for illustration reasons) separated parts. Figure 10.3 illustrates the definition of the compositional structure of the `SmartHomeSystem` and Figure 10.4 illustrates major parts of the generalization hierarchy. The following component types are defined:

- A `SmartHomeSystem` consists of a voltage source (`VoltageSource`), an optional central control unit (`CentralControlUnit`), up to five smart rooms (`SmartRoom`), and between zero and five outside sensors (`SensorDeviceOutside`).
- The `CentralControlUnit` allows a manual central regulation of all devices. The `VoltageSource` has to supply electrical power such that all network nodes can be included in the network.
- Each `SmartRoom` consists of light groups (`LightGroup`), control units (`ControlUnit`) such as switches (`Switch`) and dimmers (`Dimmer`), a sun-blinds control (`SunBlindsControl`), and several sensors (`SensorInside`).
- `LightGroups` include a number of lights that can be regulated together through a control unit (`ControlUnit`). A control unit can regulate several light groups (directed association regulates). A sun-blinds control (`SunBlindsControl`) regulates the sun blinds, which themselves are not part of the smart room model. Instances of `SensorInside` (i.e., sensors of the room) provide signals on the bus that are interpreted by an appropriate control.
