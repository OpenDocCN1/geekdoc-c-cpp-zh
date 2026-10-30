To display sensor values that we get from the `ISensorEventListener`, we’ll start with a frame-based application project in the bada IDE. Our Tilt class is defined as follows:

```
class Tilt :
    public Osp::App::Application,
    public Osp::System::IScreenEventListener,
    public Osp::Ui::IXxxxxSensorEventListener
{
public:
    // [Tilt] application must have a factory method that creates an
    // instance of itself.
    static Osp::App::Application* CreateInstance(void);

public:
    Tilt();
    ~Tilt();

    Osp::Ui::Controls::Form* pForm;        //Form
    Osp::Ui::Controls::Label* pLabel;      //Label for display
    Osp::Base::String str;                 //String for text

    Osp::Uix::SensorManager* SManager;     //Sensor manager

    // a float for each value
    float azimuth;
    float pitch;
    float roll;

public:
    bool OnAppInitializing(Osp::App::AppRegistry& appRegistry);

    // Called when the application is terminating.
    bool OnAppTerminating(Osp::App::AppRegistry& appRegistry, bool forcedTermination = false);

    // for readability we leave out the other member methods
    // ...

    // callback function to receive sensor data
    virtual void OnDataReceived(Osp::Uix::SensorData& sensorData, Osp::Uix::SensorData& sensorData, result r);
};
```

The `OnDataReceived()` method is called when the sensor manager receives sensor data. There are several sensor types available. Here, we focus on the use of the tilt sensor. For this, we select the tilt type (`SENSOR_TYPE_TILT`) as argument.

The following code snippet is a basic Form and a Label for displaying each value of the tilt sensor in `OnAppInitializing()`: