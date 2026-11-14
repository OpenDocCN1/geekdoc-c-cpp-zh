

## 10.17 调试 – 时序逻辑

back output signal. For the circuit on the left, the input pattern [0 → 1 → 1 → 0, 1, 0, x] on the respective inputs [A, B, C, D] will identify the fault. Similarly, the pattern [1, 1, 0, 0 → 1 → 1 → 0] on the respective inputs [A, B, C, D] will identify the problem in the circuit fragment on the right. Observe that for the right-hand circuit the output should never change because C should block forward signal propagation. However, the feedback fault also provides the means to overdrive the output and force a signal change.

If the signals driving the logic block are from an internal net, then one must assume that at least two outputs are fighting: signal F and the output of the device driving either A or D. We test and troubleshoot as was done with the "outputs tied" bridge fault in the earlier discussions.

Turning on, debugging, and troubleshooting the sequential machines provide the opportunity to apply engineering creativity, imagination, and intuition. Sequential logic introduces time as a variable, which somewhat complicates the test and debug process. With combinational logic, the desired (or perhaps undesired) output appears shortly after the inputs are applied. In contrast, in a sequential system, getting to the desired state often involves a specific (and sometimes tedious) series of input patterns (Refer back to the earlier chapters on finite-state machines, FSMs.)

Efficiently debugging sequential circuitry requires a bit of forethought and planning. As discussed earlier, the first step in debugging is taken during design. In any system, one should always provide a master reset input to any latch or flip-flop based logic. The signal provides the means by which to place the machine into a known initial state. Of course, if that fails, we have a place to begin troubleshooting. Moreover, that is a combinational problem, and we have just studied those.

### 验证真值表策略

At this point, one can take a variety of paths. One good approach is to verify the state machine’s truth table – we call this strategy verify the truth table strategy. Two tools are essential to begin the task: a data generator and a logic analyzer. The first gives the ability to write and produce a series of test vectors that can be applied to the circuit’s input to produce the desired transitions. The second provides the means to monitor and collect the values of the machine’s outputs for each input vector.

We will use the simple pattern recognition circuit studied earlier to illustrate the approach. The state diagram and truth table for the system presented in Figure 10.26.

![](img/679b8d2d47f1bf86e17aca48f596f5cc_592_0.png)

| 当前状态 | 下一状态 / 输出 |
|---|---|---|
| | X = 0 | X = 1 |
| A | B/0 | A/0 |
| B | B/0 | C/0 |
| C | D/0 | A/0 |
| D | B/0 | C/1 |

图 10.26 简单模式识别状态机

For this example, we will use a simple binary assignment for the state variables, which will yield the excitation table given in Figure 10.27.

| 当前状态 | 下一状态 / 输出 |
|---|---|---|
| | X = 0 | X = 1 |
| A 00 | B/0 01 / 0 | A/0 00 / 0 |
| B 01 | B/0 01 / 0 | C/0 10 / 0 |
| C 10 | D/0 11 / 0 | A/0 00 / 0 |
| D 11 | B/0 01 / 0 | C/1 10 / 1 |

图 10.27 激励表

The first step is to write a test vector that will apply the master reset and, thereby, force the system to its initial state, A, the {00} state. The next step is to select a state transition to be verified and write a homing or initialization sequence that will send the machine to the state just before the transition. For this example, we elect to test the transition from state C {1,0} to state D {1,1}.

Starting from state A, we create the data generator pattern: {Reset, X} = {(0,0), (1,0), (0,1)}. If the machine is functioning properly, it should be in state C. Next, we write a vector to effect the transition. The new vector is added to the data generator pattern: {Reset, X} = {(0,0), (1,0), (1,1), (1,0)}.

The logic analyzer is connected to the circuit and the set of test vectors is entered into the data generator. Following application of the suite of vectors, the following sequence for the state variable and output variable transitions should be captured on the logic analyzer as [M, N, Z] =

```
0 0 0
0 1 0
1 0 0
1 1 0
```

