# DRL Package
6-Pin SOT563
Top View

![](bbox=[0.38, 0.2, 0.68, 0.32])

Figure 7.14 TMP102 pin layout

TMP102 has the following operational modes:

+   - **Continuous conversion:** by default, an internal ADC converts the temperature into digital format with the default conversion rate of 4Hz, with a conversion time of 26ms. The conversion rate can be selected using bits CR1 and CR0 of the configuration register as 0.25Hz, 1Hz, 4Hz (default), and 8Hz. In this project, the default 4Hz is used.
+   - **Extended mode:** Bit EM of the configuration register selects normal mode (EM = 0), or extended mode (EM = 1). In normal mode (default mode), the converted data is 12 bits. Extended mode is used if the temperature is above 128°C and the converted data is 13 bits. In this project, the normal mode is used.
+   - **Shutdown mode:** This mode is used to save power where current consumption is reduced to less than 0.5µA. Shutdown mode is entered when configuration register bit SD = 1. The default mode is normal operation (SD = 0).
+   - **One-shot conversion:** Setting configuration register bit OS to 1 selects one-shot mode which is a single conversion mode. The default mode is continuous conversion (OS = 0).
+   - **Thermostat mode:** This mode indicates whether to operate in comparator (TM = 0) or interrupt mode (TM = 1). The default is comparator mode. In comparator mode, the Alert pin is activated when the temperature equals or exceeds the value in the THIGH register, and remains active until the temperature drops below TLOW. In interrupt mode, the Alert pin is activated when the temperature exceeds THIGH or goes below TLOW registers. The Alert pin is cleared when the host controller reads the temperature register.

A Pointer Register selects various registers in the chip as shown in Table 7.1. The upper 6 bits of this register are 0s.