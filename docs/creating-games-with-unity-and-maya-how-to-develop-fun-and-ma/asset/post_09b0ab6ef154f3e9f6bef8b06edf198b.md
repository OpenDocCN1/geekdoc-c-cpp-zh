
- **Step 86:** Insert edge loops around knuckles to allow for proper bending and additional shape definition (Figure 8.68).

- **Step 87:** Tweak new edges/vertices on the inside of fingers to help define fleshy parts of the finger (Figure 8.69).

![](img/0285f88bc840f313779e011725b623a5_242_0.png)

![](img/0285f88bc840f313779e011725b623a5_242_1.png)

**FIGURE 8.68** Added rings (via Insert Edge Loop tool) around knuckles.

**FIGURE 8.69** Tweaking new rings for fleshy finger bits.

### Why?

Deciding when to start manipulating vertices and edges and when to keep adding geometry is born of experience. In this case, it is easy to rough out some good finger flesh with very small collections of data (really four edges), so it makes sense to rough it out here instead of after further details are added.

- **Step 88:** Extrude the knuckle base. Turn Keep Faces Together back on (Polygons > Edit Mesh > Keep Faces Together). Be sure to select two faces for each knuckle (Figure 8.70). Don't select all the faces for all the knuckles.

![](img/0285f88bc840f313779e011725b623a5_242_2.png)

**FIGURE 8.70** Building the basis of the knuckles.

- Step 91: Add new geometry and sculpt as needed. Figure 8.73 shows one more ring of edges inserted to allow for some extra flesh on the outer end of the palm. At this point, there should be plenty of geometry to create a well-shaped hand. Sculpt to taste.

![](img/0285f88bc840f313779e011725b623a5_244_0.png)

FIGURE 8.73 Added geometry to better distribute polys and allow for proper form.

## Gloves

The general hand shape is complete but you might notice that they are a little bulkier than they should be. This is because (as per the style sheet) they are actually inside of gloves. We need to make sure the arm indicates this.

- Step 92: Create an extrusion midway up the forearm to create the top end of the gloves. Select an entire ring of faces and use the Extrude tool to do this (Figure 8.74).

- Step 93: Eliminate the bottom ledge of the ring by merging vertices (Figure 8.75). Select the vertices around the bottom edge of the newly extruded faces, and choose Polygons > Edit Mesh > Merge (Options). Turn the Threshold setting up to probably 1 (this may need to be changed depending on the size of the model—the results should look like Figure 8.76).

- Step 94: Create glove detail. Figure 8.77 shows details atop the top of the glove. It was created by inserting edge loops to allow for new collections of polygons to be extruded. These new polygons (with very little sculpting) are further defined by adjusting the edge normals (Polygons > Normals > Harden Edge).

![](img/0285f88bc840f313779e011725b623a5_245_0.png)

**FIGURE 8.74** Creating the top part of the glove via extrusions.

**FIGURE 8.75** Using the Merge tool to eliminate an unwanted ledge.

![](img/0285f88bc840f313779e011725b623a5_245_1.png)

**FIGURE 8.76** Results of the Merge tool.

![](img/0285f88bc840f313779e011725b623a5_245_2.png)

## 西安市灞桥区推进营商环境补短板求突破

### 持续擦亮“灞桥速办”营商环境品牌

“过去需要往返多个部门才能办好的事情，如今在政务大厅一个窗口就能直接办好，实在太方便了！”近日，在灞桥区市民中心，刚刚办结业务的西安市民张先生，对高效便捷的服务赞不绝口。

今年以来，西安市灞桥区紧扣全省“三个年”活动安排部署，坚持问题导向、目标导向、结果导向，聚焦“优服务、提效率、促发展”，不断提升政务服务标准化、规范化、便利化水平，持续擦亮“灞桥速办”营商环境品牌。

在具体实践中，灞桥区以“小切口”改革推动营商环境“大提升”，重点在“政务服务加速度”和“为民为企增温度”上下功夫，有效激发了市场主体活力和社会创造力。

下一步，灞桥区将继续坚持以人民为中心的发展思想，持续深化“放管服”改革，以更优的营商环境为区域经济社会高质量发展保驾护航。

![](img/0285f88bc840f313779e011725b623a5_249_0.png)

FIGURE 8.83 Added geometry to allow for added bending and to better define the form.

- Step 101: Model the harness from existing polygons. Do this with previously discussed methods of extruding new faces and appropriately hardening the edges (Figure 8.84).

![](img/0285f88bc840f313779e011725b623a5_249_1.png)

FIGURE 8.84 Harness modeling.

- Step 102: Refine the knees. No new techniques here, but notice in Figure 8.85 that there are 12 rings to define this knee area. Some are for allowing the bend to deform properly with joints, but some are to help define the bunching of the pants over the top of the boots.

- Step 103: Extrude down a rough boot shape (Figure 8.86).

- Step 104: Close the bottom of the boot with the Append to Polygon tool.

- Step 105: Add detail via extrusions and inserted edge loops (Figure 8.87).

