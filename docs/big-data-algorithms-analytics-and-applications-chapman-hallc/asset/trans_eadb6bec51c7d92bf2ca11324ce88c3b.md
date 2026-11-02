

直观上，一种处理方案可以利用固有的时空属性（如航向、速度和当前位置），以持续报告具有相似运动轨迹的对象组。然后，可以为每个检测到的组定期构建一条指示性的“代表”路径，因为它实际上可以概括其参与对象共享的时空特征。

该方案的主要目标是根据以下约束检测对象组：

-   *相似性*：成对相似的轨迹段之间的距离必须在 ε 以内。
-   *同时性*：在时间范围为 ω 的最近*滑动窗口* [22] 上检查位置。
-   *及时性*：每隔 β 个时间单位（即窗口滑动一次）定期调整分组，以反映对象运动的任何变化。

因此，在区间 ω 内，每个对象的成对同时记录位置不应偏离超过 ε。这种相似性概念仅限于最近的过去（窗口 ω），并不延伸到整个运动历史。此外，它可以很容易地推广到具有成对相似轨迹段的多个对象（图 14.8）。另外，在从这类轨迹分组增量创建“代表”轨迹时，会应用一个*阈值*：只有当相应组当前包含超过 *n* 个对象时，才返回合成轨迹 *T*。请注意，此类组中没有任何原始位置可以偏离其代表路径 *T* 超过给定容差 ε。

![](img/1643181e79c76dc765d55a7355afb4a4_309_0.png)

图 14.8 相似演化的轨迹及其代表路径 T。

根据带时间戳的位置来检查轨迹段的相似性，很快就会成为移动对象数量不断攀升或窗口范围扩大时的瓶颈。为了避免这种情况，在参考文献 41 中，我们选择了一种基于连续速度向量的轨迹近似表示，这些向量最终指向每个相应对象的当前位置（图 14.9）。每个向量由一个符号表征，该符号使用熟悉的罗盘概念来表示运动方向，大致体现了对象在连续位置消息之间的路线。实际上，罗盘分辨率 α 决定了运动平滑的程度；当 α = 4 时，方向符号 {N, S, E, W} 仅提供粗略的指示，但使用 α = 16 个符号（图 14.9）或更多符号可以实现更精细的表示。通常，一旦窗口在下一个执行周期滑动，一个额外的符号（近似最近 β 个时间戳内的运动）将被附加到这个先进先出（FIFO）序列的尾部，而最旧的符号（即头部）则被丢弃。因此，每条轨迹只需要维护少量符号和速度度量的序列，而不需要存储大量原始位置，从而节省了大量内存。

符号序列更适合进行相似性检查，因为它们充当运动签名。在参考文献 41 中，我们通过哈希表识别具有共同签名的对象。具有相同符号序列的对象可能具有几乎“平行”的路线，但实际上可能彼此相距甚远。我们方法的关键在于，具有相同签名且当前彼此距离在 ε 以内的对象，最近很可能遵循了相似的路径。因此，可以通过点聚类技术，根据对象的当前位置来识别具有共同签名的至少 n 个对象的组。我们暂时使用基于密度的带噪声空间聚类应用（DBSCAN）算法 [42] 来检测具有相近当前位置的相似轨迹组。之后，对于每个发现的成员数足够（>n 个对象）的簇，可以很容易地创建一条代表路径 T，只需从最新的

![](img/1643181e79c76dc765d55a7355afb4a4_310_0.png)

图 14.9 使用 16 个符号的罗盘对演化轨迹进行基于方向的编码。

例如，在车队管理、拼车服务、生物多样性保护等方面。这些概念旨在识别在一定时间段内一起移动的移动对象组。最近的聚集概念 [46] 能够对各种额外的群体事件或突发事件进行建模。例如包括庆祝活动、游行、大型商业促销、抗议、交通拥堵和其他公共集会。

关于更具体的分析，参考文献 47 中的方法识别大规模轨迹数据集上基于时间段的最频繁路径。所提出的两步策略首先构建一个包含候选路径频率的图，然后执行图搜索以查找结果。SimpleFleet 平台 [48] 聚合来自车辆轨迹的在线数据，并为大都市地区提供实时交通分析，包括路线搜索服务、统计以及路径、交通状况和等时线的地图可视化。这可能对汽车导航很有用，以便根据实际交通状况推荐路线。vTrack [49] 是一个原型系统，它使用手机从一系列不准确的位置样本中准确估计道路行驶时间。例如，如果 GPS 读数不可用或出错（例如在“城市峡谷”中），可以使用替代但噪声更大的传感器（如 Wi-Fi）来估计用户的轨迹和行驶时间。参考文献 50 中提出的技术基于根据车辆 GPS 位置构建的道路网络的多成本、时间依赖、不确定图模型。因此，对于给定的起点-终点对和开始时间，最优路线可以考虑多种成本和时间相关的不确定性。

流行的基于位置的社交网络（如 Foursquare、Facebook）的迅速普及，也产生了大量与活动信息相关的轨迹。这类活动轨迹 [51] 不仅记录了运动的时空方面，还记录了用户活动的文本描述。这引发了有趣的问题，例如相似性检索：给定一个查询位置序列，每个位置都与一组期望活动相关联，活动轨迹相似性查询返回 k 条覆盖查询活动并产生最短最小匹配距离的轨迹 [51]。可以预计，围绕活动时空描述的更多有趣问题将会出现，包括相似性检索的个性化方面 [52]。

