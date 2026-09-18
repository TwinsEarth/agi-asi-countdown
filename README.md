# AGI / ASI 倒计时网站 v6.3.2（离线静态版）

零依赖、零构建、零后端：**双击 `index.html` 即可在浏览器离线打开（file://）**。
本版在 HCI（能力余量闭合指数）与 RSI 五级路线图之外，新增 **「大模型评测基准：AI 分数是怎么测出来的」** 页签，
并搭好 AGI/ASI 三模块仪表盘骨架。纯静态，所有计算在你浏览器本地完成，可固定种子复现。

## 打开方式
- 直接双击 `index.html`（推荐 Chrome/Edge/Safari）。
- 或起本地服务：`python3 -m http.server 8080` 后访问 http://localhost:8080 。

## 页面与“真东西”对照
| 页签 | 内容 | 证据 |
|---|---|---|
| 总览·倒计时 | 浏览器端蒙特卡洛 10,000 路径（固定种子），输出 p10/p50/p90 与年份概率分布；短板达成度；能力雷达（内联 SVG） | 计算 verified；先验/雷达分为**示例种子**，待回测 |
| 过去 | EWMA 系数曲线（α=0.3，示例）、六类历史档案库 | 公式真实；曲线为示例，待 collector 数据 |
| 现在 | 六条 AGI 路线进度/ETA、六个评分数据源接入状态 | 结构真实；联网抓取为闸门 |
| 未来 | 预言库、状态、Brier 记分位（0.25=随机基准） | 结构真实；到期人工结算 |
| **v6.3 HCI 余量** | HCI 公式实时计算器、√N 加权聚合演示、10 领域 2026 HCI 条形图、RSI 上限投影 | **公式与文章数值已复算一致（verified）** |
| **v6.3 RSI 路线图** | L1–L5 自主权阶梯、人机责任划分、72 家产业映射、L5 四问 | 内容据 Theseus Labs 公开报告 |
| **v6.3.1 评测基准** | 基准四要素、6 步出分流程（可展开）、四类评分器对照、MMLU/Arena/HELM/LiveBench、分数为何变化、看榜 6 问自检清单（实时打分）、20–50 题自建小评测向导 | 方法学科普，据公开基准资料整理，不含新测量数据 |
| **v6.3.2 引用** | 评测基准页补全 5 篇原文角标与可点击参考来源（MMLU/HELM/Arena/LLM-as-judge/LiveBench） | arXiv 原文链接 |

## 本版核心公式（均在 JS 中实时计算，非写死）
- HCI = (当前分 − 基准分) / (100 − 基准分) × 100；基准=评测首年 p90。
- 领域聚合：各评测当年 HCI 取 p90，再按参与模型数 **√N 加权平均**。
- RSI 理论上限（示意系数 0.22）：R = 100 − 0.22 × (100 − HCI₂₀₂₆)。
  复算：网络安全 91.9→98.2、软件工程 52.6→89.6、搜索终端 56.8→90.5、工具 Agent 39.9→86.8。
- 倒计时：六路线月度进展随机游走（近似正态），10,000 次模拟取分位数。

## 数据来源
Theseus Labs《The Last AI Built by Humans: Toward Genuine Recursive Self-Improvement》
arXiv:2609.11873（HCI、RSI L1–L5、产业信号）。
评测基准页原文：MMLU arXiv:2009.03300、HELM arXiv:2211.09110、Chatbot Arena arXiv:2403.04132、
LLM-as-a-Judge arXiv:2306.05685、LiveBench arXiv:2406.19314。倒计时/能力评分为示例先验，
联网版采集对象：Artificial Analysis、LMArena、LLM-Stats、Epoch AI、OpenCompass、
Metaculus、The AGI Clock、AI 2027 Tracker。

## 明确未做（闸门，需资源，不以静态页冒充）
1. 真实数据闭环：collector + cron 跑 4–12 周、历史数据回测校准 α/权重/蒙特卡洛先验、
   滚动 Brier 与校准曲线（需长期在线服务器）。
2. 多 LLM 交叉评分/LLM-as-judge：需供应商 API key。
3. 后端化：FastAPI + PostgreSQL/TimescaleDB、登录、管理后台（当前为零后端静态版）。
4. 双云生产部署：阿里云（含 ICP 备案、域名、HTTPS）与 Vultr 海外、CI/CD、监控告警、灾备。
5. 实时事件 WebSocket、OTel 可观测接入（引擎侧 v7.3 已有可观测层，网站侧待对接）。

## 与引擎线关系
- 本目录是**网站产品线 v6.x**；UDOS 推演引擎是独立的 v7.x（纯引擎，无网站）。
- 后续：v6.3.x 把本静态页的数据层从“示例种子”切换为真实采集/回测产出的 JSON 快照，
  仍可保持静态优先、离线可开。
