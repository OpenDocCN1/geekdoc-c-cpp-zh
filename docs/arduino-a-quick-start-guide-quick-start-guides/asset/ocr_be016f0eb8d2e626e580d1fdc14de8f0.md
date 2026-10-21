```
Download RemoteControl/InfraredProxy/InfraredProxy.pde

Line 1
#include <SPI.h>
#include <Ethernet.h>
#include <IRremote.h>

5
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

20
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

35
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
```