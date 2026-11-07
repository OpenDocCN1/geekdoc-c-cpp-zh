
## 1.16.2 通用人工智能（AGI）

通用人工智能（AGI）^155^是指能够“执行人类所能完成的任何任务”的人工智能。^156,157^ 专家们对于通用人工智能何时或是否可能成为现实存在分歧——从最快本十年内，到未来100年内的某个时候，再到永远不会。^158,159^

## 1.16.3 人工智能里程碑

若干人工智能里程碑事件吸引了人们的注意力和想象力，使普通公众开始认为AI是真实的，并让企业开始考虑将其商业化：

- 在1997年IBM的“深蓝”计算机系统与国际象棋特级大师加里·卡斯帕罗夫的一场比赛中，“深蓝”成为第一台在锦标赛条件下击败卫冕世界国际象棋冠军的计算机。^160^ IBM为“深蓝”加载了数十万盘特级大师对局。“深蓝”能够使用暴力计算每秒评估多达2亿步棋！^161^ 这是大数据在发挥作用。IBM获得了卡内基梅隆大学的弗雷德金奖；该奖在1980年设立，向第一台击败世界国际象棋冠军的计算机的创造者提供10万美元。^162^

- 2011年，IBM的“沃森”在一场奖金为100万美元的比赛中击败了两位最优秀的人类《危险边缘！》选手。“沃森”同时使用数百种语言分析技术，在2亿页内容（包括整个维基百科）中定位正确答案，这需要4太字节的磁盘存储空间。^163,164^ “沃森”使用AI机器学习与强化学习（第1.16.6节）技术进行了训练。^165^

- 围棋——一种几千年前在中国创造的棋盘游戏^166^——被广泛认为是有史以来发明的最复杂的游戏之一，其可能的棋盘配置有10^170^种。^167^ 为了理解这个数字有多大，据信已知宇宙中（只有）10^78^到10^82^个原子！^168^ 2015年，由谷歌DeepMind团队创造的**AlphaGo**使用深度学习（第1.16.5节）这一AI技术，借助两个神经网络击败了欧洲围棋冠军樊麾。围棋被认为比国际象棋复杂得多。

- 更近些时候，谷歌将其AlphaGo AI泛化，创造出**AlphaZero**——一种能自学玩其他游戏的游戏AI。2017年12月，AlphaZero学习了规则，并使用强化学习这一AI技术，在不到四小时内自学学会下国际象棋。随后，它在一场100局比赛中击败了世界冠军国际象棋程序Stockfish 8——每一局都获胜或弈和。在仅用八小时进行围棋自我训练后，AlphaZero能够在100局比赛中击败其前身AlphaGo 60局。^169^

## 1.16.4 机器学习

**机器学习**是“人工智能的一个子领域，它使计算机能够在没有明确编程的情况下学习”。^170^ 机器学习通常使用预定义算法来构建从训练数据中学习的模型。然后，这些模型可用于做出预测。^171^ 例如，给定包含合法电子邮件和垃圾（也称为垃圾邮件）电子邮件的带标签训练数据，机器学习模型可以从训练数据中学习，然后用于将其从未“见过”的电子邮件分类为垃圾邮件或非垃圾邮件。Microsoft Outlook和Google Gmail等电子邮件应用使用此类技术将垃圾邮件移出收件箱。

## 1.16.5 深度学习

**深度学习**是机器学习的一个子集，涉及构建人工神经网络，这些网络使用“受大脑结构和功能启发的算法”。^172^ “深度”一词来自人工神经网络中软件“层”的数量——层数越多，网络越深。网络在穿过各网络层时会从训练数据中学到更多。^173^ 大数据、强大的处理器能力、更快的互联网速度以及并行计算硬件和软件的进步，使得更多组织和个人能够采用资源密集型深度学习解决方案；这些方案在计算机视觉、语音识别、语音合成和更新的生成式AI应用（第1.16.7节）中正产生令人印象深刻的结果。^174^

## 1.16.6 强化学习

**强化学习**^175^是机器学习的一个子集，其中的算法从环境中学习，类似于人类学习的方式——例如，电子游戏爱好者学习一款新游戏，或婴儿学习走路或认出父母。该算法实现一个智能体，它通过尝试执行任务、接收关于成功或失败的反馈、做出调整然后再次尝试来学习。目标是最大化奖励。智能体因做正确的事而获得正奖励，因做错误的事而获得负奖励（即惩罚）。智能体利用这些信息来确定下一步要执行的动作，并且必须努力最大化奖励。

## 1.16.7 生成式AI——ChatGPT与DALL-E 2

生成式AI衍生出的算法能够基于用户作为输入提供的提示来生成新内容——包括文本、图像、音频和视频。^176,177^

### ChatGPT

OpenAI的ChatGPT是一种基于AI的聊天机器人，你可以使用自然语言与之交谈。^178^ 例如，你可以用类似下面的文本提示它：

- “告诉我C++的历史”
- “谁创造了Metaverse（元宇宙）这个词？”或者
- “总结这篇文章，网址是”后接文章链接。

然后，ChatGPT会以看起来和感觉上仿佛由人类生成的答案来回应。ChatGPT基于一个名为GPT（生成式预训练Transformer）的**大语言模型**，^179^该模型使用多种人工智能技术在海量文本上进行了训练。^180^ 在撰写本书时，GPT-4刚刚发布。

