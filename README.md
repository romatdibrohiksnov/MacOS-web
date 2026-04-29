# MacOS-Web-Sandbox (For GUI Agent Training)

> **⚠️ 注意：** 本仓库仅包含前端沙盒靶机环境（Target Sandbox）。核心的多 Agent 调度、DOM 解析与长链推理代码（Python backend）暂未开源。

## 项目初衷
本项目的目的是为 LLM/GUI Agent 提供一个极度轻量级（单 HTML 文件、零外部依赖）的 MacOS 模拟环境。
在构建基于大模型（如 Claude-3.5-Sonnet / GPT-4o）的电脑操作智能体时，真实的操作系统环境试错成本太高，且并发渲染极占内存。

因此，我构建了这个单文件的 Web 模拟器。由于它没有任何构建工具的包袱，非常适合用 Puppeteer / Playwright 挂载，在普通的服务器上就能轻松实现上百个并发的 Headless 实例，让不同的 Agent 相互对抗和生成交互动作数据。

## 使用方式 (配合未开源的 Python 调度器)
1. Agent A 接收自然语言指令。
2. Puppeteer 加载 `index.html`。
3. 抓取 DOM Tree 转为 JSON 喂给 LLM（极大消耗 Context Token）。
4. Agent 返回坐标或 DOM 动作，沙盒页面响应变化。
