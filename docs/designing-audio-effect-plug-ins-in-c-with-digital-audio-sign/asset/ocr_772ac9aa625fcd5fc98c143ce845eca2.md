+   - COnePoleLPF
+   - CDelay
+   - CCombFilter
+   - CLPFCmbFilter
+   - CDelayAPF

When you tell RackAFX to add them to your project, RackAFX automatically copies the files, #includes them, and adds them to your C++ project file. Here's a quick reference guide to the objects. With these objects, coding our example reverb unit will be much easier than you think.

# 11.16.1 COnePoleLPF

Implements a one-pole LPF with a single coefficient, g in Figure 11.41. Table 11.4 shows object members.

![](bbox=[0.28, 0.33, 0.72, 0.45])

Figure 11.41: The one-pole LPF.

Table 11.4: The COnePoleLPF object.

| Member Variables | Purpose |
| :--- | :--- |
| float m_fLPF_g<br>float m_fLPF_z1 | Implements the one and only gain coefficient g.<br>Register to hold the single sample delay, z^-1. |
| Member Functions | |
| void setLPF_g(float fLPFg)<br>Parameters:<br>• float fLPFg | set() function for gain coefficient.<br>Input: the new gain value. |
| void init() | Function to initialize and clear out the z^-1 register. |
| bool processAudio(float* pInput, float* pOutput)<br>Parameters:<br>• float* pInput<br>• float* pOutput | Process one input sample.<br>Input: pointer to a float input sample.<br>Output: pointer to the output sample destination. |