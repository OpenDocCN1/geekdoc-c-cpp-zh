
**早期优化原则：** 如果早期优化能使程序在“可交互”与“需数分钟才能执行”之间产生差别，那么早期优化就是值得的。缩短调试周期并支持交互式测试，值得付出额外努力。

**细节层次原则：** 细节层次对效率*和*正确性都很重要。

**平均高度原则：** 单位球上半球面上一点的平均高度为 \(\frac{1}{4}\)。因此，对任意单位向量 \(\mathbf{n}\)，积分

$$\int_{\{\omega \in S^2: \omega \cdot \mathbf{n}<0\}} \omega \cdot \mathbf{n} \, d\omega = \pi.$$

**结构原则：** 把令人意外的结构对称性和非对称性既视为关于底层结构的线索，也视为提醒你检查任何方案鲁棒性的警告。例如，如果其他方面相似的要素相差几个数量级或需要不同参数——正如自然界基本力的情况——那么就有什么有趣的事情正在发生；若顺藤摸瓜，它可能带来洞见；若忽视，它可能反咬你一口。

**剔除原则：** 通常高效的做法是：用一个或多个快速而保守的解法，通过剔除明显不正确的值来缩小空间；再用一个缓慢但精确的解法，此时只需考虑较少的剩余可能性。

**设计权衡原则：** 架构设计的艺术包括识别实现者利益与用户利益之间的冲突，并做出最佳权衡。

**内存原则：** 内存的首要挑战是应对访问延迟和有限带宽。容量是次要问题。

本页有意留白

# 参考文献

