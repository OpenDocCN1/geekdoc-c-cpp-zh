# APPENDIX H

# The Analog Paradigm bus system

The Analog Paradigm model-1 analog computer features a bus system that makes it easy to extend the system with additional modules for special operations such as the logarithm function generator described in the preceding section. All computing modules are based on standard *Eurocards* (160 mm × 100 mm) using two-row (A/C) DIN 41612 connectors. Table H.1 shows the signals available on this bus system.

When designing new hardware for the Analog Paradigm Model-1 analog computer, the following constraints should be taken into account:

+   - Signals denoted by an overline are active-low logic signals.
+   - Analog and digital ground (AGND/DGND) should never be connected to each other on a module as this would introduce a ground loop and deteriorate system performance.
+   - When POTSET is active, i.e. low, the computer is set to potentiometer setting mode. The integrators are halted and the inputs of all potentiometers are connected to the positive reference voltage. Using the readout feature described below the value set on each potentiometer can then be displayed on a DVM.
+   - The OVERLOAD line can be driven by a computing module to signal an overload condition to the control unit. The driver must be of the open collector type. (A standard TTL-driver can be used but must be decoupled by a diode.)
+   - The signals MODEIC and MODEOP control the operation of the integrators of the overall system.
+   - To read the output value of a computing element its address must be placed onto the address lines A15–A0 and the READ line must be driven low. The element selected in this way will then connect its output to the READOUT