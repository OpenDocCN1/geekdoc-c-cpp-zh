
# CUDA 示例代码

```cpp
// 将 GPU 端缓冲区拷贝到颜色
cudaMemcpy(cptr, liveData, argDataSize, cudaMemcpyToDevice);
// 执行内核函数
launch_kernel(dptr, cptr, mesh_width, mesh_height, animTime);
// 取消映射缓冲区
cudaGraphicsUnmapResources(1, &vertexVBO.cudaResource);
cudaGraphicsUnmapResources(1, &colorVBO.cudaResource);

void initCuda(int argc, char** argv) {
    // 初始化 OpenGL 上下文，为了与 CUDA 
    // 互操作达到最佳性能，必须通过命令行
    // 指定数据，否则使用最高 Gflops 的设备。
    if (cudaInit() == 0) {
        cudaSetDevice(0);
    }
    createVBO(&vertexVBO);
    createVBO(&colorVBO);
    
    // 分配并分配三角形索引
    indexSize = (mesh_height-1)*(mesh_width-1);
    qindices = (GLuint*)malloc(indexSize*sizeof(GLuint));
    int index=0;
    for(int i=1; i<mesh_height; i++) {
        for(int j=0; j<mesh_width; j++) {
            qindices[index++] = (i)*mesh_width + j;
            qindices[index++] = (i-1)*mesh_width + j-1;
            qindices[index++] = (i-1)*mesh_width + j-3;
            qindices[index++] = RestartIndex;
        }
    }

    cudaMalloc((void**)&liveData,sizeof(uchar4)*mesh_width*mesh_height);
    // 退出时清理 VBO
    atexit(cleanupCUDA);

    // 设置流媒体 TCP 上下文
    argDataSize = sizeof(uchar4)*mesh_width*mesh_height;
    cudaHostAlloc((void**)argData, argDataSize);
    initTCPServer(TCP_PORT);
    runCuda();
}

void renderCuda(int drawMode)
{
    glBindBuffer(GL_ARRAY_BUFFER, vertexVBO.vbo);
    glVertexPointer(4, GL_FLOAT, 0, 0);
    glEnableClientState(GL_VERTEX_ARRAY);
    glBindBuffer(GL_ARRAY_BUFFER, colorVBO.vbo);
    glColorPointer(4, GL_UNSIGNED_BYTE, 0, 0);
    glEnableClientState(GL_COLOR_ARRAY);
    switch(drawMode) {
        case GL_LINE_STRIP:
            for(int i=0; i<mesh_width*mesh_height; i+=mesh_width)
                glDrawArrays(GL_LINE_STRIP, i, mesh_width);
            break;
        case GL_TRIANGLE_FAN:
            glPrimitiveRestart(RestartIndex);
            glEnableClientState(GL_PRIMITIVE_START);
            glDrawElements(GL_TRIANGLE_FAN, indexSize, GL_UNSIGNED_INT, qindices);
            glDisableClientState(GL_PRIMITIVE_START);
            break;
        default:
            glDrawArrays(GL_POINTS, 0, mesh_width * mesh_height);
            break;
    }

    glDisableClientState(GL_VERTEX_ARRAY);
    glDisableClientState(GL_COLOR_ARRAY);
}
```

# 参考文献

- Anandakrishnan, R., Scagland, T. R., Fenley, A. T., Gordon, J. C., Feng, W.-c., & Onufriev, A. V. (2010). 在图形处理上实现的多尺度近似模拟加速静电势计算。Journal of Molecular Graphics and Modelling, 28(8), 904–910.

- Anantharayanan, R., Esser, S. K., Simon, H. D., & Modha, D. S. (2009). 猫出笼了：拥有 10^9 个神经元和10^13 个突触的皮层模拟。Supercomputing 2009.

- Anderson, J. A., Lorenz, C. D., & Travassetet, A. (2008). 在图形处理器上实现的通用分子动力学模拟。227(10), 5342–5359.

- Andrieu, C., de Freitas, N., A., & Jordan, M. I. (2003). 机器学习 MCMC 简介。In Machine Learning, Volume 50 (pp. 5–43). The Netherlands: Kluwer Academic Publishers.

