```
ami AMI encoding
b8zs B8ZS encoding
CME_Voice(config-controller)# linecode b8zs
CME_Voice(config-controller)# clock source ?
free-running Free Running Clock
internal Internal Clock
line Recovered Clock
```

```
CME_Voice(config-controller)# clock source line
CME_Voice(config-controller)# ds0-group ?
<0-23> Group Number
CME_Voice(config-controller)# ds0-group 1
timeslots List of timeslots in the ds0-group
CME_Voice(config-controller)# ds0-group 1 timeslots ?
<1-24> List of T1 timeslots
ME_Voice(config-controller)# ds0-group 1 timeslots 1-24 ?
type Specify the type of signaling
<cr>
```

```
CME_Voice(config-controller)# ds0-group 1 timeslots 1-24 type ?
e&m-delay-dial E & M Delay Dial
e&m-fgd E & M Type II FGD
e&m-immediate-start E & M Immediate Start
e&m-lmr E & M land mobile radio
e&m-wink-start E & M Wink Start
ext-sig External Signaling
fgd-eana FGD-EANA BOC side
fxo-ground-start FXO Ground Start
fxo-loop-start FXO Loop Start
fxs-ground-start FXS Ground Start
fxs-loop-start FXS Loop Start
none Null Signifying for External Call Center
<cr>
```

```
CME_Voice(config-controller)# ds0-group 1 timeslots 1-24 type fxo-loop-start ?
CME_Voice(config-controller)#*
CME_Voice# show voice port summary
```

IN OUT
PORT CH SIG-TYPE ADMIN OP STATUS EC
=====================================
1/0:1 01 fxo-ls up down idle on-hook y
1/0:1 02 fxo-ls up down idle on-hook y
1/0:1 03 fxo-ls up down idle on-hook y
1/0:1 04 fxo-ls up down idle on-hook y
1/0:1 05 fxo-ls up down idle on-hook y
1/0:1 06 fxo-ls up down idle on-hook y
1/0:1 07 fxo-ls up down idle on-hook y