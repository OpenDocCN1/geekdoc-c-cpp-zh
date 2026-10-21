
![](img/dcfd13a1bf99c4d3f9996627012a6526_215_0.png)

Figure 9.8: An Ethernet-controllable remote control

We’ll replace <arduino-ip> with the IP address of the Arduino’s Ethernet shield. The element <protocol-name> can be one of the supported protocols (“NEC,” “SONY,” “RC5,” or “RC6”). <command-length> specifies the length of the command code in bits, and <command-code> contains the command code itself as a decimal number.

Let’s assume we’d like to send the code for the menu key on an Apple Remote, and our Arduino has the IP address 192.168.2.42. Then we’d have to point our web browser to the following URL:

http://192.168.2.42/NEC/32/2011283550

In this case, the protocol name is NEC, the length of the command code is 32 bits, and the command code is 2011283550 (the decimal representation of the hexadecimal number 0x77E1C05E).

We’ve already used the Arduino as a web client in Chapter 8, Networking with Arduino, on page 170, but now we need to turn it into a web server. The server waits for new HTTP requests like the one shown previously, parses the URL, and emits the corresponding infrared signal.

We’ll hide all these details in a class named InfraredProxy, and to keep things as easy and as concise as possible, we’ll make use of both the Ethernet and the IRremote library. The InfraredProxy class is still one of the book’s most sophisticated examples of Arduino code. Here it is:

Download RemoteControl/InfraredProxy/InfraredProxy.pde

```cpp
#include <SPI.h>
#include <Ethernet.h>
#include <IRremote.h>

class InfraredProxy {
    IRsend _infrared_sender;

    void read_line(Client& client, char* buffer, const int buffer_length) {
        int buffer_pos = 0;
        while (client.available() && (buffer_pos < buffer_length - 1)) {
            const char c = client.read();
            if (c == '\n')
                break;
            if (c != '\r')
                buffer[buffer_pos++] = c;
        }
        buffer[buffer_pos] = '\0';
    }

    bool send_ir_data(const char* protocol, const int bits, const long value) {
        bool result = true;
        if (!strcasecmp(protocol, "NEC"))
            _infrared_sender.sendNEC(value, bits);
        else if (!strcasecmp(protocol, "SONY"))
            _infrared_sender.sendSony(value, bits);
        else if (!strcasecmp(protocol, "RC5"))
            _infrared_sender.sendRC5(value, bits);
        else if (!strcasecmp(protocol, "RC6"))
            _infrared_sender.sendRC6(value, bits);
        else
            result = false;
        return result;
    }

    bool handle_command(char* line) {
        strsep(&line, " ");
        char* path = strsep(&line, " ");

        char* args[3];
        for (char** ap = args; (*ap = strsep(&path, "/")) != NULL;)
            if (**ap != '\0')
                if (++ap >= &args[3])
                    break;
        const int bits = atoi(args[1]);
        const long value = atol(args[2]);
        return send_ir_data(args[0], bits, value);
    }

public:
    void receive_from_server(Server server) {
        const int MAX_LINE = 256;
        char line[MAX_LINE];
        Client client = server.available();
        if (client) {
            while (client.connected()) {
                if (client.available()) {
                    read_line(client, line, MAX_LINE);
                    Serial.println(line);
                    if (line[0] == 'G' && line[1] == 'E' && line[2] == 'T')
                        handle_command(line);
                    if (!strcmp(line, "")) {
                        client.println("HTTP/1.1 200 OK\n");
                        break;
                    }
                }
            }
            delay(1);
            client.stop();
        }
    }
};
```

After including all libraries needed, we declare the InfraredProxy class. We define a member variable named _infrared_sender that stores an IRsend object we need to emit infrared control codes.

In line 8, we define a read_line() method that reads one line of data sent by a client. A line ends either with a newline character (\n) or with a carriage return character followed by a newline character (\r\n). read_line() expects the Ethernet Client object to read data from, a character buffer to store the data in (buffer), and the maximum length of the character buffer (buffer_length). The method ignores all newline and carriage return characters, and it sets the line's last character to \0, so the buffer to be filled will always be a null-terminated string.

The next method (send_ir_data()) starts in line 20 and emits an infrared command specified by a protocol type (protocol), the length of the code measured in bits (bits), and the code value to be sent (value). Depending on the name of the protocol, the method delegates all the real work to our IRsend instance.

handle_command() implements one of the most difficult aspects of our InfraredProxy: it parses the URL addressed by the HTTP request. To understand what this method does, we have to understand how HTTP requests work. If you wander up to your web browser's address bar and parses it, and for every line it checks whether it begins with “GET.” If yes, it calls handle_command(); otherwise, it checks whether the line is empty, because all HTTP messages are terminated by an empty line. In this case, receive_from_server() sends back an “OK” response, waits for a millisecond to give the client some time to process the response, and then disconnects from the client calling stop().

Admittedly that was a lot of code, but the effort was well worth it. Using the InfraredProxy is really simple now:

Download RemoteControl/InfraredProxy/InfraredProxy.pde

```cpp
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

![](img/dcfd13a1bf99c4d3f9996627012a6526_220_0.png)

Although we’ve used only a minimum amount of hardware (a cheap and simple infrared LED), this chapter’s projects are very useful and fairly sophisticated, at least from a software development point of view. We can now not only control any device that understands infrared signals, but we can do it using a computer’s serial port or even a web browser.

Also, you no longer need to connect the Arduino to your computer’s USB port. The Infrared proxy, for example, only needs the USB port to get some power. Plug an AC adapter into your Arduino, and you can get rid of your USB cable.

For the first time, we’ve controlled real-world devices using an Arduino. We’ll continue to do so in the next chapter, where you’ll learn how to control motors.

## 9.7 What If It Doesn’t Work?

In this chapter, we mainly used LEDs and an Ethernet shield, so all the advice from Chapter 3, *Building Binary Dice*, on page 63 and Chapter 8, *Networking with Arduino*, on page 170 also apply to this chapter.

In addition, you have to be careful about more things. For example, the distance between an infrared LED and its receiver is important.
