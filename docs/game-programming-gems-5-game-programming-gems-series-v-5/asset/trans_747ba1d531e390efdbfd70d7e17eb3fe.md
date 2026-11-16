

rendering of the level [Luebke95]. In contrast to the standard portal rendering philosophy of using convex cells connected via portals, we place no restrictions on the geometry in each cell. A disadvantage of using non-convex cells is that it can result in overdraw during rendering. This is outweighed, however, by the flexibility we gain from placing no limits on the cell geometry and the ease with which we can automatically create the portals.

To enable collision detection, we create a binary tree of axis-aligned bounding boxes (AABBs) for each model in the cell-model list in a manner similar to [Schroeder01]. Finally, since there is no direct relationship between a cell in the level (in world space) and its corresponding node in the graph, we create a hash table that maps world coordinates to nodes in the graph. Making the hash table efficient is vital since every reference to data in the level, using world coordinates, maps through the hash table. Some general knowledge of the potential layout of the level is helpful to make the hash function fast.

## 添加关卡内容

At this point, we have a basic level, perhaps large but nonetheless empty, as shown in Figure 5.9.7. Using a rule-based system, with rules derived from the design, several types of content can be added. Nodes in the graph can be annotated with environmental audio properties and other sound effects based on the size, shape, and content of each node’s geometry. Adding actual geometry falls into two categories. Static geometry includes augmentations to the level geometry such as pillars or statues. These are items we may want to weld to the existing cell geometry. If so, we need to make sure the cell geometry is not being instanced by more than one node in the graph. If it is, we will need to create a separate version of the cell geometry before we weld any new geometry to the cell. Welding new geometric features also requires an update to the cell’s AABB tree and possibly the recalculation of portals. Nonstatic geometry can simply be added at the node level without welding.

![](img/672fe9a2d008ba627b1991e15d70f43e_636_0.png)

FIGURE 5.9.7 Basic dungeon of corridors and rooms generated using a “tentacle” graph (inset). Entrance to the dungeon is via a small corridor shown at the top of the graph.

## 结论

We have presented a process for generating procedural game levels to address the large amount of content required by growing game genres such as massively multiplayer online games. Given an appropriate set of rules, our algorithm provides amplification of a simple data structure into a complex geometric game level [Roden04]. Our process begins by generating a 3D graph with appropriate rules. Prefabricated 3D geometric level pieces are then mapped to nodes of our graph. Identical geometry is instanced instead of being copied, taking care to weld sub-cell prefabs into a single model to reduce the number of redundant vertices and save on rendering time. We then compute visibility and collision detection information for later use by our portal algorithm. Finally, we add level content such as static geometry and environmental audio.

The method presented should be considered as a foundation for the reader in building their own level generator. One important issue we have not touched upon is lighting. A procedure for adding realistic lighting would depend not only on the design but also on how the level generator is used. If levels are generated as a pre-process, lighting can be computed using pre-processing techniques, whereas for dynamically generated levels, a different set of lighting techniques would be employed.

## 参考文献

- [Luebke95] Luebke, David 和 Chris Georges. “传送门与镜子：潜在可见集的简单快速评估。” 在（Pat Hanrahan 和 Jim Winget，编辑）ACM 交互式3D图形研讨会（1995年4月）：第105–106页。

- [Perry02] Perry, Lee. “模块化关卡和组件设计。” 在《游戏开发者杂志》（2002年11月）：第30–35页。

- [Roden04] Roden, Timothy 和 Ian Parberry. “从艺术到自动化：程序化内容创建的结构化方法。” 第3届娱乐计算国际会议（2004年9月）。

- [Schroeder01] Schroeder, Tim. “使用射线投射进行碰撞检测。” 在《游戏开发者杂志》（2001年8月）：第50–56页。

## 重组着色器

**Dominic Filion，人工心智与运动公司**

dfilion@hotmail.com

Graphics Processing Units (GPUs) were recently brought much closer to their CPU counterparts with the introduction of shaders. GPUs went from rigid graphics processing devices to more general chips, as can be seen in the increasing amount of research being put into using shaders for physics, math computations, and raytracing.

It was only a matter of time before the advent of GPU compilers would make shaders even more useful. GPUs are indeed seeing the same evolution as their CPU counterparts (specialized chips, evolution to general purpose, compiling tools, and optimizers) but at a much faster pace.

GPUs are at this time, however, very far behind their CPU counterparts when it comes to flexibility and ease of integration.

Some issues with GPUs include:

- **程序长度有限**：微程序长度有限意味着整个应用程序的图形管道不能放入单个程序或函数中，就像软件渲染器可能做到的那样。
- **分支有限或缺失**：大多数编程模型中缺乏分支指令是一种严重的限制，它抑制了管道的灵活性。
- **没有通用的散射-聚集**：GPU没有通用内存模型，因为它们的内存不是随机可访问的。
- **与固定管道无交互**：在API级别，着色器运行在与标准固定管道完全不同的路径上。在着色器中实现的效果必须为固定管道中可能已经存在的蒙皮、光照和其他功能提供自己的实现。无法有效地向固定管道电路进行“调用”。

### 组合效果

In practice, the very linear nature and limited scope of the graphics pipeline along with the limitations of shader programming models described earlier tend to force applications to treat shaders as a fairly hardcoded, precanned process. This is exactly what shaders were designed to prevent!

Consider the collision of a technique like matrix palette skinning and a typical special effect. It is quite common for special effect shaders to only affect lighting, texture coordinates, or any other vertex component besides position. Yet, to be combined with skinning, the vertex shader implementer must write specialized variants of an effect for skinned and unskinned versions. The combinatoric explosion that this implies for even a moderately complex graphics engine means that it becomes impossible to write a single shader that will work for all situations. In fact, just supporting the full fixed-function pipeline as specified in DirectX® 9 is not possible using a single shader [Sander03]. Thus, for maximum optimality, a different vertex shader would have to be written for every possible fixed pipeline setting combination.

In this gem, we will explore ways to handle the problem of multiple shader variants, along with effective techniques to generate the variants, store them, and generally integrate a flexible shader pipeline into a 3D engine. One specific approach for flexible shader integration is presented here, but this gem will also provide many starting points that could be used for further research into novel approaches to shader integration.

### 处理组合爆炸

First, let's categorize some of the approaches to dealing with this proliferation of shader variants.

Close-ended: This is the most common approach to the problem. Most games will write between 5 and 60+ highly specialized shaders that will handle the most common effects a game will implement. It is a viable approach when the feature set of the graphics pipeline is very clearly defined, but it does limit creativity and makes any engine code rather inflexible to changes in the game design. With this strategy, the shader variants problem is side-stepped by simply not allowing an arbitrary number of effect types to be applied in the game.

Open-ended. Generate shader variants at runtime: The most flexible approach is to actually build the shader variants at runtime. The engine renderer must analyze the current renderer settings, determine the appropriate vertex shader code fragments needed, and assemble this into a single shader. There are several ways to approach this.

- Nvidia的NVLink
- DirectX片段链接器
- HLSL

Methods to generate shader variants can be classified as additive or subtractive. Additive methods work by adding, copying, or linking fragments of code, while subtractive methods will take a large generic shader and refine it to create a specialized variant with only the relevant subset of functionality. Here, we present a brief overview of

