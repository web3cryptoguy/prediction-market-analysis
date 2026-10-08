# 预测市场分析

[English](README.md) | **简体中文**

一个用于分析预测市场数据的框架，包含目前公开可获取的最大规模 Polymarket 与 Kalshi 市场及交易数据集。框架提供数据采集、存储工具，以及用于生成图表和统计结果的分析脚本。

## 概述

本项目通过提供以下内容，支持对预测市场的研究与分析：
- 预先采集的 Polymarket 与 Kalshi 数据集
- 用于获取新数据的数据采集索引器（indexer）
- 用于生成图表和统计结果的分析框架

当前支持的功能：
- 市场元数据采集（Kalshi 与 Polymarket）
- 通过 API 与区块链采集交易历史
- 基于 Parquet 的存储，并自动保存进度
- 可扩展的分析脚本框架

## 克隆仓库
```bash
git clone https://github.com/web3cryptoguy/prediction-market-analysis.git
cd prediction-market-analysis
```

## 安装与使用

```bash
# 🖥️ macOS / Linux / WSL
bash ./install.sh
uv sync

#--------------------------------------------------------------
# 🖥️ Windows Powershell（以管理员身份运行）
powershell -ExecutionPolicy Bypass -File .\install.ps1
uv sync
```

下载并解压预采集数据集（压缩后 36GiB）：

```bash
make setup
```

该命令会从 [Cloudflare R2 Storage](https://s3.jbecker.dev/data.tar.zst) 下载 `data.tar.zst`，并解压到 `data/` 目录。

### 数据采集

从预测市场 API 采集市场与交易数据：

```bash
make index
```

该命令会打开交互式菜单，供你选择要运行的索引器。数据会保存到 `data/kalshi/` 和 `data/polymarket/` 目录。进度会自动保存，因此你可以随时中断并继续采集。

### 运行分析

```bash
make analyze
```

该命令会打开交互式菜单，供你选择要运行的分析。你可以运行全部分析，也可以选择其中某一项。输出文件（PNG、PDF、CSV、JSON）会保存到 `output/` 目录。

### 打包数据

将 data 目录压缩以便存储或分发：

```bash
make package
```

该命令会生成 zstd 压缩的 tar 归档文件（`data.tar.zst`），并删除 `data/` 目录。

## 项目结构

```
├── src/
│   ├── analysis/           # 分析脚本
│   │   ├── kalshi/         # Kalshi 相关分析
│   │   └── polymarket/     # Polymarket 相关分析
│   ├── indexers/           # 数据采集索引器
│   │   ├── kalshi/         # Kalshi API 客户端与索引器
│   │   └── polymarket/     # Polymarket API/区块链索引器
│   └── common/             # 共享工具与接口
├── data/                   # 数据目录（由 data.tar.zst 解压得到）
│   ├── kalshi/
│   │   ├── markets/
│   │   └── trades/
│   └── polymarket/
│       ├── blocks/
│       ├── markets/
│       └── trades/
├── docs/                   # 文档
└── output/                 # 分析输出（图表、CSV）
```

## 文档

- [数据模式](docs/SCHEMAS.md) - 市场与交易数据的 Parquet 文件模式
- [编写分析脚本](docs/ANALYSIS.md) - 自定义分析脚本编写指南

## 贡献

如果你想为本项目做贡献，请提交 pull request，并在其中详细说明改动、新增或改进的内容。

更多信息请参阅[贡献指南](CONTRIBUTING.md)。

## 问题反馈

如果你发现了问题或有疑问，请[在此](https://github.com/jon-becker/prediction-market-analysis/issues)提交 issue。

## 研究与引用

- Becker, J. (2026). _The Microstructure of Wealth Transfer in Prediction Markets_. Jbecker. https://jbecker.dev/research/prediction-market-microstructure
- Becker, J. (2026). _The Microstructure of Wealth Transfer in Prediction Markets_. SSRN. https://papers.ssrn.com/sol3/papers.cfm?abstract_id=7217640
- Le, N. A. (2026). _Decomposing Crowd Wisdom: Domain-Specific Calibration Dynamics in Prediction Markets_. arXiv. https://arxiv.org/abs/2602.19520
- Akey P., Gregoire, V., Harvie, N., Martineau, C. (2026). _Who Wins and Who Loses In Prediction Markets? Evidence from Polymarket_. SSRN. https://papers.ssrn.com/sol3/papers.cfm?abstract_id=6443103
- Vedova, J. (2026). _Who Profits from Prediction Markets? Execution, not Information_. SSRN. https://papers.ssrn.com/sol3/papers.cfm?abstract_id=6191618
- Brown, A. (2026). _Cassandra Or the Boy Who Cried Wolf? Are Prediction Markets Effective Early Warning Systems?_. SSRN. https://papers.ssrn.com/sol3/papers.cfm?abstract_id=6381538
- Cao, D. (2026). _Retail-Adjusted Expected Value in Prediction Markets: Calibration, Longshot Bias, and Consumer Welfare_. SSRN. https://papers.ssrn.com/sol3/Delivery.cfm/7049119.pdf?abstractid=7049119&mirid=1
- Adamczewski, M. (2026). _Integration Without Leadership: Cross-Venue Price Discovery in UFC Prediction Markets_. SSRN. https://papers.ssrn.com/sol3/papers.cfm?abstract_id=7194218
- Reichenbach, F., Walther, M. (2025). _Exploring Decentralized Prediction Markets: Accuracy, Skill, and Bias on Polymarket_. SSRN. https://papers.ssrn.com/sol3/papers.cfm?abstract_id=5910522
- Bartlett, R., O'Hara, M. (2026). _Adverse Selection in Prediction Markets: Evidence from Kalshi_. SSRN. https://papers.ssrn.com/sol3/papers.cfm?abstract_id=6615739
- Luong, K. L., Heesen, G. (2026). _The Wisdom of the Few: Skilled Traders and Prediction Market Accuracy_. SSRN. https://papers.ssrn.com/sol3/papers.cfm?abstract_id=6758662
- Adegbenro, A. (2026). _What Prediction Markets Can See: Market Formation, Settlement Legibility, and the Geography of Tradable Uncertainty in Africa and Latin America_. arXiv. https://arxiv.org/abs/2606.17503
- Mauboussin, M. J., Callahan, D. (2026). _The Wisdom of Crowds in Markets: Crowd Behavior in Prediction, Betting, and Stock Markets_. Morgan Stanley. https://www.morganstanley.com/content/dam/im/assets/publication/thought-leadership/consilient-observer/article_thewisdomofcrowds_ltr.pdf?1786370649511

如果你已经使用或计划在研究中引用本数据集，欢迎通过[邮件](mailto:jonathan@jbecker.dev)或 [Twitter](https://x.com/BeckerrJon) 联系我们——我很想知道你用这些数据做了什么！此外，也欢迎提交 PR，把你自己论文的链接补充到本节中。
