```
private InputStream _input;
private OutputStream _output;

public AnalogReader(
    final String portName,
    final int baudRate) throws Exception
{
    final int timeout = 1000;
    final String appName = "analog reader client";
    CommPortIdentifier portId =
        CommPortIdentifier.getPortIdentifier(portName);
    SerialPort port = (SerialPort)portId.open(
        appName,
        timeout
    );
    _input = port.getInputStream();
    _output = port.getOutputStream();
    port.setSerialPortParams(
        baudRate,
        SerialPort.DATABITS_8,
        SerialPort.STOPBITS_1,
        SerialPort.PARITY_NONE
    );
}

public void run() throws Exception {
    byte[] buffer = new byte[255];
    Thread.sleep(2000);
    while (true) {
        _output.write("a\0\n".getBytes());
        Thread.sleep(100);
        if (_input.available() > 0) {
            _input.read(buffer);
            System.out.print(new String(buffer));
        }
    }
}

public class AnalogReaderTest {
    public static void main(String[] args) throws Exception {
        if (args.length != 1) {
            System.out.println(
                "You have to pass the name of a serial port."
            );
            System.exit(1);
        }
        AnalogReader analogReader = new AnalogReader(args[0], 9600);
        analogReader.run();
    }
}
```