- [ABB64] G. M. Amdahl、G. A. Blaauw 和 Frederick P. Brooks。IBM System/360 的体系结构。载于 *IBM Journal of Research and Development*，第87–101页，1964年4月。
- [ABM88] Brian Apgar、Bret Bersack 和 Abraham Mammen。Stellar 图形超级计算机模型 GS1000 的显示系统。*SIGGRAPH Comput. Graph.*，22(4):255–262，1988。
- [Ado08] Adobe。文档管理——便携式文档格式——第1部分：PDF 1.7，2008。
- [AdSP07] Yeuhi Abe、Marco da Silva 和 Jovan Popović。带摩擦接触的多目标控制。载于 *Proceedings of the 2007 ACM SIGGRAPH/Eurographics Symposium on Computer Animation*，SCA '07，第249–258页，2007。Eurographics Association。
- [AFO05] Okan Arikan、David A. Forsyth 和 James F. O'Brien。推挤人物。载于 *Proceedings of the 2005 ACM SIGGRAPH/Eurographics Symposium on Computer Animation*，SCA '05，第59–66页，New York, NY, USA，2005。ACM。
- [AGCA08] Prekshu Ajmera、Rhushabh Goradia、Sharat Chandran 和 Srinivas Aluru。基于 GPU 的快速并行空间填充曲线与八叉树构建。*Poster at the 2008 Symposium on Interactive 3D Graphics and Games*，I3D '08，第10:1页，New York, NY, USA，2008。ACM。
- [AGW86] Phil Amburn、Eric Grant 和 Turner Whitted。用增强过程模型管理几何复杂性。*SIGGRAPH Comput. Graph.*，20(4):189–195，1986年8月。
- [Air90] John Milligan Airey。通过自动模型空间细分和潜在可见集计算提高建筑漫游系统的更新速率。博士学位论文，The University of North Carolina at Chapel Hill，USA，1990。
- [AK87] James Arvo 和 David Kirk。通过射线分类实现快速光线追踪。*SIGGRAPH Comput. Graph.*，21(4):55–64，1987年8月。
- [Ake93] Kurt Akeley。RealityEngine 图形。载于 *SIGGRAPH '93: Proceedings of the 20th Annual Conference on Computer Graphics and Interactive Techniques*，第109–116页，New York, NY, USA，1993。ACM。
- [Ale02] Marc Alexa。变换的线性组合。ACM Trans. Graph.，21(3):380–387，2002年7月。
- [AMD12] AMD。RenderMonkey 工具套件。http://developer.amd.com/resources/archive/archived-tools/gpu-tools-archive/rendermonkey-toolsuite/，2012。
- [AMHH08] Tomas Akenine-Möller、Eric Haines 和 Naty Hoffman。实时渲染（第3版）。A K Peters, Ltd.，Natick, MA, USA，2008。
- [AMMH07] Tomas Akenine-Möller、Jacob Munkberg 和 Jon Hasselgren。使用时间连续三角形的随机光栅化。载于 GH '07: Proceedings of the 22nd ACM SIGGRAPH/Eurographics Symposium on Graphics Hardware，第7–16页，2007。Eurographics Association。
- [App67] Arthur Appel。定量不可见性概念与实体的机器渲染。Proc. ACM Natl. Mtg.，第387页，1967。
- [App68] Arthur Appel。实体机器渲染的若干着色技术。载于 Proceedings of the April 30-May 2, 1968, Spring Joint Computer Conference，AFIPS '68 (Spring)，第37–45页，New York, NY, USA，1968。ACM。
- [ARS79] Arthur Appel、F. James Rohlf 和 Arthur J. Stein。用于隐藏线消除的晕线效果。载于 Proceedings of the 6th Annual Conference on Computer Graphics and Interactive Techniques，SIGGRAPH '79，第151–157页，New York, NY, USA，1979。ACM。
- [Arv95] James Richard Arvo。模拟光传输的解析方法。博士学位论文，Yale University，New Haven, CT, USA，1995。
- [AS95] David Adalsteinsson 和 James A. Sethian。用于传播界面的快速水平集方法。J. Comput. Phys.，118(2):269–277，1995年5月。
- [AS06] Kurt Akeley 和 Jonathan Su。正确 z 缓冲区遮挡所需的最小三角形间隔。载于 Proceedings of the 21st ACM SIGGRAPH/Eurographics Symposium on Graphics Hardware，第27–30页，New York, NY, USA，2006。ACM。
- [Ash01] Michael Ashikhmin。合成自然纹理。载于 Proceedings of the 2001 Symposium on Interactive 3D Graphics，I3D '01，第217–226页，New York, NY, USA，2001。ACM。
- [ASP07] Paul Asente、Mike Schuster 和 Teri Pettit。动态平面地图插图。载于 ACM Trans. Graph.，26(3)，30:1–30:10，2007年7月。
- [AVF04] C. Andujar、P. Vazquez 和 M. Fairén。Way-Finder：穿越复杂漫游模型的引导式游览。Computer Graphics Forum，23(3):499–508，2004。
- [AW87] J. Amanatides 和 A. Woo。用于光线追踪的快速体素遍历算法。载于 Proc. Eurographics '87，Amsterdam, The Netherlands，第1–10页，1987年8月。
- [AZ97] Johnny Accot 和 Shumin Zhai。超越 Fitts 定律：基于轨迹的 HCI 任务模型。载于 Proceedings of the ACM SIGCHI Conference on Human Factors in Computing Systems，CHI '97，第295–302页，New York, NY, USA，1997。ACM。
- [Bac] Michael Bach。视觉现象与视错觉。http://www.michaelbach.de/ot/。
- [Ban65] Thomas F. Banchoff。紧嵌入二维多面体流形。*American Journal of Mathematics*，87:465–472，1965。
- [Ban74] Thomas F. Banchoff。三重点与浸入曲面的手术。*Proceedings of the American Mathematical Society*，45(3):407–413，1974年12月。
- [Bar92] R. Barzel。*计算机图形学的基于物理建模：结构化方法*。Academic Press，1992。
- [Bau72] Bruce G. Baumgart。翼边多面体表示。技术报告，Stanford University，Stanford, CA, USA，1972。
- [BBD⁺99] C. Betrisey、J. F. Blinn、B. Dresevic、B. Hill、G. Hitchcock、B. Keely、D. P. Mitchell、J. C. Platt 和 T. Whitted。用于图案化显示器的位移滤波。载于 *Society for Information Display 1999 Digest of Technical Papers*，第296–299页，1999。
- [BBO⁺09] Bernd Bickel、Moritz Bächer、Miguel A. Otaduy、Wojciech Matusik、Hanspeter Pfister 和 Markus Gross。非线性异质软组织的捕获与建模。*ACM Trans. Graph.*，28(3):89:1–89:9，2009年7月。
- [BCfPRD61] H. P. Bishop、M. N. Crook、Tufts Inst. for Psychological Research 和 United States Wright Air Development Division。*白色和彩色背景下目标的颜色绝对辨识*。WADD 技术报告。Behavioral Sciences Laboratory、Aerospace Medical Laboratory、Wright Air Development Division、Air Research and Development Command、United States Air Force，1961。
- [BCL⁺07] Louis Bavoil、Steven P. Callahan、Aaron Lefohn、João L. D. Comba 和 Cláudio T. Silva。使用 k-buffer 在 GPU 上实现多片段效果。载于 *Proceedings of the 2007 Symposium on Interactive 3D Graphics and Games, I3D ’07*，第97–104页，New York, NY, USA，2007。ACM。
- [BCWG09] Mirela Ben-Chen、Ofir Weber 和 Craig Gotsman。空间变形迁移。载于 *Proceedings of the 2009 ACM SIGGRAPH/Eurographics Symposium on Computer Animation, SCA ’09*，第67–74页，New York, NY, USA，2009。ACM。
- [BD80] J. K. Bowmaker 和 H. J. Dartnall。人视网膜中视杆和视锥的视觉色素。*The Journal of Physiology*，298:501–511，1980年1月。
- [BD02] David Benson 和 Joel Davis。八叉树纹理。*ACM Trans. Graph.*，21(3):785–790，2002年7月。
- [BEG98] B. Wyvill、E. Galin 和 A. Guy。隐式曲面建模系统中的 Blob Tree、扭曲、混合与布尔运算。载于 *Implicit Surfaces ’98*，1998年6月。
- [BF01] Samuel R. Buss 和 Jay P. Fillmore。球面平均及其在球面样条与插值中的应用。*ACM Trans. Graph.*，20(2):95–126，2001年4月。
- [BHW96] Ronen Barzel、John E. Hughes 和 Daniel N. Wood。用于计算机图形动画的合理运动模拟。载于 *Proceedings of the Eurographics Workshop on Computer Animation and Simulation ’96*，第183–197页，New York, NY, USA，1996。Springer-Verlag New York, Inc.
- [Bir61] Faber Birren。*创造性色彩*。Reinhold Pub. Corp.，1961。
