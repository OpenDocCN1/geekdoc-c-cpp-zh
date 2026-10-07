Notice that we don't have to open a TCP socket as we did in the case of acting as a client. The TCP socket has already been opened by the client connecting to the server and when the transaction is complete we can close it:

```
ManagedString cmd = "AT+IPSEND="+id + "",*"
ManagedString(data.length()) + "\r\n"
uBit.serial.send(cmd, SYNC_SPINWAIT);
s = 40;
int retry = 0;
dn {
	uBit.sleep(100);
	s = s + uBit.serial.read(500, ASYNC);
	retry--;
} while (debug("", s) == 0 && retry != 0);
```

Now, at last, we can send the data to the client:
uBit.serial.send(data, SYNC_SPINWAIT);
if (waitWiFi("OK", 100, 100) == 0) return 0;
if (DEBUG)debug("\n\rData Sent\n\r");

And wait for it to complete.
Finally we close the connection and complete the loop to wait for another connection:

```
cmd = "AT+CIPCLOSE=" + id + "\n"
uBit.serial.send(cmd, SYNC_SPINWAIT);
if (waitForWiFi("OK", 100, 100) == 0) return 0;
};
```

Try it out with a main program something like:
int main() {
	uBit.init();
initWiFi();
modeWiFi(1);
tconnectWiFi("ssid","pass");
getIPWiFi();
startServerWiFi();
}

You should now be able to connect to the IP address that is displayed and retrieve the web page that displays:
{"humidity":81%","air temperature":23.5C"}

# Where Next?

There are a lot of WiFi commands that haven't been covered in this chapter, but now that you have seen examples of most of the basic types and encountered the typical problems that occur you should be able to implement any that you need.