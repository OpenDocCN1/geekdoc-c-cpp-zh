
# Fault Tree

![](img/2d1450514bb14a0cdf0eb5048614afab_173_0.png)

**Figure 19.13** Server 1 and Server 2 - $R(t) \times t$.

```
$\frac{\partial R(t)}{\partial R_{hw1}} = R_{nw}(t)R_{os1}(t)(1 - (1 - R_{a1}(t))(1 - R_{b1}(t)))$
$(1 - R_{hw2}(t))R_{os2}(t)(1 - (1 - R_{a2}(t))(1 - R_{b2}(t)))$
$\frac{\partial R(t)}{\partial R_{hw2}} = R_{nw}(t)R_{os2}(t)(1 - (1 - R_{a2}(t))(1 - R_{b2}(t)))$
$(1 - R_{hw1}(t))R_{os1}(t)(1 - (1 - R_{a1}(t))(1 - R_{b1}(t)))$
$\frac{\partial R(t)}{\partial R_{os1}} = R_{hw1}(t)R_{nw}(t)(1 - (1 - R_{a1}(t))(1 - R_{b1}(t)))$
$(1 - R_{hw2}(t))R_{os2}(t)(1 - (1 - R_{a2}(t))(1 - R_{b2}(t)))$
$\frac{\partial R(t)}{\partial R_{os2}} = R_{hw2}(t)R_{nw}(t)(1 - (1 - R_{a2}(t))(1 - R_{b2}(t)))$
$(1 - R_{hw1}(t))R_{os1}(t)(1 - (1 - R_{a1}(t))(1 - R_{b1}(t)))$
$\frac{\partial R(t)}{\partial R_{a1}} = (1 - R_{b1}(t))R_{hw1}(t)R_{nw}(t)R_{os1}(t)$
$(1 - R_{hw2}(t))R_{os2}(t)(1 - (1 - R_{a2}(t))(1 - R_{b2}(t)))$
$\frac{\partial R(t)}{\partial R_{a2}} = (1 - R_{b2}(t))R_{hw2}(t)R_{nw}(t)R_{os2}(t)$
$(1 - R_{hw1}(t))R_{os1}(t)(1 - (1 - R_{a1}(t))(1 - R_{b1}(t)))$
```

158 Performance, Reliability, and Availability Evaluation of Computational Systems

$$\frac{\partial R(t)}{\partial R_{b1}} = (1-R_{a1}(t))R_{hw1}(t)R_{nw}(t)R_{os1}(t)$$
$(1-R_{hw2}(t))R_{os2}(t)(1-(1-R_{a2}(t))(1-R_{b2}(t))),$$

$$\frac{\partial R(t)}{\partial R_{b2}} = (1-R_{a2}(t))R_{hw2}(t)R_{nw}(t)R_{os2}(t)$$
$(1-R_{hw1}(t))R_{os1}(t)(1-(1-R_{a1}(t))(1-R_{b1}(t))),$$

and

$$\frac{\partial R(t)}{\partial R_{nw}} = 1-(1-R_{hw1}(t)R_{os1}(t)(1-(1-R_{a1}(t))(1-R_{b1}(t))))(1-R_{hw2}(t)R_{os2}(t))\times$$
$(1-R_{a2}(t))(1-R_{b2}(t))).$$

The reliability importance of each component in the interval (0, 4000h) is shown in Figure 19.14. As the importance of each component changes over time, the mission time is essential when adopting these importance indices.

![](img/2d1450514bb14a0cdf0eb5048614afab_174_0.png)

**Figure 19.14** Reliability Importance - $\partial R(t)/\partial R(t) \times t$.

**Example 19.3.2.** Let us calculate the steady-state availability of a computational system composed of an application server (AS), one database-server (DBS), and network attached storage (NAS). Figure 19.15 shows this system. This system fails if the application server (AS) or database-server (DBS) or network attached storage

# Fault Tree

| A1 | A2 | B1 |
|---|---|---|
| VM1 | | VM2 |
| | VMM | |
| | OS_ap | DBMS |
| AS | HW_ap | OS_dbs |
| | | HW_dbs | DBS |

![](img/2d1450514bb14a0cdf0eb5048614afab_175_0.png)

Figure 19.15 Application Server, Database server, and NAS.

(NAS) fails, that is $\Psi(AS, DBS, NAS) = AS \vee DBS \vee NAS$. The FT represents computational system failure is shown in Figure 19.16.
The application server is composed of its hardware ($HW_{as}$), its operational system ($OS_{as}$), a virtual machine manager ($VMM$), and two virtual machines ($VM1$ and $VM2$). $VM1$ hosts two applications, $A1$ and $VM2$ also hosts two other program applications, $B1$ and $B2$. The application server fails if both virtual machine applications fail or the hardware server or the operating system or the virtual machine manager fails. This is specified by

$$\Psi(BS)_{as} = HW_{as} \vee OS_{as} \vee VMM \vee (VM1 \vee (A1 \wedge A2)) \vee (VM2 \vee (B1 \wedge B2)),$$

![](img/2d1450514bb14a0cdf0eb5048614afab_175_1.png)

Figure 19.16 The Computational System Failure - $\Psi(AS, DBS, NAS) = AS \vee DBS \vee NAS$.

# 160 Performance, Reliability, and Availability Evaluation of Computational Systems

$BS = (HW_{as}, OS_{as}, VMM, VM1, VM2, A1, A2, B1, B2)$. The FT in Figure 19.17 represents this failure mode.

