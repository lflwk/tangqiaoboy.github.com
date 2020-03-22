---
title: 美股期权学习笔记（三）
date: 2020-03-21 11:02:41
categories: summary
tags: books
---

这篇再展开讨论一下期权的指标。

## 影响期权的变量

期权因为相关的变量很多，包括时间，行权价等。所以任何一个变量变化就会影响期权的价格。人们研究发现，影响期权的价格因素一共有如下 6 个：

 - 标的资产价格。对于看涨期权，标的资产上涨，看涨期权也上涨。
 - 期权行权价格。
 - 距离到期时间的长短。
 - 标的波动率。标的波动率越高，期权价格越高。
 - 短期利率，一般是 90 天的短期票据利率。
 - 股息。公司如果提高股息，看涨期权会下跌，看跌期权上涨。因为股价会随着派息后下降，但是期权所有人无法获得股息。

实值期权和虚值期权受到期时间的影响不一样：

 * 距离到期时间越近，虚值期权的价格越低。所以会出现随着临近，虚值的看涨和看跌期权都下跌的情况。
 * 距离到期时间越近，实值期权的价值越来越接近标的行权价与市场价的差价。

对此，《麦克米伦谈期权》1.9.2 节有一个汇总表格：

{% img /images/option-price-factors.jpg %}

## 期权的指标

为了更好的理解期权，人们又抽象出一些指标来描述它。

### Delta

Delta 表示随着股价的变化，期权价格的变化速度。Delta 变化区间在 `[-1, 1]` 之间。其中看涨期权的 Delta 变化区间在 `[0, 1]`，看跌期权的 Delta 变化区间在 `[-1, 0]`。

比如 Delta 为 0.5 就表示，股价每变化 1 点，期权变化 0.5 点。比如实值的看涨期权，Delta 就比较高，股价每上涨 1 点，期权几乎也上涨 1 点。

实值看涨期权的 Delta 接近 1，虚值看涨期权的 Delta 接近 0 一些。说明实值看涨期权更像是股票。

如果 Delta 为 0，则表示无论股价怎么变化，该组合的价格都不会变化，这种情况下，我们也称作该组合的 Delta 是中性，这也解释了上面提到的套利为什么被称作 **Delta 中性头寸**。

Delta 随着时间也会变化。比如对于虚值期权来说，随着时间流逝，它的 Delta 会趋于 0。因为时间越接近，股价的波动除非将虚值改变为实值，否则就没有意义。

与虚值期权相反，实值期权随着时间的流逝，它的 Delta 会趋近于 1（或-1）。因为这个时候，期权的时间价值几乎没有了，它的价格反映的就是行权价和股价之间的差。

书中对 Delta 还有一种另类的看待角度：**Delta 可以看作期权最终到期时为实值期权的概率**。虽然数学解释不严谨，但是很有效。

### 波动率

波动率是用来衡量标的价格变化速度。

 * 历史波动率（historical volatility）是根据股票历史的波动率数据，是算出来的。
 * 隐含波动率（implied volatility）是隐含在场内期权价格中的未来波动率水平。

当隐含波动率远高于历史波动率，说明股票在经历一些事件，例如：并购，诉讼，重大合作，重大危机，这些事件因为没有确定，所以买卖双方力量均衡，但事件结束后股票就会有大的变化。

书中 6.6.2 节举了一个有趣的例子：

> 1994 年，一家名为 Gensia 的制药公司被 FDA 宣布，将对它的主要药品举行听证会。该公司的股票没有什么巨大的波动，因为 FDA 的结果没有出来，所以看多和看空的双方力量均衡。
> 但是，这家公司的期权的隐含波动率即上升至 140% 左右的区域。这是因为交易者知道 FDA 的结果将决定这家公司的成败。结果 FDA 最终做出了不利于这家公司的决定。
> 这家公司股价瞬间下跌 50%，同时期权的隐含波动率回归到了正常水平。

### Vega

Vega 描述的是波动率的变化如何影响期权价格（假定其它变量不变）。实际上 Vaga 就是代表的是隐含波动率。

 * Vega 值如果为 -5.0，则表示波动率每增加 1 点，期权会亏损 500 元。
 * Vega 值如果为 +5.0，则表示波动率每增加 1 点，期权会收益 500 元。

所以 Vega 代表的是波动率变化后，期权价格的变化情况。

### Theta

Theta 表示的是期权时间价值的减少。它是用负数来表示的，期权每过一天它的时间价值就会减少一些。

如果一个期权到期时间还很长，那么它的 Theta 值可能非常低。

例如：下图是 哔哩哔哩（BILI）在 3.20 的一份 7.17 到期的 22.5 PUT 合约，可以看到因为到期时间还有 4 个月，所以每天由于时间因素带来的影响只有 -0.014：

{% img /images/theta.jpg %}

而与此对比，只有一周就到期的 3.27 Tesla PUT 的 Theta 则高达 -0.23：

{% img /images/theta-tesla.jpg %}

### Rho

Rho 表示的是利率变化对于期权价格的影响。但是大部分活跃的期权交易因为到期时间都比较短（1-3个月），所以 Rho 的值都很小。

### Gamma 

因为 Delta 和 Vaga 值会变化得非常快，不利于构建中性头寸，所以理论家们又引入了 Gamma。

Gamma 是衡量 Delta 变化快慢的指标。如果 Delta 和 Gamma 都是中性的，那么组合保持中性的概率就高了很多。

对于如何建立一个中性头寸组合，书中介绍了详细的方法，但估计一般人都应该用不到，我就不展开介绍了。

### 时间价值

期权时间价值是指期权合约的购买者为购买期权而支付的权利金超过期权内在价值的那部分价值。期权购买者之所以愿意支付时间价值，是因为他预期随着时间的推移和市价的变动，期权的内在价值会增加。

期权的内在价值是通过对标的股票价格变化而变化的，如果股票没有超着预期的方向波动，那么期权的内在价值就不会增加，而随着时间流逝，期权的时间价值又会减少，期权的价值就会减少。

## 小结

因为期权的影响因素很多，所以人们抽像出来 Delta, Vega, Theta 等指标来更好地理解它。

本系列文章汇总：
 * [美股期权学习笔记（一）](/2020/02/08/option-learning-note/)
 * [美股期权学习笔记（二）](/2020/03/15/option-learning-notes-1/)
 * [美股期权学习笔记（三）](/2020/03/21/option-learning-notes-3/)
 * [美股期权学习笔记（四）](/2020/03/22/option-learning-notes-3/)









