
```cpp
{
public:
    void outputEvent(adevs::Event<double> y, double t);
    void stateChange(adevs::Atomic<double>*,double){};
    CartPID();
protected:
    // OMNeT++ method for model initialization
    void initialize();
    // Method for processing OMNeT++ events
    void handleMessage(cMessage *msg);
    void registerDSAP(const char* gate);
private:
    PIDControl *pid; // The PID controller
    adevs::Hybrid<double> *hysm; // Model of the cart and arm
    TrajRecorder *traj; // Listener for recording the cart trajectory
    adevs::SimpleDigraph<double> *top_model; // Holds the PID and cart
    adevs::Simulator<double> *sim; // Simulator for our model
    cMessage self_event; // OMNeT++ event for our internal events
    adevs::Bag<adevs::Event<double> > xbag; // Bag for OMNeT++ inputs
    std::ofstream sensor_rx_strm; // Records receipt of sensor msgs
};

#endif
```

## CartPID 类的源文件

```cpp
#include "CartPID.h"
#include "ByteArrayMessage.h"
#include "MACAddress.h"
#include "Ieee802Ctrl_m.h"
#include <string>

// Network addresses for the OMNeT++ network model
static const MACAddress SENSOR_ADDR("999999999999"),
    CONTROL_ADDR("888888888888");
static const int SAP = 9999; // OMNeT++ application ID for the cart/PID
Define_Module(CartPID); // Make CartPID into an OMNeT++ module

// OMNeT++ calls this method at the start of the simulation
void CartPID::initialize()
{
    // Create the cart and controller
    pid = new PIDControl();
    CartModel *cart = new CartModel();
    hysm = new adevs::Hybrid<double>(
        cart,
        new adevs::corrected_euler<double>(cart,1E-8,0.001),
        new adevs::linear_event_locator<double>(cart,1E-10)
    );
    traj = new TrajRecorder(cart,hysm);
    top_model = new adevs::SimpleDigraph<double>();
    // Models are not coupled because communication is through the
    // OMNeT++ model of the Ethernet.
    top_model->add(hysm); top_model->add(pid);
    sim = new adevs::Simulator<double>(top_model);
    sim->addEventListener(traj);
    sim->addEventListener(hysm);
    // Schedule first internal event
    if (sim->nextEventTime() < DBL_MAX)
        scheduleAt(SimTime(sim->nextEventTime()), &self_event);
    // Register with the OMNeT++ LLC
    registerDSAP("sensorIn");
    registerDSAP("controlOut");
}

void CartPID::registerDSAP(const char* gate_name)
{
    Ieee802Ctrl *etherctrl = new Ieee802Ctrl();
    etherctrl->setDsap(SAP);
    cMessage *msg =
        new cMessage("register_DSAP", IEEE802CTRL_REGISTER_DSAP);
    msg->setControlInfo(etherctrl);
    send(msg,gate_name);
}

// OMNeT++ calls this method when an event occurs at the CartPID model.
// These can be self-scheduled events or the arrival of a message
// from the network.
void CartPID::handleMessage(cMessage *msg)
{
    SimTime simtime = sim->nextEventTime();
    // Internal event
    if (msg == &self_event) sim->execNextEvent();
    // External event
    else {
        // Cancel any pending self events
        if (self_event.isScheduled()) cancelEvent(&self_event);
        // Convert to the expected message type
        ByteArrayMessage *data = dynamic_cast<ByteArrayMessage*>(msg);
        assert(data != NULL);
        // Get the data from the message
        adevs::Event<double> x;
        data->copyDataToBuffer(&x.value(), sizeof(double));
        // Inject a sensor reading into the controller
        if (std::string(data->getArrivalGate()->getBaseName()) == "sensorIn")
            x.model = pid;
        // Control data goes to the cart
        else x.model = hysm;
        // Clean up the message
        delete data;
        // Inject the event into the simulator
        xbag.insert(x);
        sim->computeNextState(xbag, simTime().dbl());
        xbag.clear();
    }
    // Process instantaneous responses to the input
    while (SimTime(sim->nextEventTime()) <= simTime())
        sim->execNextEvent();
    // Schedule the next internal event
    if (sim->nextEventTime() < DBL_MAX)
        scheduleAt(SimTime(sim->nextEventTime()), &self_event);
}

// This method is called by our simulator whenever the cart or
// controller produces an output event.
void CartPID::outputEvent(adevs::Event<double> y, double t)
{
    Ieee802Ctrl *etherctrl = new Ieee802Ctrl();
    etherctrl->setSap(SAP);
    etherctrl->setDsap(SAP);
    // Sensor output; send it to the controller
    if (y.model == hysm) {
        etherctrl->setDest(CONTROL_ADDR);
        ByteArrayMessage *msg =
            new ByteArrayMessage("Sensor_data",IEEE802CTRL_DATA);
        msg->setControlInfo(etherctrl);
        msg->setDataFromBuffer(&(y.value),sizeof(double));
        send(msg,"sensorOut");
    }
    // Control output; send it to the sensor
    else {
        etherctrl->setDest(SENSOR_ADDR);
        ByteArrayMessage *msg =
            new ByteArrayMessage("Control_data",IEEE802CTRL_DATA);
        msg->setControlInfo(etherctrl);
        msg->setDataFromBuffer(&(y.value),sizeof(double));
        send(msg,"controlOut");
    }
}

CartPID::~CartPID()
{
    delete sim; delete top_model; delete traj;
}
```

