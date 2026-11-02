# 2.3 **DESIGN OF THE TANK SIMULATOR**

The simulator has four parts: the simulation engine, the model of the tank, the driver’s interface, and the network interface. Figure 2.10 shows the classes that implement these parts and their relationships. The simulation engine and tank, which are our main concern, are implemented by the *Simulator* class and *SimEventListener* interface and the *Tank* class, respectively. The user interface is implemented by the *Display* class and *DisplayEventListener* interface, which take input from the user and display the motion of the tank. The *UDPSocket* class implements the network interface by which the simulator receives commands from the driver.

![](bbox=[0.122, 0.334, 0.888, 0.882])

**FIGURE 2.10** Class diagram showing the major components of the simulation software.