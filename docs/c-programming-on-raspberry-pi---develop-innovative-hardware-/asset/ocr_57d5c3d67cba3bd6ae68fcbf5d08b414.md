```
<center><h2>Web Server Example with 2 LEDs</h2></center>\n \
<form>\n \
<button name=\"LED0\" button style=\"color:green\" value=\"ON\" type=\"submit\">LED0 ON</button>\n \
<button name=\"LED0\" button style=\"color:red\" value=\"OFF\" type=\"submit\">LED0 OFF</button><br><br>\n \
<button name=\"LED1\" button style=\"color:green\" value=\"ON\" type=\"submit\">LED1 ON</button>\n \
<button name=\"LED1\" button style=\"color:red\" value=\"OFF\" type=\"submit\">LED1 OFF</button>\n \
</form></body></html>\n\";\n\n//\n// Configure LED0 and LED1 as outputs and turn them OFF\n//\nvoid Configure()\n{\n    pinMode(LED0, OUTPUT);\n    pinMode(LED1, OUTPUT);\n    digitalWrite(LED0, LOW);\n    digitalWrite(LED1, LOW);\n}\n\n//\n// Start of MAIN program. Inside the main program we send the\n// HTML file so that it is displayed on user's device. The user\n// clicks the buttons to control the LEDs. We control the LEDs\n// depending upon the key click. Variabl request holds the request\n// and we search this string to see which LED should be turned\n// ON/OFF. The contents of request is of the form (for example, to\n// turn OFF LED0): \" ?LED0=OFF\", or similarly, to turn LED1 ON:\n// \" ?LED1=ON\"\n//\nint main(void)\n{\n    int sock, len, num, cli,flag = 1;\n    char buffer[BUFSIZE];\n    struct sockaddr_in serveraddr, clientaddr;\n\n    wiringPiSetupGpio();\n    Configure();\n\n    sock = socket(AF_INET, SOCK_STREAM, 0);\n    len = sizeof(clientaddr);\n\n    bzero(&serveraddr, sizeof(serveraddr));
```