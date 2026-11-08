
由于步骤结果需要能在不同对象（如全局属性）中访问，因此使用了单例模式（Gamma 1994）。可以通过调用静态 `getInstance()` 方法来访问该实例，该方法能够访问受保护的构造函数。此外，在使用多线程的情况下，该方法必须同步，以保证数据一致性。

## 3.3 `InfectionParameters` 类

该类管理的属性描述疾病、人口统计和行为参数。初始化值是一组参数，可用于模拟具有高传染性和高死亡率的禽流感。此外，可以设置隔离和药物治疗参数，以模拟不同情景。

```java
package Pandemie;

import java.util.Random;

public class InfectionParameters {
    private static InfectionParameters instance;

    protected int latentPeriodDays = 3;
    protected int infectiousPeriodDays = 10;
    protected int recoveredRemovedAfterDays = 15;
    protected int incubationPeriodDays = 3;
    protected int symptomaticPeriodDays = 4;

    protected double birthrate = 0.002d;
    protected double deathrate = 0.001d;

    protected double virus_morbidity_percent = 0.63d;

    protected double spontaneous_infection_rate = 0.000001d;

    protected double vectored_infection_rate = 0.35d;
    protected double contact_infection_rate = 0.45d;

    protected double movement_probability = 0.4d;

    protected double immigrate = 0.0000001;

    protected boolean useQuarantine = false;

    protected boolean handleMedication = false;
    protected double medicationOne = 3.5d;
    protected double medicationTwo = 5.5d;

    protected int susceptible_again_after_recover = 100;
    protected int birthimmunitydays = 20;

    protected long maxCellCapacity = 500;

    protected static Random randomGenerator;

    public static synchronized InfectionParameters getInstance() {
        if (instance == null) {
            randomGenerator = new Random();
            instance = new InfectionParameters();
        }
        return instance;
    }

    protected InfectionParameters() {
    }
}
```

由于许多对象都需要访问这些参数，因此也使用单例模式实现。

### 3.3.1 DiseaseCell 类

DiseaseCell 类表示 CA 模型中的一个细胞，个体在其中出现并按照既定规则相互作用。状态转移函数 δ 继承自超类。该函数负责计算传播过程以及应如何处理感染者。因此，该函数计算由疾病导致的死亡，随后添加新生儿并移除自然死亡病例。然后，估计迁入者和迁出者，计算媒介感染、接触感染和自发感染，最后一步执行个体移动。

```java
package Pandemie;

public class DiseaseCell extends Cell {
    private ArrayList<CellIndividual> individuals;
```

第 4 行引入了一种动态数据结构，用于存储该细胞中的个体。

```java
public DiseaseCell(int numberOfIndividuals) {
    individuals = new ArrayList<CellIndividual>();

    for (int i = 0; i <= numberOfIndividuals - 1; i++) {
        individuals.add(new CellIndividual());
    }
}
```

当实例化一个细胞对象时，构造函数会创建用于保存个体的动态数据结构。此外，个体在循环中生成，并使用该数据结构存储。

```java
public boolean performCellAction(CellularAutomaton ca) {
    this.handleNaturalDeath();
    this.handleNewborns();

    this.handleImmigrants();
    this.handleSpontaneousInfections();

    this.handleContactInfections(ca);
    this.handleVectoredInfections();

    this.updateCellIndividuals();

    this.handleMovement(ca);
    return true;
}
```

```java
            next();
        if (individual.getState() == StateType.DIED) continue;
        if (individual.getState() == StateType.KILLEDBYDISEASE)
            continue;

        if (this.isTheCase(szParam.getDeathrate())) {
            if (individual.getAgeType() == AgeType.KID)
            if (individual.getAgeType() == AgeType.TEEN)
            if (individual.getAgeType() == AgeType.ADULT) {
                if (this.isTheCase(0.7d)) {
                    individual.setStateType(StateType.DIED);
                } else {
                    individual.setStateType(StateType.DIED);
                }
            }
        }
    }
}
```

handleNewborns() 和 handleNaturalDeath() 这两个方法实现了由已定义的出生和死亡参数引起的种群自然增长和缩减。当个体出生时，会施加暂时免疫，保护该个体免于因疾病传播而患病。此外，在该模型中，只有成人可以生育孩子，这与自然行为一致。在计算自然死亡病例时，使用了随机函数，该函数为不同年龄组（儿童、青少年、成人、老年人）赋予不同的死亡概率。

```java
public void handleImmigrants() {
    InfectionParameters szParam = InfectionParameters.getInstance();
    StepResult res = StepResult.getInstance();

    if (this.isTheCase(szParam.getImmigrantrate())) {
        CellIndividual immigrant = new CellIndividual();
        if (immigrant.getAgeType() == AgeType.KID)
            immigrant.setAgeType(AgeType.ADULT);

        individuals.add(immigrant);
        res.setImmigrant(res.getImmigrant() + 1);
    }
}
```

根据迁入率参数，计算新迁入者出现的概率。如果该函数返回允许新迁入者进入模拟，则将该迁入者作为新成员添加到细胞中。此外，存在一项限制：只允许成人和老年人进入。如果不属于该年龄类型的个体试图进入，则会调整其年龄组以满足要求。

```java
protected void handleNeighborCellInfections(
    CellularAutomaton ca, InfectionParameters szParam,
    StepResult res, double probability) {
    DiseaseCell regSZNeighbourCell;

    for (Iterator individualIterator = individuals.iterator();
         individualIterator.hasNext();) {
        CellIndividual individual = (CellIndividual) individualIterator.next();

        if (szParam.isUseQuarantine() &&
            (individual.getQuarantineType() == QuarantineType.QUARANTINE))
            continue;

        for (Iterator it = neighbourCellIndexList.iterator();
             it.hasNext();) {
            Long element = (Long) it.next();
            try {
                regSZNeighbourCell = (DiseaseCell) ca.getCell(element);
            } catch (Exception e) {
                continue;
            }

            for (Iterator adjacentIndividual = regSZNeighbourCell.
                getIndividuals().iterator();
                adjacentIndividual.hasNext();) {
                CellIndividual adjacent = (CellIndividual)
                    adjacentIndividual.next();

                if (szParam.isUseQuarantine() &&
                    (individual.getQuarantineType() == QuarantineType.
                        QUARANTINE))
                    continue;

                if (individual.getStateType() == StateType.INFECTIVE) {
                    switch (adjacent.getStateType()) {
                    case SUSCEPTIBLE:
                        boolean infection = this.isTheCase(probability);
                        if (adjacent.getSusceptibleInDays() > 0) infection =
                            false;
                        if (individual.getDiseaseCycle() == DiseaseCycle.
                            LATENT)
                            infection = false;

                        if (infection) {
                            adjacent.setStateType(StateType.INFECTIVE);
                            adjacent.setDiseaseCycle(DiseaseCycle.LATENT);

                            adjacent.setInfectedSinceDays(1);
                            res.setContact(res.getContact() + 1);
                        }
                        break;
                    }
                }
            }
        }
    }
}

protected void handleSameCellInfections(
    StepResult res, double probability, boolean contactInfection) {
    ...
}
```

