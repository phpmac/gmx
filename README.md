# gmx.io 黑客事件研究


AUM（资产管理规模，Assets Under Management）在GMX中的计算公式是：AUM = poolAmount ± global long PnL ± global short PnL，也就是GMX池子里所有代币的总量，加上所有多头头寸的总盈亏，再加上所有空头头寸的总盈亏。

GLP（流动性提供者代币）的价格就是用AUM除以GLP的总供应量得出，所以AUM的准确性直接影响GLP的价值和整个池子的安全。

这次GMX V1被攻击的根本原因，就是AUM的计算方式存在漏洞，被黑客利用，导致资金池被盗走超4000万美元。


## 官方说明 - [查看链接](https://x.com/GMX_IO/status/1942958365862236300)

紧急：对于所有 GMX V1 叉，GMX V1 已被利用。

可以通过执行以下操作来缓解此问题：

1. 禁用杠杆：可以通过设置 Vault.setIsLeverageEnabled(false) 来实现，或者，如果使用了 Vault Timelock，则可以通过设置 Timelock.setShouldToggleIsLeverageEnabled(false) 来实现

2. 使用 Vault.setTokenConfig 或 Timelock.setTokenConfig 将所有 maxUsdgAmounts 设置为“1”，以防止 GLP 铸造

请注意，该值必须为“1”而不是“0”，因为“0”表示没有上限


## 慢雾分析结果 - [查看链接](https://x.com/peckshield/status/1942970395830923732)

今天的 
@GMX_IO
 黑客攻击导致 >$4000 万的损失，这是由于 AUM 的计算方式造成的。

我们已经与团队分享了我们的初步分析和根本原因。

我们预计所有当前的 GMX v1 分叉都存在漏洞，请立即按照以下建议禁用杠杆和 GLP 铸造。

![](/docs/1.jpeg)

## 相关资料

- [交易图谱](https://usdc.range.org/usdc?txhash=0xDF3340A436c27655bA62F8281565C9925C3a5221&showPending=true) - [来源](https://x.com/zachxbt/status/1942961205519540369)



## 你可以

> 欢迎贡献思路,这是如何实现的,您可以修改并提交我将允许您的更新