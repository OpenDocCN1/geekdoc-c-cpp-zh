

## CartModel 类的头文件

```
    #ifndef CART_MODEL_H
    #define CART_MODEL_H
    #include "adevs.h"

    #define PI 3.1415926535897931
    #define RAD_TO_DEG (180.0/PI)
    // This is the dynamic model of the pendulum. The only input
    // is the force applied by the cart's motor and the only output
    // is the arm angle measurement.
    class CartModel: public adevs::ode_system<double>
    {
      public:
        CartModel();
        // Arm angle in degrees; zero degrees is straight down
        // and rotation is clockwise.
        double angle(const double* q) const { return RAD_TO_DEG*q[theta]; }
        void init(double* q);
        void der_func(const double *q, double *dq);
        void state_event_func(const double *q, double *z);
        void internal_event(double* q, const bool* state_event);
        void external_event(double* q, double e,
            const adevs::Bag<double>& xb);
        void confluent_event(double *q, const bool* state_event,
            const adevs::Bag<double>& xb);
        void output_func(const double *q, const bool* state_event,
            adevs::Bag<double>& yb);
        double time_event_func(const double*){ return DBL_MAX; }
        void gc_output(adevs::Bag<double>&){}
      private:
        // State variable indices
        const int x, theta, dx, dtheta, t;
        // Model parameters
        const double armMass, armFric, cartMass, cartFric,
            armLen, g, mAngle;
        int k; // Last output level for the quantized sensor
        // Constraint matrix and vector for A [ddx ddtheta]^T = B
        double A[4][4], B[2];
        double F; // Motor force
    };

    #endif
```

## CartModel 类的源文件

```
    #include "CartModel.h"
    using namespace std;
    using namespace adevs;
```

```cpp
CartModel::CartModel():
  ode_system<double>(5,2), // five cont. states, two event surfaces
  x(0), // position index
  theta(1), // arm angle index
  dx(2), // cart velocity index
  dtheta(3), // arm angular velocity index
  t(4), // time
  armMass(1.0), // mass of the arm in kilograms
  armFric(1E-4), // resistance to rotation
  cartMass(1.0), // mass of the cart in kilograms
  cartFric(1E-4), // resistance to lateral motion
  armLen(0.5), // length of the arm in meters
  g(9.8), // acc. due to gravity in meters/second^2
  mAngle(2.0*PI/1024.0), // sensor thresholds
  k(0)
{
  k = 0; // Arm angle is initially zero
  F = 0.0; // No initial control force
  // Compute the entries of the constraint matrix that are fixed
  A[0][0] = cartMass*armMass;
  A[1][1] = armLen*armLen*armMass/4.0;
}

void CartModel::init(double* q)
{
  q[x] = 0.0; // Start at the middle of the track
  q[theta] = k*mAngle;
  q[dx] = q[dtheta] = 0.0; // No motion
  q[t] = 0.0;
}

void CartModel::der_func(const double* q, double* dq)
{
  dq[t] = 1.0; // Time
  dq[x] = q[dx]; // Velocities
  dq[theta] = q[dtheta];
  // Compute the constraint matrices
  double Ffudge = 10.0*exp(-20.0*q[t]);
  A[1][0] = A[0][1] = -armLen*armMass*cos(q[theta])/2.0;
  B[0] = (F+Ffudge)
      - armMass*armLen*q[dtheta]*q[dtheta]*sin(q[theta])/2.0
      - cartFric*q[dx];
  B[1] = armMass*armLen*sin(q[theta])/2.0 - armFric*q[dtheta];
  // Compute determinant of the constraint matrix
  double det = A[0][0]*A[1][1]-A[0][1]*A[1][0];
  // Solve for the accelerations
  dq[dx] = (A[1][1]*B[0]-A[0][1]*B[1])/det;
  dq[dtheta] = (A[0][0]*B[1]-A[1][0]*B[0])/det;
}
```

```cpp
54
55 void CartModel::state_event_func(const double* q, double* z)
56 {
57     z[0] = q[theta] - mAngle*(k-1);
58     z[1] = q[theta] - mAngle*(k+1);
59 }
60
61 void CartModel::internal_event(double *q, const bool *event_flags)
62 {
63     if (event_flags[0]) k--;
64     else k++;
65 }
66
67 void CartModel::external_event(double* q, double e, const Bag<double>& xb)
68 {
69     F = *(xb.begin());
70 }
71
72 void CartModel::confluent_event(double* q, const bool * event_flags,
73                                 const Bag<double>& xb)
74 {
75     internal_event(q,event_flags);
76     external_event(q,0.0,xb);
77 }
78
79 void CartModel::output_func(const double *q, const bool *event_flags,
80                             Bag<double> &yb)
81 {
82     if (event_flags[0]) yb.insert((k-1)*mAngle);
83     else yb.insert((k+1)*mAngle);
84 }
```

