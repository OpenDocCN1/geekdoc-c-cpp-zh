
```python
    self.char = self.attrib_dict["char"]
    self.str = self.attrib_dict["str"]
    self.dex = self.attrib_dict["dex"]
    self.will = self.attrib_dict["will"]

    #---军衔属性
    self.rank = ""
    self.rankName = ""
    self.modifier = self.intel * .1 #军衔修正值

    #---军事职业（MOS）属性
    self.mos = ""
    self.mosSpecialty = ""
    self.mosSelection = {0:"补给", 1:"组长", 2:"步兵"}

#---确定军衔---
def setRank(self):
    """确定海军陆战队的军衔。"""

    if (self.intel + self.char) > 23: #高级军衔
        self.roll = multiDie(1,2) + self.modifierValue()
        self.rank = self.seniorRank(self.roll)
    else: #初级军衔
        self.roll = multiDie(1,2)
        self.rank = self.lowerRank(self.roll)

    #---将数值军衔转换为全称---
    if self.rank == "E1":
        self.rankName = "列兵"
    elif self.rank == "E2":
        self.rankName = "一等兵"
    elif self.rank == "E3":
        self.rank名 = "二等兵"
    elif self.rank == "E4":
        self.rankName = "下士"
    elif self.rank == "E5":
        self.rankName = "中士"
    elif self.rank == "E6":
        self.rankName = "上士"
    elif self.rank == "E7":
        self.rankName = "军士长"
    elif self.rank == "E8":
        self.rankName = "一级军士长"
    elif self.rank == "O1":
        self.rankName = "少尉"
    elif self.rank == "O2":
        self.rankName = "中尉"
    elif self.rank == "O3":
        self.rankName = "上尉"
    elif self.rank == "O4":
        self.rankName = "少校"
    else:
        print("无效军衔。")

def modifierValue(self):
    """确定军衔修正值。"""
    if self.modifier % 1 < .5:  #向下舍入
        self.modifier = int(self.modifier)
    elif self.modifier % 1 >= .5:    #向上舍入
        self.modifier = int(self.modifier) + 1
    return self.modifier

def lowerRank(self, roll):
    """确定初级海军陆战队员的军衔。"""
    if self.roll == 1:
        self.rank = "E1"
    elif self.roll == 2:
        self.rank = "E2"
    elif self.roll == 3 or self.roll == 4:
        self.rank = "E3"
    elif self.roll == 5 or self.roll == 6:
        self.rank = "E4"
    elif 7 <= self.roll <= 9:
        self.rank = "E5"
    elif self.roll == 10:
        self.rank = "E6"
    else: #不应该到达这里
        print("军衔投掷无效")
    return self.rank

def seniorRank(self, roll):
    """确定军衔，并判断角色是否为
    高级士官或军官。"""
    if self.roll > 5: #角色是军官
        self.new_roll = multiDie(1, 2) + self.modifierValue()
        if 1 <= self.new_roll <= 3:
            self.rank = "O1"
        elif 4 <= self.new_roll <= 7:
            self.rank = "O2"
        elif 8 <= self.new_roll <= 10:
            self.rank = "O3"
        elif self.new_roll > 10:
            self.rank = "O4"
        else: #不应该到达这里
            print("军衔投掷无效")
    else: #角色是高级士官
        self.new_roll = multiDie(1, 2)
        if 1 <= self.new_roll <= 4:
            self.rank = "E6"
        elif 5 <= self.new_roll <= 8:
            self.rank = "E7"
        elif 9 <= self.new_roll <= 11:
            self.rank = "E8"
        elif self.new_roll > 11:
            self.rank = "E9"
        else: #不应该到达这里
            print("军衔投掷无效")
    return self.rank

#-----获取军事职业（MOS-----）

def requirements(self):
    """将符合条件的军事职业（MOS）添加
    到选择字典中。

    根据各种角色属性，
    判断是否有额外的军事职业（MOS）选择。"""

    if self.intel >= 11:
        self.mosSelection[3] = "医疗"
    ###值 "4" 因位置变化而缺失
    if self.str >= 12:
        self.mosSelection[5] = "重武器"
    if (self.dex + self.intel + self.will) >= 40:
        if multiDie(1, 3) >= 85:
            self.mosSelection[6] = "侦察/狙击手"
    if (self.str + self.dex + self.intel + self.will) >= 50:
        if multiDie(1, 3) >= 85:
            self.mosSelection[7] = "侦察兵"
    if self.str >= 10 and self.intel >= 10:
        self.mosSelection[8] = "战斗工兵"
    if self.dex >= 11:  #装甲车辆军事职业（MOS）
        self.mosSelection[9] = "坦克驾驶员"
        self.mosSelection[10] = "坦克炮手"
        self.mosSelection[11] = "装甲车驾驶员"
        self.mosSelection[12] = "装甲车炮手"
    if self.intel + self.will >= 27:   #情报军事职业（MOS）
        self.mosSelection[15] = "情报分析员"
        self.mosSelection[16] = "审讯官"
        self.mosSelection[17] = "情报：异形"
    if self.intel >= 10 and self.dex >= 10 and ("O1" <= self.rank <= "O4"):
        self.mosSelection[18] = "飞行员"
        self.mosSelection[19] = "副驾驶/炮手"
    ###坦克和装甲车指挥官的军事职业（MOS）具有
    # 与飞行员相同的要求
    # 但在“装甲车辆”军事职业（MOS）之后添加。
    self.mosSelection[13] = "坦克指挥官"
    self.mosSelection[14] = "装甲车指挥官"

def eligibleMOS(self):
    """显示角色可选择的军事职业（MOS）。
    """

    print("您有资格选择以下军事职业（MOS）：")
    for key in self.mosSelection.keys():
        print(key, self.mosSelection[key])
    self.mosChoice = int(input("\n请选择您想要选择的军事职业（MOS）的编号： "))
    self.mos = self.mosSelection[self.mosChoice] #重命名选择
    print("您选择了", self.mos, "专业。")
    ###移除子类以便将来使用
    #if self.mosChoice == 2 or self.mosChoice == 4 or self.mosChoice == 9 or self.mosChoice == 10:
    #   self.mosSpecialty = self.subClass(self.mosChoice)
    #if self.mosSpecialty == "":
    #   self.mos = self.mosSelection[self.mosChoice]
    #else:
    #   self.mos = self.mosSelection[self.mosChoice] + " (" + self.mosSpecialty + ")"
    return self.mos

def mosSkills(self, mosChoice):
    """根据军事职业（MOS）确定默认技能等级。"""
    if self.mosChoice == 0: #补给
        self.chosenSkills["补给"] = 20
    elif self.mosChoice == 1:   #组长
        self.chosenSkills["机械"] = 20
    elif self.mosChoice == 2:   #步兵
        self.chosenSkills["轻武器"] = 20
        self.chosenSkills["持械格斗"] = 10
        self.chosenSkills["徒手格斗"] = 10
        self.chosenSkills["游泳"] = 10
    elif self.mosChoice == 3:   #医疗
        self.chosenSkills["急救"] = 20
    elif self.mosChoice == 4:   #非有效值
        pass
    elif self.mosChoice == 5:   #重武器
        self.chosenSkills["重武器"] = 20
        self.chosenSkills["轻武器"] = 10
        self.chosenSkills["持械格斗"] = 10
        self.chosenSkills["徒手格斗"] = 10
    elif self.mosChoice == 6:   #侦察/狙击手
        self.chosenSkills["侦察"] = 15
        self.chosenSkills["前观察员"] = 10
        self.chosenSkills["轻武器"] = 25
        self.chosenSkills["持械格斗"] = 10
        self.chosenSkills["徒手格斗"] = 10
        self.chosenSkills["游泳"] = 10
        self.chosenSkills["导航"] = 10
    elif self.mosChoice == 7:  #侦察兵
        self.chosenSkills["侦察"] = 20
        self.chosenSkills["前观察员"] = 10
        self.chosenSkills["轻武器"] = 20
        self.chosenSkills["持械格斗"] = 10
        self.chosenSkills["徒手格斗"] = 10
        self.chosenSkills["游泳"] = 10
        self.chosenSkills["登山"] = 10
        self.chosenSkills["跳伞"] = 10
        self.chosenSkills["导航"] = 10
    elif self.mosChoice == 8:   #战斗工兵
        self.chosenSkills["战斗工兵"] = 20
    elif self.mosChoice == 9:   #坦克驾驶员
        self.chosenSkills["履带车辆"] = 20
    elif self.mosChoice == 11:  #装甲车驾驶员
        self.chosenSkills["轮式车辆"] = 20
    elif self.mosChoice == 10 or self.mosChoice == 12:  #车辆炮手
        self.chosenSkills["车辆武器"] = 20
        self.chosenSkills["间射火力"] = 10
    elif self.mosChoice == 13 or self.mosChoice == 14: #车辆指挥官
        self.chosenSkills["导航"] = 15
        self.chosenSkills["履带车辆"] = 10
        self.chosenSkills["轮式车辆"] = 10
        self.chosenSkills["车辆武器"] = 10
        self.chosenSkills["间射火力"] = 10
        self.chosenSkills["前观察员"] = 10
    elif self.mosChoice == 15: #分析员
        self.chosenSkills["电子学"] = 20
        self.chosenSkills["计算机"] = 20
    elif self.mosChoice == 16: #审讯
        self.chosenSkills["电子学"] = 10
        self.chosenSkills["计算机"] = 10
        self.chosenSkills["审讯"] = 20
    elif self.mosChoice == 17: #异形
        self.chosenSkills["电子学"] = 10
        self.chosenSkills["计算机"] = 10
        self.chosenSkills["异形"] = 20
        self.chosenSkills["生物学"] = 10
        self.chosenSkills["化学"] = 10
    elif self.mosChoice == 18: #飞行员
        self.chosenSkills["飞行器"] = 20
        self.chosenSkills["车辆武器"] = 10
    elif self.mosChoice == 19: #副驾驶/炮手
        self.chosenSkills["飞行器"] = 10
        self.chosenSkills["车辆武器"] = 20
    else:
        print("无效选项") # 不应该到达这里

#---基础先攻值---
```
