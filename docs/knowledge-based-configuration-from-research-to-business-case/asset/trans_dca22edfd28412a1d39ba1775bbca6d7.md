

![](img/214a17cc1f5bbf0914497c7414128438_152_0.png)

**图 10.4** Smarthome 系统模型（第 2 部分）包含属性的分量层次结构。SmartHomeObject 是所有类的分类学根。

- 外部传感器（`SensorDeviceOutside`）为控制单元提供传感器数据。在我们的模型中，`SunBlindsControl` 解释传感器数据，而 `ControlUnit` 也对传感器数据以及手动操作（例如通过 `Switch`）做出反应。房间内的特定传感器控制房间内人员的存在。
- 分量类型 `Switch` 和 `SunBlindsControl` 具有 `SwitchType`。因此，`SwitchType` 是一个 *共享类*；然而，每个控制都有其单独的开关类型。

图 10.4 说明了系统模型中使用的所有类的泛化层次结构。虽然组合层次结构基于通用类，但泛化层次结构包括特定公司的特定组件。例如，通用类 `SensorInside` 被细化为可检测存在和亮度的内部传感器（此处称为 `PBS-A` 和 `PBS-B`，即 Presence-Brightness Sensor，两者均为 `PresenceAndBrightness` 类型）或 additionally 测量温度（`PBTS-A`，类型为 `PresenceAndBrightnessAndTemperature`）。

如第 10.2 小节所述，一个本地操作网络连接各组件。类 `NetworkNode` 汇总了通过总线连接的所有组件（即传感器和控制单元）。通过这样做，可以定义适用于所有网络节点属性以及约束。作为示例，请参阅第 10.4.2 小节中的 *系统属性约束*，其限制了 `NetworkNodes` 的 `PowerConsumption`。

外部传感器（`SensorDeviceOutside`）可以专门化为特定传感器设备 `SensorAggregate`，该设备可能包含多种类型的传感器（例如风或温度传感器），或可专门化为 `Multisensor`。`SensorAggregate` 的部件（即 `WindSensor`、`OutsideTemperatureSensor`、`BrightnessSensor` 和 `RainfallSensor`）被建模为进一步的传感器。`Multisensor` 将亮度和存在传感器集成到一个组件中。这种将不同的传感器组合成传感器聚合与使用包含各种传感器的一个多传感器之间的选择，是 Smarthome 系统的一个主要系统相关决策。根据所选功能，可以组合传感器或选择多传感器。约束 *fsc-3* 表示这种依赖关系（参见第 10.4.3 小节和表 10.1）。这些传感器还说明了属性 `Price` 的使用，所有基本组件类型都通过继承自 `ProductComponent` 而拥有该属性。因此，属性 `Price` 不必为每种组件类型建模，只需为更具体的组件定义特定的价格。

## 10.4 配置模型：约束

与结构模型类似，我们将建筑自动化系统的约束分为 *特征模型约束*（参见第 10.4.1 小节）和 *系统模型约束*（参见第 10.4.2 小节）。此外，第 10.4.3 小节提供了特征模型与系统模型之间的约束。我们提供了一组约束示例摘录，说明了以下约束类型：*资源约束*、*不兼容和兼容约束*、*requires 约束*、*共享类约束*、用于计算的 *代数约束*、*n 元基数约束*、对任意数量属性的 *all 约束*，以及通过枚举变量值可能组合来外延表达关系的 *表约束*。

### 10.4.1 特征模型约束

*图 10.2* 中定义的特征模型指定了特征的组合。通过遵循 *不兼容* 和 *requires 特征模型约束* 来减少这些组合。

**不兼容。** 同一房间中类型为 `SwitchableLightControl` 的灯组与类型为 `DimmableLightControl` 的灯组 *不兼容*。因此，用户不能同时选择这两个特征。

**共享类约束。** 每个具有 `PresenceDependent` 的 `LightGroupFeature` 需要一个 *不同的* `PresenceDetection`。因此，特征 `PresenceDetection` 仅在类层面共享，而非实例层面。

### 10.4.2 系统模型约束