One additional input vector will now confirm the output logic for Z as well. This process is repeated for each transition to be verified.

Recall that in the formal model of the FSM, the next state is given by the mapping:

```
δ : S × X → S (10.4)
```

All this equation states is that the output of a flip-flop comprising the FSM depends on the combinational logic providing the input. Thus, if a failure occurs, the data generator can be used to debug the combinational logic portion of the machine, exactly as was done with a pure combinational logic system earlier.

In order for the test just completed to succeed, there must have also been successful transitions from A to B and then to C. From the results of one test, we have confirmed a significant portion of the logic. A failure also lays the groundwork for a debugging strategy. In such an event, we split the state transition sequence in half – do a binary search. We ask: "Did we get to state C?" If not, we explore the early transitions; otherwise we examine the later ones.

## 10.18 扫描设计测试

### 选择、测试扫描输入输出

The strategy for debugging sequential machines using scan design techniques is rather straightforward. The flip-flops are at the heart of the circuit and the technique, so it is best to ensure that they are functioning properly first. We repeat the drawing of a state machine with scan design support in Figure 10.28.

![](img/679b8d2d47f1bf86e17aca48f596f5cc_594_0.png)

图 10.28 带扫描路径逻辑的基本状态机

Initially the select input is placed into the test mode. With the flip-flops configured as a shift register, a pattern of alternating 0's and 1's is entered on the scan in input and monitored on the scan out output. If the pattern that has been entered appears properly on the output, we assume that the devices are working correctly and can proceed.

If the output appears as a constant 0 or 1, then we infer that one of the devices (or its input) is malfunctioning. If manual access to the individual flip-flop pins is possible, we debug by probing those signals. If such access is not available, little can be done.

Assuming that the necessary access is available, the first debugging step is to verify the reset signal (if it is present) to ensure that the machine is not being held in the reset state.

The same is done with the preset signal. Next, the presence of the clock on each device is confirmed. If those signals are operating properly, the flip-flop outputs are examined to determine how far through the register the test pattern has correctly propagated.

- 卡住故障测试策略，正常测试扫描输出
- 验证真值表策略，正常测试

Once the flip-flops are confirmed to be functioning correctly, the combinational logic is addressed. If one is using a test for stuck-at strategy, then the test mode is selected and the shift register and the primary inputs {Xn} are used to enter the test vectors to be applied to the combinational net. The logic is switched to normal mode and the state of the {Ym(t)} signals is strobed into the flip-flops. Going back to the test mode once again allows the state of the combinational logic to be shifted out through the scan out line where it and the {Zn} values are compared with the proper values.

A verify the truth table strategy is not much more complex. Let's repeat the previous exercise and see how scan design now applies. As a first step, select a state transition to be verified. Next, select the test mode, shift in the values for {Ym(t)} that will cause the transition, enter the normal mode, execute the transition, go back to test, and clock out and confirm the flip-flop state. This process is repeated for each transition to be verified. The truth table is redrawn in Figure 10.29 for reference.

| 当前状态 | 下一状态 / 输出 |
|---|---|---|
| | X = 0 | X = 1 |
| A | B/0 | A/0 |
| B | B/0 | C/0 |
| C | D/0 | A/0 |
| D | B/0 | C/1 |

图 10.29 UUT 状态机转换表

Once again, a simple binary assignment for the state variables is used; this will yield the excitation table given in Figure 10.30.

| 当前状态 | 下一状态 / 输出 |
|---|---|---|
| | X = 0 | X = 1 |
| A 00 | B/0 01 / 0 | A/0 00 / 0 |
| B 01 | B/0 01 / 0 | C/0 10 / 0 |
| C 10 | D/0 11 / 0 | A/0 00 / 0 |
| D 11 | B/0 01 / 0 | C/1 10 / 1 |

图 10.30 UUT 状态机转换表

The test begins by placing the machine into state A, the {00} state. The initialization is accomplished by placing the FSM into the test mode and entering the pattern {00} on the scan in line. The X input is placed in the logical 0 state and the state machine into the