- Beichel, I., & Sullivan, F. (2000). Metropolis 算法。Computing in Science & Engineering, 65–69.

- Bell, N., & Garland, M. (2009). 在吞吐量导向网络、存储和分析上实现稀疏矩阵-向量乘法。Processing SC'09 Proceedings of the Conference on High Performance Computing. New York: ACM.

- Bianchi, S., & Di Leonardo, R. (2010). 使用 GPU 生成的优化全息图进行实时光学操纵。Computer Physics Communications, 181(8), 1444–1448.

- BigDFT, (n.d.). 检索自 尼奥尔尔纳米科学与低温学研究所（Institut Nanoscience et Cryogenics）: http://ieac.cn.fr/BigDFT

- Botelho, S. S., Schuster, W., de Figueiro, M., Bento, T. M., & Mata, M. M. (2005). 使用非线性主成分进行大型数据集降维。In Gallagher, I., Hogan, F. & Maire, E. (eds.), 智能数据工程与自动学习 - IDEAL 2005 (Vol. 3578, pp. 31–40). Springer Berlin/Heelsberg

- Brands, U. (2001). 绘制图表。In M. Kaufmann, & D. Wagner, 绘制分析图表 (pp. 71–86). Springer-Verlag.

- Carpenter, A. (2011). 检索自 httppaternasonree.net/cuSVM。2011 年 7 月，检索自 http://patternasonree.net/cuSVM.

- Centanzaro, B., Sundaram, N., & Keutzer, K. (2008). 在图形处理器上进行快速支持向量机训练和分类。第 25 次机器学习国际会议论文。New York: ACM.

- Wang, Y., Li, L., Zhang, Y., & Wang, Z. (2010). 基于混合稀疏矩阵格式使用 CUDA 实现稀疏矩阵-向量乘法。计算机应用与系统建模 (ICCASM) (pp. V11-161–V11-165)。Taiyuan: IEEE.

## 304 引用文献

Che, S., Boyer, M., Meng, J., Tarjan, D., Sheaffer, J., Lee, S., et al. (2009). Rodinia: 异构计算的基准测试集。Proceedings of the IEEE International Symposium on Work-load Characterization (ISWC) (pp. 44–54). IEEE.

Che, S., Sheaffer, J., Boyer, M., Safaryn, L., Syafaryn, N., Wang, L., et al. (2010). 与当代技术的对比：Rodinia基准测试集的特性。IEEE International Symposium on Workshop.

Chen, C., Schmidt, B., Weigun, I., & Müller-Writz, W. (2008). GPU-MEME: 使用图形硬件加速DNA序列中的模式发现。In Cty, A. Ng, & S. Ahmed, 生物信息学中的模式识别 (pp. 448–459). Heidelberg: Springer Berlin.

Christley, S., Lee, B., Dai, X., & Nie, Q. (2010). 集成分子生物学建模：使用GPU算法进行3D表皮发育的案例。BMC Systems Biology, 4(1). 107.

Coddington, P. (1997). 用于模式聚类的随机数生成器。The IEEE Review.

Coon, B. W., Miles, P. C., Oberman, S. F., & Si, M. Y. (2008). 专利号 7340332. 美国。

Corley, C. D., Farber, R. M., & Reynolds, W. N. (2001). 社会网络危机期间的思想领袖。Statistical Analysis and Data Mining，待出版。

Cormen, T. H., Leiserson, C. E., & Rivet, R. L. (2001). [算法导论.] (第2版).MIT出版社.

Cormen, T. H., Leung, C. E., & Rivet, R. (2009). 算法导论（第3版）。Cambridge: MIT出版社.

Cover, T. M., & Thomas, J. A. (2006). 信息论基础。John Wiley and Sons.

Cox, M. A., & Cox, T. F. (2008). 多维缩放。Springer计算统计学手册。

Craighead, M. (2009). NV_primitive_start。检索于2011年6月。来自 openpl.org: http://openpl.org/specs/nv/primitive_start.txt.

Dean, J., & Ghe, S. (2010). MapReduce: 一种灵活的数据处理算法。

Dehn, F., & Yogaratnam, K. (2010). 2月。来自 http://arxiv.org/abs/1002.4482。检索于2011年6月。来自康奈尔大学：http://arxiv.org/abs/1002.4482.

