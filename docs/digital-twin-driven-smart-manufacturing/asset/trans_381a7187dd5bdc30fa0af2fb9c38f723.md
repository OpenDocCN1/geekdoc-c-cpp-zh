

technologies play important roles in SoSM. With the IoT and Internet technologies, various data in all aspects of manufacturing can be collected, and be converged continuously to the cloud from the terminals. Cloud computing and big data technologies process these original data through sorting, classification, analysis, and other operations to extract the value of the data. Through learning wisdom from the cloud, manufacturing equipment and enterprises can better understand the demands of customers, and these data are encapsulated into services. Through these services and data, coupled with the corresponding software, manufacturing big data are converted into practical information such as yield, quality records, health status of manufacturing elements, and energy efficiency. This information can further help manufacturers better judge and understand the status of manufacturing production. The interconnection and interoperability between the physical space and the virtual space enable SoSM to become a cyber-physical system. Through new generation information technology (New IT), the virtual space in SoSM can be more extensive to connect all things, more intelligent to capture and analyze data, and more proactive to provide services. The physical space can be more efficient to implement manufacturing activities, utilizing the potential of SoSM as a cyber-physical system [26].

## 10.3 SERVICES IN DIGITAL TWIN

All manufacturing resources and capabilities in the product lifecycle can be virtualized and then encapsulated into services. According to different existence forms and usage patterns, services can be mainly divided into resource services and information resources. The former is developed from hardware resources in manufacturing, such as manufacturing equipment, computing equipment, and materials, while the latter is from software resources, such as professional software, experience models, domain knowledge, and algorithms [27]. In addition, in a specific manufacturing activity, the resources can be extended to certain capabilities, such as in design, simulation, production, and maintenance [27-29].

For the DT, services can be secured from two perspectives. On one hand, services form a crucial component of the five-dimension DT. For example, when a production task is input, the service system can invoke corresponding services to complete the task through service scheduling and combination. On the other hand, the other components of the five-dimension DT (i.e., physical entity, virtual entity, data, and connection)
can also be encapsulated into services. Benefiting from comprehensive servitization, the DT can be uniformly managed in a service platform. When a task is submitted to the platform, the suitable services among all the candidates are invoked and combined to form a complete DT first, and then perform the task collaboratively.

## 10.4 DIGITAL TWIN SERVICE GENERATION

Models and data are the cores of the DT. However, the creation of virtual models and fusion of data are complex and specialized projects. For users who do not have relevant knowledge, it is difficult to build and use the DT. Therefore, it is imperative that the models can be shared by users and data analysis can be outsourced to third-party professional organizations. Moreover, in the context of manufacturing socialization, the physical resources involved in manufacturing are geographically distributed. With the characteristics of on-demand use, dynamic reconfiguration, and platform independence, services pave way for the problems mentioned above [30]. In the following sections, servitization of physical entities, virtual entities, and data in the DT [33] is mainly discussed.

### 10.4.1 Physical Entity Servitization

Service encapsulation translates various components of the DT into services with uniform description [31]. As shown in Fig. 10.2 [30], the first and most important step of service encapsulation is to establish the information template, which consists of rich information [32]. For the physical entity, the information includes basic attributes (e.g., name, ID, address), quality of service (QoS) (e.g., time, cost, reliabilities, satisfaction), capacities (e.g., precision, size, process), real-time status (e.g., overload, idle, in maintenance), as well as input and output. The information templates of the physical entity (i.e., PE) can be described as (10.1) [30].

```
PE = {Basic, QoS, Cap, Status, Input, Output}    (10.1)
```

wherein, Basic refers to the basic attributes for identifying the physical entity. QoS denotes the evaluation for the performance of the physical entity in conducting the user selection. Cap represents the functions of the physical entity. Status indicates whether the physical entity is available. Taking an NC machine tool as an example, the production capacity includes the capacities for shape processing (e.g., plane, hole, thread),
precision (e.g., roughness, deflection), parts processing (e.g., gear, plate), size (e.g., height, width, coordinates). Status can be overloaded, idle, in maintenance, etc. With respect to input and output, the input of the NC machine tool can be materials, such as steel, aluminum alloy, etc. And the output can be a part, or a small product. They can be formulized as (10.2)–(10.5) [30]:

```
Basic = {type, name, ID, address, color, delivery_time, ...}  (10.2)
```

```
QoS = {cost, time, reliability, trust, Fun_similarity, ...}  (10.3)
```

```
Cap = {shape_cap, precision_cap, parts_cap, size_cap,...}  (10.4)
```

```
Status = {load, health, ...}  (10.5)
```

![](img/5042607b423be4a5ee3f15dae22cc5bb_208_0.png)

# Figure 10.2 DT service encapsulation.

### 10.4.2 Virtual Entity Servitization

Similarly, the virtual entity, which is composed of a set of virtual models, can also be described by the information template. Different from the physical entity, the virtual entity can be used by multiple users at the same
time, and can be copied without repetitive creation for the same or equal physical entity. Therefore, when the virtual entity is encapsulated into services that can be shared by users, not only can the creators of the virtual models receive benefits, but the users can also reduce costs and time. The information templates of the virtual entity (i.e., VE) can be described as in (10.6) [30].

```
VE = { Ori_phy, Creator, Ori_ID, Cur_ID, Owner, QoS, Online_site, Input, Output, ... } (10.6)
```

wherein, Ori_phy denotes the original physical entity corresponding to the virtual entity. Creator is the one who builds the virtual entity based on his specialized knowledge. Ori_ID is the original identifying number when the virtual entity is first created. Cur_ID represents the identifying number of the current copy. Owner is the one who possesses the virtual entity. The owner has copyright or may be the creator, and can earn profits through renting out the models or selling copies. Similar to the physical entity, QoS denotes the evaluation of the performance of the virtual entity, including cost, reliability, functions, etc. Online_site denotes the online address where users can access or download the models. Input and Output may vary according to the specific models [30].

### 10.4.3 Data Servitization

In addition, data are very important for smart manufacturing [33]. However, because of the various standards and communication protocols/interfaces, data are often difficult to acquire and understand. Through using the unified templates to describe the data, users can conveniently use the data. In general, data information includes the data provider who owns the data, data sources where the data is collected, data ID used to identify the data, data type (which denotes the kind of the data), and data abstract, which is a brief introduction to data value. Therefore, data (i.e., DD) can be described as in (10.7) [30].

```
DD = { D_prov, D_source, D_ID, D_type, D_abstract, ... } (10.7)
```

The information templates describe most of the information that users want to know and have to know. After the information templates are established, various kinds of physical entities, virtual entities, and data are encapsulated into services based on the service description language, such as XML. As an example, the information template of a punching machine