系统模型必须满足以下 *系统模型约束*，分为 *系统结构约束 (ssc)* 和 *系统属性约束 (sac)*。系统结构约束限制组件类型、关联以及组合关系的基数，从而影响结果配置（解）中创建的实例的类型和数量。系统属性约束限制组件属性。

**Requires 约束 (ssc)。** 智能房间的 `SwitchableLightGroup` *需要* 该房间中的一个 `Switch`。因此，在结果配置中，两类组件的实例总是同时出现。

**共享类约束 (ssc)。** 每个 `LightGroup` 和每个 `SunBlindsControl` *必须具有其单独的* `SwitchType`；即，`SwitchType` 仅在类层面共享，而非实例层面。

**不兼容 (ssc)。** 存在和亮度传感器 `PBS-A` 和 `PBS-B` *不兼容*——它们不能在同一房间中使用。因此，这两种组件类型的实例不能出现在同一个 Smarthome 配置中。

**组合关系的代数约束 (ssc)。** 房间的 `PresenceDetection` 需要对 `PresenceDetectors` 的数量进行 *计算*。该数量取决于房间的尺寸（`RoomWidth`、`RoomHeight`）。因此，如果选择了存在依赖，则房间的尺寸必须由用户（客户）决定。

**n 元基数约束 (ssc)。** `SmartRoom` 的部件数量应为 *最小* 1 个，*最大* 26 个。因此，该约束对 *图 10.3* 中为组件类型 `SmartRoom` 所示的基数添加了进一步的限制，导致一个 n 元组合关系。

**表达物理限制的代数约束 (sac)。** `VoltageSource` 的 `ElectricalPower`、`Voltage` 和 `Current` 属性必须满足方程：`ElectricalPower = Voltage * Current`。因此，该约束计算为 `VoltageSource` 定义的属性 *电功率*（`ElectricalPower`）。

**资源约束 (sac)。** 所有 `NetworkNodes` 的 `PowerConsumption` 之和必须小于 `VoltageSource` 的 `ElectricalPower`。该约束将网络节点的功耗（`PowerConsumption`）与计算得到的 `VoltageSource` 的 `ElectricalPower` 关联起来。

**对可变数量属性的代数约束 (sac)。** 所有 `ProductComponents` 的 `Price` 之和必须等于 `SmartHome` 的 `Price`。因此，参与此约束的 `ProductComponents` 类型的实例数量不是固定的。该约束通过汇总其产品组件的价格来计算 Smarthome 的价格。

### 10.4.3 特征模型与系统模型之间的约束

`realize` 关联指定了特征模型与系统模型之间主要约束（`fsc`）。对于每个 realize 关联，都需要一个 requires 约束来确保存在实现该特征的组件。此类约束的示例有：

- **fsc-1** `LightGroupFeature` *需要* 智能房间中的一个 `LightGroup`。
- **fsc-2** `LightGroupFeature` 的 `ManualControl` *需要* 智能房间中的一个 `Dimmer` **或** 一个 `Switch`。
- **fsc-3** `SunBlindsFeature` *需要* 如表 10.1 所示的智能房间的组件。

`fsc-3` 确定了如果选择了 `SunBlindsFeature`，房间所需的传感器组合（参见表 10.1）。左侧列 *Feature Selection* 枚举了每种可能的特征选择，右侧列 *Required Components* 列出了所需的传感器。例如，在第三行，遮阳篷通过风和温度变化进行控制（即 `WindDep` 和 `TemperatureDep` 等于 yes）。因此，`WindSensor` 和 `TemperatureSensor` 包括集成的 `SensorAggregate` 必须存在于结果系统中。基本上，如果需要风依赖控制（特征 `WindDep` 等于 yes，即前四行），则必须选择具有特定传感器组合的 `SensorAggregate`，否则（第 5 至 7 行）可以选择 `Multisensor`。

**表 10.1** 某些组件实现了 `SunBlindsFeature` 的组合。一个外延表通过枚举可能的传感器组合来表示约束 `fsc-3`。以下缩写适用：WD：`WindDep`，BD：`BrightnessDep`，TD：`TemperatureDep`，SA：`SensorAggregate`，WS：`WindSensor`，BS：`BrightnessSensor`，TS：`TemperatureSensor`，MS：`MultiSensor`。

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