![](img/2d1450514bb14a0cdf0eb5048614afab_176_0.png)

# Figure 19.17 Application Server Failure.

The database-server is composed of its hardware ($HW_{dbs}$), its operational system ($OS_{dbs}$), and the database management system ($DBMS$). The database-server fails if its hardware or its operational system or database management system fail. Formally, $\Psi(HW_{dbs}, OS_{dbs}, DBMS) = HW_{dbs} \vee OS_{dbs} \vee DBMS$. The FT represents computational system failure is shown in Figure 19.18.

![](img/2d1450514bb14a0cdf0eb5048614afab_176_1.png)

# Figure 19.18 Database Server.

# Fault Tree

The network-attached system is composed of a controller (NASC) and the storage, which is composed of disks (D1, D2, D3, D4, D5, D6). The NAS fails if its controller or the storage fails. Storage (RAID5) fails if two disks out of D1, D2, and D3, or two disks out of D4, D5, and D6 fail. The network-attached system is represented by

$$\Psi(BS)_{nas} = NASC \vee ((D1 \wedge D2) \vee (D1 \wedge D3) \vee (D2 \wedge D3)) \vee (D4 \wedge D5) \vee (D4 \wedge D6) \vee (D5 \wedge D6))$$

![](img/2d1450514bb14a0cdf0eb5048614afab_177_0.png)

Figure 19.19 NAS.

The hardware of each server ($HW_{as}$) is composed of a motherboard ($MB$), a controller ($NC$), a disk ($D$), and two power sources ($S^1, S^2$). The hardware fails if the motherboard, the controller, the disk, or both power sources fail. The hardware is represented by

$$\Psi(BS)_{hw} = MB \vee NC \vee D \vee (S^1 \wedge S^2)$$

# Performance, Reliability, and Availability Evaluation of Computational Systems

The steady-state availability of a computational system can be calculated using the reliability importance. The reliability importance of each component in the interval (0, 4000h) is shown in Figure 19.14. As the importance of each component changes over time, the mission time is essential when adopting these importance indices.

Example 19.3.2. Let us calculate the steady-state availability of a computational system composed of an application server (AS), one database-server (DBS), and network attached storage (NAS). Figure 19.15 shows this system. This system fails if the application server (AS) or database-server (DBS) or network attached storage (NAS) fails, that is $\Psi(AS, DBS, NAS) = AS \vee DBS \vee NAS$. The FT represents computational system failure is shown in Figure 19.16.

The application server is composed of its hardware ($HW_{as}$), its operational system ($OS_{as}$), a virtual machine manager ($VMM$), and two virtual machines ($VM1$ and $VM2$). $VM1$ hosts two applications, $A1$ and $VM2$ also hosts two other program applications, $B1$ and $B2$. The application server fails if both virtual machine applications fail or the hardware server or the operating system or the virtual machine manager fails. This is specified by

$$\Psi(BS)_{as} = HW_{as} \vee OS_{as} \vee VMM \vee (VM1 \vee (A1 \wedge A2)) \vee (VM2 \vee (B1 \wedge B2)),$$

$BS = (HW_{as}, OS_{as}, VMM, VM1, VM2, A1, A2, B1, B2)$. The FT in Figure 19.17 represents this failure mode.

The database-server is composed of its hardware ($HW_{dbs}$), its operational system ($OS_{dbs}$), and the database management system ($DBMS$). The database-server fails if its hardware or its operational system or database management system fail. Formally, $\Psi(HW_{dbs}, OS_{dbs}, DBMS) = HW_{dbs} \vee OS_{dbs} \vee DBMS$. The FT represents computational system failure is shown in Figure 19.18.

The network-attached system is composed of a controller (NASC) and the storage, which is composed of disks (D1, D2, D3, D4, D5, D6). The NAS fails if its controller or the storage fails. Storage (RAID5) fails if two disks out of D1, D2, and D3, or two disks out of D4, D5, and D6 fail. The network-attached system is represented by

$$\Psi(BS)_{nas} = NASC \vee ((D1 \wedge D2) \vee (D1 \wedge D3) \vee (D2 \wedge D3)) \vee (D4 \wedge D5) \vee (D4 \wedge D6) \vee (D5 \wedge D6))$$

The hardware of each server ($HW_{as}$) is composed of a motherboard ($MB$), a controller ($NC$), a disk ($D$), and two power sources ($S^1, S^2$). The hardware fails if the motherboard, the controller, the disk, or both power sources fail. The hardware is represented by

$$\Psi(BS)_{hw} = MB \vee NC \vee D \vee (S^1 \wedge S^2)$$

The steady-state availability of a computational system can be calculated using the reliability importance. The reliability importance of each component in the interval (0, 4000h) is shown in Figure 19.14. As the importance of each component changes over time, the mission time is essential when adopting these importance indices.

| Component | MTTF (h) | MTTR (h) |
|---|---|---|
| OS | 2000 | 4 |
| VMM | 3000 | 5 |
| VM1 | 2000 | 4 |
| VM2 | 2000 | 4 |
| A1 | 1200 | 2 |
| A2 | 1200 | 2 |
| B1 | 1500 | 3 |
| B2 | 1500 | 3 |

The steady-state availability of a computational system can be calculated using the reliability importance. The reliability importance of each component in the interval (0, 4000h) is shown in Figure 19.14. As the importance of each component changes over time, the mission time is essential when adopting these importance indices.
