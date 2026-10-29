
# Index

+   Maps rollout, 462–463, 496–499
+   Marble map, 484
+   Mask map, 490
+   Mass property, 1051
+   Master Block Parameters dialog box, 859–860
+   Master Point controller, 861–862
+   Master Track Key Info dialog box, 861–862
+   Material Editor
+     additional properties, 439–440
+     applying materials to scene objects, 7
+     colors, 437–438
+     enabling SuperSampling, 621
+     Material Explorer, 449–452
+     Material/Map Browser, 448–449
+     opacity, 438
+     reflection, 439
+     refraction, 439
+     shininess, 439
+     Slate Material Editor, 440–447
+     specular highlights, 439
+     transparency, 438
+   Material IDs, Surface Properties rollout, 335–336
+   material modifiers
+     Disp Approx, 517–518
+     Displace Mesh, 517–518
+     MaterialByElement, 516–517
+     overview, 516
+   Material XML Exporter Utility, 96
+   MaterialByElement modifier, 516–517
+   Material/Map Browser, 448–449
+   materials. See also standard materials
+     adding to animation, 6–9
+     animating with Expression controller, 872
+     Architectural material, 765–766
+     defined, 439–440
+     DirectX Shader material, 766–767
+     Ink ’n Paint material, 763–765
+     keyframe animation, 586
+     lighting, 1091–1092
+     matte/shadow materials, 761–763
+     mental ray materials, 769–772
+     MetaSL Shader material, 766–767
+     shaders, 767–769
+   Materials panel, Lighting Analysis Assistant dialog box, 1093

+   Materials/Maps option, Schematic View Preferences dialog box, 669
+   matte/shadow materials, 761–762
+   Max 2.5 Star SuperSampling method, 462
+   Max File Finder utility, 100
+   Max QuadTree Depth settings, Ray Traced Shadows parameters rollout, 552
+   MAXScript
+     arrays, 1179
+     collections, 1179
+     comments, 1175–1176
+     conditions, 1178–1179
+     data types, 1173–1174
+     Debugger, 1169–1171
+     defined, 1159–1160
+     Editor windows, 1166
+     expressions, 1176–1178
+     functions, 1181–1182
+     laying out rollout, 1190–1194
+     Listener window, 1162–1164
+     loops, 1170–1171
+     Macro Recorder, 1166–1168
+     Macro scripts, 1172
+     menu, 1160
+     program flow, 1175–1176
+     scripted mouse tools, 1173
+     scripted plug-ins, 1178
+     scripted right-click menus, 1173
+     scripted utilities, 1173
+     setting preferences, 1171–1172
+     Utility rollout, 1160–1161
+   MAXScript
+     variables, 1173–1174
+     Visual MAXScript Editor interface, 1188–1190
+   Maya software, 93
+   Measure Distance tool, 272
+   Measure utility, 273
+   Melt modifier, 845
+   mental ray
+     caustics, 1133–1135
+     enabling, 1127–1129
+     indirect illumination, 1136–1139
+     lights and shadows, 1129–1132
+     materials, 769–772
+     photons, 1133–1135
+     shaders, 768

## 3.2.1 单源最短路径

给定一个带权有向图 G=(V,E)，其中每条边的权是一个实数。另外，还给定 V 中的一个顶点，称为源。我们要计算从源到所有其他各顶点的最短路径长度。这里路径的长度是指路径上各边权之和。这个问题通常称为单源最短路径问题。

Dijkstra 算法是解决单源最短路径问题的一个贪心算法。它通过逐步扩展已知最短路径的顶点集合来求解。

算法描述：

+   1. 初始化：设源点为 s，dist[s]=0，其余顶点 dist[v]=∞。
+   2. 选择：从未处理的顶点中选择 dist 值最小的顶点 u。
+   3. 更新：对于 u 的所有邻接边 (u,v)，若 dist[u]+w(u,v) < dist[v]，则更新 dist[v]。
+   4. 标记：将 u 标记为已处理。
+   5. 重复步骤 2-4，直到所有顶点都被处理。

下面给出一个示例图：

![](img/ebbb4844f027f7d1c580e48108d2b6cb_1295_0.png)

算法复杂度为 O(V²)，若使用优先队列可优化至 O((V+E)logV)。

```
```python
def dijkstra(graph, source):
    dist = {v: float('inf') for v in graph}
    dist[source] = 0
    visited = set()
    while len(visited) < len(graph):
        u = min((v for v in graph if v not in visited), key=lambda x: dist[x])
        visited.add(u)
        for v, w in graph[u].items():
            if dist[u] + w < dist[v]:
                dist[v] = dist[u] + w
    return dist
```
```

Orientation constraint, 602
Orientation Constraint rollout, 602
Origin control, System Unit Scale dialog box, 123
Orthographic view, 40
OSM (Object Space Modifiers), 846
outer envelope, 978
Outline button
editing subobjects, 336
Polygons rollout, 372
Outline tool, Modify Selection panel, 406
out-of-range curves, 903-905
Output Path, Resource Collector utility, 101
Output rollout, 474-475, 819-820
Overlapping Faces feature, 57
Overlapping UVW Faces feature, 58
Overlapping Vertices feature, 58

