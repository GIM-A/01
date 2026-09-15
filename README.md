# 7 天学习计划：dive-into-llms 项目

> 
> 你的基础：已经学完 Python、API 调用、Day1 手写 ReAct、Day2 智谱 GLM Function Calling 计算器 Agent
> 仓库地址：[https://github.com/Lordog/dive-into-llms](https://github.com/Lordog/dive-into-llms)
> 目标：7 天完整过一遍仓库核心章节，跑通对应 Notebook，理解原理，产出可演示代码，优先聚焦**提示工程、Agent、微调**，偏应用层；RLHF、知识编辑、模型水印这类偏底层实验浅尝即可。
> 设备：蛟龙 16K；API：智谱 GLM（免费额度）；本地小模型可跑 Qwen1.5-1.8B/4B。
> 前置准备（今天一次性装好）
> 安装：`jupyter notebook`、`transformers`、`datasets`、`peft`、`accelerate`、`gradio`、`torch`
> 克隆仓库：`git clone https://github.com/Lordog/dive-into-llms.git`

> 
> 时间安排：每天 2～3 小时，包含「理论学习 + 运行代码 + 整理笔记（面试可用）」

## Day1｜衔接已有知识，完成仓库 Chapter2：提示工程 & CoT 思维链（2～3h）

**今日目标**：打通你之前学的 Agent 和提示工程，跑通仓库 Chapter2 所有 notebook

1. 学习内容
   - Few-shot / Zero-shot 提示词
   - CoT 思维链、PoT 程序思维链（和你的计算器 Agent 强关联）
   - 提示词的编写原则
2. 动手任务
   1. 打开仓库 Chapter2 的 ipynb，逐块运行
   2. 修改案例：把数学题换成你之前的 `(128+45)*3`，对比普通 prompt vs CoT prompt 结果差异
   3. 自己写 1 组 PoT 提示，让模型输出 Python 代码计算数学题
3. 笔记整理（面试）
   - CoT：让模型分步思考，提升推理能力；PoT：让模型生成代码交给解释器执行，适合数学计算
4. 验收标准：成功运行 Notebook，能口述 CoT 和 PoT 区别

## Day2｜Chapter1：大模型微调、LoRA + Gradio 网页部署（2～3h）

**今日目标**：学会轻量微调 LoRA，并且把模型封装成网页 Demo

1. 学习内容
   - SFT 监督微调概念
   - LoRA 原理：冻结基座大模型，只训练少量低秩矩阵，节省显存（蛟龙 16K 可以跑小模型 LoRA）
   - Gradio 快速搭建网页交互界面
2. 动手任务
   1. 运行 Chapter1 Notebook，加载 Qwen1.5-1.8B 小模型，跑通 LoRA 微调 Demo
   2. 运行 Gradio 代码，本地弹出网页，和模型对话
   3. 记录：完整流程：加载基座模型 → 加载数据集 → LoRA 训练 → 推理 → WebUI 展示
3. 笔记整理
   - LoRA 为什么省显存；SFT 作用是什么

> 
> ⚠️ 如果本地 GPU 显存不够：可以只跑推理代码，微调部分看代码理解逻辑，不强行训练。

## Day3｜Chapter9：GUI 智能体（Agent 重点，你的核心兴趣）（2～3h）

**今日目标**：理解 GUI Agent 原理，区分普通工具 Agent 和屏幕感知 Agent

1. 学习内容
   - GUI Agent 整套流程：截图 → 多模态模型理解画面 → 输出操作指令（点击 / 输入）→ 执行操作
   - 多模态模型 Function Calling
   - 电脑屏幕捕获、模拟鼠标键盘操作基础库（pyautogui、mss）
2. 动手任务
   1. 阅读 Chapter9 文档和代码，看懂完整链路
   2. 写最小 Demo：截取屏幕，调用 GLM-V（智谱多模态）识别截图内容
   3. 理解：GUI Agent 本质是多模态版 ReAct 循环
3. 笔记整理
   - 普通文本 Agent：工具是计算器、查天气；GUI Agent：工具是鼠标键盘，输入是屏幕图像

> 
> 注意：完整 GUI 自动操作代码本地跑会有安全风险，只做演示识别，不要直接执行任意自动操作。

## Day4｜Chapter10：Agent 安全（面试高频）+ 复盘前面所有 Agent 代码（2～3h）

**今日目标**：补齐 Agent 安全知识，整合你 Day1、Day2 写的 Agent 代码

1. 学习内容
   - 提示注入（Prompt Injection）
   - Agent 工具滥用风险：比如 Agent 调用危险 shell 命令
   - 工具权限校验、输入过滤、安全沙箱概念
2. 动手任务
   1. 运行 Chapter10 Notebook，测试提示注入案例
   2. 修改你之前的计算器 Agent：增加输入过滤，禁止危险表达式（限制 eval 风险）
   3. 合并代码：把手写 ReAct、Function Calling 两份代码整理到项目文件夹
3. 笔记整理
   - Agent 安全风险来源；如何简单防护工具调用

## Day5｜Chapter4：数学推理；Chapter6：提示越狱攻击（2～3h）

**今日目标**：拓展模型推理边界，了解大模型安全攻防

1. 学习内容
   - GSM8K 数学数据集，模型推理失败原因
   - 越狱、提示注入的攻击思路；大模型安全对齐的意义
2. 动手任务
   1. 运行 Chapter4 数学推理实验，对比普通提问 / CoT / PoT 的正确率
   2. 阅读 Chapter6 案例，看懂越狱提示原理，**仅学习原理，不要尝试攻击线上大模型**
3. 笔记整理
   - 对齐是什么；越狱攻击的原理

## Day6｜选学章节：Chapter3 知识编辑、Chapter7 模型隐写（浅读）（2h）

> 
> 这两部分偏底层实验，不需要完整复现，看懂原理即可，用来丰富毕设 / 面试素材

1. 学习内容
   - 知识编辑 ROME：直接修改模型权重，修改模型记住的知识，不需要重新微调
   - 文本隐写：在模型输出文本内嵌入隐藏信息
2. 动手任务
   1. 阅读 Notebook，看懂输入输出效果
   2. 整理 2 段原理简述，面试备用
3. 剩余时间：回看前面所有代码，标记不懂的地方

## Day7｜Chapter11 RLHF/PPO（理论为主）+ 项目整体复盘 + 整理作品集（2～3h）

1. 学习内容

> 
> 数学难度高，**不要求复现训练，看懂流程即可**
   - RLHF 全流程：SFT → 训练奖励模型 → PPO 强化学习对齐
   - PPO 的核心思想：用奖励模型反馈优化大模型输出
2. 动手任务
   1. 浏览 Chapter11 的 Notebook，梳理 RLHF 完整流水线
   2. 作品集整理：汇总 7 天所有代码：
      - 手写 ReAct Agent
      - 智谱 Function Calling 计算器 Agent
      - CoT 提示词 Demo
      - LoRA 微调 + Gradio 网页 Demo
      - GUI 截图识别小 Demo
   3. 写一段项目简介（简历 / 毕设可用）

> 
> 项目简介参考：基于 dive-into-llms 项目系统学习大模型应用技术，实现 CoT 提示推理、LoRA 轻量微调、基于 Function Calling 的 AI Agent，研究 GUI 智能体与 Agent 安全问题，搭建 Gradio 可视化交互页面。
