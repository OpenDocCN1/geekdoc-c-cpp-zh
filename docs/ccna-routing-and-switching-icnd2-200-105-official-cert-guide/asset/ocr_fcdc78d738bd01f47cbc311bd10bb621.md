+   1. Which of the following network commands, following the command router ospf 1, tells this router to start using OSPF on interfaces whose IP addresses are 10.1.1.1, 10.1.100.1, and 10.1.120.1?
+       a. network 10.0.0.0 255.0.0.0 area 0
+       b. network 10.0.0.0 0.255.255.255 area 0
+       c. network 10.0.0.1 0.0.0.255 area 0
+       d. network 10.0.0.1 0.0.255.255 area 0

+   2. Which of the following network commands, following the command router ospf 1, tells this router to start using OSPF on interfaces whose IP addresses are 10.1.1.1, 10.1.100.1, and 10.1.120.1?
+       a. network 10.1.0.0 0.0.255.255 area 0
+       b. network 10.0.0.0 0.255.255.0 area 0
+       c. network 10.1.1.0 0.x.1x.0 area 0
+       d. network 10.1.1.0 255.0.0.0 area 0
+       e. network 10.0.0.0 255.0.0.0 area 0

+   3. Which of the following commands list the OSPF neighbors off interface serial 0/0? (Choose two answers.)
+       a. show ip ospf neighbor
+       b. show ip ospf interface brief
+       c. show ip neighbor
+       d. show ip interface
+       e. show ip ospf neighbor serial 0/0

+   4. Routers R1, R2, and R3 are internal routers in areas 1, 2, and 3, respectively. Router R4 is an ABR connected to the backbone area (0) and to areas 1, 2, and 3. Which of the following answers describes the configuration on Router R4, which is different from the other three routers, that makes it an ABR?
+       a. The abr enable router subcommand.
+       b. The network router subcommands refer to a single nonbackbone area.
+       c. The network router subcommands refer to multiple areas, including the backbone.
+       d. The router has an interface in area 0, whereas an OSPF neighbor's interface sits in a different area.

+   5. An engineer connects to Router R1 and issues a show ip ospf neighbor command. The status of neighbor 2.2.2.2 lists FULL/BDR. What does the BDR mean?
+       a. R1 is an Area Border Router.
+       b. R1 is a backup designated router.
+       c. Router 2.2.2.2 is an Area Border Router.
+       d. Router 2.2.2.2 is a backup designated router.