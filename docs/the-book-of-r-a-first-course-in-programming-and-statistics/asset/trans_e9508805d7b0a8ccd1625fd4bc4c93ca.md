

写作手的掌宽 (Wr.Hnd)。帮助页面 ?survey 显示数据也已收集了非写作手的掌宽 (Nw.Hnd)。可以合理预期这两个变量高度相关，这正是之前我避免使用 Nw.Hnd 的原因。事实上，执行

```
R cor(survey$Wr.Hnd,survey$Nw.Hnd,use="complete.obs")
[1] 0.948310
```

揭示了一个很高的相关系数，表明学生在写作手和非写作手掌宽之间存在很强的线性关联。换句话说，这两个变量在任何给定模型中应代表几乎相同的信息。

现在，你已从之前拟合的模型中得知，写作手掌宽对预测学生平均身高具有显著且正向的影响。以下代码通过简单的线性回归快速确认了这一点。

```
R> summary(lm(Height ~Wr.Hnd,data=survey))
```

```
Call:
lm(formula = Height ~ Wr.Hnd, data = survey)
```

```
Residuals:
Min 1Q Median 3Q Max
-19.7276 -5.0706 -0.8269 4.9473 25.8704
```

```
Coefficients:
Estimate Std. Error t value Pr(>|t|)
(Intercept) 113.9536 5.4416 20.94 <2e-16 ***
Wr.Hnd 3.1166 0.2888 10.79 <2e-16 ***
```

```
Sig. codes: 0 *** 0.001 '** 0.01 '*' 0.05 '.' 0.1 ' ' 1
```

Residual standard error: 7.909 on 206 degrees of freedom
(29 observations deleted due to missing)
Multiple R-squared: 0.3612, Adjusted R-squared: 0.3581
F-statistic: 116.5 on 1 and 206, p-value: < 2.2e-16

Wr.Hnd 与 Nw.Hnd 之间很高的正相关性表明，使用 Nw.Hnd 代替应具有类似的效果。

```
R> summary(lm(Height~Nw.Hnd,data=survey))
```

```
Call:
lm(formula = Height ~ Nw.Hnd, data = survey)
```

```
Residuals:
Min 1Q Median 3Q Max
-21.8285 -5.1397 -0.2867 4.5611 25.5750
```

Coefficients:

|  | Estimate | Std. Error | t value | Pr(>|t|) |
| (Intercept) | 118.0324 | 5.2912 | 22.31 | <2e-16 *** |
| Nw.Hnd | 2.9107 | 0.2818 | 10.33 | <2e-16 *** |

Signif. codes: 0 *** 0.001 ** 0.01 * 0.05 . 0.1 ' 1

Residual standard error: 8.032 on 206 degrees of freedom
(29 observations deleted due to missing)
Multiple R-squared: 0.3412, Adjusted R-squared: 0.338
F-statistic: 106.7 on 1 and 206 DF, p-value: <2.2e-16

你可以看到这些结果确实如此。
然而，看看如果尝试同时基于这两个预测变量建模身高会发生什么：

```
R> summary(lm(Height~Wr.Hnd+Nw.Hnd,data=survey))
```

Call:
lm(formula = Height ~ Wr.Hnd + Nw.Hnd, data = survey)

Residuals:

|  | Min | 1Q | Median | 3Q | Max |
| -20.0144 | -5.0533 | -0.8558 | 4.7486 | 25.8380 |

Coefficients:

|  | Estimate | Std. Error | t value | Pr(>|t|) |
| (Intercept) | 113.9962 | 5.4545 | 20.900 | <2e-16 *** |
| Wr.Hnd | 2.7451 | 1.0728 | 2.559 | 0.0112 * |
| Nw.Hnd | 0.3707 | 1.0309 | 0.360 | 0.7195 |

Signif. codes: 0 *** 0.001 ** 0.01 * 0.05 . 0.1 ' 1

Residual standard error: 7.926 on 205 degrees of freedom
(29 observations deleted due to missing)
Multiple R-squared: 0.3616, Adjusted R-squared: 0.3554
F-statistic: 58.06 on 2 and 205 DF, p-value: < 2.2e-16

> 由于 Wr.Hnd 和 Nw.Hnd 的效应相互交织，同时包含两者会严重掩盖对响应建模的任何个体贡献。预测变量的统计显著性几乎不存在；其效应与单预测变量拟合相比具有高得多、非常高的 p 值。尽管如此，总体 F 检验仍然高度显著，给出了之前提到的第一个警告信号的例子。

## 本章的重要代码

| Function/operator | Brief description | First occurrence |
|---|---|---|
| anova | Partial F-tests | Section 22.2.1, p. 531 |
| add1 | Review single-term additions | Section 22.2.2, p. 533 |
| update | Make changes to fitted model | Section 22.2.2, p. 534 |
| drop1 | Review single-term deletions | Section 22.2.3, p. 538 |
| step | Stepwise AIC model selection | Section 22.2.4, p. 543 |
| plot (used on lm object) | Model diagnostics | Section 22.3.1, p. 551 |
| rstandard | Extract standardized residuals | Section 22.3.2, p. 555 |
| shapiro.test | Shapiro-Wilk test of normality | Section 22.3.2, p. 555 |
| shapivalues | Calculate leverages | Section 22.3.4, p. 558 |
| cooks.distance | Calculate Cook's distances | Section 22.3.5, p. 561 |