P
Paint Behavior rollout, 780
Paint Connect (PConnect) tool, 408
Paint Controls rollout, 763
Paint Deform tools
Exaggerate tool, 424
Flatten brush, 424
Noise tool, 424
Pinch/Spread tool, 424
Push/Pull tool, 424
Relax/Soften tool, 424
Revert tool, 424
Shift tool, 423
Smudge tool, 424
Paint icon, Viewport Canvas, 776
Paint Objects panel, 427
Paint Selection Region tool, 174
Paintbox palette, Vertex Paint modifier, 784
Painter Options dialog box, 680
painting, See also Object Paint tools; Paint Deform tools;
Viewport Canvas
deformations, 675-676
with light, 1087-1088
weights, 982
PaintSS panel, 402
Pan mode, SteeringWheel gizmo, 44
Panel Buttons display mode, Ribbon, 24
Panel Titles display mode, Ribbon, 24
panning view, 49
Panorama Exporter Utility, 96, 630
panoramic images, 630-631
Param Curve Out-of-Range Types dialog box, 904
Parameter Collector dialog box, 875-876
parameter controllers
Barycentric Morph controller, 859
Block controller, 859-861
Boolean controller, 856
Cubic Morph controller, 859
IK controller, 861
Limit controller, 856
list controller, 856-857
Master Point controller, 861-862
On/Off controller, 857
Waveform controller, 857-859
Parameter Editor dialog box, 878
parameter keys, Track Bar, 575
Parameter pane, Particle View window, 1014
Parameter Wiring dialog box, 872-873
Parameters tabbed panel, Lens Effects Globals rollout, 1110
Parametric Deformer modifiers
Affect Region modifier, 288
Bend modifier, 288-289
Displace modifier, 289-291
Lattice modifier, 291
Mirror modifier, 291-292
Noise modifier, 292-293
Preserve modifier, 294
Push modifier, 293
Relax modifier, 294
Ripple modifier, 294
Shell modifier, 294-295
Skew modifier, 296-297
Slice modifier, 295-296
Spherify modifier, 298
Squeeze modifier, 299-300
Stretch modifier, 297-298
Substitute modifier, 302
Taper modifier, 300-301
Twist modifier, 300
Wave modifier, 303
XForm modifier, 302
Parametric Deformers menu, 284
parametric objects, 160, 261-263
Parent Coordinate System, 205
parenting objects, 252-253

# Index

+   - PArray particle system — Overview, 994, 1009–1010
+   - splitting objects, 1010
+   - Particle Age map, 485, 1012
+   - Particle Flow system
+     - actions, 1015
+     - debugging test actions, 1018
+     - events, 706
+     - helpers, 1016
+     - overview, 993
+     - Particle View window, 1013–1014
+     - Standard Flow, 1014–1015
+     - wiring events, 1016–1017
+   - Particle Generation rollout, Super Spray particle system, 998–999
+   - Particle MBlur map, 485, 1012
+   - Particle Spawn rollout, Super Spray particle system, 1007–1008
+   - particle systems. *See also* Super Spray particle system
+     - Blizzard, 1008–1009
+     - combining with Space Warps, 1041–1043
+     - creating, 994–995
+     - maps, 1011–1013
+     - overview, 993–994
+     - PArray, 1009–1011
+     - Particle Flow, 1014–1020
+     - PCloud, 1011
+     - Snow, 996–997
+     - Spray, 995–996
+   - Particle systems model type, 263
+   - Particle View window, 1013–1014
+     - pasting
+       - joints, 932
+       - modifiers, 278
+       - time, 896
+   - Patch Select modifier, 394
+   - PatchDeform modifier, 845–846
+   - patches
+     - Edit Patch modifier, 382
+     - editing edges, 388–390
+     - editing handles, 388
+     - editing subobjects, 390–393
+     - editing vertices, 385–388
+     - Geometry rollout, 384–385
+     - patch grids, 379–381
+     - selecting subobjects, 381–382
+     - using modifiers on objects, 394–398

+   - Patches model type, 262
+   - Patch/Plain Editing menu, 284
+   - Path Commands rollout, Fit Deformation Dialog Box, 723
+   - Path constraint, 584, 597–598
+   - Path Follow behavior, 969
+   - Path Follow Space Warp, 1029–1030
+   - Path menu, Asset Tracking interface, 653
+   - Path Parameters rollout, 597, 715–716
+   - Path value, 715–716
+   - PathDeform modifier, 846
+   - paths
+     - configuring, 120–122
+     - Loft compound objects, 724
+   - PBomb Space Warp, 1028–1029
+   - PCloud Particle system, 994, 1011
+   - PConnect (Paint Connect) tool, 408
+   - pelt mapping
+     - defined, 789
+     - overview, 808–809
+     - positioning projection gizmo, 809–810
+     - selecting seams, 809
+     - stretching, 811–812
+   - Pelt Options rollout, 812
+   - Performance menu, Preview window, 1060
+   - Perlin Marble map, 485
+   - perpendicular snap point, 222
+   - persistent dialog boxes, 33–34
+   - Perspective, 522
+   - Perspective view, 40, 65–66
+   - Phong shader, 456–458
+   - Photographic Exposure Control, 1097–1098
+   - photometric light parameters
+     - color options, 553–554
+     - distribution options, 552–553
+     - intensity and attenuation options, 554
+     - light shapes, 554–555
+   - photometric lights, 542–543
+   - Photometric Web distribution type, 553
+   - photons, mental ray, 1133–1135
+   - Physique modifier, 292, 948, 975
+   - Pick button, 421
+   - Pick Button element, Visual MAXScript, 1189
+   - Pick Coordinate System, 205
+   - Pick Targets rollout, 696–697
+   - Pick Texture drop-down list, Edit UVWs interface, 795
+   - Pinch button, Soft Selection feature, 268
+   - Pinch edit mode, 402