- 155. “通用人工智能。”维基百科。维基媒体基金会。访问于2023年3月18日。https://en.wikipedia.org/wiki/Artificial_general_intelligence.
- 156. Kerem Gülen。“我们距离具备人类能力的AI还有多近？”2022年10月6日。访问于2023年3月18日。https://dataconomy.com/2022/10/artificial-general-intelligence-definition/.
- 157. “技术奇点。”维基百科。维基媒体基金会。访问于2023年3月18日。https://en.wikipedia.org/wiki/Technological_singularity.
- 158. Gary Marcus。“通用人工智能并不像你想象的那么迫在眉睫。”2022年7月1日。访问于2023年3月25日。https://www.scientificamerican.com/article/artificial-general-intelligence-is-not-as-imminent-as-you-might-think1/.
- 159. Max Roser。“AI时间线：人工智能专家对未来有何预期？”2023年2月7日。访问于2023年3月25日。https://ourworldindata.org/ai-timelines.
- 160. “深蓝对阵加里·卡斯帕罗夫。”维基百科。维基媒体基金会。访问于2023年3月18日。https://en.wikipedia.org/wiki/Deep_Blue_versus_Garry_Kasparov.
- 161. “深蓝（国际象棋计算机）。”维基百科。维基媒体基金会。访问于2023年3月18日。https://en.wikipedia.org/wiki/Deep_Blue_(chess_computer).
- 162. “IBM深蓝团队获得10万美元奖金。”访问于2023年3月18日。https://articles.latimes.com/1997/jul/30/news/mn-17696.
- 163. Jo Best。“IBM Watson：这台赢得《危险边缘！》的超级计算机如何诞生的内幕，以及它接下来想做什么。”访问于2023年3月18日。https://www.techrepublic.com/article/ibm-watson-the-inside-story-of-how-the-jeopardy-winning-supercomputer-was-born-and-what-it-wants-to-do-next/.
- 164. “沃森（计算机）。”维基百科。维基媒体基金会。访问于2023年3月18日。https://en.wikipedia.org/wiki/Watson_(computer).
- 165. Ferrucci, D., Brown, E., Chu-Carroll, J., Fan, J., Gondek, D., Kalyanpur, A. A., Lally, A., Murdock, J. W., Nyberg, E., Prager, J., Schlaefer, N., & Welty, C. (2010)。“构建沃森：DeepQA项目概述。”《AI Magazine》，31(3)，59-79。https://doi.org/10.1609/aimag.v31i3.2303.
- 166. “围棋简史。”访问于2023年3月18日。http://www.usgo.org/brief-history-go.
- 167. Nsikan Akpan，“谷歌人工智能在世界最复杂的棋盘游戏中击败冠军。”访问于2023年3月18日。https://www.pbs.org/newshour/science/google-artificial-intelligence-beats-champion-at-worlds-most-complicated-board-game.
- 168. John Carl Villanueva，“宇宙中有多少个原子？”访问于2023年3月18日。https://www.universetoday.com/36302/atoms-in-the-universe/.
- 169. Samuel Gibbs，“AlphaZero AI在四小时内自学后击败冠军国际象棋程序。”访问于2023年3月18日。https://www.theguardian.com/technology/2017/dec/07/alphazero-google-deepmind-ai-beats-champion-program-teaching-itself-to-play-four-hours.
- 170. Sara Brown，“机器学习详解。”2021年4月21日。访问于2023年3月18日。https://mitsloan.mit.edu/ideas-made-to-matter/machine-learning-explained.
- 171. “机器学习。”维基百科。维基媒体基金会。访问于2023年3月18日。https://en.wikipedia.org/wiki/Machine_learning.
- 172. Jason Brownlee，“什么是深度学习？”2019年8月16日。访问于2023年3月18日。https://machinelearningmastery.com/what-is-deep-learning/.
- 173. “深度学习。”维基百科。维基媒体基金会。访问于2023年3月18日。https://en.wikipedia.org/wiki/Deep_learning.
- 174. Sharon Goldman，“10年后，深度学习‘革命’仍在继续，AI先驱Hinton、LeCun和Li说。”2022年9月14日。访问于2023年3月27日。https://venturebeat.com/ai/10-years-on-ai-pioneers-hinton-lecun-li-say-deep-learning-revolution-will-continue/.
- 175. M. Tim Jones，“通过强化学习训练软件智能体理性行为。”2017年10月11日。访问于2023年3月27日。https://developer.ibm.com/articles/cc-reinforcement-learning-train-a-software-agent/.
- 176. “什么是生成式AI？”2023年1月19日。访问于2023年3月18日。https://www.mckinsey.com/featured-insights/mckinsey-explains/what-is-generative-ai.
- 177. “生成式人工智能。”维基百科。维基媒体基金会。访问于2023年3月18日。https://en.wikipedia.org/wiki/Generative_artificial_intelligence.
- 178. “ChatGPT简介。”访问于2023年3月18日。https://openai.com/blog/chatgpt.
- 179. “大语言模型。”维基百科。维基媒体基金会。访问于2023年3月18日。https://en.wikipedia.org/wiki/Large_language_model.
- 180. “ChatGPT。”维基百科。维基媒体基金会。访问于2023年3月18日。https://en.wikipedia.org/wiki/ChatGPT.