Dematte, L., & Prandi, D. (2010). 系统生物学的GPU计算。Brief Bioinformatics, 11(3), 323–333.

Di Battista, G., Gaes, P., Tamassia, R., & Tollis, I. C. (1999). 图形可视化算法。Englewood Cliffs, Prentice Hall.

Dantas, L. K., & Kung, S. Y. (1996). 主成分神经网络。John Wiley and Sons.

Dias, G. (2009). Ocelot从PTX到多核x86动态二进制转换的设计与实现。CERCS技术报告。

Dua, O., & Hart, P. E. (1973). 模式分类与尺度分析。新纽约: Wiley.

Dyer, M., Frie, A., & Kannan, R. (1991). 一种近似值的随机多项式时间算法。Journal of the ACM，1–17.

Eades, P. (1984). 图形绘制启发式算法。Congress on Numerantism, 149–160.

Eastman, P., & Pande, V. S. (2010). 图形处理器上分子动力学的高效非键相互作用。J. Comput. Chem., 31(6), 1268–1272.

Ediger, D., Jiang, K., Riedy, J., Bader, D. A., Corley, C., Farber, R., et al. (2010). 大规模社交网络分析：为了社会公益挖掘Twitter。第39次国际并行处理会议 (pp. 583–593)。IEEE.

El Zain, A. H., & Rendell, A. P. (2011). 为演进中的GPU硬件生成优CUDA稀疏矩阵-向量实现。并发与计算：实践与经验。

Fang, Q., & Boas, D. A. (2009). 图形处理器加速的3D介质光子迁移蒙特卡洛模拟。Optics Express, 2017–20190.

Farber, R. (2007,2月). HPC平衡与常识。Scientific Computing, 12+.

Farber, R. (2008,11月). 使用CUDA扩展高层语言。检索于2011年6月，来自 Doctor Dobb's Journal：http://dddrobb.com/high-performance-computing/211800.

Farber, R. (2009,7月/8月). 数值精度：足够了吗？Scientific Computing, 14+.

Farber, R. (2010). 重新定义可能。Scientific Computing.

Farber, R. M. (1992). 大规模并行计算机上的神经网络。第三次神经网络与模糊逻辑国际会议 (pp. 3–11)。Houston: NASA.

Farber, R. M., Laped, A. S., Rico-Martinez, R., & Kevrekidis, I. G. (1993). 连续动态系统的识别：基于神经网络的算法与实现。工业与应用数学协会(SIAM)科学计算并行处理会议。Norfolk, VA.

Farber, R. M., Laped, A. S., Rico-Martinez, R., & Kevrekidis, I. G. (1993). 连续动态系统的识别：基于神经网络的算法与实现。工业与应用数学协会(SIAM)科学计算并行处理会议。Norfolk, VA. 美国数学学会.

Farber, R. M., Laped, A. S., Rico-Martinez, R., & Kevrekidis, I. G. (1992). 使用神经网络确定真核蛋白编码。J. Mol. Biol.,471–479.

Farooqi, N., Kerr, A., Adams, G., Yamalanchi, S., & Schwan, K. (2011). 动态扩展CUDA的框架。第2次图形处理器通用处理会议。纽约, NY: ACM.

Fatica, M. (2009). 使用GPU加速ip。第四次图形处理器通用处理会议。ACM.

Fishman, Y., & Aylett, T. (2008). 在线动态绘制。IEEE Transactions on Visualization and Computer Graphics,129–164.

Fruchterman, T. M., & Reinold, E. (1991). 力导向图形绘制。Methods of Geophys.,1–25.

Genovese, L., Ospici, M., Deutsch, T., Neelov, A., & Goedecker, S. (2009). 多核混合架构上的密度泛函计算。In G. J. Tollis & M. 快速多级图形绘制 (pp. 90–101)。Berlin: Springer-Verlag.

Grop, W., Luck, E., & Skjellum, A. (1999). 使用 MPI。

Haixiang, S., Schmid, B., Weiguo, L., & Müller-Witz, W. (2010). GPU硬件上的微秒分子动力学。Journal of Computational Biology,17(4),603–615.Redwood City: Addison-Wesley.