其余的集成使用 OMNeT++ GUI（图形用户界面）完成。图 6.4 显示了网络的最终配置。*controlAndPlant* 组件包含 *CartPID* 模型，将其输出和输入连接到两个以太网协议栈：一个用于传感器，另一个用于控制器。网络的其余部分由现有组件构建。

网络有两个参数对我们的实验感兴趣。首先是 *CartPID* 的协议栈中 MAC 将为传输数据包所做的尝试次数。默认情况下，该数字为 16；该默认值被产生背景流量的模型的 MAC 使用。然而，通过减少控制器和小车的尝试次数，我们希望提高控制器对网络拥塞的鲁棒性。感兴趣的第二个参数是其他用户尝试发送数据的频率。这些用户的每个数据包大小固定为 1000 字节（8000 位），并且每个用户以指数分布的间隔产生数据包（即，数据包产生由泊松到达过程建模）。指数分布的均值决定了数据速率，因此决定了这些用户消耗了网络容量的多少。

### 6.1.3 实验

当网络 10 Mbps 的 40% 被背景流量消耗时，控制器在默认的重传次数下仍然工作得非常好。然而，在 50% 时，出现了明显的恶化，如图 6.5 所示，而在 75% 时，控制器失效且摆锤倒下。因此，这两种情况是对减少重试次数可提高性能这一假设的良好测试。

最极端的情况是将最大重传尝试次数从 16 减少到 0，这样做能显著帮助控制器。图 6.6 显示了此调整对摆锤轨迹的影响，该轨迹与图 6.5 中所示的相同 50% 利用率场景相对应。将这些轨迹与图 6.2 进行比较，显著的效果立即显现。轨迹后期摆锤的大幅摆动已被抑制，振荡几乎保持在理想情况下看到的 3° 带内。

这种巨大改进的原因在于，来自控制器和臂角传感器的旧数据不会阻碍更新、更准确数据的传输。例如，假设传感器在 t = 1 时产生 1° 的测量值。该数据被插入到数据包中并发送到 MAC 设备进行传输。如果发生冲突，MAC 设备会暂时保留数据，然后尝试重新发送。在 MAC 设备等待的同时，传感器在 t = 1.1 时产生第二个测量值，例如 1.35°。然而，这些更新、更有用的数据必须等待，直到旧的、现在无用的数据被传输完毕。在 50% 利用率场景中，使用默认的重传尝试次数限制，小车和控制器平均交换总共 248.45 条消息，这些消息总体上平均受到 116 次退避的影响。因此，刚才描述的情况发生在大约一半的传输尝试中。通过不尝试重传旧数据，可以避免这种情况，并且控制器通过始终使用最新信息做得更好。
