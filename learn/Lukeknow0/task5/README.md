# Task 5 — Avalanche RWA Token 合约实战

- GitHub 用户名：`Lukeknow0`
- 项目仓库：https://github.com/Lukeknow0/avalanche-launch-token
- 网络：Avalanche Fuji C-Chain（Chain ID `43113`）

> 本项目只用于测试网技术学习与业务模拟；不代表真实资产、募资、投资建议或金融产品发行。

## 1. RWA 业务场景

本作业选择“社区太阳能收益权”作为 RWA 场景。`AvalancheSolarYieldToken`（符号 `ASYT`）代表一组被模拟登记的社区太阳能项目收益份额。

在真实项目中，项目方或经审计的资产服务商会托管发电记录、收益结算资料和对应资产登记证明；链上 Token 不应单独被视为资产真实性的证明。本合约的 `assetDocument` 仅保存一个模拟的资产报告 URI，便于演示链上可追踪的证明信息更新。

- 1 ASYT：模拟代表 1 个太阳能收益权单位。
- 发行（mint）：模拟新增登记且经过发行方确认的收益权单位。
- 转让（transfer）：模拟登记持有人之间的权益变更。
- 销毁（burn）：模拟赎回、注销或从登记中移除的收益权单位。

## 2. 合约与权限设计

合约文件：

- [`AvalancheSolarYieldToken.sol`](https://github.com/Lukeknow0/avalanche-launch-token/blob/main/packages/hardhat/contracts/AvalancheSolarYieldToken.sol)
- [测试文件](https://github.com/Lukeknow0/avalanche-launch-token/blob/main/packages/hardhat/test/AvalancheSolarYieldToken.ts)

合约基于 OpenZeppelin `ERC20`、`ERC20Burnable` 与 `Ownable` 实现：

| 功能 | 实现 |
| --- | --- |
| Token 名称/符号 | `Avalanche Solar Yield Token` / `ASYT` |
| 发行 | `mint(address,uint256)`，仅 `owner` 可调用 |
| 转让和余额/总量查询 | ERC-20 标准 `transfer`、`balanceOf`、`totalSupply` |
| 销毁 | 持有人调用 `burn(uint256)` |
| 资产证明 | `assetDocument()` 查询，`updateAssetDocument(string)` 仅 owner 可调用 |
| 审计事件 | ERC-20 `Transfer` 事件与 `AssetDocumentUpdated` 事件 |

本地测试覆盖：部署、Token 元数据、初始发行、授权发行、未授权发行/更新拒绝、转账、销毁和总量变化。当前测试结果为 **7/7 passing**。

## 3. Fuji 部署与链上交互

- 合约地址：待 Fuji 钱包部署后补充
- 部署交易：待 Fuji 钱包部署后补充
- Snowtrace 链接：待 Fuji 钱包部署后补充
- 部署、发行、转账、销毁截图：待完成真实测试网交互后补充

## 4. 风险边界

本合约没有接入线下托管方、法务合规系统、KYC、收益分配、储备证明或预言机，因此不能证明任何现实资产权属或收益，也不应部署到主网用于真实资产发行。其唯一目的，是展示 RWA Token 的基础代币、权限和资产证明引用设计。
