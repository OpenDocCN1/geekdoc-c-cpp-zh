

The resulting Peripheral turns an LED on and off when instructed, and reports that it’s processed the command.

When the Central sends the “Light On” command, the Serial Monitor should resemble this (Figure 12-4):

## Example code

The code for this chapter is available online at: [https://github.com/BluetoothLowEnergyInArduino101/Chapter12](https://github.com/BluetoothLowEnergyInArduino101/Chapter12)

## Appendix I: Bluetooth Properties

For reference, the following are properties of the Bluetooth Low Energy network and hardware.

| Property | Value |
|---|---|
| Range | 100 m (330 ft) |
| Data Rate | 1M bit/s |
| Application Throughput | 0.27 Mbit/s |
| Security | 128-bit AES with Counter Mode CBC-MAC and application layer user data encryption (BEWARE: this encryption has vulnerabilities) |
| Robustness | Adaptive Frequency Hopping, Layer Acknowledgement, 24-bit CRC, 32-bit Message Integrity Check |
| Peak Current Consumption | < 15 mA |
| Byte-Order in Broadcast | Big Endian (most significant bit at ... ) |

## Appendix II: UUID Format

Bluetooth Low Energy has tight space requirements. Therefore it is preferred to transmit 16-bit UUIDs instead of 32-bit UUIDs. UUIDs can be converted between 16-bit and 32-bit with the standard Bluetooth Low Energy UUID format:

**Table II-1. 16-bit to 32-bit UUID Conversion Standard**

| UUID Format | uuid16 | Resulting uuid32 |
|---|---|---|
| 00000000-0000-1000-8000-00805f9b34fb | 0x2A56 | 00002A56-0000-1000-8000-00805f9b34fb |

## Appendix III: Minimal Recommended GATT

As a best practice, it is good to host a standard set of Services and Characteristics in a Peripheral's GATT Profile. These Characteristics allow connected Centrals to get the make and model number of the device, and the battery level if the Peripheral is battery-powered:

**Table III-1. Minimal GATT Profile**

| GATT Type | Name | Data Type | UUID |
|---|---|---|---|
| Service | Device Information Service |  | 0x180A |
| Characteristic | Device Name | char array | 0x2A00 |
| Characteristic | Model Number | char array | 0x2A24 |
| Characteristic | Serial Number | char array | 0x2A25 |
| Service | Battery Service |  | 0x180F |
| Characteristic | Battery Level | integer | 0x2A19 |

| Service | UUID | Name |
|---|---|---|
| Battery Service | 0x180F | org.bluetooth.service.battery_service |
| Blood Pressure | 0x1810 | org.bluetooth.service.blood_pressure |
| Body Composition | 0x181B | org.bluetooth.service.body_composition |
| Bond Management | 0x181E | org.bluetooth.service.bond_management |
| Continuous Glucose Monitoring | 0x181F | org.bluetooth.service.continuous_glucose_monitoring |
| Current Time Service | 0x1805 | org.bluetooth.service.current_time |
| Cycling Power | 0x1818 | org.bluetooth.service.cycling_power |
| Cycling Speed and Cadence | 0x1816 | org.bluetooth.service.cycling_speed_and_cadence |
| Device Information | 0x180A | org.bluetooth.service.device_information |
| Environmental Sensing | 0x181A | org.bluetooth.service.environmental_sensing |
| Generic Access | 0x1800 | org.bluetooth.service.generic_access |
| Generic |  |  |

| 属性 | UUID | 服务 UUID |
| --- | --- | --- |
| 通用属性 | 0x1801 | org.bluetooth.service.generic_attribute |
| 血糖 | 0x1808 | org.bluetooth.service.glucose |
| 健康体温计 | 0x1809 | org.bluetooth.service.health_thermometer |
| 心率 | 0x180D | org.bluetooth.service.heart_rate |
| HTTP 代理 | 0x1823 | org.bluetooth.service.http_proxy |
| 人机接口设备 | 0x1812 | org.bluetooth.service.human_interface_device |
| 立即警报 | 0x1802 | org.bluetooth.service.immediate_alert |
| 室内定位 | 0x1821 | org.bluetooth.service.indoor_positioning |
| 互联网协议支持 | 0x1820 | org.bluetooth.service.internet_protocol_support |
| 链路丢失 | 0x1803 | org.bluetooth.service.link_loss |
| 位置与导航 | 0x1819 | org.bluetooth.service.location_and_navigation |
| 下次夏令时变更服务 | 0x1807 | org.bluetooth.service.next_dst_change_service |
| 对象传输 | 0x1825 | org.bluetooth.service.object_transfer |
| 电话提醒状态服务 | 0x180E | org.bluetooth.service.phone_alert_status |
| 脉搏血氧仪 | 0x1822 | org.bluetooth.service.pulse_oximeter |
| 参考时间更新服务 | 0x1806 | org.bluetooth.service.reference_time_update |
| 跑步速度与步频 | 0x1814 | org.bluetooth.service.running_speed_and_cadence |
| 扫描参数 | 0x1813 | org.bluetooth.service.scan_parameters |
| 传输发现 | 0x1824 | org.bluetooth.service.transport_discovery |
| 发射功率 | 0x1804 | org.bluetooth.service.tx_power |
| 用户数据 | 0x181C | org.bluetooth.service.user_data |
| 体重秤 | 0x181D | org.bluetooth.service.weight_scale |

**来源：** Bluetooth SIG：GATT 服务

摘自 https://www.bluetooth.com/specifications/gatt/services

| 名称 | UUID | 描述 |
| --- | --- | --- |
| 视风风向 | 0x2A73 | org.bluetooth.characteristic.apparent_wind_direction |
| 视风风速 | 0x2A72 | org.bluetooth.characteristic.apparent_wind_speed |
| 外观 | 0x2A01 | org.bluetooth.characteristic.gap.appearance |
| 气压趋势 | 0x2AA3 | org.bluetooth.characteristic.barometric_pressure_trend |
| 电池电量 | 0x2A19 | org.bluetooth.characteristic.battery_level |
| 血压特征 | 0x2A49 | org.bluetooth.characteristic.blood_pressure_feature |
| 血压测量 | 0x2A35 | org.bluetooth.characteristic.blood_pressure_measurement |
| 身体成分特征 | 0x2A9B | org.bluetooth.characteristic.body_composition_feature |
| 身体成分测量 | 0x2A9C | org.bluetooth.characteristic.body_composition_measurement |
| 身体传感器位置 | 0x2A38 | org.bluetooth.characteristic.body_sensor_location |
| CGM 会话运行时间 | 0x2AAB | org.bluetooth.characteristic.cgm_session_run_time |
| CGM 会话开始时间 | 0x2AAA | org.bluetooth.characteristic.cgm_session_start_time |
| CGM 特定操作控制点 | 0x2AAC | org.bluetooth.characteristic.cgm_specific_ops_control_point |
| CGM 状态 | 0x2AA9 | org.bluetooth.characteristic.cgm_status |
| CSC 特征 | 0x2A5C | org.bluetooth.characteristic.csc_feature |
| CSC 测量 | 0x2A5B | org.bluetooth.characteristic.csc_measurement |
| 当前时间 | 0x2A2B | org.bluetooth.characteristic.current_time |
| 骑行功率控制点 | 0x2A66 | org.bluetooth.characteristic.cycling_power_control_point |
| 骑行功率特征 | 0x2A65 | org.bluetooth.characteristic.cycling_power_feature |
| 骑行功率测量 | 0x2A63 | org.bluetooth.characteristic.cycling_power_measurement |
| 骑行功率向量 | 0x2A64 | org.bluetooth.characteristic.cycling_power_vector |
| 数据库更改增量 | 0x2A99 | org.bluetooth.characteristic.database_change_increment |
| 出生日期 | 0x2A85 | org.bluetooth.characteristic.date_of_birth |
| 阈值评估日期 | 0x2A86 | org.bluetooth.characteristic.date_of_threshold_assessment |
| 日期时间 | 0x2A08 | org.bluetooth.characteristic.date_time |
| 日日期时间 | 0x2A0A | org.bluetooth.characteristic.day_date_time |
| 星期几 | 0x2A09 | org.bluetooth.characteristic.day_of_week |
| 描述符值已更改 | 0x2A7D | org.bluetooth.characteristic.descriptor_value_changed |
| 设备名称 | 0x2A00 | org.bluetooth.characteristic.gap.device_name |
| 露点 | 0x2A7B | org.bluetooth.characteristic.dew_point |
| 数字 | 0x2A56 | org.bluetooth.characteristic.digital |
| 夏令时偏移 | 0x2A0D | org.bluetooth.characteristic.dst_offset |
| 海拔 | 0x2A6C | org.bluetooth.characteristic.elevation |
| 电子邮件地址 | 0x2A87 | org.bluetooth.characteristic.email_address |
| 精确时间 256 | 0x2A0C | org.bluetooth.characteristic.exact_time_256 |
| 燃脂心率 | 0x2A88 | org.bluetooth.characteristic.fat_burn_heart_rate |
| HTTP 状态码 | 0x2AB8 | org.bluetooth.characteristic.http_status_code |
| HTTPS 安全性 | 0x2ABB | org.bluetooth.characteristic.https_security |
| 湿度 | 0x2A6F | org.bluetooth.characteristic.humidity |
| IEEE 11073-20601 监管认证数据列表 | 0x2A2A | org.bluetooth.characteristic.ieee_11073-20601_regulatory_certification_data_list |
| 室内定位配置 | 0x2AAD | org.bluetooth.characteristic.indoor_positioning_configuration |
| 中间袖带压力 | 0x2A36 | org.bluetooth.characteristic.intermediate_cuff_pressure |
| 中间温度 | 0x2A1E | org.bluetooth.characteristic.intermediate_temperature |
| 辐照度 | 0x2A77 | org.bluetooth.characteristic.irradiance |
| 语言 | 0x2AA2 | org.bluetooth.characteristic.language |
| 姓氏 | 0x2A90 | org.bluetooth.characteristic.last_name |
| 纬度 | 0x2AAE | org.bluetooth.characteristic.latitude |
| LN 控制 | 0x2A6B | org.bluetooth.characteristic.ln_control |
| 最大推荐心率 | 0x2A91 | org.bluetooth.characteristic.maximum_recommended_heart_rate |
| 测量间隔 | 0x2A21 | org.bluetooth.characteristic.measurement_interval |
| 型号字符串 | 0x2A24 | org.bluetooth.characteristic.model_number_string |
| 导航 | 0x2A68 | org.bluetooth.characteristic.navigation |
| 新提醒 | 0x2A46 | org.bluetooth.characteristic.new_alert |
| 对象操作控制点 | 0x2AC5 | org.bluetooth.characteristic.object_action_control_point |
| 对象已更改 | 0x2AC8 | org.bluetooth.characteristic.object_changed |
| 对象首次创建 | 0x2AC1 | org.bluetooth.characteristic.object_first_created |
| 对象 ID | 0x2AC3 | org.bluetooth.characteristic.object_id |
| 对象上次修改 | 0x2AC2 | org.bluetooth.characteristic.object_last_modified |
| 对象列表控制点 | 0x2AC6 | org.bluetooth.characteristic.object_list_control_point |
| 对象列表过滤器 | 0x2AC7 | org.bluetooth.characteristic.object_list_filter |
| 对象名称 | 0x2ABE | org.bluetooth.characteristic.object_name |
| 对象属性 | 0x2AC4 | org.bluetooth.characteristic.object_properties |
| 对象大小 | 0x2AC0 | org.bluetooth.characteristic.object_size |
| 对象类型 | 0x2ABF | org.bluetooth.characteristic.object_type |
| OTS 特征 | 0x2ABD | org.bluetooth.characteristic.ots_feature |
| 外设首选连接参数 | 0x2A04 | org.bluetooth.characteristic.gap.peripheral_preferred_connection_parameters |
| 外设隐私标志 | 0x2A02 | org.bluetooth.characteristic.gap.peripheral_privacy_flag |
| PLX 连续测量 | 0x2A5F | org.bluetooth.characteristic.plx_continuous_measurement |
| PLX 特征 | 0x2A60 | org.bluetooth.characteristic.plx_features |
| PLX 抽查测量 | 0x2A5E | org.bluetooth.characteristic.plx_spot_check_measurement |
| PnP ID | 0x2A50 | org.bluetooth.characteristic.pnp_id |
| 花粉浓度 | 0x2A75 | org.bluetooth.characteristic.pollen_concentration |
| RSC 特征 | 0x2A54 | org.bluetooth.characteristic.rsc_feature |
| RSC 测量 | 0x2A53 | org.bluetooth.characteristic.rsc_measurement |
| SC 控制点 | 0x2A55 | org.bluetooth.characteristic.sc_control_point |
| 扫描间隔窗口 | 0x2A4F | org.bluetooth.characteristic.scan_interval_window |
| 扫描刷新 | 0x2A31 | org.bluetooth.characteristic.scan_refresh |
| 传感器位置 | 0x2A5D | org.bluetooth.characteristic.sensor_location |
| 序列号字符串 | 0x2A25 | org.bluetooth.characteristic.serial_number_string |
| 服务已更改 | 0x2A05 | org.bluetooth.characteristic.gatt.service_changed |
| 软件版本字符串 | 0x2A28 | org.bluetooth.characteristic.software_revision_string |
| 有氧和无氧阈值的运动类型 | 0x2A93 | org.bluetooth.characteristic.sport_type_for_aerobic_and_anaerobic_thresholds |
| 支持的新提醒类别 | 0x2A47 | org.bluetooth.characteristic.supported_new_alert_category |

| 名称 | UUID | 描述 |
|---|---|---|
| 受支持的新警报类别 | 0x2A47 | org.bluetooth.characteristic.supported_new_alert_category |
| 受支持的未读警报类别 | 0x2A48 | org.bluetooth.characteristic.supported_unread_alert_category |
| 系统 ID | 0x2A23 | org.bluetooth.characteristic.system_id |
| TDS 控制点 | 0x2ABC | org.bluetooth.characteristic.tds_control_point |
| 温度 | 0x2A6E | org.bluetooth.characteristic.temperature |
| 温度测量 | 0x2A1C | org.bluetooth.characteristic.temperature_measurement |
| 温度类型 | 0x2A1D | org.bluetooth.characteristic.temperature_type |
| 三区心率限值 | 0x2A94 | org.bluetooth.characteristic.three_zone_heart_rate_limits |
| 时间精度 | 0x2A12 | org.bluetooth.characteristic.time_accuracy |
| 时间源 | 0x2A13 | org.bluetooth.characteristic.time_source |
| 时间更新控制点 | 0x2A16 | org.bluetooth.characteristic.time_update_control_point |
| 时间更新状态 | 0x2A17 | org.bluetooth.characteristic.time_update_state |
| 含夏令时的时间 | 0x2A11 | org.bluetooth.characteristic.time_with_dst |
| 时区 | 0x2A0E | org.bluetooth.characteristic.time_zone |
| 真风向 | 0x2A71 | org.bluetooth.characteristic.true_wind_direction |
| 真风速 | 0x2A70 | org.bluetooth.characteristic.true_wind_speed |
| 双区心率限值 | 0x2A95 | org.bluetooth.characteristic.two_zone_heart_rate_limit |
| 发射功率电平 | 0x2A07 | org.bluetooth.characteristic.tx_power_level |
| 不确定性 | 0x2AB4 | org.bluetooth.characteristic.uncertainty |
| 未读警报状态 | 0x2A45 | org.bluetooth.characteristic.unread_alert_status |
| URI | 0x2AB6 | org.bluetooth.characteristic.uri |
| 用户控制点 | 0x2A9F | org.bluetooth.characteristic.user_control_point |
| 用户索引 | 0x2A9A | org.bluetooth.characteristic.user_index |
| 紫外线指数 | 0x2A76 | org.bluetooth.characteristic.uv_index |
| 最大摄氧量 | 0x2A96 | org.bluetooth.characteristic.vo2_max |
| 腰围 | 0x2A97 | org.bluetooth.characteristic.waist_circumference |
| 重量 | 0x2A98 | org.bluetooth.characteristic.weight |
| 重量测量 | 0x2A9D | org.bluetooth.characteristic.weight_measurement |
| 体重秤功能 | 0x2A9E | org.bluetooth.characteristic.weight_scale_feature |
| 风寒指数 | 0x2A79 | org.bluetooth.characteristic.wind_chill |

**来源：** Bluetooth SIG：GATT 特征。取自 https://www.bluetooth.com/specifications/gatt/characteristics

## 附录 VI：GATT 描述符

以下 GATT 描述符 UUID 已保留用于特定用途。

GATT 描述符用于描述特征中可修改的属性，例如，客户端特征配置（0x2902）可被标记，以允许已连接的中央设备订阅某特征的通知。

### 表 VI-1. 保留的 GATT 描述符

| 规范名称 | UUID | 规范 |
|---|---|---|
| 特征聚合格式 | 0x2905 | org.bluetooth.descriptor.gatt.characteristic_aggregate_format |
| 特征扩展属性 | 0x2900 | org.bluetooth.descriptor.gatt.characteristic_extended_properties |
| 特征表示格式 | 0x2904 | org.bluetooth.descriptor.gatt.characteristic_presentation_format |
| 特征用户描述 | 0x2901 | org.bluetooth.descriptor.gatt.characteristic_user_description |
| 客户端特征配置 | 0x2902 | org.bluetooth.descriptor.gatt.client_characteristic_configuration |
| 环境传感配置 | 0x290B | org.bluetooth.descriptor.es_configuration |
| 环境传感测量 | 0x290C | org.bluetooth.descriptor.es_measurement |
| 环境传感触发设置 | 0x290D | org.bluetooth.descriptor.es_trigger_setting |
| 外部报告引用 | 0x2907 | org.bluetooth.descriptor.external_report_reference |
| 数字量数目 | 0x2909 | org.bluetooth.descriptor.number_of_digitals |
| 报告引用 | 0x2908 | org.bluetooth.descriptor.report_reference |
| 服务端特征配置 | 0x2903 | org.bluetooth.descriptor.gatt.server_characteristic_configuration |
| 时间触发设置 | 0x290E | org.bluetooth.descriptor.time_trigger_setting |
| 有效范围 | 0x2906 | org.bluetooth.descriptor.valid_range |
| 值触发设置 | 0x290A | org.bluetooth.descriptor.value_trigger_setting |

**来源：** Bluetooth SIG：GATT 描述符。取自 https://www.bluetooth.com/specifications/gatt/descriptors

## 附录 VII：公司标识符

以下公司拥有特定的制造商标识符，用于在通用访问规范（GAP）中标识蓝牙设备。没有特定制造商的外设使用 ID 65535（0xffff）。所有其他 ID 均被保留，即使尚未分配。

此列表并非详尽无遗。完整且更新的列表可在 Bluetooth SIG 网站上找到。

### 表 VII-1. 公司标识符

| 十进制 | 十六进制 | 公司 |
|---|---|---|
| 0 | 0x0000 | 爱立信技术许可 |
| 1 | 0x0001 | 诺基亚移动电话 |
| 2 | 0x0002 | 英特尔公司 |
| 3 | 0x0003 | IBM 公司 |
| 4 | 0x0004 | 东芝公司 |
| 5 | 0x0005 | 3Com 公司 |
| 6 | 0x0006 | 微软 |
| 7 | 0x0007 | 朗讯 |
| 8 | 0x0008 | 摩托罗拉 |
| 13 | 0x000D | 德州仪器公司 |
| 19 | 0x0013 | 爱特梅尔公司 |
| 29 | 0x001D | 高通 |
| 36 | 0x0024 | 阿尔卡特 |
| 37 | 0x0025 | 恩智浦半导体（前身为飞利浦半导体） |
| 60 | 0x003C | 黑莓有限公司（前身为 RIM 公司） |
| 76 | 0x004C | 苹果公司 |
| 86 | 0x0056 | 索尼爱立信移动通信 |
| 89 | 0x0059 | 北欧半导体公司 |
| 92 | 0x005C | 贝尔金国际公司 |
| 93 | 0x005D | 瑞昱半导体公司 |
| 101 | 0x0065 | 惠普公司 |
| 104 | 0x0068 | 通用汽车 |
| 117 | 0x0075 | 三星电子有限公司 |
| 120 | 0x0078 | 耐克公司 |
| 135 | 0x0087 | 佳明国际公司 |
| 138 | 0x008A | Jawbone |
| 184 | 0x00B8 | 高通创新中心（QuIC） |
| 215 | 0x00D7 | 高通技术公司 |
| 216 | 0x00D8 | 高通互联体验 |
| 220 | 0x00DC | 宝洁 |
| 224 | 0x00E0 | 谷歌 |
| 359 | 0x0167 | 拜耳医疗保健 |
| 367 | 0x016F | Podo 实验室公司 |
| 369 | 0x0171 | 亚马逊物流服务 |
| 387 | 0x0183 | 华特迪士尼 |
| 398 | 0x018E | Fitbit 公司 |
| 425 | 0x01A9 | 佳能公司 |
| 427 | 0x01AB | Facebook 公司 |
| 474 | 0x01DA | 罗技国际公司 |
| 558 | 0x022E | 西门子股份公司 |
| 605 | 0x025D | 利盟国际公司 |
| 637 | 0x027D | 华为技术有限公司 |
| 720 | 0x02D0 | 3M 公司 |
| 876 | 0x036C | Zipcar |
| 897 | 0x0381 | 夏普公司 |
| 921 | 0x0399 | 尼康公司 |
| 1117 | 0x045D | 波士顿科学公司 |
| 65535 | 0xFFFF | 无设备 ID |

**来源：** Bluetooth SIG：公司标识符。取自 https://www.bluetooth.com/specifications/assigned-numbers/company-identifiers

## 术语表

以下是蓝牙低功耗相关术语及其含义的列表。

- **安卓** - 一种用于智能手机和平板电脑的开源操作系统。
- **Arduino** - 一个开源计算机硬件与软件公司、项目及用户社区，设计并制造单板微控制器和微控制器套件，用于构建能够感知和控制现实世界物体的数字设备与交互式对象。
- **属性** - GATT 配置文件中的一个单元，可供中央设备访问，例如服务或特征。
- **信标** - 一种持续广播的蓝牙低功耗外设，使中央设备能够从广播属性中收集的信息来辨别自己的位置。
- **蓝牙低功耗（BLE）** - 一种用于微型电子设备的低功率、短距离无线协议。
- **广播** - 蓝牙低功耗的一项功能，外设通过它输出自己的名称和其他特定数据。

- **中心设备** - 一种低功耗蓝牙设备，可连接多个外围设备。
- **信道** - 一种经过精细调谐的射频频率，用于广播或数据传输。
- **特征** - 一个端口或数据端点，可在此读取或写入数据。
- **描述符** - 特征的一项功能，允许某种数据交互，例如读取、写入或通知。
- **E0** - 低功耗蓝牙内置的加密算法。
- **通用属性（GATT）配置文件** - 一组服务和特征的列表，这些服务和特征是外围设备所特有的，并描述外围设备如何提供数据。GATT配置文件由外围设备托管。
- **iBeacon** - 一种与苹果兼容的信标，允许中心设备下载特定的数据包，以告知中心设备其绝对位置和其他属性。
- **Intel® Curie™模块** - 为Arduino 101提供支持并包含蓝牙芯片组的Intel®模块。
- **通知** - 外围设备提醒中心设备数据发生变化的一种操作。
- **外围设备** - 一种低功耗蓝牙设备，可连接到单个中心设备。外围设备托管通用属性（GATT）配置文件。
- **读取** - 中心设备从特征下载数据的一种操作。
- **扫描** - 中心设备搜索广播中的外围设备的过程。
- **扫描响应** - 低功耗蓝牙的一项功能，允许中心设备在不连接的情况下下载一小包数据。
- **服务** - 用于组织数据端点的容器结构。服务由外围设备托管。
- **通用唯一标识符（UUID）** - 一个较长、随机生成的字母数字字符串，无论在哪里使用都是唯一的。UUID旨在避免无数程序相互交互时可能发生的名称冲突。
- **写入** - 中心设备更改特征上数据的一种操作。

## 关于作者

![](img/d7b9d81704fe6839dbdc99a45736bfb5_219_0.png)

托尼有着无穷无尽的好奇心，这促使他想要探索和学习他所接触的一切；而他的热情又驱使他将所学分享给他人。

他有两大真正的热爱：品牌塑造和发明创造。

他对品牌塑造的热情促使他创办了一家公司，为苹果、英特尔和索尼BMG等企业在四个国家开展品牌和营销业务。他喜欢将设计、写作、产品和战略等元素编织成一个定义公司的本质真理。

他对发明的热情促使他创办了一家利用脑成像技术量化冥想并预测癫痫发作的公司。该公司获得了150万美元的融资，并在旧金山孵化，他目前居住在那里。

同样的热情也让他经历了一些冒险，包括与希腊东正教僧侣一起住在修道院里，以及跟随西班牙的一位吉普赛人学习弹奏弗拉门戈吉他。

## 关于本书

本书是一本实用的指南，介绍如何在Android手机和平板电脑上进行低功耗蓝牙编程。

在本书中，你将学习如何编写Android设备程序，使其通过低功耗蓝牙与任何中心设备或外围设备通信的基础知识。本书的每一章都建立在前一章的基础上，最终形成了三个项目：

- 信标与扫描器
- 回显服务器与客户端
- 遥控设备

在阅读本书的过程中，你将学习到一些重要的概念，这些概念涉及：

- 低功耗蓝牙如何工作
- 数据如何发送和接收
- 处理数据的常见范式

## 技能水平

无论你对Android上的Java编程有基础还是高级知识，这本书都非常适合你。

## 本系列其他图书

如果你对其他低功耗蓝牙设备的编程感兴趣，请查看本系列的其他图书，或访问[bluetoothlowenergybooks.com](http://bluetoothlowenergybooks.com)：

![](img/d7b9d81704fe6839dbdc99a45736bfb5_223_0.png)

### Android Java中的低功耗蓝牙编程

Tony Gaitatzis, 2017

ISBN: 978-1-7751280-1-4

![](img/d7b9d81704fe6839dbdc99a45736bfb5_224_0.png)

### iOS Swift中的低功耗蓝牙编程

Tony Gaitatzis, 2017

ISBN: 978-1-7751280-0-7

![](img/d7b9d81704fe6839dbdc99a45736bfb5_224_1.png)

### 面向nRF微控制器的C++低功耗蓝牙编程

Tony Gaitatzis, 2017

ISBN: 978-1-7751280-3-8

（此页有意留白。）

- **广播** - 低功耗蓝牙的一项功能，外围设备借此输出自己的名称和其他特定数据。
- **属性** - GATT配置文件中的一个单元，可由中心设备访问，例如服务或特征。
- **信标** - 一种低功耗蓝牙外围设备，通过持续广播，使中心设备能够从广播属性中获取的信息来辨别它们的位置。
- **大端** - 一种以二进制存储数字的机制，数字的最高有效值最先存储，通常显示在屏幕右侧。
- **低功耗蓝牙（BLE）** - 一种供微电子设备使用的低功耗、短距离无线协议。
- **中心设备** - 一种低功耗蓝牙设备，可连接多个外围设备。
- **信道** - 一种经过精细调谐的射频频率，用于广播或数据传输。
- **特征** - 一个端口或数据端点，可在此读取或写入数据。
- **描述符** - 特征的一项功能，允许某种数据交互，例如读取、写入或通知。
- **E0** - 低功耗蓝牙内置的加密算法。
- **通用访问配置文件（GAP）** - 关于外围设备的标识信息，用于通过名称、服务列表、可连接性或其他自定义数据来识别外围设备。这些数据在连接后可访问，并以大端格式存储。
- **iBeacon** - 一种与苹果兼容的信标，允许中心设备下载特定的数据包，以告知中心设备其绝对位置和其他属性。
- **小端** - 一种以二进制存储数字的机制，数字的最低有效值最先存储，通常显示在屏幕右侧。
- **通知** - 外围设备提醒中心设备数据发生变化的一种操作。
- **外围设备** - 一种低功耗蓝牙设备，可连接到单个中心设备。外围设备托管通用属性（GATT）配置文件。
- **读取** - 中心设备从特征下载数据的一种操作。
- **扫描** - 中心设备搜索广播中的外围设备的过程。
- **扫描响应** - 低功耗蓝牙的一项功能，允许中心设备在不连接的情况下下载一小包数据。
- **服务** - 用于组织数据端点的容器结构。服务由外围设备托管。
- **通用唯一标识符（UUID）** - 一个较长、随机生成的字母数字字符串，无论在哪里使用都是唯一的。UUID旨在避免无数程序相互交互时可能发生的名称冲突。
- **写入** - 中心设备更改特征上数据的一种操作。
- **Android** - 用于智能手机和平板电脑的开源操作系统。
- **广播** - 低功耗蓝牙的一项功能，外围设备借此输出自己的名称和其他特定数据。
- **信标** - 一种低功耗蓝牙外围设备，通过持续广播，使中心设备能够从广播属性中获取的信息来辨别它们的位置。
- **大端** - 一种以二进制存储数字的机制，数字的最高有效值最先存储，通常显示在屏幕右侧。
- **低功耗蓝牙（BLE）** - 一种供微电子设备使用的低功耗、短距离无线协议。
- **中心设备** - 一种低功耗蓝牙设备，可连接多个外围设备。
- **信道** - 一种经过精细调谐的射频频率，用于广播或数据传输。

## 特征

可以读取或写入数据的端口或数据端点。

## 描述符

特征的一项特性，允许进行某种数据交互，如读取、写入或通知。

## E0

低功耗蓝牙内置的加密算法。

## 通用访问配置文件（GAP）

关于外围设备的识别信息，通过名称、服务列表、可连接性或其他自定义数据来标识外围设备。此数据在连接后可访问，并以大端格式存储。

## iBeacon

一种兼容苹果的信标，允许中心设备下载特定数据包，以告知中心设备其绝对位置和其他属性。

## 小端序

一种以二进制存储数字的机制，其中数字的最低有效值最先存储，通常在屏幕的右侧表示。

## 通知

外围设备向中心设备提醒数据发生变化的一种操作。

## 外围设备

一种低功耗蓝牙设备，可以连接到单个中心设备。外围设备托管通用属性（GATT）配置文件。

## 读取

中心设备从特征下载数据的一种操作。

## 扫描

中心设备搜索广播外围设备的过程。

## 扫描响应

低功耗蓝牙的一项功能，允许中心设备在不连接的情况下下载一个小数据包。

## 服务

用于组织数据端点的容器结构。服务由外围设备托管。

## 写入

中心设备修改特征上数据的一种操作。

## Android

用于智能手机和平板电脑的开源操作系统。

