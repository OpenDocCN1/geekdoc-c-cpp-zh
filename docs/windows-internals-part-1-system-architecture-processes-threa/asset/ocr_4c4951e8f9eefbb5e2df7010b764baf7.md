# TABLE 7-24 Generalized description of elements protected by HyperGuard

| Component | Legitimate Usage | Potential Unwanted Usage |
|---|---|-|
|Executable code in the kernel, its dependencies, and well as the Import Table (IAT) of these components | Refer to Table 7-23. | Refer to Table 7-23. |
Global Descriptor Table (GDT) | Refer to Table 7-23. | Refer to Table 7-23. |
Interrupt Descriptor Table (IDT) or Interrupt Vector Table | Refer to Table 7-23. | Refer to Table 7-23. |
Critical CPU registers such as Control Registers, GDTR, IDTR, Vector Base Register, and Model Specific Registers | Refer to Table 7-23. | Refer to Table 7-23. |
Executable code, callbacks, and data regions in the Secure Kernel and its dependencies, including HyperGuard itself | Standard Windows components operation of VTL 1 and secure kernel-mode usage. | Patching code in these components implies that attacker has access to some sort of vulnerability in VTL 1, either through hardware or the hypervisor. Could be used to divert Device Guard, HyperGuard, and Credential. |
Structures and features used by Trustlets | Sharing data between one Trustlet to another, or Trustlets and the kernel, and Trusts | Implies some vulnerability might exist in one or more Trustlets, which could be used to hide features such as Credential or Shielded Fabric/VTM. |
Hypervisor structures and regions | Used by the hypervisor to communicate with VTL 1 | Implies a vulnerability in VTL 1 or the hypervisor which may be accessible from 0 in VTL 0. |
Kernel CFG bitmap | Used to identify valid functions that are subject of indirect function calls or jumps, as described earlier. | Implies that an attacker has been able to perform a modification to the VTL 1-protected KCFG bitmap through some sort of hardware or hypervisor exploit. |
Page verification | Used to implement HVCI-related work for Device Guard. | Implies that an attacker has attacked SKCI, which could result in Device Guard compromise or non-authorized IUM Trusts. |
NULL page | None. | Implies that an attacker has coerced the kernel and/or secure kernel to validate page 0, which can be used to exploit NULL vulnerabilities in VTL 0 or VTL 1.

Systems with VBS enabled, there is another security-related feature that is worth describing, which is implemented in the hypervisor itself: Non-Privileged Instruction Execution Prevention (NPIEP). This mitigation mitigates specific x64 instructions that can be used to leak the kernel-mode addresses of the GDT, IDT, and LDT, which are SGDT, SIDT, and SLDT. With NPIEP, these instructions are still allowed to execute (due to compatibility concerns), but return a per-processor unique number that is not actually the kernel address of these structures. This serves as a mitigation against Kernel ASLR (KASLR) information leaks from local attackers.

Finally, note that there is no way to disable PatchGuard or HyperGuard once they are enabled. However, device-driver developers might need to make changes to a running system as of debugging, PatchGuard is not enabled when the system boots in debugging mode with an active remote-debugging connection. Similarly, HyperGuard is disabled if the hypervisor boots in debugging mode with a remote debugger attached.