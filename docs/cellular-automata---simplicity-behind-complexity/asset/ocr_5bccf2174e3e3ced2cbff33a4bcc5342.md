```
```csharp
while (true)
{
    BufReceived = MyIoBuf.Receive();
    for (int i=BvReceived.i-1; i<=BvReceived.i+1; i++)
    {
        for (int j=BvReceived.j-1; j<=BvReceived.j+1; j++) // for each i,j
        {
            // when i,j are not out of the matrix
            if ((i>=0 && i<TamMatrix.X) && (j>=0 && j<TamMatrix.Y))
            {
                // Adds the corresponding kernel coefficient.
                NewState[State[i,j].Kernel(i-BvReceived.i,j-BvReceived.j)];
                if NewState < Threshold:
                {
                    State[i, j] = NewState;
                }
                else
                {
                    State[i, j] = 0;
                    NewOutEvent.i = i;
                    NewOutEvent.j = j;
                    MyOutBuf.Send(NewOutEvent);
                }
            }
        }
    }
}
```
```

Fig. 4. C# code for simulating the AER-CA

# # 5. Hardware design of an AER-CA

Once the behaviour of the AER-CA is checked in the simulator, we are going to explain a first hardware implementation of the prototype. As seen in figure 5, this hardware will consist basically of an input stage that controls the input AER bus and sends a signal to the corresponding cell of the cellular automaton from the input AER event received. The output stage moderates the signals received from the cells of the cellular automaton and translates them into AER events, which are sent through the output bus. The setting parameters that have been sent by USB are recorded in registries by the USB Controller. The cells of the cellular automaton modify their state from the setting parameters, Kernel Coefficients and Threshold, and the pulses received from the input stage.

![](bbox=[0.15, 0.6, 0.85, 0.75])

Fig. 5. USB-AER boards and MultiLoadFPGA application

One possible implementation of this system for a 3x3 kernel without the USB Controller is shown in figure 6. AER input is connected to the grid through two-level decoders. When an event comes, e.g. from a vision sensor, its address is divided into row and column. The first level decodes the row by Input Event X and the second level decodes the column by Input Event Y in order to select the targeted cell. Input Req signal notifies when the new event arrived.