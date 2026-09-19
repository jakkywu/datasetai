<p align="center">
  <img src="assets/app_icon.svg" width="128" alt="幻金 Logo">
</p>

<h1 align="center">幻金</h1>

<p align="center">
  智能财务数据分析工具<br>
  从 A 股财报 PDF 到结构化数据、风险扫描、归因分析与 AI 解读
</p>

<p align="center">
  <a href="../../releases/latest">下载最新版本</a> ·
  <a href="docs/用户手册.md">用户手册</a> ·
  <a href="docs/msix_store_packaging.md">打包文档</a> ·
  <a href="CHANGELOG.md">更新日志</a>
</p>

## 项目简介

幻金是一款面向个人投资者、分析师和金融从业者的 Windows 桌面财务分析工具。它读取 A 股上市公司公开披露的年报、中报和季报，在本地完成 PDF 解析、表格提取、指标计算和风险扫描，并可选接入大语言模型生成辅助解读。

相比只提供数据查询和图表的工具，幻金更关注三件事：

- 从原始财报 PDF 精确提取资产负债表、利润表和现金流量表。
- 通过规则、组合、魔法指标和异常检测识别潜在风险。
- 将指标变化、利润归因、同行对比和风险证据整理成可追溯的报告。

> 所有分析结果均基于公开数据和自动化规则，仅供参考，不构成投资建议。AI 生成内容会在界面中明确标识。

## 主要功能

| 功能 | 说明 |
|---|---|
| 一键下载 | 下载公开财报 PDF，并构建结构化报表和附注指标 |
| 一键尽调 | 执行规则扫描、五维评估、风险核查和 AI 摘要 |
| 财务概览 | 查看核心指标趋势、季度数据、同行分位和异常信号 |
| 年度报告 | 生成完整 HTML 财务报告，支持 PDF 原文溯源 |
| 财务报表 | 展示资产负债表、利润表和现金流量表 |
| 归因分析 | 将利润变动拆解到收入、成本、费用和减值等科目 |
| 积极信号 | 汇总增长、现金流、偿债能力和盈利质量等正向指标 |
| 季度趋势 | 展示近三年单季度营收与归母净利润趋势 |
| 跨公司对比 | 对比多只股票的 ROE、利润率、增长和偿债指标 |
| 选股筛选 | 按财务指标筛选 A 股公司，并查看行业相对位置 |
| 批量下载 | 支持 CSI300、CSI500、CSI1000 和自选股批量处理 |

## 界面预览

<p align="center">
  <img src="docs/assets/ui_snapshot.png" width="49%" alt="幻金财报分析界面">
  <img src="docs/assets/ui_statements.png" width="49%" alt="幻金财务报表界面">
</p>

<p align="center">
  <img src="docs/assets/ui_manage.png" width="72%" alt="幻金数据管理界面">
</p>

## 下载与运行

### 独立运行包

1. 从 [Releases](../../releases/latest) 下载 `DatasetAI.Standalone-<版本>.zip`。
2. 解压到普通可写目录，不要直接在压缩包内运行。
3. 双击 `幻金.exe` 启动。
4. 如安全软件拦截，可将整个程序目录加入白名单；不要单独移动 `_internal` 目录。

运行环境：

- Windows 10/11 64 位
- 建议 16 GB 内存
- 联网用于下载公开财报和可选 AI 分析

### Microsoft Store

同一代码库也支持构建 MSIX 包。商店包与本独立运行包使用相同分析逻辑，但使用不同的分发、授权和更新渠道。具体流程见 [Microsoft Store 打包指南](docs/msix_store_packaging.md)。

## 快速使用

1. 打开「管理」页面，添加股票代码或名称，例如 `600519`。
2. 点击「一键下载」或等待自动下载公开财报。
3. 进入「财报分析」页面，选择公司、年份和报告期。
4. 使用「一键尽调」「财务概览」「年度报告」「归因分析」等功能。
5. 点击指标后的溯源标记，可跳转到财报 PDF 对应页面。

详细说明见 [用户手册](docs/用户手册.md)。

## 数据与隐私

- 财报解析、结构化处理、指标计算和风险规则在本地运行。
- 用户选择的 PDF、下载缓存和分析结果默认保存在本机。
- 联网请求仅用于获取公开披露文件、市场数据，以及用户主动启用的 AI 分析。
- AI 分析需要用户自行配置模型 API，未配置时本地规则与报表功能不受影响。