- Step 106: Add a sole to the boot. Further extrusions. Notice that a few extra loops are also added here to allow for the boot to deform right around the ball of the foot (Figure 8.88).

- Step 107: Add pants (pocket detail). Use the same techniques as already covered, but remember to make careful use of hard and soft normals (Figure 8.89).

- Step 108: Tweak and sculpt as desired. The model as constructed thus far is shown in Figure 8.90.

![](img/0285f88bc840f313779e011725b623a5_250_0.png)

**FIGURE 8.85** Knee area (and coincidentally the top of the foot area).

![](img/0285f88bc840f313779e011725b623a5_250_1.png)

**FIGURE 8.86** Roughing out the boot with some careful extrusions.

![](img/0285f88bc840f313779e011725b623a5_250_2.png)

**FIGURE 8.87** Added detail to boot.

## AI Hardware Evolution

The rapid advancement of artificial intelligence has driven unprecedented growth in specialized hardware. From early GPUs to modern TPUs and neural processing units, the landscape continues to evolve.

### Key Developments in 2026

- **Chiplet Architecture**: Modular designs enable heterogeneous integration.
- **Photonic Computing**: Optical interconnects reduce latency and power.
- **Quantum-AI Hybrids**: Experimental systems combine quantum processors with AI accelerators.

> The next leap in AI requires rethinking the entire computing stack, not just adding more cores.

![](img/0285f88bc840f313779e011725b623a5_251_0.png)

```python
def run_inference(model, input_data):
    return model.predict(input_data)
```

| Hardware | TOPS/W | Year |
|----------|--------|------|
| NVIDIA A100 | 0.5 | 2020 |
| Google TPU v5 | 1.2 | 2023 |
| Cerebras WSE-3 | 2.0 | 2025 |

- **Step 110:** Clean up the mirror plane. Select all the vertices that should be right on the mirror plane and snap them in the middle (you may want to double-check that Retain Component Spacing is still turned off in the Move tool settings).

- **Step 111:** Select the mesh in object mode, and choose Polygons > Mesh > Mirror Geometry Options. Click the –X radio button and check the Merge With Original check box. Press Mirror.

**Why?**

If you have the left side of Aegis (his left), the mirrored version would be in the –X direction (and thus the –X radio button). By clicking the Merge With Original check box, the mirrored version of Aegis will also merge up the middle, making it truly one mesh with shared vertices along the middle of the form.

- **Step 112:** If needed, soften the edges along the middle of the new single mesh model.

**Asymmetrical Details**

Now is the chance to make that big leap from tutorial following to asset building. Figures 8.91, 8.92, and 8.93 show a completed Aegis Chung. Everything on him was modeled using techniques covered in this chapter with the guns using a few techniques from the level modeling chapter. All it takes is time and a bit of sweat equity to get him complete.

![](img/0285f88bc840f313779e011725b623a5_252_0.png)

FIGURE 8.91 *Aegis Chung*

## UV Mapping

UV mapping characters can be a daunting task. When UV mapping the level, we were generally working with fairly simple shapes that lent themselves easily to planar maps and cylindrical maps. The human form really is much more complex than that at first blush.

Fortunately, there have been some important tools that have emerged in the last few years that can assist in efficiently and quickly created UV maps. Maya actually has some of my favorite UV editing tools; however applications like Modo have emerged with some really powerful UV tools that are much more efficient than Maya's. To make matters even more complicated, there are free tools like RoadKill (http://www.pullin-shapes.co.uk/page8.htm) that integrate fairly seamlessly with Maya that allow for some extraordinarily fast UV mapping using all the latest pelt/LCSM mapping technologies. If you do a lot of UV mapping, or plan to, learning one of these two tools may be in your best interest.

With all that said, Maya's UV mapping tools have done some catching up in recent versions, and many of the tools and techniques available in Modo and Roadkill are available in Maya as well. There are enough available that we will stick to Maya's tool set for this chapter's tutorials. Many of the techniques used for UV mapping the human form are similar to those used for mapping the level, so building upon the toolset you are already familiar with will move us along quickest.

### Tutorial 9.1: Character UV Mapping

In this tutorial we will be doing several things. First, Maya's UV tools are powerful, but sometimes require some very specifically created polygonal structure. Before we even start building UV maps, we will take a moment to make sure that the geometry built in the last chapter does indeed fit into these Maya-imposed requirements. The requirements actually are good to keep our eye out for (they are mostly concerned with the problems that arise from non-four-sided polygons) since identifying and fixing them at this state will ultimately save time within Unity.

#### Mesh Inspection and Cleanup

- **Step 1:** Open Maya and set the project to Incursion-Maya.
- **Step 2:** Open AegisChung.mb.
- **Step 3:** Turn on Backface Culling. In the persp view panel, choose Shading > Backface Culling (Figure 9.1).

> **Why?**
>
> Figure 9.1 shows the results of the last chapter with backface culling activated. It appears that the entire body has the normals facing the wrong way. If you are using the version of Aegis Chung that is included
