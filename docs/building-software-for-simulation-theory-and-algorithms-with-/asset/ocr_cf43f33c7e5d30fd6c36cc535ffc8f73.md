```
```cpp
// Counters for the clock and machine cycle
int clk = 0, machine_cycle = 0;
// Run the simulation
while (true) {
    // Get the input from stdin
    adtss::Bag<adtss::Event<port_value_t> > input;
    port_value_t x1, x2;
    x1.port = N1::x1;
    x2.port = N1::x2;
    cin >> x1.bit >> x2.bit;
    // Quit if the input has ended
    if (cin.eof()) break;
    input.insert(adtss::Event<port_value_t>(m,x1));
    input.insert(adtss::Event<port_value_t>(m,x2));
    // Print the time and input
    cout << " xx M" << machine_cycle << " C" << clk <<
         "\t" << x1.bit << " " << x2.bit << "\t";
    // Print the time and output at the next machine cycle
    cout << " yy M" << ++machine_cycle << " C" << clk << "-" << clk+2 << "\t";
    // Advance the simulation by one machine cycle
    for (int t = 0; t < 3; t++) {
        clk++;
        sim->computeNextState(input);
    }
    cout << endl;
}
// Clean up and exit
delete sim; delete l1; delete m;
return 0;
}
```
```

# 3.4 MEALY/MOORE-TYPE SYSTEMS

The output of a Moore-type system is a function of its state; a Moore output function has the form

$$\lambda : S \to Y$$

These systems are already familiar to us. The output of a Mealy-type system is a function of its state and current input; a Mealy output function has the form

$$\lambda : S \times X \to Y$$

By discarding the input that is supplied to the output function, we can build a Mealy-type system to mimic any Moore-type system. In this sense, the Mealy-type system