
![](img/214a17cc1f5bbf0914497c7414128438_152_0.png)

**FIGURE 10.4** The Smarthome system model (Part 2) with component hierarchy including attributes. SmartHomeObject is the taxonomical root of all classes.

- The outside sensors (`SensorDeviceOutside`) provide the sensor data for the control units. In our model, the `SunBlindsControl` interprets sensor data, while a `ControlUnit` reacts on sensor data as well as on manual actions (e.g., via a `Switch`). Specific sensors inside a room control the presence of a person in the room.
- The component types `Switch` and `SunBlindsControl` have a `SwitchType`. Thus, `SwitchType` is a *shared class*; however, each control has its individual switch type.

Figure 10.4 illustrates the generalization hierarchy of all classes used in the system model. While the compositional hierarchy is based on general classes, the generalization hierarchy includes specific components of certain companies. For example, the general class `SensorInside` is specialized into inside sensors that can detect both presence and brightness (here called `PBS-A` and `PBS-B` for Presence-Brightness Sensor, both of type `PresenceAndBrightness`) or additionally measure temperature (`PBTS-A` of type `PresenceAndBrightnessAndTemperature`).

As mentioned in Subsection 10.2, a local operating network connects the components. The class `NetworkNode` summarizes all components that are connected through the bus (i.e., sensors and control units). By doing so, it is possible to define attributes as well as constraints that apply to all network nodes. As an example, see the *System Attribute Constraints* in Subsection 10.4.2, which restrict the `PowerConsumption` of `NetworkNodes`.

The outside sensors (`SensorDeviceOutside`) can be specialized to the specific sensor device `SensorAggregate` that may contain several types of sensors (such as wind or temperature sensors) or can be specialized to `Multisensor`. The parts of `SensorAggregate` (i.e., `WindSensor`, `OutsideTemperatureSensor`, `BrightnessSensor`, and `RainfallSensor`) are modeled as further sensors. A `Multisensor` covers brightness and presence sensors in one component. This choice between a combination of distinct sensors into a sensor aggregate and the use of one multisensor, which includes various sensors, is one of the major system-related decisions for a Smarthome system. Depending on the selected features, a combination of sensors or choice of the multisensor is possible. The Constraint *fsc-3* represents this dependency (see Subsection 10.4.3 and Table 10.1). These sensors furthermore illustrate the use of attribute `Price`, which all basic component types have by inheriting it from `ProductComponent`. Thus, the attribute `Price` does not have to be modeled for each component type and only specific prices have to be defined for the more specific components.

## 10.4 Configuration Model: Constraints

Like the structure model, we divide the constraints for a building automation system into *feature model constraints* (see Subsection 10.4.1) and *system model constraints* (see Subsection 10.4.2). Additionally, Subsection 10.4.3 provides constraints between the feature model and the system model. We provide an excerpt of constraint examples that illustrate the following constraint types: *resource constraint*, *incompatibility and compatibility constraint*, *requires constraint*, *constraint for sharing classes*, *algebraic constraint* for computations, *n-ary cardinality constraint*, *all-constraint* over an arbitrary number of attributes, and *table constraint*, which expresses a relation extensionally by enumerating possible combinations of variable values.

### 10.4.1 Feature Model Constraints

The feature model defined in *Figure 10.2* specifies combinations of features. A reduction of these combinations is achieved by following *incompatibility* and *requires Feature Model Constraints*.

**Incompatibility.** A light group of type `SwitchableLightControl` is *incompatible* with a light group of type `DimmableLightControl` in the same room. Thus, both features cannot be selected at the same time by the user.

**Constraint for sharing classes.** Each `LightGroupFeature` with a `PresenceDependent` requires a *distinct* `PresenceDetection`. Thus, the feature `PresenceDetection` is only shared for classes and not for instances.

### 10.4.2 System Model Constraints

The system model has to fulfill the following *System Model Constraints*, which are divided into *System Structure Constraints (ssc)* and *System Attribute Constraints (sac)*. System Structure Constraints restrict component types, associations, and cardinalities of compositional relations and, hence, influence the type and number of created instances for the resulting configuration (solution). System Attribute Constraints restrict component attributes.

**Requires constraint (ssc).** A `SwitchableLightGroup` of a smart room *requires* a `Switch` in that room. Thus, instances of both component types always occur together in the resulting configuration.

