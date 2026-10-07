# Modeling Availability, Reliability, and Capacity with CTMC

# Table 21.8
Tiny-Private Cloud System Parameters

| Component | MTTF (h) | MTTR (h) | MTTS (h) |
| Mother board (MB) | 80000 | | |
| Memory (M) | 40000 | | |
| Network controller (NC) | 60000 | | |
| Video controller (VC) | 50000 | | |
| Hard disk controller (HDC) | 45000 | | |
| Hard disk (HD) | 35000 | | |
| Power source (PS) | 20000 | | |
| Operational system (OS) | 4000 | 1 | |
| Hypervisor (HP) | 5000 | 1 | |
| Virtual Machine | 4000 | 0.25 | |
| NAS Controller (NASC) | 50000 | 4 | |
| Cloud Manager Software (CMS) | 3000 | 2 | |
| Server Handler | | 24 | |
| CM | | 8 | |
| CM' | | 8 | 0.1 |

comprises two cloud managers (CM + CM') configured in cold-standby. Each cloud manager is operational if its hardware, its operating system, and the cloud manager software (CMS) are operational. Each server is operational if its hardware, its operational system, the virtual machine manager (VMM), and at least one virtual machine (VM) are functional. Each server provides four VMs. The tiny-private cloud system is operational if at least one virtual machine is operational. Assume the times-tofailure and the times-to-repair are exponentially distributed. The time to start (TTS) the CM' is also exponentially distributed with rate $\delta$. The MTTFs, the MTTRs, and the MTTS are depicted in Table 21.8. Consider only one repair team. (a) Compute the availability, (b) downtime, (c) capacity-oriented availability, and (d) mean number of operational VMs of the system. Hint: use RBDs or FT and CTMCs.