## PIDControl 类

```cpp
1 #ifndef PIDCONTROL_H
2 #define PIDCONTROL_H
3 #include "adevs.h"
4
5 // This is a PID controller for the cart.
6 class PIDControl: public adevs::Atomic<double>
7 {
8   public:
9     PIDControl():adevs::Atomic<double>(),
10       err(0.0),err_int(0.0),
11       csignal(0.0),send_control(false){}
12     void delta_int() { send_control = false; }
13     void delta_ext(double e, const adevs::Bag<double>& xb)
14     {
15       // Error is the difference of the arm angle from zero
```

```cpp
double new_err = -(*(xb.begin())); // New error value
err_int += new_err*err; // Integral of the error
double derr = (new_err-err)/e; // Derivative of the error
err = new_err; // Value of the error
csignal = 50.0*err+5.0*err_int+1.0*derr; // Control signal
send_control = true; // Send a new control value
}
void delta_conf(const adevs::Bag<double>& xb)
{
    delta_int(); delta_ext(0.0,xb);
}
double ta() { if (send_control) return 0.0; return DBL_MAX; }
void output (const adevs::Bag<double>& yb) { yb.insert(csignal); }
void gc_output(adevs::Bag<double>&){}
private:
    double err, err_int, csignal;
    bool send_control;
};

#endif
```

## 6.1.2 与以太网仿真器的集成

现在，小车及其控制器通过一条与其他若干台计算机共享的 10 Mbps（兆比特每秒）以太网分隔开来。这些其他计算机的行为并不重要，但会占用网络吞吐量的部分比例。从小车和控制器的角度看，额外的网络流量会引入延迟、延迟变化，某些情况下还会导致数据丢失，从而降低通信信道的性能。当其他用户向网络注入的数据很少时，他们对控制器性能的影响可以忽略不计。在其他用户消耗高达 40% 的网络容量之前，小车和摆锤的轨迹不会出现明显变化；但网络使用量继续增加时，控制器性能会下降。

该系统的仿真器由三部分组成：控制器和小车、以太网，以及后台流量源。第一部分使用我们的仿真框架构建。网络和流量生成器模型随 OMNeT++（面向对象的模块化网络测试平台）仿真工具及其 INET 扩展提供（该软件可从 http://www.omnetpp.org/ 下载）。要构建集成模型，需要把控制器和小车的仿真器嵌入到 OMNeT++ 组件中，该组件再连接到 OMNeT++ 的以太网帧封装器和 MAC 设备模型。网络其余部分使用 OMNeT++ 自带的图形化工具和 NED 语言构建。

图 6.3 展示了直接参与将小车与控制器模型集成到 OMNeT++ 仿真器中的类。*CartPID* 类把 *Simulator*、*PIDControl* 和 *CartModel* 类封装在单个 OMNeT++ 模块中。该模块做三件事：（1）它拦截来自

![](img/df6085a1b35edf9c9ea818a5c66ccad9_256_0.png)

**图 6.3** 直接参与将小车和控制器集成到以太网网络 OMNeT++ 模型中的类。

OMNeT++ 网络的消息，并通过 *Simulator* 的 *computeNextState* 方法将其注入小车-控制器模型；（2）它根据从 *Simulator* 的 *nextEventTime* 方法获得的下一事件时间，为 OMNeT++ 仿真器调度自事件；（3）它拦截小车和控制器的输出，并将其转换为承载传感器和控制数据的以太网帧。下面列出了 *CartPID* 类的代码。其大部分特性与之前的示例相同：使用 *EventListener* 拦截输出事件和状态变化，并使用 *Simulator* 控制时间与注入输入。

它唯一不寻常之处，是在收到消息时取消自事件。这一步是必要的，因为 OMNeT++ 会把所有事件放入同一个未来事件列表中，只有事件时间到期或事件被显式删除时，才会从列表中移除。小车和控制器的下一事件时间一旦改变，原已调度的下一事件就会失效，因此必须将其从未来事件列表中移除，并插入新的有效时间。

## CartPID 类的头文件

```
```cpp
#ifndef __CARTPID_H__
#define __CARTPID_H__
#include "omnetpp.h"
#include "CartModel.h"
#include "PIDControl.h"
#include "TrajRecorder.h"

class CartPID: public cSimpleModule, // From OMNET++
    public adevs::EventListener<double>
```