## PART V

ADVANCED GRAPHICS

## 23

## ADVANCED PLOT CUSTOMIZATION

许多用户最初被吸引到 R 是因为其令人印象深刻的图形灵活性和控制和定制 resulting 视觉的便捷性。在本章中，你将更仔细地查看基础 R 图形设备，以及如何微调你已熟悉的绘图，以充分利用你的可视化。在接下来的章节中，你将在 ggplot2 和传统的 R 图形中扩展你的技能。

本章的大部分内容假定你熟悉第 7 章和第 14 章的内容。一般来说，我还假定你使用的是标准的基础 R 应用程序（例如 Mac 上的 R.app 或 Windows 中的 Rgui.exe——参见附录 A），因为如果你在不同环境中使用 R，某些命令的行为和可用性可能会有所不同。

根据你的操作系统，用于在计算机屏幕上渲染图形显示的默认软件驱动程序也不同。
例如，在 Mac 上的标准 R.app 应用程序中，你会注意到

生成实时绘图会打开一个窗口，其横幅标题看起来像 Quartz:2 [*]——OS X 的图形设备驱动程序是 Quartz 窗口系统。在 Windows 机器上，你会看到 R Graphics: Device 2 (ACTIVE)。任何图形设备的编号总是从 2 开始；设备 1 被称为空设备，意味着目前没有任何活动。

> 要列出会话中可用的设备，请在提示符下输入 ?Devices。你会注意到列表中包含诸如 png 和 pdf 之类的命令，它们是所谓的静默图形设备，可实现直接到文件的绘图，如第 8 章所述。如果你愿意，可以为任何绘图使用不同的设备，尽管如果直接绘图到屏幕，默认设置几乎是合适的。

## 处理图形设备

到目前为止，你的绘图一次处理一个图像。可以打开多个图形设备，但一次只有一个会被视为活动设备（横幅标题用 [*] 或 (ACTIVE) 突出显示当前活动设备）。当你在多个绘图上工作或想要更改一个绘图而不关闭其他绘图时，这很有用。

### 23.1.1 手动打开新设备

你已经遇到的典型 R 命令（例如 plot、hist、boxplot 等）如果当前没有打开设备，将自动打开设备进行绘图并绘制所需绘图。你也可以使用 dev.new() 打开新窗口；这个最新窗口会立即变为活动状态，任何后续绘图命令都会影响该特定设备。

作为示例，首先关闭任何打开的图形窗口，然后在 R 提示符下输入以下内容：

```
R> plot(quakes$long,quakes$lat)
```

这将生成 quakes 数据框中 1000 个地震事件发生空间位置的绘图。如果当前唯一可用的设备是设备 1，空设备，任何刷新绘图窗口并产生新图像的绘图命令（例如 plot 或更专业的命令如 hist 或 boxplot）将在绘图数据之前自动打开默认图形设备的新实例。在我的机器上，我看到 Quartz 2 [/] 打开并显示空间坐标的绘图。

现在，假设你还想查看每个事件检测到的站点数量的直方图。执行以下操作以打开新的绘图窗口：

```
R> dev.new()
```

这个新窗口将被编号为 3（它通常会自己置于之前打开的窗口之上，因此你可能想用鼠标将其移至一侧）。重要的是，你会看到它成为活动设备：在 Mac 上 [*] 现在位于设备 3 横幅上；在 Windows 中，设备 3 将显示 (ACTIVE)，而设备 2 现在将显示 (inactive)。

此时，你可以输入通常的命令在设备 3 中显示所需的直方图：

```
R> hist(quakes$stations)
```

如果你没有使用 dev.new，直方图将只是覆盖设备 2 中地震事件空间位置的绘图。

### 23.1.2 在设备之间切换

要更改设备 2 中的内容而不关闭设备 3，请使用 dev.set 后跟你想要设为活动的设备号。以下代码激活设备 2 并重新绘制地震事件的位置，使每个事件的大小与检测到该事件的站点数量成比例。它清理了轴标签。

```
R> dev.set(2)
quartz
2
R> plot(quakes$long,quakes$lat,cex=0.02+quakes$stations, xlab="Longitude",ylab="Latitude")
```

使用 dev.set 总是会通过打印到控制台来确认新活动设备；具体文本会根据你的操作系统和设备类型而有所不同。

切换回设备 3，作为最后的调整，添加一条垂直线标记检测站点的平均数量。

```
R> dev.set(3)
quartz
3
R> abline(v=mean(quakes$stations),lty=2)
```

图 23-1 显示了在进行这些更改后两个图形设备。

