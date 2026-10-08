programmer. Figure 11.11 shows the MSSP block diagram for the I²C.

SSPSR is the shift register used for shifting data in or out. SSPBUF is the register to which data bytes are written to or read from. SSPADD register holds the slave device address when the MSSP is configured in I²C Slave mode. When the MSSP is configured in Master mode, the lower seven bits of SSPADD act as the Baud Rate Generator reload value. When SSPSR receives a complete byte, it is transferred to SSPBUF and an interrupt is set. A write to SSPBUF will write to both SSPBUF and SSPSR.

# **PIC18F MSSP Registers for I²C mode** The following registers included in the MSSP module are used for the I²C mode:

+   * SSPSTAT (Figure 11.12)
* SSPCON1 (Figure 11.13)
* SSPCON2 (Figure 11.14)
* SSPADD (Figure 11.15)

# **SSPSTAT register (Figure 11.12)** Upper two bits (SMP and CKE) are read/write and other bits are read-only.

+   * BF (Buffer Full): If this is 1, it means the SSPBUF is loaded with 8-bit. This bit will be cleared if the SSPBUF is read.
* R/W (Read/Write): This bit tells when the Master is reading from or writing to the slave device.
* S (Start): If we set this bit, the START condition will occur.
* P (Stop): If we set this bit, the STOP condition will occur.
* CKE (Clock Edge) enables (synchronizes with) or disables the SMBus. Note that the SMBus (System Management Bus) is a serial protocol based on I²C. The SMBus is a two-wire bus commonly used in computer motherboards for monitoring voltage and temperature. SMBus only goes up to 100kHz.
* SMP (Slow rate control): Enabled (SMP cleared to 0) for 400kHz and disabled (SMP set to 1) for 100kHz. Note that slow rate control is primarily an EMI (ElectroMagnetic Interference) control feature. When using slow-speed along with long-wire I²C setups,

![](bbox=[0.15, 0.65, 0.85, 0.88])