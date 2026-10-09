
在时间 `$T_B$` 伸出的二级分支 `$\tilde{S}^{T_B}$` 是同一场景的一部分，并按如下方式模拟：

- 对于 `t <= T_B`，`$\tilde{S}^{T_B}$` 是同一场景的一部分；
- 对于 `t > T_B`，`$\tilde{S}^{T_B} = a(\tilde{S}, t)dt + b(\tilde{S}, t)dW`。

## 股票看涨期权

| 行权价 | 120 |
| :--- | :--- |
| 到期 | 01Jun2021 |
| 看涨期权(S,K) | `max(0, S-K)` |
| 到期 | 期权支付 `CALL ( Spot(), STRIKE)` |

## 外汇障碍期权

| 索引 | `fx( EUR, USD)` |
| :--- | :--- |
| 行权价 | 100 |
| 障碍价 | 120 |
| 收益(S, K) | `max(0, S-K)` |
| 到期 | 01Jun2021 |
| 障碍开始 | 01Jun2020 |
| 障碍结束 | 01Jun2021 |
| 障碍频率 | 1m |

| 障碍开始 | `vAlive = 1` |
| :--- | :--- |
| 到期 | 期权支付 `vAlive * PAYOFF( INDEX, STRIKE)` |

开始：`BARSTART`
结束：`BAREND`
频率：`BARFREQ`
锁价：end
`if INDEX > BARRIER then vAlive = 0 endIf`

## 篮子期权

| 交易日 | 01Jun2020 |
| :--- | :--- |
| 到期 | 01Jun2021 |
| 行权价 0.1 |

| 股票 | 权重 |
| :--- | :--- |
| `STOCK1` | 0.2 |
| `STOCK2` | 0.1 |
| `STOCK3` | 0.15 |
| `STOCK4` | 0.25 |
| `STOCK5` | 0.3 |

## 结语

| 交易日 | `loop (0, NSTOCKS) s0[ii] = spot(stocks[ii]) endLoop` `loop (0, NSTOCKS)` `s1 = spot(stocks[ii])` |
| 到期 | `perf = perf + weights[ii] * ( s1 - s0[ii] ) / s0[ii]` `endLoop` 期权支付 `max( 0, perf - STRIKE)` |

## 利率互换

| 开始日期 | 01Jun2020 |
| 结束日期 | 01Jun2030 |
| 浮频率 | 3m |
| 浮基 | act/360 |
| 浮动指数 | L3M |
| 锁频率 | 1y |
| 锁基 | 30/360 |
| 票息 | 2% |

- 开始：`STARTDATE` 互换支付 `-libor(StartPeriod, EndPeriod, FLBAS)`
结束：`ENDDATE FLIDX)`
频率：`FLFREQ * cvg(StartPeriod, EndPeriod, FLBAS)`
锁价：EndPeriod 前两个交易日

- 开始：`STARTDATE` 互换支付 `CPN`
结束：`ENDDATE cvg(StartPeriod, EndPeriod, FIXBAS)`
频率：`FIXFREQ`
锁价：EndPeriod 前两个交易日

## 利率上限

| 开始日期 | 01Jun2020 |
| 结束日期 | 01Jun2030 |
| 浮频率 | 3m |
| 浮基 | act/360 |
| 浮动指数 | L3M |
| 行权价 | 1.5% |

- 开始：`STARTDATE` 上限期权支付`( 0, libor(StartPeriod, EndPeriod, FLBAS, FLIDX`
结束：`ENDDATE -STRIKE`
频率：`FLFREQ cvg(StartPeriod, EndPeriod, FLBAS)`
锁价：EndPeriod 前两个交易日

## 带上限票息的利率互换

| 开始日期 | 01Jun2020 |
| 结束日期 | 01Jun2030 |
| 频率 | 3m |
| 浮基 | act/360 |
| 浮动指数 | L3M |
| 锁频率 | 1y |
| 锁基 | 30/360 |
| 票息 | 2% |

- 开始：`STARTDATE`
`vAlive = 1`
期权支付 `vAlive * PAYOFF( INDEX, STRIKE)`
结束：`ENDDATE -STRIKE`
频率：`FLFREQ cvg(StartPeriod, EndPeriod, FLBAS)`
锁价：EndPeriod 前两个交易日

## 上限期权

| 开始日期 | 01Jun2020 |
| 结束日期 | 01Jun2030 |
| 浮频率 | 3m |
| 浮基 | act/360 |
| 浮动指数 | L3M |
| 行权价 | 1.5% |

- 开始：`STARTDATE` 上限期权支付`( 0, libor(StartPeriod, EndPeriod, FLBAS, FLIDX`
结束：`ENDDATE -STRIKE`
频率：`FLFREQ cvg(StartPeriod, EndPeriod, FLBAS)`
锁价：EndPeriod 前两个交易日

## 解析

```cpp
{
  // 拷贝事件日期
  myEventDates.push_back(evtIt->first);
  // 解析事件字符串
  myEvents.push_back(parse(evtIt->second));
};
```

我们通过调用父级解析函数来解析每个事件字符串：

```cpp
// Event = vector<Statement> = vector<ExprTree>
Event parse(const string& eventString)
{
  Event e;
  auto tokens = tokenize(eventString);
  auto it = tokens.begin();
  while (it != tokens.end()) {
    e.push_back(Parser<decltype(it)>()());
    parseStatement(it, tokens.end());
  }
  // C++11 --> vectors 会被移动，而不是拷贝
  return e;
}
```