类似地，解读人类生活方式 [53] 不仅对许多科学学科至关重要，而且对地理营销应用具有深远的商业影响。设计算法，将数百万个人的多个社交网络账户数据及其存储在基于位置的社交网络中的公开异构行为数据整合起来，可能会产生有趣的分类方案。这些结果对于个性化推荐和定向广告非常宝贵。

另一个日益常见的趋势是自愿社区创建的地理信息的出现，称为自愿地理信息（VGI）或众包地理空间数据 [54]。OpenStreetMap 项目 [55] 是最成功的 VGI 项目之一，旨在利用志愿者的贡献开发一个协作、免费可用的全球数字地图。众包的另一种形式是社交媒体中的位置共享，例如带注释的 Twitter 帖子 [56] 或 Flickr 中的地理标记照片 [57]。除了隐私问题 [58] 之外，还需要对这些社交媒体数据进行额外处理以检索任何空间信息 [59]。由于非权威性，VGI 项目关于所收集信息的质量和可靠性经常受到质疑。VGI 的预处理和噪声去除似乎是解决这些时空数据不确定性的一个有前途的研究方向。

最后但同样重要的是，下一代平台应向用户提供高级功能，以更好地处理轨迹数据中的特殊性并更好地解释隐藏属性。交互式地图工具应通过根据实际地图比例、不同对象的数量、其轨迹的复杂性等利用表示细节来承载大量数据。在应用开发中，能够将动态位置数据与静态数据集（例如交通网络或行政边界）或其他轨迹关联起来的复杂事件进行细粒度控制的 API 也将很有价值。最后，处理无序或噪声等固有流缺陷将提供动态修订查询结果的能力，从而提高答案的质量。

## 参考文献

-   1. Agrawal, D., P. Bernstein, E. Bertino, S. Davidson, U. Dayal, M. Franklin, J. Gehrke, L. Haas, A. Halevy, J. Han, H.V. Jagadish, A. Labrinidis, S. Madden, Y. Papakonstantinou, J.M. Patel, R. Ramakrishnan, K. Ross, C. Shahabi, D. Suciu, S. Vaithyanathan, and J. Widom. 2012. Challenges and Opportunities with Big Data—A Community White Paper Developed by Leading Researchers across the United States. Available at http://www.cra.org/ccc/files/docs/init/bigdatawhitepaper.pdf (accessed April 30, 2014).
-   2. Stonebraker, M., U. Cetintemel, and S. Zdonik. 2005. The 8 Requirements of Real-Time Stream Processing. ACM SIGMOD Record, 34(4):42–47.
-   3. Mouratidis, K., M. Hadjieleftheriou, and D. Papadias. 2005. Conceptual Partitioning: An Efficient Method for Continuous Nearest Neighbor Monitoring. In Proceedings of the 24th ACM SIGMOD International Conference on Management of Data, pp. 634–645.
-   4. Hu, H., I. Xu, and D.L. Lee. 2005. A Generic Framework for Monitoring Continuous Spatial Queries over Moving Objects. In Proceedings of the 24th ACM SIGMOD International Conference on Management of Data, pp. 479–490.
-   5. Vieira, M., P. Bakalov, and V.J. Tsotras. 2009. On-line Discovery of Flock Patterns in Spatio-Temporal Data. In Proceedings of the 17th ACM SIGSPATIAL International Conference on Advances in Geographic Information Systems (ACM GIS), pp. 286–295.
-   6. Jeung, H., M.L. Yiu, X. Zhou, C.S. Jensen, and H.T. Shen. 2008. Discovery of Convoys in Trajectory Databases. Proceedings of Very Large Data Bases (PVLDB), 1(1):1068–1080.
-   7. Lee, J., J. Han, and K. Whang. 2007. Trajectory Clustering: A Partition-and-Group Framework. In Proceedings of the 26th ACM SIGMOD International Conference on Management of Data, pp. 593–604.
-   8. Bakalov, P., M. Hadjieleftheriou, E. Keogh, and V.I. Tsotras. 2005. Efficient Trajectory Joins Using Symbolic Representations. In MDM, pp. 86–93.
-   9. Chen, Z., H.T. Shen, and X. Zhou. 2011. Discovering Popular Routes from Trajectories. In Proceedings of the 27th International Conference on Data Engineering (ICDE), pp. 900–911.
-   10. Sacharidis, D., K. Patroumpas, M. Terrovitis, V. Kantere, M. Potamias, K. Mouratidis, and T. Sellis. 2008. Online Discovery of Hot Motion Paths. In Proceedings of the 11th International Conference on Extending Database Technology (EDBT), pp. 392–403.
-   11. Manyika, J., M. Chui, B. Brown, J. Bughin, R. Dobbs, C. Roxburgh, and A.H. Byers. 2011. Big Data: The Next Frontier for Innovation, Competition, and Productivity. McKinsey Global Institute, New York. Available at http://www.mckinsey.com/insights/business_technology/big_data_the_next_frontier_for_innovation (accessed April 30, 2014).

