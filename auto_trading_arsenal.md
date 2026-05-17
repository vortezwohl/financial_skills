# 自动交易武器库 — MCP + Skills 全栈调研报告

> 覆盖 56 个 MCP/API/SDK 工具 + 12 个 Claude Code 开箱即用 Skills，含仓库地址、安装命令、调用方式、MCP支持状态与适用场景。
> 调研时间：2026-05

---

## 目录

- [一、MCP协议核心工具（12个）](#一mcp协议核心工具12个)
- [二、股票交易工具（8个）](#二股票交易工具8个)
- [三、期货交易工具（6个）](#三期货交易工具6个)
- [四、基金与资产管理工具（6个）](#四基金与资产管理工具6个)
- [五、量化交易框架（7个）](#五量化交易框架7个)
- [六、投研与分析工具（7个）](#六投研与分析工具7个)
- [七、短线交易与高频工具（5个）](#七短线交易与高频工具5个)
- [八、风投与另类投资工具（5个）](#八风投与另类投资工具5个)
- [九、Claude Code Skills 开箱即用（12个）](#九claude-code-skills-开箱即用12个)
- [快速集成建议](#快速集成建议)

---

## 一、MCP协议核心工具（12个）

> MCP（Model Context Protocol）协议允许 AI 助手（Claude、Cursor 等）通过自然语言直接调用金融数据与交易接口。

### 1. Stock MCP（finance-mcp）

| 维度 | 详情 |
|------|------|
| **GitHub** | [Eternity714/finance-mcp](https://github.com/Eternity714/finance-mcp)（上游：[huweihua123/stock-mcp](https://github.com/huweihua123/stock-mcp)） |
| **技术栈** | Python + FastAPI + Docker + Redis |
| **覆盖市场** | A股 / 港股 / 美股 |
| **MCP支持** | ✅ 原生 MCP 协议 |
| **核心特性** | 多数据源融合（AKShare、Tushare、yFinance、Finnhub）；新闻情绪分析、深度研究报告、智能搜索；宏观经济数据（GDP/CPI/PMI/PPI/M2）；Docker 一键部署（5分钟启动）；Redis 缓存 + 自动降级 |
| **适用场景** | 需要多市场数据聚合的 AI Agent，快速搭建交易数据中台 |

### 2. Alpha Vantage MCP

| 维度 | 详情 |
|------|------|
| **官方 API** | [alphavantage.co](https://www.alphavantage.co/) |
| **社区实现（推荐）** | [OriShmila/alpha-vantage-mcp-server](https://github.com/OriShmila/alpha-vantage-mcp-server)（Python，25+ tools，2025年8月活跃） |
| **其他实现** | [berlinbra/alpha-vantage-mcp](https://github.com/berlinbra/alpha-vantage-mcp)（Python+Docker）；[MissionSquad/mcp-avantage](https://github.com/MissionSquad/mcp-avantage)（TypeScript）；[matteoantoci/mcp-alphavantage](https://github.com/matteoantoci/mcp-alphavantage)（TypeScript/Node.js） |
| **MCP支持** | ✅ 多条社区 MCP 服务器（无官方 MCP） |
| **核心特性** | 实时/历史股票数据；外汇、加密货币、商品数据；技术指标（SMA/EMA/RSI/MACD）；经济指标；市场情报 |
| **适用场景** | 全球市场数据获取，需要免费层级的 API（25请求/天免费） |

### 3. Finnhub MCP

| 维度 | 详情 |
|------|------|
| **推荐实现** | [sverze/stock-market-mcp-server](https://github.com/sverze/stock-market-mcp-server)（Python 3.8+，stdio MCP） |
| **其他实现** | [catherinedparnell/mcp-finnhub](https://github.com/catherinedparnell/mcp-finnhub)（Python 3.13 + FastMCP，⭐7）；[mseep-mcp-finnhub](https://pypi.org/project/mseep-mcp-finnhub/)（PyPI包，v0.1.2，2025.05） |
| **MCP工具数** | 约6-15个（实时/历史报价、基本面指标、新闻、K线、推荐趋势） |
| **核心特性** | 100+ Finnhub API 端点覆盖；实时数据 + 技术指标 + 基本面；另类数据（社交媒体情绪、国会交易等） |
| **适用场景** | 美股深度分析，需要另类数据和基本面数据的场景 |

### 4. QuantConnect MCP

| 维度 | 详情 |
|------|------|
| **官方 Docker** | `docker pull quantconnect/mcp-server`（60个MCP工具） |
| **社区 PyPI** | [quantconnect-mcp](https://pypi.org/project/quantconnect-mcp/0.1.5/)（`uvx quantconnect-mcp`，Python 3.12+） |
| **引擎仓库** | [QuantConnect/Lean](https://github.com/QuantConnect/Lean)（C#，Apache 2.0） |
| **MCP支持** | ✅ 官方 + 社区 MCP 服务器 |
| **核心特性** | 研究环境（QuantBook）；PCA + 协整检验 + 均值回归分析；稀疏投资组合优化（Huber Downward Risk）；ETF成分分析 + 多标准资产筛选；实盘部署/监控/清算 |
| **适用场景** | 专业级算法交易，需要云端回测和实盘部署的机构用户 |

### 5. Alpaca MCP Server

| 维度 | 详情 |
|------|------|
| **官方仓库** | [alpacahq/alpaca-mcp-server](https://github.com/alpacahq/alpaca-mcp-server)（⭐最高） |
| **官方文档** | [docs.alpaca.markets/docs/alpaca-mcp-server](https://docs.alpaca.markets/docs/alpaca-mcp-server) |
| **安装方式** | `uvx alpaca-mcp-server init` |
| **MCP支持** | ✅ 官方 MCP（43个API端点） |
| **核心特性** | 股票/ETF/加密货币/期权全覆盖；自然语言下单（市价/限价/止损/跟踪止损/多腿期权）；期权 Greeks + IV + 合约搜索；Watchlists CRUD + 公司事件（财报/拆股/股息）；默认纸交易模式（安全） |
| **适用场景** | 需要快速打通"AI分析→下单交易"闭环的美股/加密交易者 |

### 6. iTick MCP Server

| 维度 | 详情 |
|------|------|
| **官方文档** | [itick-org/docs](https://github.com/itick-org/docs)（中文）、[itick-org/docs.en](https://github.com/itick-org/docs.en)（英文） |
| **免费 API** | [itick-org/free-stock-api](https://github.com/itick-org/free-stock-api) |
| **MCP 包** | [alltick-stock-mcp-server](https://www.npmjs.com/package/alltick-stock-mcp-server)（npm，v1.0.3） |
| **MCP支持** | ✅ 社区 MCP（`npx -y alltick-stock-mcp-server@1.0.3`） |
| **核心特性** | REST + WebSocket + FIX 三协议支持；覆盖全球主流市场（美股/港股/A股/新加坡/日本）；实时报价 + 历史K线；市场情绪、资金流向、龙虎榜、期货基差；免费额度可用（约11秒/次） |
| **适用场景** | 需要全球多市场实时行情数据的 AI Agent |

### 7. Smart Financial MCP

| 维度 | 详情 |
|------|------|
| **GitHub** | [YUHAI0/smart-financial-mcp](https://github.com/YUHAI0/smart-financial-mcp) |
| **安装方式** | `uvx smart-financial-mcp` |
| **数据源** | Tushare Pro API |
| **MCP支持** | ✅ 原生 MCP（15个工具） |
| **核心特性** | 股票/ETF/指数/期货全面覆盖；自动生成财务分析报告和可视化表格；本地加密存储 API Token（`~/.tushare_mcp/.env`）；智能股票搜索；财经快讯推送 |
| **MCP工具** | `get_stock_basic_info`, `get_daily_stock_price`, `get_realtime_stock_price`, `get_etf_daily_price`, `get_index_daily_price`, `get_futures_daily_price`, `get_daily_basic_indicators`, `get_income_statement`, `get_financial_news`, `search_stocks` 等 |
| **适用场景** | Tushare 用户的 AI 助手对接，A股基本面+行情分析 |

### 8. Finance Trading AI Agents MCP

| 维度 | 详情 |
|------|------|
| **GitHub** | [aitrados/finance-trading-ai-agents-mcp](https://github.com/aitrados/finance-trading-ai-agents-mcp)（⭐~90） |
| **PyPI** | `pip install finance-trading-ai-agents-mcp`（v0.0.92） |
| **MCP支持** | ✅ 原生 MCP + 多智能体架构 |
| **核心特性** | **6部门仿真实金融公司架构**：Project Manager(AI Bus) → 技术指标分析师 + 裸K分析师 + 新闻情绪分析师 + 经济日历分析师 → 最终决策官；实时流式 OHLC 数据；券商集成（查询账户/下单/撤单）；local RPC/PubSub 跨进程通信 |
| **适用场景** | 需要多智能体协作的 AI 交易决策系统 |

### 9. Open Stocks MCP

| 维度 | 详情 |
|------|------|
| **PyPI** | [open-stocks-mcp](https://www.piwheels.org/project/open-stocks-mcp/)（`pip install open-stocks-mcp`，v0.1.7，2025.07） |
| **关联项目** | [syyunn/rb-mcp-robinhood-mcp-server](https://github.com/syyunn/rb-mcp-robinhood-mcp-server)（Robinhood MCP）；[schwab_mcp](https://rubygems.org/gems/schwab_mcp)（Ruby, Schwab API, v0.3.0）；[Trade Agent MCP](https://mcp.thetradeagent.ai/sse)（SaaS，多券商） |
| **MCP支持** | ✅ Python 包 + Ruby Gem 社区实现 |
| **核心特性** | 基于 Robin Stocks 等开源库；多券商覆盖（Robinhood + Charles Schwab）；股票报价/市价单/限价单/持仓监控 |
| **适用场景** | 美股散户 AI 辅助交易，Robinhood/Schwab 用户 |

### 10. IB MCP（Interactive Brokers）

| 维度 | 详情 |
|------|------|
| **推荐实现 1** | [omdv/ibkr-llm-assistant](https://github.com/omdv/ibkr-llm-assistant)（Python，基于 ib_async，Telegram交易审批） |
| **推荐实现 2** | [kelvingao/ezib-mcp](https://github.com/kelvingao/ezib-mcp)（Python 3.11+，SSE + stdio，Docker） |
| **推荐实现 3** | [ricaardo/IBKR TWS MCP](https://github.com/ricaardo/ibkr-tws-mcp)（48个工具/8大插件类别，FastMCP） |
| **底层库** | [mdelvaux/ib_async](https://github.com/mdelvaux/ib_async)（原 ib_insync，2024年更名） |
| **MCP支持** | ✅ 3个活跃社区 MCP 实现（均基于 ib_async） |
| **核心特性** | 48个MCP工具（行情/合约/账户/订单/风控/扫描/新闻/策略）；多传输模式（stdio/SSE/HTTP）；插件化架构（`plugins.yaml` 动态配置） |
| **适用场景** | 需要对接盈透证券（IBKR）的 AI 交易系统 |

### 11. FinanceMCP（Tushare数据）

| 维度 | 详情 |
|------|------|
| **主力仓库** | [guangxiangdebizi/FinanceMCP](https://github.com/guangxiangdebizi/FinanceMCP)（TypeScript/Node.js, v4.7.0, 2025年） |
| **扩展仓库** | [FinanceMCP-DCTHS](https://github.com/guangxiangdebizi/FinanceMCP-DCTHS)（东方财富+同花顺板块）；[FinanceMCP-Alpha](https://github.com/guangxiangdebizi/FinanceMCP-Alpha)（WorldQuant 101 Alpha因子） |
| **Python版本** | [YUHAI0/smart-financial-mcp](https://github.com/YUHAI0/smart-financial-mcp)（见 #7） |
| **MCP支持** | ✅ 原生 MCP（43+ Tushare API） |
| **核心特性** | A股/港股/美股/加密市场全覆盖；5大技术指标（MACD/RSI/KDJ/BOLL/MA）；分钟级K线；宏观经济（GDP/CPI/PPI/PMI/Shibor等11项）；财务分析（13种数据类型）；资金流向/融资融券/龙虎榜；免费公共云 MCP 服务 |
| **适用场景** | **中国金融市场 AI 分析的首选方案**（数据最全面） |

### 12. FinMCP（统一金融 AI 生态）

| 维度 | 详情 |
|------|------|
| **GitHub** | [Finance-LLMs/FinMCP](https://github.com/Finance-LLMs/FinMCP)（⭐新项目，2025年9月活跃） |
| **评测基准** | [FinMCP-Bench](https://huggingface.co/DianJin/FinMCP-Bench)（盈米基金×阿里云，65个金融MCP工具，10大场景） |
| **MCP支持** | ✅ 生态系统级 MCP |
| **核心特性** | Deep Research Engine（AI 驱动迭代研究，网页抓取+内容合成）；印度市场(NSE/BSE) + 全球市场(Yahoo Finance)；Upstox 交易平台对接；Digital Persona AI（金融文档分析 + LLM微调 LoRA/4-bit量化） |
| **适用场景** | 需要一站式金融 AI 生态的团队，多市场全球覆盖 |

---

## 二、股票交易工具（8个）

### 13. yfinance

| 维度 | 详情 |
|------|------|
| **GitHub** | [ranaroussi/yfinance](https://github.com/ranaroussi/yfinance) |
| **PyPI** | `pip install yfinance` |
| **MCP支持** | ❌ 无原生 MCP（可通过 MCP 桥接封装） |
| **核心特性** | 免费获取美股/ETF/指数历史行情、财务报表、实时报价；与 Pandas 深度集成；全球 60+ 交易所 |
| **适用场景** | 美股数据获取的 Python 标准库，研究和小规模回测 |

### 14. Tushare

| 维度 | 详情 |
|------|------|
| **官网** | [tushare.pro](https://tushare.pro) |
| **PyPI** | `pip install tushare` |
| **MCP支持** | ✅ 通过 FinanceMCP / Smart Financial MCP 桥接 |
| **核心特性** | A股/基金/宏观经济/新闻情绪全覆盖；Pro 版提供更全面的金融数据服务；免费积分获取（学生可申请2000分） |
| **适用场景** | 中国A股市场数据获取的中文用户首选 |

### 15. AKShare

| 维度 | 详情 |
|------|------|
| **GitHub** | [akfamily/akshare](https://github.com/akfamily/akshare)（⭐12,200+） |
| **PyPI** | `pip install akshare`（v1.17.88） |
| **MCP支持** | ✅ 通过 [China Stock MCP Server](https://langdb.ai/app/mcp-servers/china-stock-mcp-server) 桥接 |
| **核心特性** | 纯 Python 无依赖；覆盖股票/期货/基金/债券/外汇/加密货币；统一 pandas DataFrame 输出；2300+ Forks / 91 位贡献者 |
| **适用场景** | **新兴黑马**，适合需要最广泛中国金融数据覆盖且不想折腾多数据源的用户 |

### 16. efinance

| 维度 | 详情 |
|------|------|
| **GitHub** | [Micro-sheep/efinance](https://github.com/Micro-sheep/efinance) |
| **PyPI** | `pip install efinance` |
| **MCP支持** | ❌ |
| **核心特性** | 跨市场接口抽象，一致的数据访问体验；支持A股/港股/美股/基金 |
| **适用场景** | 需要统一 API 访问多市场数据的轻量级场景 |

### 17. EasyTrader

| 维度 | 详情 |
|------|------|
| **GitHub** | [shidenggui/easytrader](https://github.com/shidenggui/easytrader) |
| **MCP支持** | ❌ |
| **核心特性** | 同花顺/国金/华泰/雪球程序化交易接口；基金和股票自动交易 |
| **适用场景** | 国内券商客户端自动化操作（非API级，基于UI自动化） |

### 18. Market Data Python SDK

| 维度 | 详情 |
|------|------|
| **官网** | [marketdata.app](https://www.marketdata.app/) |
| **MCP支持** | ❌ |
| **核心特性** | 美股股票和期权实时/历史数据；pandas/polars 输出支持；REST + WebSocket |
| **适用场景** | 需要高质量美股期权数据的付费用户 |

### 19. Alpha Vantage Python SDK

| 维度 | 详情 |
|------|------|
| **PyPI** | `pip install alpha_vantage` |
| **MCP支持** | ✅ 通过社区 MCP 桥接 |
| **核心特性** | 股票/期货/加密货币/外汇实时和历史数据；免费层级：25请求/天 |
| **适用场景** | 全球市场数据获取，适合学习和小规模应用 |

### 20. iTick Java SDK

| 维度 | 详情 |
|------|------|
| **官网** | [itick.org](https://itick.org) |
| **MCP支持** | ✅ 通过 alltick-stock-mcp-server 桥接 |
| **核心特性** | Java 版本 iTick API SDK；基础数据/IPO/除权除息/实时数据/WebSocket 订阅 |
| **适用场景** | Java 技术栈的金融数据接入 |

---

## 三、期货交易工具（6个）

### 21. vn.py (VeighNa)

| 维度 | 详情 |
|------|------|
| **GitHub** | [vnpy/vnpy](https://github.com/vnpy/vnpy)（⭐27,800+） |
| **CTP接口** | [vnpy/vnpy_ctp](https://github.com/vnpy/vnpy_ctp) |
| **最新版本** | v4.0.0（Python 3.12 支持） |
| **MCP支持** | ❌ 无原生 MCP（可自建桥接） |
| **核心特性** | 149家期货公司 CTP 接入；五大期货交易所全品种；15类预置风控规则；Tick级精度回测；事件驱动 + asyncio 混合架构；"策略即对象"范式 |
| **适用场景** | **国内期货量化交易的事实标准**，从学习到千万级资金实盘全覆盖 |

### 22. RQAlpha

| 维度 | 详情 |
|------|------|
| **GitHub** | [ricequant/rqalpha](https://github.com/ricequant/rqalpha)（⭐5,983） |
| **PyPI** | `pip install rqalpha`（v6.1.4，2026.04） |
| **MCP支持** | ❌ |
| **核心特性** | 灵活配置；Mod 模块化扩展（可对接 VNPY/TuShare/Sentry）；内置风控/模拟撮合/交易税费计算；多品种支持（股票+期货） |
| **适用场景** | 需要米筐生态的策略回测，中文社区友好 |

### 23. Backtrader

| 维度 | 详情 |
|------|------|
| **GitHub** | [mementum/backtrader](https://github.com/mementum/backtrader)（⭐13,900+） |
| **活跃 Fork** | [dennisdeh/backtrader-slim](https://github.com/dennisdeh/backtrader-slim)（2025年7月活跃，Python 3.10+） |
| **MCP支持** | ❌ |
| **核心特性** | 122个内置指标；事件驱动架构；多资产/多时间周期回测；GPLv3 开源；backtrader-slim 持续现代化 |
| **注意** | 原版 2023年后停止更新，推荐使用 backtrader-slim fork |
| **适用场景** | Python 回测入门学习，成熟文档和丰富社区教程 |

### 24. QuantConnect Lean

| 维度 | 详情 |
|------|------|
| **GitHub** | [QuantConnect/Lean](https://github.com/QuantConnect/Lean) |
| **语言** | C#（支持 Python 策略） |
| **MCP支持** | ✅ 官方 MCP（见 #4） |
| **核心特性** | 事件驱动/模块化设计；股票/期货/期权/外汇/加密货币全资产；云端回测 + 本地部署；Apache 2.0 开源 |
| **适用场景** | 机构级多资产算法交易引擎 |

### 25. CTP API

| 维度 | 详情 |
|------|------|
| **接口标准** | 中国期货市场官方交易接口（上期所技术支持） |
| **Python桥接** | vn.py_ctp / openctp / ctpwrapper |
| **MCP支持** | ❌（底层 API，需桥接） |
| **核心特性** | 几乎所有国内期货公司支持；低延迟；C++/Java/C#/Python 多语言 |
| **适用场景** | 期货实盘交易的必要接口 |

### 26. Futures API（AKShare 期货模块）

| 维度 | 详情 |
|------|------|
| **GitHub** | [akfamily/akshare](https://github.com/akfamily/akshare)（见 #15） |
| **MCP支持** | ✅ 通过 China Stock MCP Server 桥接 |
| **核心特性** | 实时行情、历史数据、持仓分析；上海/大连/郑州/中金所/广期所全覆盖 |
| **适用场景** | 免费获取国内期货数据的首选方案 |

---

## 四、基金与资产管理工具（6个）

### 27. Fund API（AKShare 基金模块）

| 维度 | 详情 |
|------|------|
| **数据源** | [akfamily/akshare](https://github.com/akfamily/akshare) 基金 API |
| **MCP支持** | ✅ 间接 |
| **核心特性** | 公募基金净值/持仓/业绩/分红全覆盖 |
| **适用场景** | 基金投研数据获取 |

### 28. Portfolio Manager（vn.py 内置模块）

| 维度 | 详情 |
|------|------|
| **GitHub** | [vnpy/vnpy_portfoliomanager](https://github.com/vnpy/vnpy_portfoliomanager) |
| **MCP支持** | ❌ |
| **核心特性** | 委托成交记录管理；仓位自动跟踪；盈亏实时统计 |
| **适用场景** | 多策略组合管理，实时盈亏监控 |

### 29. Crypto Funds MCP

| 维度 | 详情 |
|------|------|
| **定位** | 加密货币基金数据 MCP 服务器 |
| **核心特性** | 基金列表/搜索/基本指标/团队信息 |
| **适用场景** | 加密基金投研 |

### 30. PyPortfolioOpt

| 维度 | 详情 |
|------|------|
| **GitHub** | [robertmartin8/PyPortfolioOpt](https://github.com/robertmartin8/PyPortfolioOpt)（⭐4,600+） |
| **MCP支持** | ❌ |
| **核心特性** | 均值-方差有效前沿；Black-Litterman 模型；层次风险平价（HRP）；条件风险价值（CVaR）优化；MIT 开源 |
| **适用场景** | 经典投资组合理论的 Python 实现，教学和研究的首选 |

### 31. Riskfolio-Lib

| 维度 | 详情 |
|------|------|
| **GitHub** | [dcajasn/Riskfolio-Lib](https://github.com/dcajasn/Riskfolio-Lib)（⭐3,100+） |
| **最新版本** | v7.0.1（2025年5月） |
| **MCP支持** | ❌ |
| **核心特性** | 24种凸风险度量；25种风险平价方法；35种层次聚类风险度量（HRP/HERC/NCO）；支持 MOSEK/GUROBI 商业求解器 |
| **适用场景** | **工业级投资组合优化**，功能远超 PyPortfolioOpt |

### 32. QuantConnect Portfolio Optimization

| 维度 | 详情 |
|------|------|
| **定位** | QuantConnect MCP 内置模块（见 #4） |
| **核心特性** | 基于 Huber Downward Risk 最小化的稀疏投资组合优化 |
| **适用场景** | 在 QuantConnect 生态内进行投资组合优化 |

---

## 五、量化交易框架（7个）

### 33. Qbot

| 维度 | 详情 |
|------|------|
| **GitHub** | [UFund-Me/Qbot](https://github.com/UFund-Me/Qbot) |
| **最新版本** | V3.1.15（2025.05.14） |
| **MCP支持** | ❌ |
| **核心特性** | **300+ AI模型 / 40+论文复现**：XGBoost/LightGBM/CatBoost/LSTM/GRU/Transformer/FinGPT；AI自动量化交易全闭环；wxPython GUI + Web分析前端；支持中泰XTP/华鑫奇点/华锐ATP/CTP等多券商 |
| **适用场景** | AI驱动的全栈量化投研平台，适合希望一站式搞定"数据→模型→回测→实盘"的个人/小团队 |

### 34. Qlib

| 维度 | 详情 |
|------|------|
| **GitHub** | [microsoft/qlib](https://github.com/microsoft/qlib)（⭐31,900+） |
| **安装** | `pip install pyqlib` |
| **MCP支持** | ❌（可自建桥接） |
| **核心特性** | **2024年重大更新**：RD-Agent（LLM驱动自动因子挖掘+模型优化）；RD-Agent-Quant（多Agent框架，数据为中心的因子和模型联合优化）；30+ SOTA 模型；高性能二进制数据引擎（比传统快数十倍）；已服务国内 Top5 券商中的3家（研发效率提升40%+）；数据处理：10年分钟级从72h缩短到8h |
| **适用场景** | **AI量化投资平台的金标准**，适合有机器学习背景的量化团队 |

### 35. Freqtrade

| 维度 | 详情 |
|------|------|
| **GitHub** | [freqtrade/freqtrade](https://github.com/freqtrade/freqtrade) |
| **最新要求** | Python 3.11+（2025年7月起） |
| **MCP支持** | ❌ |
| **核心特性** | 2025年每月发版；FreqAI（自适应ML预测建模）；Hyperopt（超参数优化）；内置 WebUI + Telegram 远程控制；10+ 加密交易所（含 Hyperliquid DEX）；SQLite 持久化；Dry-run 模拟交易 |
| **适用场景** | **加密货币算法交易最成熟的开源机器人** |

### 36. QuantDinger

| 维度 | 详情 |
|------|------|
| **GitHub** | [brokermr810/QuantDinger](https://github.com/brokermr810/QuantDinger)（⭐3,100+，Apache 2.0） |
| **最新版本** | v2.0.2（2025年，13位贡献者） |
| **MCP支持** | ❌ |
| **核心特性** | **Vibe Coding**：自然语言描述→AI生成Python策略→回测→实盘；**7 Agent AI分析引擎**：并行分析→多空辩论→最终决策；5+ LLM供应商（OpenRouter/OpenAI/Gemini/DeepSeek/Grok）；Docker Compose 2分钟部署；Vue.js + Flask + PostgreSQL |
| **适用场景** | **零代码量化交易**，适合想让AI自动生成策略的交易者 |

### 37. Zipline（zipline-reloaded）

| 维度 | 详情 |
|------|------|
| **GitHub** | [stefan-jansen/zipline-reloaded](https://github.com/stefan-jansen/zipline-reloaded)（维护者：Stefan Jansen） |
| **PyPI** | `pip install zipline-reloaded`（v3.0+，支持 Python 3.9-3.12） |
| **新项目** | [Limex-com/ziplime](https://github.com/Limex-com/ziplime)（基于 Polars 重构） |
| **MCP支持** | ❌ |
| **核心特性** | 事件驱动回测；Pipeline API（因子研究/股票筛选）；pyfolio + alphalens 集成；pandas 2.x / NumPy 2.0 兼容 |
| **适用场景** | 经典事件驱动回测，Quantopian 遗留策略迁移 |

### 38. VectorBT

| 维度 | 详情 |
|------|------|
| **GitHub** | [polakowo/vectorbt](https://github.com/polakowo/vectorbt) |
| **MCP支持** | ❌ |
| **核心特性** | 向量化 + Numba JIT 编译，**比传统框架快100倍+**；N维矩阵并行回测；Plotly 交互可视化；Yahoo Finance + CCXT 数据源；支持大规模参数网格搜索 |
| **适用场景** | **最高性能回测**，中高级量化交易者的策略迭代利器 |

### 39. Backtesting.py

| 维度 | 详情 |
|------|------|
| **GitHub** | [kernc/backtesting.py](https://github.com/kernc/backtesting.py)（⭐活跃，42位贡献者） |
| **最新版本** | v0.6.5（2025.07.30） |
| **MCP支持** | ❌ |
| **核心特性** | 2025年6+版本发布（极快迭代）；MultiBacktest（多品种并行回测）；FractionalBacktest（小数单位交易）；SAMBO优化器；Bokeh 交互图表；TrailingStrategy（百分比跟踪止损） |
| **适用场景** | **最活跃的回测框架**，简洁至上，适合快速策略原型验证 |

---

## 六、投研与分析工具（7个）

### 40. TA-Lib

| 维度 | 详情 |
|------|------|
| **GitHub** | [TA-Lib/ta-lib-python](https://github.com/TA-Lib/ta-lib-python)（Cython 封装，替代 SWIG 版） |
| **PyPI** | `pip install TA-Lib`（v0.5.5，支持 NumPy 2 + Polars） |
| **MCP支持** | ❌ |
| **核心特性** | 150+ 技术指标（MACD/RSI/布林带/ADX/Stochastic等）；63种蜡烛图形态识别；C 底层，纯 Python 封装的 2-4 倍速度 |
| **注意** | 需系统预装 TA-Lib C 库（Windows 推荐 Conda 安装） |
| **适用场景** | **技术分析指标金标准**，几乎所有量化框架的底层依赖 |

### 41. Pandas TA

| 维度 | 详情 |
|------|------|
| **GitHub** | [twopirllc/pandas-ta](https://github.com/twopirllc/pandas-ta) |
| **PyPI** | `pip install pandas-ta`（v0.4.71b0，2025年） |
| **MCP支持** | ❌ |
| **核心特性** | 150+ 指标 + 60种蜡烛图形态；`df.ta` 扩展语法（深度 Pandas 集成）；Numba JIT 加速；多进程批量计算（Strategy 类）；可选 TA-Lib 后端加速 |
| **注意** | 维护者告警可能于2026年7月归档，建议关注社区 Fork |
| **适用场景** | Pandas 用户的"一键技术分析"方案 |

### 42. FinBERT

| 维度 | 详情 |
|------|------|
| **HuggingFace** | [ProsusAI/finbert](https://huggingface.co/ProsusAI/finbert) |
| **增强版** | [project-aps/finbert-finetune](https://github.com/project-aps/finbert-finetune)（+38%准确率提升，2025年） |
| **市场版** | [baptle/FinBERT_market_based](https://huggingface.co/baptle/FinBERT_market_based)（基于市场反应训练，GPT-4对比中+15%精确率） |
| **MCP支持** | ❌（可自建封装） |
| **核心特性** | 金融文本三分类（正面/负面/中性）；基于 BERT 在 ~4.9B token 金融语料上预训练；Fine-tune 版达到 ~99% 准确率（Financial PhraseBank）；**小模型可超越 GPT-3.5/GPT-4 零样本金融情感分析** |
| **适用场景** | 财报情绪分析、新闻情感评分、市场舆情监控 |

### 43. Deep Research Engine（FinMCP 内置）

| 维度 | 详情 |
|------|------|
| **所属** | [Finance-LLMs/FinMCP](https://github.com/Finance-LLMs/FinMCP)（见 #12） |
| **MCP支持** | ✅ |
| **核心特性** | AI 驱动的迭代研究引擎；网页抓取 + 内容合成 |
| **适用场景** | 自动化金融研究报告生成 |

### 44. News Service（Finance Trading AI Agents MCP 内置）

| 维度 | 详情 |
|------|------|
| **所属** | [aitrados/finance-trading-ai-agents-mcp](https://github.com/aitrados/finance-trading-ai-agents-mcp)（见 #8） |
| **MCP支持** | ✅ |
| **核心特性** | 实时新闻获取和分析服务；多智能体架构中的新闻分析师角色 |
| **适用场景** | AI 交易系统中的新闻事件驱动分析 |

### 45. Economic Calendar

| 维度 | 详情 |
|------|------|
| **主要来源** | Finnhub MCP / Finance Trading AI Agents MCP / Alpha Vantage |
| **MCP支持** | ✅ 多个 MCP 服务器内置 |
| **核心特性** | 全球重要经济事件和数据发布时间；利率决议/非农/GDP/CPI等 |
| **适用场景** | 宏观事件驱动交易策略 |

### 46. Financial Modeling Prep API

| 维度 | 详情 |
|------|------|
| **官网** | [financialmodelingprep.com](https://financialmodelingprep.com) |
| **MCP实现** | [kablewy/financial-analysis-mcp-server](https://github.com/kablewy/financial-analysis-mcp-server)（Alpha Vantage + FMP 双API） |
| **MCP支持** | ✅ 社区实现 |
| **核心特性** | 公司财务报表/估值/市场数据全覆盖 |
| **适用场景** | 美股基本面深度分析 |

---

## 七、短线交易与高频工具（5个）

### 47. CryptoAnalysisMCP

| 维度 | 详情 |
|------|------|
| **GitHub** | [M-Pineapple/CryptoAnalysisMCP](https://github.com/M-Pineapple/CryptoAnalysisMCP) |
| **技术栈** | Swift 5.5+（macOS 10.15+） |
| **最新版本** | v1.1（2025年，700万+ tokens，DexPaprika集成） |
| **MCP支持** | ✅ 原生 MCP |
| **核心特性** | 实时技术指标（RSI/MACD/均线/布林带）；图表模式检测（头肩顶/三角形/双顶双底）；支撑阻力自动识别；多时间框架分析；23+区块链 DEX 数据；交易信号（保守/中性/激进三档） |
| **适用场景** | 加密货币技术分析的 AI 助手，macOS 用户 |

### 48. Live Streaming OHLC Service

| 维度 | 详情 |
|------|------|
| **所属** | [aitrados/finance-trading-ai-agents-mcp](https://github.com/aitrados/finance-trading-ai-agents-mcp)（见 #8） |
| **MCP支持** | ✅ 内置 |
| **核心特性** | 实时 OHLC 数据流处理；WebSocket 连接管理 |
| **适用场景** | AI Agent 的实时行情推送 |

### 49. Tick Data Recorder（vn.py 内置）

| 维度 | 详情 |
|------|------|
| **所属** | [vnpy/vnpy](https://github.com/vnpy/vnpy) 行情记录模块（见 #21） |
| **MCP支持** | ❌ |
| **核心特性** | 图形界面配置；实时录制 Tick/K线行情到数据库 |
| **适用场景** | 期货 Tick 级别数据积累和回放 |

### 50. WebSocket API（实时数据）

| 维度 | 详情 |
|------|------|
| **主要提供者** | iTick（REST+WS+FIX）/ Alpha Vantage / Alpaca / IBKR |
| **MCP支持** | ✅ 部分集成（iTick / Alpaca） |
| **核心特性** | 实时数据推送，低延迟，适合高频交易 |
| **适用场景** | 需要实时行情的高频/日内策略 |

### 51. C++ QuantLib

| 维度 | 详情 |
|------|------|
| **GitHub** | [lballabio/QuantLib](https://github.com/lballabio/QuantLib) |
| **Python 绑定** | [lballabio/QuantLib-SWIG](https://github.com/lballabio/QuantLib-SWIG)（v1.39，2025.07） |
| **最新版本** | v1.39（2025.07）/ v1.40（2025.10，FreshPorts） |
| **MCP支持** | ❌（可自建 Python 桥接） |
| **核心特性** | 定价/风险/数值计算全功能；2024-2025年 C++17 现代化（弃用 Boost → std）；SARON 指数 / 部分时间障碍期权 / SABR校准改进；Python 自由线程初步支持（PEP 703） |
| **适用场景** | 低延迟定价和风险管理，机构级衍生品定价 |

---

## 八、风投与另类投资工具（5个）

### 52. Crunchbase API

| 维度 | 详情 |
|------|------|
| **官网** | [crunchbase.com](https://www.crunchbase.com) |
| **MCP支持** | ❌ |
| **核心特性** | 全球初创公司/投资者/融资轮次数据 |
| **适用场景** | VC 行业研究、融资趋势分析、竞品追踪 |

### 53. PitchBook API

| 维度 | 详情 |
|------|------|
| **官网** | [pitchbook.com](https://pitchbook.com) |
| **MCP支持** | ❌ |
| **核心特性** | PE/VC 市场专业数据平台 |
| **适用场景** | 私募股权投资研究，机构级非公开市场数据 |

### 54. AngelList API

| 维度 | 详情 |
|------|------|
| **官网** | [angellist.com](https://www.angellist.com)（现为 Wellfound） |
| **MCP支持** | ❌ |
| **核心特性** | 天使投资/初创公司数据 |
| **适用场景** | 早期投资标的发现 |

### 55. CB Insights API

| 维度 | 详情 |
|------|------|
| **官网** | [cbinsights.com](https://www.cbinsights.com) |
| **MCP支持** | ❌ |
| **核心特性** | 科技行业/VC 研究报告和数据 |
| **适用场景** | 科技产业分析和投资趋势研究 |

### 56. Alternative Data API（Finnhub 等）

| 维度 | 详情 |
|------|------|
| **主要提供者** | Finnhub / Alpha Vantage / Quandl |
| **MCP支持** | ✅ 通过 Finnhub MCP 等桥接 |
| **核心特性** | 卫星图像/信用卡消费/网络流量/社交媒体情绪等非传统数据 |
| **适用场景** | 量化因子的差异化 Alpha 来源 |

---

## 九、Claude Code Skills 开箱即用（12个）

> **什么是 Skill？** Claude Code 的原生扩展机制。一个 Skill 就是一个带 YAML frontmatter 的 Markdown 文件（`SKILL.md`），放入 `.claude/skills/` 目录即可通过 `/` 斜杠命令调用。Skills 比 MCP 更进一步：**无需启动外部服务，直接在 Claude Code 对话中运行**，支持子代理并发、自动触发、模型覆盖等高级特性。

### Skills vs MCP：选型速查

| 维度 | MCP Server | Claude Code Skill |
|------|-----------|-------------------|
| **安装方式** | 启动外部进程（Python/Node/Docker） | 复制 `.md` 文件到 `.claude/skills/` |
| **调用方式** | AI 自动选择 MCP 工具 | `/command` 斜杠命令 或 AI 自动触发 |
| **运行环境** | 独立进程，需持续运行 | Claude Code 内置，零额外资源 |
| **适用场景** | 实时数据推送、交易执行、WebSocket | 分析工作流、多智能体协作、报告生成 |
| **并发能力** | 取决于服务端实现 | 原生支持子代理并行 |
| **离线可用** | ❌ 依赖外部服务 | ✅ 纯工作流编排可离线 |

### 安装方式速查

```bash
# 方式一：Claude Code 插件市场（推荐）
/plugin marketplace add <owner>/<repo>
/plugin install <plugin-name>

# 方式二：手动安装 Skills
git clone <repo>
cp -r <repo>/.claude/skills/* .claude/skills/
# 或
cp <repo>/*.skill.md .claude/skills/<name>/SKILL.md

# 方式三：npx 社区工具
npx skills add <owner>/<repo>

# 验证安装
/help  # 查看所有可用命令
```

---

### 57. TradingAgents — 多智能体交易团队

| 维度 | 详情 |
|------|------|
| **GitHub** | [gonewx/TradingAgents](https://github.com/gonewx/TradingAgents) |
| **安装** | `git clone` → 复制 `.claude/skills/` 目录 |
| **调用方式** | `/trade-analyze AAPL`, `/market-scan 半导体`, `/portfolio-review`, `/risk-assessment NVDA`, `/backtest 双均线策略`, `/memory-train` |
| **子代理数** | 13个（market-analyst, fundamentals-analyst, news-analyst, social-analyst, bull/bear-researcher, trader, risk-manager, portfolio-manager, 3个风险偏好分析师） |
| **数据源** | yfinance（免费无限）, Alpha Vantage（500次/天）, Google News, Reddit sentiment |
| **特色** | SQLite记忆系统（越用越准）；多空辩论机制（Bull vs Bear → 最终决策）；支持 A/港/美股 |
| **安全边界** | ⚠️ 仅用于技术研究，禁止实际投资用途 |

### 58. Claude Equity Research — 机构级个股研报

| 维度 | 详情 |
|------|------|
| **GitHub** | [quant-sentiment-ai/claude-equity-research](https://github.com/quant-sentiment-ai/claude-equity-research) |
| **安装** | `/plugin marketplace add quant-sentiment-ai/claude-equity-research` → `/plugin install` |
| **调用方式** | `/trading-ideas AAPL` 或 `/trading-ideas NVDA --detailed` |
| **报告结构** | 8 个模块（基本面/技术面/催化剂/估值/风险/仓位/内部人信号/ESG） |
| **输出** | BUY/SELL/HOLD 评级 + 目标价 + 置信度 + 仓位建议 |
| **数据源** | 实时市场数据、SEC Filing、分析师覆盖、期权流 |
| **特色** | 零配置（安装即用，无需 API Key）；Goldman Sachs 风格报告 |
| **安全边界** | ⚠️ 教育用途，不构成投资建议 |

### 59. Stock Deep Research Agent — 8阶段尽职调查

| 维度 | 详情 |
|------|------|
| **GitHub** | [liangdabiao/Claude-Code-Stock-Deep-Research-Agent](https://github.com/liangdabiao/Claude-Code-Stock-Deep-Research-Agent)（MIT, ⭐291） |
| **安装** | `git clone` → 复制 `.claude/` 到项目目录 |
| **调用方式** | `/stock-research AAPL` 或 `/stock-research 600519`（贵州茅台） |
| **流程** | 8阶段：商业基础 → 行业分析 → 业务拆分 → 财务质量 → 治理 → 市场情绪 → 估值护城河 → 综合报告 |
| **子代理数** | ~28 个并行研究代理 |
| **输出** | 完整尽调报告（20+文件），含 DCF/反向DCF/相对估值/情景分析 |
| **耗时** | 2-4小时（标准尽调） |
| **特色** | 多空平衡、数据交叉验证、来源A-E评级；支持 A/港/美股 |
| **安全边界** | ⚠️ 不提供投资建议，信号评级仅供基本面参考 |

### 60. ConsensusAI — 12位投资大师共识决策

| 维度 | 详情 |
|------|------|
| **GitHub** | [ancs21/ai-sub-invest](https://github.com/ancs21/ai-sub-invest) |
| **安装** | `git clone` → `uv sync`（需 Python 3.11+） |
| **调用方式** | 对话式：`"Analyze AAPL like Warren Buffett"` 或 `"Run all analysts on TSLA"`；SDK：`uv run python src/sdk_main.py AAPL,MSFT,NVDA 2025-12-06 --cash 50000` |
| **12位分析师** | 巴菲特（价值）、芒格（心智模型）、格雷厄姆（深度价值）、林奇（GARP）、费雪（15点清单）、Burry（逆向）、Pabrai（Dhandho）、Ackman（激进）、Wood（颠覆创新）、Druckenmiller（宏观）、Jhunjhunwala（新兴市场）、Damodaran（DCF估值） |
| **9项分析技能** | 基本面、技术面、估值（DCF）、情绪、新闻情绪、增长分析、风险管理、投资组合管理、财务数据 |
| **特色** | 所有分析师并行运行 → 信号聚合 → 共识买卖建议 + 置信度评分 |
| **安全边界** | ⚠️ 仅供教育/研究 |

### 61. claude-trading-skills — 50+交易技能包

| 维度 | 详情 |
|------|------|
| **GitHub** | [tradermonty/claude-trading-skills](https://github.com/tradermonty/claude-trading-skills)（⭐533+） |
| **文档** | [tradermonty.github.io/claude-trading-skills](https://tradermonty.github.io/claude-trading-skills/) |
| **安装** | 复制 `.skill` 文件到 `.claude/skills/` |
| **核心 Skills（精选）** |  |
| | `market-breadth-analyzer` — 市场宽度分析 |
| | `uptrend-analyzer` — 上升趋势确认 |
| | `exposure-coach` — 仓位暴露建议 |
| | `portfolio-manager` — 投资组合管理 |
| | `value-dividend-screener` — 价值股息筛选 |
| | `vcp-screener` — VCP形态筛选（Volatility Contraction Pattern） |
| | `canslim-screener` — CANSLIM选股法（William O'Neil体系） |
| | `breakout-trade-planner` — 突破交易计划 |
| | `position-sizer` — 仓位大小计算 |
| | `technical-analyst` — 周线技术分析（道氏/波浪/蜡烛图/支撑阻力/动量） |
| | `trader-memory-core` — 交易记忆（经验积累） |
| | `signal-postmortem` — 交易信号复盘 |
| | `backtest-expert` — 回测专家 |
| | `edge-pipeline-orchestrator` — 策略优势管道编排 |
| | `parabolic-short-trade-planner` — 抛物线做空计划 |
| | `earnings-trade-analyzer` — 财报交易分析 |
| | `options-strategy-advisor` — 期权策略顾问 |
| **API需求** | 部分需 FMP / FINVIZ Elite / Alpaca；部分仅需免费数据源（GitHub CSV / yfinance） |
| **特色** | **最全面的交易 Skills 集合**；涵盖选股→技术分析→仓位→风控→复盘全流程 |
| **安全边界** | ⚠️ 仅供教育/研究用途 |

### 62. Autonomous Trading Skill — 全自动定时交易

| 维度 | 详情 |
|------|------|
| **来源** | [claude-plugins.dev](https://claude-plugins.dev/skills/@AkhilGurrapu/kubera/autonomous-trading)（@AkhilGurrapu） |
| **安装** | 插件市场安装 |
| **执行时间表** | 盘前筛选(9:00) → 开盘交易(9:30) → 午盘检查(12:00) → 收盘总结(16:00) |
| **工作流** | 自动选股(NASDAQ 100 多维度评分) → 多模型分析 → 自动执行 → Telegram 通知 |
| **券商** | Alpaca Paper Trading（模拟交易） |
| **特色** | 完全无人值守；Cron 定时调度；Telegram 实时通知 |
| **安全边界** | ⚠️ 默认纸交易，可切实盘（谨慎） |

### 63. Quantitative Trading System (QTS) — 量化交易插件套件

| 维度 | 详情 |
|------|------|
| **GitHub** | [jmanhype/claude-code-plugin-marketplace](https://github.com/jmanhype/claude-code-plugin-marketplace)（23个插件） |
| **安装** | `/plugin marketplace add jmanhype/claude-code-plugin-marketplace` |
| **交易相关插件** | `quant-trading-system`（策略/风控/执行/市场情报/研究管道）、`market-intelligence`（市场分析代理定义）、`tournament-runner`（策略锦标赛）、`swarm-coordination`（群体智能）、`consensus-protocols`（共识协议） |
| **特色** | 纸交易 + CCXT 实盘；风控默认：1x杠杆上限/单标的25%上限/-5%日止损/-10%最大回撤；支持 ETH/SOL/XRP 等多币种 |
| **安全边界** | ⚠️ 风控参数可配置，实盘需谨慎 |

### 64. NautilusTrader Skill — 专业算法交易平台

| 维度 | 详情 |
|------|------|
| **来源** | [claude-plugins.dev](https://claude-plugins.dev/skills/@Patrick-code-Bot/nautilus_AItrader/nautilustrader) |
| **安装** | 插件市场安装 |
| **核心能力** | 策略构建/回测/实盘/数据处理；完整策略生命周期（订单/持仓/风控/时钟/定时器） |
| **底层** | [NautilusTrader](https://github.com/nautechsystems/nautilus_trader)（高性能Rust+Python算法交易平台） |
| **特色** | 机构级性能（Rust核心）；Python策略开发；多交易所支持 |
| **安全边界** | ⚠️ 支持实盘，需自行评估风险 |

### 65. Claude Code Trading Terminal — Solana链上交易终端

| 维度 | 详情 |
|------|------|
| **GitHub** | [degentic-tools/claude-code-trading-terminal](https://github.com/degentic-tools/claude-code-trading-terminal) |
| **安装** | `git clone` → 配置 `.claude/` |
| **核心能力** | 多DEX聚合 (Jupiter/Raydium/Meteora)；限价单/止损/止盈/DCA；PumpFun Meme币工具（风险评估/趋势扫描/快速买入）；做市机器人（50/50再平衡） |
| **数据** | WebSocket实时数据管道 |
| **风控** | 3级仓位管理系统 |
| **特色** | 专为 Solana 链上交易设计；Agent-Native 架构 |
| **安全边界** | ⚠️ 链上交易，资金风险极高 |

### 66. Anthropic 官方金融服务插件

| 维度 | 详情 |
|------|------|
| **来源** | Anthropic 官方 |
| **安装** | `claude plugin marketplace add anthropics/financial-services-plugins` |
| **覆盖领域** | 投资银行、股票研究、私募股权、财富管理 |
| **数据连接器** | FactSet, PitchBook, S&P Global, Morningstar, Daloopa, Moody's 等 11 家 |
| **特色** | **唯一官方支持的金融服务插件**；企业级数据合规；SOC 2 Type 2 |
| **适用场景** | 专业金融机构，需要合规数据源的企业用户 |

### 67. AI Neural Trader — 神经网络预测交易

| 维度 | 详情 |
|------|------|
| **来源** | [CyberBedouinMonk Gist](https://gist.github.com/CyberBedouinMonk/bc9f1bd95f72c3e66a624b97bab32e0a) |
| **核心模型** | NHITS + NBEATSx 神经预测（+25%准确率提升，<10ms推理） |
| **加速** | CUDA GPU（6250倍加速） |
| **MCP工具** | 41个专业 MCP 工具 |
| **集成** | Polymarket 预测市场交易 + SPARC 17 种专业模式 |
| **特色** | 首个将神经预测 + MCP + Claude Code 深度集成的系统 |
| **安全边界** | ⚠️ 实验性项目 |

### 68. SuperClaude v3 — 增强型配置框架

| 维度 | 详情 |
|------|------|
| **GitHub** | [MCPVOT/SuperClaude](https://github.com/MCPVOT/SuperClaude) |
| **安装** | `git clone` → 配置 |
| **斜杠命令** | 16个（`/sc:implement`, `/sc:build`, `/sc:design`, `/sc:analyze` 等） |
| **特色** | 智能 Persona 系统（架构师/前端/后端/安全等）；生产级交易系统集成 |
| **适用场景** | 需要统一 Claude Code 配置管理的团队 |

---

### Skills 组合推荐

| 投资风格 | 推荐 Skills 组合 | 安装时间 |
|----------|-----------------|---------|
| **A股价值投资** | Stock Deep Research (#59) + claude-trading-skills (#61) + TradingAgents (#57) | 15分钟 |
| **美股基本面** | claude-equity-research (#58) + ConsensusAI (#60) + Financial Services (#66) | 10分钟 |
| **加密货币短线** | Trading Terminal (#65) + QTS (#63) + AI Neural Trader (#67) | 20分钟 |
| **量化策略开发** | NautilusTrader (#64) + Autonomous Trading (#62) + QTS (#63) | 25分钟 |
| **全自动无人值守** | Autonomous Trading (#62) + QTS (#63) + TradingAgents (#57) | 20分钟 |

---

## 快速集成建议

### 分层部署架构（MCP + Skills 融合）

```
┌──────────────────────────────────────────────────────┐
│  Skills 层    │ /trade-analyze → 13 子代理并行分析     │
│  (斜杠命令)   │ /stock-research → 28 代理深度尽调      │
│               │ /trading-ideas → 8 模块机构研报        │
│               │ /canslim-screener → CANSLIM 选股       │
├──────────────────────────────────────────────────────┤
│  MCP 网关     │ Stock MCP + FinanceMCP + Alpaca MCP   │
│  (数据+交易)  │ → 56 个 MCP 工具提供行情/下单/风控     │
├──────────────────────────────────────────────────────┤
│  策略引擎     │ Qlib (AI因子挖掘) + Backtrader (回测)   │
│  (回测&优化)  │ + VectorBT (高速参数扫描)              │
├──────────────────────────────────────────────────────┤
│  数据层       │ AKShare (中国) + yfinance (美股)        │
│  (行情&基本面)│ + Tushare (补充) + CCXT (加密)          │
├──────────────────────────────────────────────────────┤
│  风控层       │ vn.py Risk Manager + QTS风控参数        │
│  (交易流控)   │ + 自建风险仪表盘                        │
└──────────────────────────────────────────────────────┘
```

### 按市场的最强组合（Skills优先）

| 市场 | Skills（/命令） | MCP 网关 | 策略引擎 | 执行层 |
|------|----------------|---------|--------|--------|
| **A股** | /stock-research + /trade-analyze | FinanceMCP (#11) | Qlib (#34) | EasyTrader (#17) |
| **美股** | /trading-ideas + ConsensusAI | Alpaca MCP (#5) | VectorBT (#38) | Alpaca/IB MCP (#5/#10) |
| **期货** | /backtest + claude-trading-skills | Smart Financial (#7) | vn.py (#21) | vn.py + CTP (#25) |
| **加密** | Trading Terminal + QTS | CryptoAnalysisMCP (#47) | Freqtrade (#35) | QuantDinger (#36) |

### 最小可用集（5分钟启动）

```bash
# === MCP 层（行情+交易） ===
npx -y finance-mcp                  # 中国金融数据
uvx alpha-vantage-mcp-server        # 全球市场数据

# === Skills 层（分析+决策） ===
/plugin marketplace add quant-sentiment-ai/claude-equity-research
git clone https://github.com/liangdabiao/Claude-Code-Stock-Deep-Research-Agent
cp -r Claude-Code-Stock-Deep-Research-Agent/.claude/* .claude/

# === 验证 ===
/stock-research AAPL       # 深度尽调
/trading-ideas NVDA         # 机构研报
```

### 从零到AI交易员的推荐路线

| 阶段 | 工具 | 投入 | 目标 |
|------|------|------|------|
| **第1天** | Stock Deep Research (#59) + TradingAgents (#57) | 0元，30分钟 | 能用 `/` 命令生成个股深度报告 |
| **第1周** | + FinanceMCP (#11) + AKShare (#15) | 0元，2小时配置 | 覆盖 A股/港股 实时数据 |
| **第1月** | + claude-trading-skills (#61) + Backtrader (#23) | 0元，1周学习 | 掌握技术分析 + 回测能力 |
| **第3月** | + Alpaca MCP (#5) + Qlib (#34) | Alpaca API Key | 美股 AI 模型 + 纸交易 |
| **第6月** | + vn.py (#21) + CTP (#25) | 期货开户 | 期货实盘交易 |

---

> **免责声明**：本文所列工具仅供研究和学习用途，不构成投资建议。实盘交易风险自负。