**Constraint for sharing classes (ssc).** Each `LightGroup` and each `SunBlindsControl` *has to have its individual* `SwitchType`; that is, the `SwitchType` is only shared for classes and not for instances.

**Incompatibility (ssc).** The presence and brightness sensors `PBS-A` and `PBS-B` are *incompatible*—they cannot be used together in a room. Thus, instances of those component types cannot occur in one Smarthome configuration.

**Algebraic constraint for a compositional relation (ssc).** A `PresenceDetection` of a room requires a *computation* of the number of `PresenceDetectors`. This number depends on the size (`RoomWidth`, `RoomHeight`) of the room. Thus, the size of a room has to be decided by the user (customer) if presence dependency was selected.

**N-ary cardinality constraint (ssc).** The number of parts of a `SmartRoom` shall be 1 at *minimum* and 26 at *maximum*. Thus, this constraint adds a further cardinality restriction to the ones shown in *Figure 10.3* for the component type `SmartRoom`, which leads to an n-ary compositional relation.

**Algebraic constraint for expressing a physical restriction (sac).** The `ElectricalPower`, `Voltage`, and `Current` attributes of `VoltageSource` have to fulfill the equation: `ElectricalPower = Voltage * Current`. Thus, the constraint computes the attribute *electrical power* (`ElectricalPower`) defined for the `VoltageSource`.

**Resource constraint (sac).** The sum of the `PowerConsumption` of all `NetworkNodes` has to be less than the `ElectricalPower` of `VoltageSource`. The constraint relates the power consumption of the network nodes (`PowerConsumption`) to the computed `ElectricalPower` of `VoltageSource`.

**Algebraic constraint for a varying number of attributes (sac).** The sum of the `Price` of all `ProductComponents` has to be equal to the `Price` of the `SmartHome`. Consequently, the number of instances of type `ProductComponents` involved in this constraint is not fixed. The constraint computes the price of the Smarthome by summing up the price of its product components.

### 10.4.3 Constraints between Feature Model and System Model

The `realize` association specifies the major constraints between the feature model and the system model (`fsc`). For each realize association a requires constraint is needed that ensures the existence of a component that realizes a feature. Examples of such constraints are:

- **fsc-1** The `LightGroupFeature` *requires* a `LightGroup` in the smart room.
- **fsc-2** The `ManualControl` of `LightGroupFeature` *requires* a `Dimmer` **or** a `Switch` in the smart room.
- **fsc-3** `SunBlindsFeature` *requires* components for a smart room as illustrated in Table 10.1.

`fsc-3` determines which combinations of sensors are required for a room, if the `SunBlindsFeature` is selected (see Table 10.1). Each possible selection of features is enumerated on the left columns *Feature Selection* and the required sensors are listed on the right columns *Required Components*. For example, in the third row the sun blinds are controlled through wind and temperature changes (i.e., `WindDep` and `TemperatureDep` equal to yes). Thus, a `WindSensor` and `TemperatureSensor` including the integrating `SensorAggregate` must be in the resulting system. Basically, if a wind-dependent control is needed (feature `WindDep` equals to yes, i.e., the first four rows) the `SensorAggregate` with a certain combination of sensors has to be selected, otherwise (row 5 to 7) the `Multisensor` can be selected.

**Table 10.1** Certain components realize combinations of the `SunBlindsFeature`. An extensional table represents the constraint `fsc-3` by enumerating possible sensor combinations. The following abbreviations hold: WD: `WindDep`, BD: `BrightnessDep`, TD: `TemperatureDep`, SA: `SensorAggregate`, WS: `WindSensor`, BS: `BrightnessSensor`, TS: `TemperatureSensor`, MS: `MultiSensor`.

| WD | BD | TD | SA | WS | BS | TS | MS |
| --- | --- | --- | --- | --- | --- | --- | --- |
| yes | yes | yes | yes | yes | yes | yes | no |
| yes | yes | no | yes | yes | yes | no | no |
| yes | no | yes | yes | yes | no | yes | no |
| yes | no | no | yes | yes | no | no | no |
| no | yes | yes | no | no | no | no | yes |
| no | yes | no | no | no | no | no | yes |
| no | no | yes | no | no | no | no | yes |
| no | no | no | no | no | no | no | no |
