
global illumination, and document layout, even visibility algorithms that are currently out of favor for primary rays may be preferred in other applications.

- **36.1 Introduction** ... 1023
  - 36.1.1 The Visibility Function ... 1025
  - 36.1.2 Primary Visibility ... 1027
  - 36.1.3 (Binary) Coverage ... 1027
  - 36.1.4 Current Practice and Motivation ... 1028
- **36.2 Ray Casting** ... 1029
  - 36.2.1 BSP Ray-Primitive Intersection ... 1030
  - 36.2.2 Parallel Evaluation of Ray Tests ... 1032
- **36.3 The Depth Buffer** ... 1034
  - 36.3.1 Common Depth Buffer Encodings ... 1037
- **36.4 List-Priority Algorithms** ... 1040
  - 36.4.1 The Painter’s Algorithm ... 1041
  - 36.4.2 The Depth-Sort Algorithm ... 1042
  - 36.4.3 Clusters and BSP Sort ... 1043
- **36.5 Frustum Culling and Clipping** ... 1044
  - 36.5.1 Frustum Culling ... 1044
  - 36.5.2 Clipping ... 1045
  - 36.5.3 Clipping to the Whole Frustum ... 1047
- **36.6 Backface Culling** ... 1047
- **36.7 Hierarchical Occlusion Culling** ... 1049
- **36.8 Sector-based Conservative Visibility** ... 1050
  - 36.8.1 Stabbing Trees ... 1051
  - 36.8.2 Portals and Mirrors ... 1052
- **36.9 Partial Coverage** ... 1054
  - 36.9.1 Spatial Antialiasing (xy) ... 1055
  - 36.9.2 Defocus (uv) ... 1060
  - 36.9.3 Motion Blur (t) ... 1061
  - 36.9.4 Coverage as a Material Property (α) ... 1062
- **36.10 Discussion and Further Reading** ... 1063
- **36.11 Exercise** ... 1063
- **37 Spatial Data Structures** ... 1065

Spatial data structures like bounding volume hierarchies provide intersection queries and set operations on geometry embedded in a metric space. Intersection queries are necessary for light transport, interaction, and dynamics simulation. These structures are classic data structures like hash tables, trees, and graphs extended with the constraints of 3D geometry.

  - 37.1 Introduction ... 1065
    - 37.1.1 Motivating Examples ... 1066
  - 37.2 Programmatic Interfaces ... 1068
    - 37.2.1 Intersection Methods ... 1069
    - 37.2.2 Extracting Keys and Bounds ... 1073
  - 37.3 Characterizing Data Structures ... 1077
    - 37.3.1 1D Linked List Example ... 1078
    - 37.3.2 1D Tree Example ... 1079
  - 37.4 Overview of kd Structures ... 1080
  - 37.5 List ... 1081
  - 37.6 Trees ... 1083
    - 37.6.1 Binary Space Partition (BSP) Trees ... 1084
    - 37.6.2 Building BSP Trees: oct tree, quad tree, BSP tree, kd tree ... 1089
    - 37.6.3 Bounding Volume Hierarchy ... 1092
  - 37.7 Grid ... 1093
    - 37.7.1 Construction ... 1093
    - 37.7.2 Ray Intersection ... 1095
    - 37.7.3 Selecting Grid Resolution ... 1099
  - 37.8 Discussion and Further Reading ... 1101
- **38 Modern Graphics Hardware** ... 1103

We describe the structure of modern graphics cards, their design, and some of the engineering trade-offs that influence this design.

  - 38.1 Introduction ... 1103
  - 38.2 NVIDIA GeForce 9800 GTX ... 1105
  - 38.3 Architecture and Implementation ... 1107
    - 38.3.1 GPU Architecture ... 1108
    - 38.3.2 GPU Implementation ... 1111
  - 38.4 Parallelism ... 1111
  - 38.5 Programmability ... 1114
  - 38.6 Texture, Memory, and Latency ... 1117
    - 38.6.1 Texture Mapping ... 1118
    - 38.6.2 Memory Basics ... 1121
    - 38.6.3 Coping with Latency ... 1124
  - 38.7 Locality ... 1127
    - 38.7.1 Locality of Reference ... 1127
    - 38.7.2 Cache Memory ... 1129
    - 38.7.3 Divergence ... 1132
  - 38.8 Organizational Alternatives ... 1135
    - 38.8.1 Deferred Shading ... 1135
    - 38.8.2 Binned Rendering ... 1137
    - 38.8.3 Larrabee: A CPU/GPU Hybrid ... 1138
  - 38.9 GPUs as Compute Engines ... 1142
  - 38.10 Discussion and Further Reading ... 1143
  - 38.11 Exercises ... 1143
- List of Principles ... 1145
- Bibliography ... 1149
- Index ... 1183

*This page intentionally left blank*

## Preface

This book presents many of the important ideas of computer graphics to students, researchers, and practitioners. Several of these ideas are not new: They have already appeared in widely available scholarly publications, technical reports, textbooks, and lay-press articles. The advantage of writing a textbook sometime after the appearance of an idea is that its long-term impact can be understood better and placed in a larger context. Our aim has been to treat ideas with as much sophistication as possible (which includes omitting ideas that are no longer as important as they once were), while still introducing beginning students to the subject lucidly and gracefully.

This is a second-generation graphics book: Rather than treating all prior work as implicitly valid, we evaluate it in the context of today's understanding, and update the presentation as appropriate.

Even the most elementary issues can turn out to be remarkably subtle. Suppose, for instance, that you're designing a program that must run in a low-light environment—a darkened movie theatre, for instance. Obviously you cannot use a bright display, and so using brightness contrast to distinguish among different items in your program display would be inappropriate. You decide to use color instead. Unfortunately, color perception in low-light environments is not nearly as good as in high-light environments, and some text colors are easier to read than others in low light. Is your cursor still easy to see? Maybe to make that simpler, you should make the cursor constantly jitter, exploiting the motion sensitivity of the eye. So what seemed like a simple question turns out to involve issues of interface design, color theory, and human perception.

This example, simple as it is, also makes some unspoken assumptions: that the application uses graphics (rather than, say, tactile output or a well-isolated audio earpiece), that it does not use the regular theatre screen, and that it does not use a head-worn display. It makes explicit assumptions as well—for instance, that a cursor will be used (some UIs intentionally don't use a cursor). Each of these assumptions reflects a user-interface choice as well.

Unfortunately, this interrelatedness of things makes it impossible to present topics in a completely ordered fashion and still motivate them well; the subject is simply no longer linearizable. We could have covered all the mathematics, theory of perception, and other, more abstract, topics first, and only then moved on to their graphics applications. Although this might produce a better reference work (you know just where to look to learn about generalized cross products,
