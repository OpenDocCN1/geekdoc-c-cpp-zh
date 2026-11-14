level. The approach tends to be more useful for developing the hardware rather than the software side. It is useful for verifying detailed and critical timing, hardware and software interactions, the boot process and memory interfaces and subsystems.

+   - **Hardware Emulation**
+   Under such an emulation, the hardware is modeled through some form of arrayed logic. Specifically this is an emulation; however, execution speed approaches that of a full ASIC. Contemporary arrayed logics can support the inclusion of CPU cores that will enable and facilitate both hardware and software debug.

# ## 9.24 OTHER CONSIDERATIONS

Several other factors must also be taken into consideration. The product must be able to be manufactured and tested. Such factors must be addressed early in the definition and design process. The three additional complementary and concurrent activities that need to be considered in today's business world are capitalization, reuse, and requirements and traceability management. Let us look briefly at capitalization; design reuse is one of the central threads in this text.

# ### 9.24.1 Capitalization and Reuse

# #### 9.24.1.1 Capitalization

Capitalization is an essential element of the contemporary design process. Specifically, proper and efficient exploitation of intellectual properties (IPs) is very important today. Intellectual properties are designs, often patented, that can be sold or licensed to another party to develop and sell as (a part of) their product. The company MIPS, for example, designs computer architectures. It doesn't actually do any implementation itself; the design is its product; the ARM corporation does a similar thing.

# #### 9.24.1.2 Reuse

Any consideration of component reuse is an activity that should be addressed and done during the functional and architectural design phases of the development process. Such activities can be considered sometimes during prototyping as well. The end purpose is to help designers shorten development cycles.

Component reuse is facilitated in two ways: present and future.

+   - **Present**
+   By identifying external (existing) functional or architectural components that can satisfy some portions of the currents system's desired functionality.

+   - **Future**
+   By identifying components of the solution under design that can or will be reusable on other or future projects or products.

To be reused, a component needs to be:

+   - Well defined
+   - Properly modularized
+   - In conformance to some interchange standard.