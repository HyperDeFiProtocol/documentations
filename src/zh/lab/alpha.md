# Alpha 测试覆盖

独立测试（即算好数据后，发出测试交易前，应无其它人正在交易）

## 1. 测试买入

### 1.1 未买过的钱包买入小于鲸鱼量

应扣 10%

### 1.2 未买入的钱包买入超过鲸鱼量

`买入量 x (1 - 30%)` 超过鲸鱼

应扣 30%

### 1.3 已买入过的钱包买入小于鲸鱼量

- 如 `前余额 + 买入量` 小于鲸鱼，应扣 10%
- 如 `前余额 + 买入量 x (1 - 30%)` 超过鲸鱼，应扣 30%

### 1.4 已买入过的钱包买入超过鲸鱼量

应扣 30%

### 1.5 已买入过的钱包买到小于鲸鱼量

即 `前余额 + 买入量 x (1 - 30%)` 小于鲸鱼

应扣 10%

### 1.6 已买入过的钱包买到超过鲸鱼量

- 如 `前余额 + 买入量 x (1 - 30%)` 超过鲸鱼，应扣 30%


## 2. 测试钱包到钱包的普通转账

- 如当前钱包不是鲸鱼，应扣 15%
- 如当前钱包已是鲸鱼，应扣 30%

同时

- 如缓冲池显示就续，应触发缓冲回流（即查看交易详情能看到有关 BUSD 的换币和流动性加池记录）
- 如缓冲池未显示就续，应只完成授权

触发缓冲回流的记录里 PancakeSwap Liquidity 新铸币的 LP Token 应进黑洞，即 `0x000000000000000000000000000000000000dead`

## 3. 测试卖出前的 Approve 授权动作

- 如缓冲池显示就续，应触发缓冲回流（即查看授权交易详情能看到记录）
- 如缓冲池未显示就续，应只完成授权

触发缓冲回流的记录里 PancakeSwap Liquidity 新铸币的 LP Token 应进黑洞，即 `0x000000000000000000000000000000000000dead`

## 4. 测试卖出

### 4.1 非鲸鱼卖出

应扣 15%

### 4.2 鲸鱼卖出

应扣 30%
