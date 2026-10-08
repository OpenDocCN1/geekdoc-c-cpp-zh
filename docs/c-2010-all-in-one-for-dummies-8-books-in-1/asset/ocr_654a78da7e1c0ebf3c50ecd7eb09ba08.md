```
public bool SetTemperature(int newTemperature)
{
    return true;
}
public bool SetFanSpeed(string newFanSpeed)
{
    return true;
}
```

The interface in this example is chatty (in case you couldn't tell from its class name). Every time you change a knob on the controller, a call is made to a service. Move the temperature to 72 degrees and call the service. Turn the fan to its High setting and call the service. Turn the temperature back down and call the service. The client "chats" with the service.

Nothing is intrinsically wrong with this implementation. For a service, though, with more network overhead for every call, it is not the best way to build methods. Instead, want your client to change settings and then pull a lever on the side to make all the changes at one time.

A chatty interface provides a domain model for the client to use, with properties to set. After all settings are in the model object, send the whole shootin match to the service. It looks like this:

```
namespace HomeCenter{
    public class Chunky : IChunky{
        public bool UpdateHeaterSettings(HeaterModule heaterModule)
        {
            return true;
        }
        public class HeaterModule{
            public int Temperature { get; set; }
            public bool FanOn { get; set; }
            public string FanSpeed { get; set; }
        }
    }
```

No, no matter how often you make changes, the service is called only when you "pull the big lever" (update it). This action prevents users from updating after every change depends on your interface. In general, this design principle is the best for service development.

You may wonder why anyone would bother with a concept as convoluted as Web services. I can assure that good reasons exist and that you will want to use this technology on a project.