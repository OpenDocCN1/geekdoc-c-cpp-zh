

## Display 9.4 将单条记录扩展为多条记录

```
data D6;
    input name $ sex $ t1 t2 t3 t4 t5 time6 time_7;

ARRAY num_array{*} _NUMERIC_;
DO inum = 1 to dim(num_array);
    time = inum;
    ADL = num_array{inum};
    output;
END;
keep name sex time ADL;

datalines;
Smith M 6 6 5 5 5 4 3
Jones F 7 5 4 4 3 2 1
Fisher M 5 5 5 3 2 2 1
;
run;
```

数组语句收集了所有数值变量。dim 函数返回该数组的长度（本例中为 =7）。time 变量在循环中定义，ADL 变量根据每个数组元素定义。此迭代赋值的結果输出到数据集中。（该数据集巧妙地命名为 D6，因为这是本章中定义的第六个数据集。也许重新阅读第 1 章关于命名数据集的内容会有所帮助。）keep 语句仅保留了数据集中四个变量。试试看：如果不使用 keep 语句运行此代码会发生什么。

关于数组的最后一点说明是，数组可以定义为多于一个维度，尽管在求助于更高维度的数据数组之前，你可能更喜欢在 PROC IML 中使用矩阵。

## 9.2 案例研究 1：空间随机性检验的蒙特卡洛 p 值

p 值，即在原假设为真时，观察到检验统计量至少与检验统计量的观测值一样极端的概率，通常在统计推断中报告。当检验统计量的抽样分布具有熟悉的形式时，可以使用标准统计分布（例如 t 或 F）来计算 p 值。在其他情况下，如果检验统计量不具有熟悉的形式，则计算 p 值可能非常困难。在下面的示例中，数组用于基于平均最近邻检验统计量的蒙特卡洛 p 值计算。

感兴趣的数量的空间分布可能是聚集的或规则间隔的。聚集的观测值往往比完全空间随机（CSR）观测值之间的距离更小。规则间隔的观测值往往比 CSR 观测值之间的距离更大。虽然在此上下文中应考虑更复杂的检验统计量（Ripley 1981, Waller and Gotway 2004），但选择了一个非常简单的统计量——平均最近邻距离。定义观测值 i 的最近邻距离如下：

d(i)=min(d_i1, d_i2, ..., d_i(i-1), d_i(i+1), ..., d_in) 其中 d_ij=观测值 i 与观测值 j 之间的欧几里得距离（i≠j）。

假设数据集中有 n 个观测值。平均最近邻距离为 Σd(i)/n。

让我们看看当有 n=4 棵树的正方形地块时发生了什么，这些树位于坐标点（.25, .65）、（.25, .75）、（.35, .65）和（.35, .75）。（在不泄露答案的情况下，你可以看到这些坐标点在单位正方形中是聚集的。答案已经被泄露了！确定分析是否证实了眼球内伤检验。）

本分析的策略如下：

- 1. 确定观测数据的最近邻距离。
- 2. 计算观测数据的平均最近邻距离。
- 3. 假设原假设 CSR 观测值为真，生成在感兴趣区域随机分布的观测样本。
- 4. 计算此模拟数据的平均最近邻距离。
- 5. 重复步骤 3 和 4 多次。
- 6. 蒙特卡洛 p 值是生成的样本比观测数据更极端的比例。为了检验聚集，确定模拟数据的平均最近邻距离是否小于观测数据的平均最近邻距离。

这六个步骤可以被视为计算用于检测聚集的蒙特卡洛 p 值的程序的伪代码。前一章的建议是充实伪代码。在 Display 9.5 中，这六个步骤在实现此分析的程序中用注释标识。

## Display 9.5 计算用于检测聚集的蒙特卡洛 p 值

