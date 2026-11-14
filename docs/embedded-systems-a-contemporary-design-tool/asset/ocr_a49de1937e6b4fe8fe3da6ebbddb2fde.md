The next code module in Figure A.30 illustrates a more commonly used approach for modeling counting, timing, or registered types of designs. Rather than working with individual flip-flops, the design is approached algorithmically.

```
// Build a synchronous two bit binary up counter
module TwoBitCntr(state, clr, clk);
    input clr, clk;
    output[1:0] state;

    reg[1:0] state;

// Name the states
parameter state0 = 2'b00;
parameter state1 = 2'b01;
parameter state2 = 2'b10;
parameter state3 = 2'b11;

// Build a synchronous two bit binary up counter
always @(-clr or negedge clk)
begin
    if(-clr)
    begin
        state = state0;
    end

    else case(state)
    state0:
        state = state1;
    state1:
        state = state2;
    state2:
        state = state3;
    state3:
        state = state0;
    endcase
end
endmodule
```

Figure A.30 A Behavioral Model of a 2-Bit Binary up Counter using a Case Statement.

# A.5 TESTING AND VERIFYING THE CIRCUIT

Once the circuit is designed and modeled in Verilog, we move into the next phase. We first need to verify that the model functions properly. The next step is to use it for its intended purpose. To that end, we perform any functional, parametric, and stress tests on the design, through the model, that we deem necessary to confirm the design before committing to hardware.