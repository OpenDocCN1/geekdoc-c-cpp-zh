poses, and for every line it checks whether it begins with “GET.” If yes, it calls handle_command(); otherwise, it checks whether the line is empty, because all HTTP messages are terminated by an empty line. In this case, receive_from_server() sends back an “OK” response, waits for a millisecond to give the client some time to process the response, and then disconnects from the client calling stop().

Admittedly that was a lot of code, but the effort was well worth it. Using the InfraredProxy is really simple now:

```
Download RemoteControl/InfraredProxy/InfraredProxy.pde
const unsigned int PROXY_PORT = 80;
const unsigned int BAUD_RATE = 9600;

byte mac[] = { 0xDE, 0xAD, 0xBE, 0xEF, 0xFE, 0xED };
byte ip[] = { 192, 168, 2, 42 };

Server server(PROXY_PORT);
InfraredProxy ir_proxy;

void setup() {
  Serial.begin(BAUD_RATE);
  Ethernet.begin(mac, ip);
  server.begin();
}

void loop() {
  ir_proxy.receive_from_server(server);
}
```

As usual, we define the MAC and IP addresses we’d like to use. Then we define a Server object, passing it the port it should listen to, 80 (the standard HTTP port). Also, we initialize a new InfraredProxy object.

In the setup() method, we initialize the serial port for debug purposes. We also initialize the Ethernet shield, and we call Server’s begin() method to start our server’s listener. In loop(), we only call the InfraredProxy’s receive_from_server() method, passing it our Server instance.

Let’s finally test the code! Attach the Ethernet shield to your Arduino, and attach the infrared LED circuit to the shield. Configure the MAC and IP addresses, compile it, and upload it to your Arduino. Point your web browser to http://192.168.2.42/NEC/32/2011283550 (adjust the URL to your local settings!), and see what happens to your Mac or whatever device you want to control (in Figure 9.9, on the following page, you can see a typical output of the infrared proxy on the serial monitor).