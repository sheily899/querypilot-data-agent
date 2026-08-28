# QueryPilot 数据查询智能体

[English README](README.md)

QueryPilot 面向结构化数据库，将业务人员的自然语言问题转换为只读查询，并通过网页工作台展示结果。

## 先体验离线演示

无需模型密钥、数据库或网络：[打开可交互的离线 Demo](https://htmlpreview.github.io/?https://github.com/sheily899/querypilot-data-agent/blob/main/demo/index.html)，也可以下载仓库后直接打开 `demo/index.html`。

![QueryPilot 查询结果](docs/assets/query-result.png)

离线页面使用固定的脱敏示例数据，只用于体验交互流程，不代表在线模型评测结果。

## 当前包含的能力

- 区分新查询与上下文追问；
- 结合关键词、语义匹配、排名融合和重排序定位相关字段；
- 根据表间关系构建结构图；
- 通过单库查询智能体调用本地工具；
- 执行前检查只读语句、单条语句、表访问权限和危险操作；
- 提供对话、结果表格、查询语句查看和导出功能。

当前版本限定为单数据库执行，多数据库任务拆分和结果合并尚未启用。

## 运行完整本地应用

### 启动后端

Windows 推荐使用 Python 3.11。先根据 `.env.example` 创建 `backend/.env`，填写模型接口地址和密钥。

```powershell
cd backend
python -m venv .venv
.\.venv\Scripts\Activate.ps1
python -m pip install -r requirements.txt
python run.py
```

### 启动前端

```powershell
cd frontend
npm install
npm run dev
```

打开前端开发服务器输出的地址。完整应用会调用配置的模型服务；离线演示不会访问网络。

## 评测结果摘要

以下数字来自项目中 80 条问题的评测记录。加入业务背景说明的运行中，79 条完整执行，1 条被标记为基础设施失败。

| 指标 | 结果 |
|---|---:|
| 最终输入结构字段召回率 | 82.97% |
| 最终输入结构字段精确率 | 31.04% |
| 查询执行准确率 | 53.16%（42/79） |
| 端到端耗时中位数 | 57.67 秒 |
| 端到端耗时95分位数 | 92.94 秒 |

这些数字是工程评测快照，不是生产环境承诺。网络或模型接口故障单独统计，不混入能力指标。

## 仓库范围

公开仓库包含可运行的产品核心代码和自包含的界面演示。内部评测数据、运行记录、临时诊断脚本、本地数据库、日志和密钥均未上传。

## 许可证

MIT，详见 [LICENSE](LICENSE)。
