

开发者会大量使用这种结果类型的返回值，以便进行异常检查。这里仅举一个例子：`Osp::Media` 命名空间中的 `Camera` 类提供了 `StartPreview()` 方法，其定义如下：

```
result
Osp::Media::Camera::StartPreview(
    const Osp::Graphics::BufferInfo* pBufferInfo,
    bool previewedData = false
);
```

此方法会开始显示摄像头设备的预览图像。如果 `pBufferInfo` 为 `null`，则不会显示预览图像。如果 `previewedData` 为 `true`，预览图像数据会根据帧率定期传递给 `ICameraEventListener::OnCameraPreviewed()` 方法；否则不会调用该回调。`previewedData` 的默认值为 `false`。本示例关注的是该方法的返回值，其类型为 `result`，用于表示可能发生的异常。此方法可能发生的异常汇总在表 R1.1 中。

### 表 R1.1 调用 Camera::StartPreview 时可能返回的错误代码

| 错误代码 | 描述 |
|---|---|
| E_SUCCESS | 方法执行成功 |
| E_INVALID_STATE | 摄像头当前状态下无法调用此方法 |
| E_UNSUPPORTED_FORMAT | 不支持指定的格式 |
| E_DEVICE_BUSY | 设备正在执行其他操作，无法访问 |
| E_DEVICE_UNAVAILABLE | 设备不可用 |
| E_DEVICE_FAILED | 设备操作失败 |
| E_OUT_OF_MEMORY | 内存不足 |
| E_PRIVILEGE_DENIED | 应用程序没有调用此方法所需的权限 |

以下代码片段展示了如何在 bada 中使用这种异常处理机制：

```
result r = E_SUCCESS;
// 假设我们已构造了一个 Camera* 类型的 pCamera 对象
r = pCamera->StartPreview(null, false);

if(IsFailed(r))
{
    // 处理错误情况
}
else
{
    // 正常继续执行
}
```

bada 异常处理的另一种用法适用于方法已返回其他值或数据类型的情况。在这种情况下，我们无法直接使用 `result` 作为返回类型。为此，bada 提供了静态方法 `GetLastResult()`，它会返回最后一次发生的异常，或通过 `SetLastResult()` 方法设置的结果。此值对每个线程而言都是唯一的，并会持续保留，直到再次为该线程调用 `SetLastResult()`。为了获得更具说明性的错误消息，可以将 `result` 类型所保存的错误代码转换为 bada SDK 中预定义的语句。转换通过调用静态方法 `GetErrorMessage()` 完成，该方法返回一个 `char*`。

下面仍以 `Camera` 类为例，介绍另一个返回类型不是 `result` 的方法。该方法名为 `GetSupportedPreviewResolutionListN()`，返回一个尺寸列表，用于表示摄像头支持的分辨率。如果返回 `null`，则表示发生了异常。该方法的签名如下：

```
Osp::Base::Collection::IList*
GetSupportedPreviewResolutionListN(void);
```

此方法中发生的异常可以通过 `GetLastResult()` 方法处理，具体如以下代码片段所示：

```
result r = E_SUCCESS;

// 假设我们已构造了一个 Camera* 类型的 pCamera 对象
Osp::Base::Collection::IList* pList = null;

pList = pCamera->GetSupportedPreviewResolutionListN();
if (pList == null)
{
    r = GetLastResult();
    AppLog("Operation failed with error: %s", GetErrorMessage(r));
    // 继续执行后续必要操作
}
```

bada 预定义的错误代码及其对应的返回情形列于表 R1.2。

### 表 R1.2 bada 错误代码

