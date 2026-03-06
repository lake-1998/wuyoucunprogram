# 【无忧存】【AI功能】智能寄存推荐需求文档

# 版本信息

| **更新时间** | **更新内容** | **更新人** |
| --- | --- | --- |
| 2025-10-29 | 初版需求文档-Ai功能一期需求-首页Ai入口&Ai对话页面 | $\color{#0089FF}{@石佳惠}$ |
| 添加日期 |  | $\color{#0089FF}{@}$ |

# 需求背景

*   用户需在出行时快速找到合适的寄存点，但当前小程序主要依赖关键词搜索与地图浏览，流程繁琐、信息不集中。
    

*   引入 AI 对话能够降低用户查询门槛（自然语言输入），并结合公司寄存点数据库，提供准确的结构化推荐与出行建议，从而提高下单率与满意度。
    

*   技术选型：采通用大模型（云 API）+ RAG（向量检索，本地寄存点库）；不考虑自研模型以降低时间/维护成本。
    

# 产品架构

##  业务流程

![image](https://alidocs.oss-cn-zhangjiakou.aliyuncs.com/a/Rb5P2jr1kSkQeOAJ/97d0617f4c82497e87e17e060d8c4f8f2624.png)

##  功能架构

![image](https://alidocs.oss-cn-zhangjiakou.aliyuncs.com/a/Rb5P2jr1kSkQeOAJ/9fbc2cad9f5a4286b53540b64ebb94022624.png)

## 信息架构

![image](https://alidocs.oss-cn-zhangjiakou.aliyuncs.com/a/Rb5P2jr1kSkQeOAJ/3924eb01e7b4495aafcfac59003601252624.png)

# 交互方案

## 交互概览

![image.png](https://alidocs.oss-cn-zhangjiakou.aliyuncs.com/res/Q35O8512E1L6Jl9V/img/2536b5fb-d724-412c-b255-6a1cbd52a127.png)

## 交互说明

### 首页

| **功能点** | **交互页面** | **交互说明** |
| --- | --- | --- |
| 首页 | ![image.png](https://alidocs.oss-cn-zhangjiakou.aliyuncs.com/res/Q35O8512E1L6Jl9V/img/13ac41c8-416e-47b9-957e-475a32bddf5e.png) | 搜索框增加“进入ai搜索”，点击进入AI对话页 |

### AI对话页

| **功能点** | **交互页面** | **交互说明** |
| --- | --- | --- |
| AI对话页 | ![image.png](https://alidocs.oss-cn-zhangjiakou.aliyuncs.com/res/Q35O8512E1L6Jl9V/img/27517299-3e66-4ee3-9174-1dc013702122.png) | 1.  进入根据城市提供提示语，目的地选取为推荐景点第一<br>    <br>    以深圳为例：我想去莲花山公园<br>    <br>2.  根据用户输入地点，检索数据库进行地点推荐<br>    <br>3.  推荐气泡下方出现后续推荐问题<br>    <br>4.  输入框提供提示用户输入 |

# 问答设计

![image](https://alidocs.oss-cn-zhangjiakou.aliyuncs.com/a/Rb5P2jr1kSkQeOAJ/2f2d459cbac247369ad82eac0255dd3b2624.png)

边界情况问答梳理：[《无忧存边界情况梳理》](https://alidocs.dingtalk.com/i/nodes/Obva6QBXJw69z5xEU6mApjNYVn4qY5Pr?utm_scene=person_space)

# 功能里程碑

考虑到涉及AI应用，对话会出现非常多的可能，

| 阶段 | 功能 |
| --- | --- |
| 阶段一 | 完成对话页，确保对话无异常 |
| 阶段二 | 首页增加ai功能入口 |
| 阶段三（视首页使用情况待定） | 搜索地点页增加ai功能展示或开启方式 |

# 数据需求

![image.png](https://alidocs.oss-cn-zhangjiakou.aliyuncs.com/res/Q35O8512E1L6Jl9V/img/cdc2c670-6487-4d20-a5ca-d3e4d5907f44.png)

| 事件名称 | 采集逻辑 | 事件属性 | 备注 |
| --- | --- | --- | --- |
| 首页ai入口曝光 | 首页渲染出 AI 入口组件时触发 |  | 用于计算 AI 入口曝光量 |
| 首页ai入口点击 | 点击首页 AI 入口时触发 |  | 用于计算 AI 入口点击率、转化到对话页的比例 |
| ai对话页曝光 | 进入 AI 对话页时触发 |  |  |
| ai触发寄存点检索 | AI 收集到足够信息并调用寄存点检索接口时触发 |  | 用于评估 AI 收敛能力和检索成功率 |
| ai检索无结果 | 寄存点检索结果为 0 或无可用点时触发 |  | 用于监控“找不到寄存点”的比例 |
| ai推荐结果曝光 | AI 在对话中展示推荐卡片时触发 |  | 衡量“有推荐结果”的会话量和推荐结构 |
| 从ai对话查看寄存点 | 在 AI 对话页点击推荐卡片进入寄存点详情 |  | 评估 AI 推荐列表的点击率、命中率 |
| ai推荐进入下单页 | 从 AI 推荐卡片点击“查看”时触发 |  | 观察 AI 推荐到“发起下单”的转化 |
| ai推荐下单成功 | 订单创建成功且来源为 AI 时触发 |  | 用于计算“AI 使用 → 下单成功”的漏斗转化 |

# 后续迭代要点

（1）根据实际使用情况考虑是否需要限制用户对话次数

（2）重复追问同一个地点，类似于“深圳市南山区还有寄存点吗？”“还有吗”“还有吗”，目前因为上下文记忆最长3条的原因，会出现重复推荐的情况，后续可考虑优化仅展示未推荐过的点