```
/* enter the observed data into data arrays  */
data plot_obs;
    array xobs(4) xobs1-xobs4;
    array yobs(4) yobs1-yobs4;
    do idat = 1 to 4;
        input xobs(idat) yobs(idat) @@;
    end;
datalines;
.25 .65 .25 .75 .35 .65 .35 .75
;
run;

/* STEP 1: Determine nearest-neighbor distances for observed data  */
data plot1;  set plot_obs;
    array xobs(4) xobs1-xobs4;
    array yobs(4) yobs1-yobs4;
    array nnobs(4) nnobs1-nnobs4;

/* Determine nearest-neighbor distance for each point  */
sumnnobs = 0;
do i=1 to 4;      * find nearest-neighbor distance for each point;
    nnobs(i) = 100;  * initialize distances to be large;

/* calculate the Euclidean distance between the ith tree and
   all others - save the smallest value as the distance to its
   nearest neighbor and compare the ith point to all others.
*/
    do j=1 to 4;
        d=sqrt( (xobs(i)-xobs(j))**2 + (yobs(i)-yobs(j))**2 );
        if (d<nnobs(i)) and (d>0) then nnobs(i)=d;
    end;
/* Note: Each point is also compared to itself - thus, d=0
       omitted from updated of nearest neighbor distance. */
    sumnnobs=sumnnobs+nnobs(i);
end;

/* STEP 2: Calculate average nearest-neighbor distance for observed data  */
avgnnobs = sumnnobs/4;
run;

/* Simulate plots under CSR  */
data mccsr1; set plot1;
    array xobs xobs1-xobs4; * observed data;
    array yobs yobs1-yobs4;
    array xsim xsim1-xsim4; * CSR simulated data;
    array ysim ysim1-ysim4;
```

## Display 9.5 （续）

```
array nnobs nnobs1-nnobs4; * observed NN distances;
array nncsr nncsr1-nncsr4; * simulated NN distances;

/* STEP 3: Generate many CSR plots with four trees */

* initialize counters of nn avg dist le or ge than observed;
numle = 0;
* numge = 0; * commented out since focus on clustering here;

nsim = 4000;      * user-specified option;
seed1 = 12345;    * if =0, then uses time since midnight;
call streaminit(seed1);

do isim = 1 to nsim;

/* STEP 5: Repeat steps 3 and 4 many times */
do ii = 1 to 4;
    xsim(ii) = RAND('uniform');
    ysim(ii) = RAND('uniform');
end;

/* STEP 4: Calculate average nearest-neighbor distance for simulated data */

sumnncsr = 0;
do i=1 to 4;
    nncsr(i) = 100;  * initialize;

    do j=1 to 4;
        d=sqrt( (xsim(i)-xsim(j))**2 + (ysim(i)-ysim(j))**2 );
        if (d<nncsr(i)) and (d>0) then nncsr(i)=d;
    end;

    sumnncsr=sumnncsr+nncsr(i);
end;
avgnncsr = sumnncsr/4;

/* Accumulate counts of patterns consistent with clustering */
ile = (avgnncsr <= avgnnobs);
numle = numle + ile;

* ige = (avgnncsr >= avgnnobs);
* numge = numge + ige;

drop i j ii xobs1-xobs4 yobs1-yobs4 nnobs1-nnobs4
      sumnnobs sumnncsr;
output;
end;      * of the isim - simulation loop;
```

## Display 9.5 （续）

```
/* STEP 6: Calculate the Monte Carlo p-value */
MC_P_value_Cluster = numle/nsim;

* write results to log file with PUT statements;
put "MC P-value (Clustering) = " MC_P_value_Cluster;
put " (based on " nsim " simulated plots)";
run;
```

执行此代码会将结果写入日志文件。以下是结果：

MC P-value (Clustering) = 0.006
(based on 4000 simulated plots)

聚集检验的 p 值估计为 0.006，来自假设原假设为 CSR 观测值的蒙特卡洛模拟。

## 9.3 在观测之间记住变量值

通常在记录内操作变量是相当直接的。棘手的是跨记录操作变量。SAS 在开始处理新观测时将数据集中每个变量初始化为缺失值。然而，你可能希望 SAS 在开始处理新观测时记住变量的值。RETAIN 语句实现了这一目标。当你看到它在实际操作中时，更容易理解 RETAIN 语句。

### 9.3.1 为单个观测处理多个观测

下面的示例基于需要跟踪个人随时间变化的情况。这些个人正在参与一个在社区中接受服务的项目。个人可以随时从项目中退出（例如，当他或她被送入医院或疗养院时）。个人也可以随时重新加入项目。对于示例，创建了一个小数据文件。数据文件有三个人，其中个人 1（id=1）只有一次入组和退出时间。个人二（id=2）有两次入组和退出时间。个人 3（id=3）有三次入组和退出时间。（此小数据文件所基于的原始数据集要复杂得多。但小数据文件抓住了分析的精髓。）假设你有以下目标：