Windows 默认数据目录：

```text
%LOCALAPPDATA%\DatasetAI\workspaces\
```

可通过设置环境变量 `DATASETAI_WS_ROOT` 或 `DATASETAI_WORKSPACE` 调整工作区位置和名称。

## 分析流程

```text
公开财报 PDF
    ↓
版面解析与表格提取
    ↓
三大报表与附注指标
    ↓
规则 / 魔法 / 组合 / 异常检测
    ↓
趋势、同行对比、归因与评分
    ↓
尽调摘要、财务概览与年度报告
```

核心模块：

| 目录 | 作用 |
|---|---|
| `app/` | PySide6 桌面界面与启动入口 |
| `pipeline/` | PDF 下载、解析、报表提取和转换流程 |
| `analysis/` | 风险规则、归因、异常检测和趋势分析 |
| `core/` | 指标、配置、路径、评分和信号合并 |
| `retrieval/` | 查询、市场数据、同行对比和 AI 接入 |
| `render/` | 财务概览、年度报告、图表和分享卡 |
| `data/` | 股票列表、指数成分和行业缓存 |
| `scripts/` | 构建、审计、数据修复和发布脚本 |

## 从源码运行

环境要求：

- Python 3.11
- Windows 10/11
- PowerShell 5.1 或 PowerShell 7

```powershell
Set-Location D:\wuyue\Work\Code\DatasetAI

python -m venv .venv
.\.venv\Scripts\Activate.ps1
.\.venv\Scripts\python.exe -m pip install --upgrade pip
.\.venv\Scripts\python.exe -m pip install -r requirements.txt

.\.venv\Scripts\python.exe -m app.main
```

开发模式使用仓库下的 `workspaces\`；PyInstaller 和 Store 版本使用 `%LOCALAPPDATA%\DatasetAI\workspaces\`。

## 测试

运行完整测试：

```powershell
.\.venv\Scripts\python.exe -m pytest
```

运行与本次改动相关的测试：

```powershell
.\.venv\Scripts\python.exe -m pytest test\core\test_workspace.py -q
.\.venv\Scripts\python.exe -m pytest test\test_website_zip_packaging.py -q
```

## 构建发布包

### 独立运行 ZIP

先构建 PyInstaller one-dir 产物：

```powershell
.\.venv\Scripts\pyinstaller.exe --clean --noconfirm DatasetAI.spec
```

再生成官网独立运行包：

```powershell
.\scripts\build_website_zip.ps1 -Version '1.0.1.0'
```

默认输出：

```text
build\DatasetAI.Standalone-1.0.1.0.zip
```

脚本会校验 `幻金.exe`、`_internal`、ZIP 路径格式，并输出 SHA256。

### Microsoft Store MSIX

```powershell
.\scripts\build_msix.ps1 `
    -Channel store `
    -Version '1.0.1.0' `
    -Output 'build\msix\DatasetAI.Store-1.0.1.0.msix'
```

正式 Store 包不要添加 `-LocalTest` 或 `-Sign`。

## 常见问题

### 解压后为什么不能只运行某个 DLL 或 `_internal` 里的文件？

`幻金.exe` 和整个 `_internal` 目录是一套完整运行时，必须保持相对位置。请直接运行解压目录中的 `幻金.exe`。

### 更新 JSON 数据会覆盖自选股吗？

不要直接覆盖本地的 `stock_universe.json`。程序更新系统指数时会保留 `sectors.user_added` 和 `watchlist`。如手工更新，应只更新 `csi300`、`zz500`、`csi1000` 等系统板块。

### AI 不可用会影响本地分析吗？

不会。规则扫描、指标计算、财务概览、报表展示和 PDF 溯源均可离线使用；AI 只负责可选的摘要和自然语言解读。

## 联系方式

- 网站：<https://datasetai.cn/>
- 邮箱：<datasetai@sina.com>
- 问题反馈：请通过 GitHub Issues 提交，并附上股票代码、报告期、操作步骤和错误截图。

## 免责声明

本项目提供的财务指标、风险提示、评分、归因和 AI 摘要均由自动化程序基于公开数据生成，可能存在数据缺失、解析误差或规则误判。任何内容都不构成投资建议，使用者应结合原始公告独立判断并自行承担决策风险。
