```
m_vpg.setVpgStep(1, 0.0, 1.0, 2000, false);
m_VPG.setProgramStep(2, 1.0, 0.0, 2000, true);
m_VPG.setProgramStep(3, 0.0, -1.0, 2000, true);
```

```
// --- RAFX version, VPG is disabled so you can use the easy
// programJoystick in RAFX (hit the Program button)
m_bEnableVPG = false;
// m_bEnableVPG = true; //<-- uncomment to use VPG instead of JSProgram

#else
// -- the flag argument means you used the rotated coordinates
m_VPG.setProgramStep(0, -1.0, 1.0, 2000, false);

m_VPG.setProgramStep(1, 1.0, 1.0, 2000, false);
m_VPG.setProgramStep(2, 1.0, -1.0, 2000, false);
m_VPG.setProgramStep(3, -1.0, -1.0, 2000, false);

// --- for VST3/AU, there is no built-in program generator, so do it by
// hand here
m_bEnableVPG = true;
#endif
```

initializations. You need to update the new global parameter variables here, where you simply parse the variables offyour global parameter structure.

# reset()

In reset() you just call the base class function.

# noteOn()

In noteOn() you need to add a call to start up the vector path generator or RackAFX joystick program; the path is executed for each note that is played. This is done after calling the base class implementation. Notice the use of the m_bEnableVPG flag and checking of the JSProgram pointer prior to calling the startProgram() function.

# noteOff()

In noteOff() you need to add a call to resume the vector path generator or RackAFX joystick program if in sustain mode since these objects will halt their programs at the second-to-last vertex during the sustain portion of the event.