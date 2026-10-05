

# 27 • 应用示例 865

```cpp
int main()
{
    int CRV, index, num, sel;
    Msg msg;

    CRV = 100; // 仅仅是一个初始值。
    while(1) {
        cout << "\noperations\n";
        cout << "--------------------\n";

        cout << "\1. 建立调用\n";
        cout << "\2. 释放调用\n";
        cout << "\3. 显示调用\n";
        cout << "\4. 退出\n";

        cout << "\n输入选择: ";
        cin >> sel;

        switch(sel) {
            case 1:
                msg.code = SETUP;
                msg.CRV = CRV; // 调用标识符。
                CRV++; /* 为了简单起见，每次调用的 CRV
                增加1。 */
                prctl.handle_up_msg(&msg); /* 在实际
                应用中，用户输入调用相关的信息，例如
                被叫用户的电话号码。 */
                break;
            case 2:
                cout << "\nent要释放的调用的 CRV: ";
                cin >> num;
                index = prctl.find_call(num); /* 我们找到
                调用，即 CRV 与用户输入的 CRV 相同的那个调用。 */
                if(index != -1) {
                    msg.code = RELEASE;
                    msg.CRV = num;
                    prctl.call_index = index;
                    prctl.handle_up_msg(&msg); /* 激活
                    调用释放程序。 */
                }
                else {
                    cout << "\n调用不存在\n";
                    break;
            case 3:
                prctl.show();
                break;
            case 4:
                return 0;
            default:
                cout << "\n无效的选择\n";
                break;
        }
    }
    return 0;
}
```

# 866 C++ 导言

```cpp
int Prtcl::handle_up_msg(Msg *p) /* 处理来自上层的消息。 */
{
    int index;
    if(p->code == SETUP) {
        Call c(p->CRV); // 创建一个对象来管理调用。
        calls.push_back(c); // 保存对象
        index = calls.size()-1;
        map_CRV(p->CRV) = index; /* 将 CRV 映射到对象在 vector 中的位置。 */
        calls[index].fsm(); /* 将消息传递给管理调用的对象。 */
    } else if (p->code == RELEASE) {
        index = p->call_index;
        calls[index].fsm(p);
    } else {
        cout << "上层消息 " << p->code << " 不支持\n";
        return -1;
    }
    return 0;
}
```

int Prtcl::handle_low_msg(int data[]) /* 处理来自下层的消息。 */
{
    int index;
    Msg msg; /* 来自下层的信息存储在 Msg 成员中。 */
    index = find_call(data[0]); /* 我们找到调用，即与消息中包含的 CRV 相同的对象。 */
    if(index == -1) {
        cout << "调用不存在\n";
        return -1;
    }
    msg.code = data[1];
    switch(msg.code) {
        case CONNECT:
            calls[index].fsm(&msg); /* 将消息传递给管理调用的对象。 */
            break;
        case RELEASE_COMPLETE:
            ret = calls[index].fsm(&msg); /* 这是一个检查
            返回值的示例。相应的对象被删除。 */
            if(ret == CLEAR_CALL)
            {
                calls.erase(calls.begin()+index);
                map_CRV.erase(data[0]);
            }
            break;
        default:
            cout << "收到的消息_" << msg.code << " 不支持\n";
            return -1;
    }
    return 0;
}
```

```cpp
int Prtcl::find_call(int CRV) const /* 为了找到对象，我们使用 map_CRV，
它将 CRV 映射到其在 vector 中的位置。 */
{
    auto it = map_CRV.find(CRV);
    if(it != map_CRV.end())
        return it->second;
    return -1;
}
```

当接收到上层的消息时，会调用 `handle_up_msg()`。在我们的示例中，这一层连接到应用程序菜单，该菜单提供了一些可以的操作。如果用户选择调用选项，将创建一个新对象来管理该调用，并且消息应该发送给被叫用户。在实际应用中，此消息是在呼叫者与被叫用户建立通信时创建（例如拨号），网卡将其发送到物理介质（例如光纤），消息穿越 ISDN 网络到达目的地。

当接收到下层的消息时，会调用 `handle_low_msg()`。例如，在实际应用中，消息从网卡接收，传递给应用程序的驱动程序，驱动程序将其转发给应用程序。在我们的示例中，消息包含在数据数组中。在实际应用中，`handle_low_msg()` 和 `handle_up_msg()` 是异步调用并访问资源的，我将它们放在线程中并使用信号量进行多线程处理。将其视为一个独立的程序。在本书书中我们不讨论线程，我只是在未来提供类似的内容。后续文件是 `fsm.cpp` 和 `fsm.h`。这些文件实现了协议的状态机。为了简单起见，当在 IDLE 状态下接收到消息时，状态变为 `CALL_INIT`。