| 错误代码 | 描述 |
|---|---|
| E_ADDRESS_CHANGED | 网络地址已被外部更改 |
| E_ALREADY_BOUND | 目标已绑定到其他源 |
| E_ALREADY_CONNECTED | 目标已连接到其他源 |
| E_ALREADY_OPENED | 目标已打开 |
| E_AUTHENTICATION | 身份验证请求失败 |
| E_CONNECTION_BUSY | 连接正忙，无法处理新请求 |
| E_CONNECTION_FAILED | 与指定目标的连接失败 |
| E_CONNECTION_RESET | 其他线程仍在使用连接时，该连接被重置 |
| E_DATA_NOT_FOUND | 请求的数据不存在 |
| E_DATABASE | 底层数据库系统引发了异常 |
| E_DECODING_FAILED | 解码操作失败 |
| E_DEVICE_BUSY | 设备正在处理先前的任务，无法处理新任务 |
| E_DEVICE_FAILED | 设备因未知原因发生故障 |
| E_DEVICE_INCOMPATIBLE | 设备不支持指定的请求 |
| E_DEVICE_UNAVAILABLE | 设备未安装，或完全没有响应 |
| E_DHCP | 一般 DHCP 异常 |
| E_DNS | 一般 DNS 异常 |
| E_DNS_NOT_FOUND | DNS 无法解析请求的地址 |
| E_EFFECTS_DISABLED | 已禁用当前触觉设备正在播放的效果 |
| E_EMPTY_BODY | 正文为空 |
| E_ENCODING_FAILED | 编码操作失败 |
| E_END_OF_FILE | 输入操作期间意外到达文件或数据流末尾 |
| E_FDN_MODE | 启用 FDN 模式时，应用程序尝试拨打不允许的号码 |
| E_FILE_ALREADY_EXIST | 尝试创建指定路径名所表示的文件失败 |
| E_FILE_NOT_FOUND | 尝试打开指定路径名所表示的文件失败 |
| E_GROUP_NOT_FOUND | 所需的组不存在 |
| E_HOST_NOT_FOUND | 找不到目标主机 |
| E_HOST_UNREACHABLE | 无法连接到目标主机 |
| E_ILLEGAL_ACCESS | 用户没有适当的权限 |
| E_INVALID_SESSION | 相关会话无效 |
| E_INVALID_SOCKET | 负责处理应用程序请求的套接字无效 |
| E_INVALID_STATE | 实例处于无效状态 |
| E_INVALID_TRANSACTION | 相关事务无效 |
| E_IO | 输入/输出（I/O）操作期间发生异常。这是由 I/O 操作失败或中断引起的一般异常 |
| E_KEY_ALREADY_EXIST | 指定的键已存在 |
| E_KEY_NOT_FOUND | 所需的键不存在 |
| E_LANDMARK | 处理地标时发生错误 |
| E_LIBRARY_NOT_FOUND | 指定的库不存在 |
| E_LIBRARY_NOT_LOADED | 指定的库尚未加载 |
| E_LINK | 发生链接错误 |
| E_LOCATION | 发生 Location API 特定错误 |
| E_LOCATION_SERVICE | 处理服务提供商请求时发生错误 |
| E_LOCK_FAILED | 逻辑中的加锁（或解锁）失败，因此无法保证同步操作 |
| E_MAX_EXCEEDED | 超出定义的限制 |
| E_MISSING_INPUT | 未提供一个或多个必需的输入项 |
| E_NETWORK_FAILED | 一般网络异常 |
| E_NETWORK_UNAVAILABLE | 网络未启用 |
| E_NOT_A_MEMBER | 仅允许成员执行此操作，而当前用户不是成员 |
| E_NOT_PAIRED | 尚未建立蓝牙配对 |
| E_NOT_RESPONDING | 目标无响应 |
| E_NUM_FORMAT | 指定的字符串不是有效数字 |
| E_OBJ_ALREADY_EXIST | 指定的实例已存在 |
| E_OBJ_NOT_FOUND | 所需的实例不存在 |
| E_ON_INITIALIZING | 目标仍在初始化时收到请求 |
| E_OPERATION_CANCELED | 操作已被明确取消 |
| E_OPERATION_FAILED | 操作因特定原因失败 |
| E_OUT_OF_MEMORY | 内存不足，无法执行请求的操作 |
| E_OUT_OF_RANGE | 当前实例的内部状态超出有效范围 |
| E_OVERFLOW | 操作导致溢出 |
| E_PAIRING_FAILED | 请求的蓝牙配对失败 |
| E_PARSING_FAILED | 解析某类内容失败 |
| E_PRIVILEGE_DENIED | 应用程序在没有适当权限的情况下调用了 API |
| E_READ_ONLY | 对处于只读模式的实例请求执行写操作 |
| E_REJECTED | 远程站点拒绝了该操作 |
| E_RESOURCE_UNAVAILABLE | 所需资源当前不可用 |
| E_RIGHT_EXPIRED | 获取服务的权利已过期 |
| E_SECTION_ALREADY_EXIST | 指定的节已存在 |
| E_SECTION_NOT_FOUND | 所需的节不存在 |
| E_SERVER | 服务器通知设备操作因某种原因失败。错误代码后会附带详细信息和错误消息 |
| E_SERVICE_BUSY | 专用服务模块过于繁忙，无法处理其他请求 |
| E_SERVICE_LIMITED | 特定服务受到策略限制 |
| E_SERVICE_LOCKED | 服务已锁定 |
| E_SERVICE_UNAVAILABLE | 专用服务不可用 |
| E_SESSION_DEACTIVATED | 基础会话在仍被使用时已停用 |
| E_STORAGE_FULL | 存储空间已满 |
| E_SYMBOL_NOT_FOUND | 找不到指定的符号 |
| E_SYNTAX | 输入语句不符合指定语法 |
| E_SYSTEM | 底层系统发生故障 |
| E_TABLE_NOT_FOUND | 指定的表不存在 |
| E_TIMEOUT | 无法在指定时间段内完成操作 |
| E_TYPE_MISMATCH | 指定的类型不匹配 |

