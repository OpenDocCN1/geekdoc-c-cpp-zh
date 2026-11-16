```
unsigned int byte_counter ;
void Send_Request_For_Data(void)
{
byte_counter = 0 ;
outputb(CMD_PORT, RQST_DATA_CMD) ;
}
void Process_One_Data_Byte(void)
{
BYTE8 data = inportb(DATA_PORT) ;
switch (++byte_counter)
{
case 1: Process_Temperature(data); break ;
case 2: Process_Allitude(data); break ;
case 3: Process_Humidity(data); break ;
...
}
}
```

> This counter holds state information. It allows us to distinguish data bytes according to the order in which they are received.

# FIGURE 9-2 Example of state information within an ISR.

request for data and then returns an entire set of data values in response. Each data byte in the set might be associated with a particular measurement, with bytes distinguished only by the relative order in which they arrive. If each byte causes a new interrupt request, then processing the data properly requires that the corresponding ISR provide a counter that is reset to zero when the original command is issued and then incremented on each input interrupt. The counter shown in the example of Figure 9-2 provides a simple form of state information for the input task.

# 9.1.2 Managing Latency

If the task implemented by an ISR performs all of the work associated with an external event, it may have quite a bit of work to do. It then becomes important to implement an interrupt priority system in hardware and to re-enable higher-priority interrupts as soon as possible near the beginning of each ISR. Do not forget, however, that lower-priority interrupts remain disabled as long as we stay in the ISR! If the ISR contains a lot of code, then the latency times imposed on lower-priority interrupts may still be intolerable if they are not re-enabled until the end of the ISR.

For example, an ISR that handles an input device might need to process the input data and then the results to some output device. But of course you cannot write to the output device until it is ready. If the ready status of the output device is polled inside the ISR, as shown in Figure 9-3, any pending lower-priority interrupts will have to wait an unspecified amount of time. This is obviously unacceptable.