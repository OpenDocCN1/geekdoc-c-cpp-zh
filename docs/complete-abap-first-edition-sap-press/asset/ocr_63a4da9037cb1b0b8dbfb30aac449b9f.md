limitation on the possible UI elements that can used on the screen. Many desktop applications that users are accustomed to may provide better UI experiences than what was traditionally possible with SAP screens. Understanding this gap, SAP introduced the Control Framework with SAP ERP 4.5.

The Control Framework allows you to create complex screens that are intuitive and fluid. It enables you to create custom controls on the user's client from your ABAP programs. This framework involves two types of components: server-side components and client-side components.

On the server side, the framework implements a series of ABAP objects, which are collectively called *ABAP Objects Control Framework*. On the client side, the framework is managed by a component called the *Automation Controller* (or *Automation Client*). The Automation Client manages all the custom control instances and takes care of the communication between the custom controls in the presentation layer and the ABAP Objects Control Framework in the application server.

In the following subsections, we'll discuss how to use container controls and then how to implement custom controls using the Control Framework.

# 12.10.1 Using Container Controls

Custom controls are integrated in the SAP GUI client, which implements either Active X controls or JavaBeans depending on the GUI client version. Custom controls allow you to create many complex controls, such as ALV Grid Controls, SAP calendar controls, SAP picture controls, and so on. Each custom control is exposed as an ABAP object of the corresponding control type.

A custom control runs inside a container control. Each container control is exposed as an ABAP object that acts as a parent to the custom control. Different container controls are described in Table 12.3.

| Container Control | Class | Description |
| --- | --- | --- |
| Custom container | CL_GUI_CUSTOM_CONTAINER | The custom container is defined on the screen using Screen Painter. The custom control is displayed inside the container. One screen can have multiple containers. |

**Table 12.3** Container Controls