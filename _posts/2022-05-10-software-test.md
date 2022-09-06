---
layout: post
title: 软件测试复习参考
subtitle: 背就完事
author: RuntimeEroor
categories: 学业
tags: 软件测试
---
# 软件测试

## 引论

软件测试是一种检测软件的正确性、完整性、安全性和评估其质量的活动过程。是一种以发现程序错误、衡量软件质量为目的，并对其是否满足用户需求进行评估的活动过程。

### 法则

1. 对于任何系统，穷尽测试不可能；
2. 测试工作可以具有创造性，但较困难；
3. 测试旨在减少系统中缺陷数目，不太可能完全消除系统所有缺陷；
4. 测试是有风险的、成本高昂的；
5. 测试需要有计划性，否则无法确保测试项目顺利完成；
6. 测试需要有独立性，否则难以让人信服。

### 瀑布模型

1. 需求分析
2. 设计
3. 编程
4. 测试
5. 维护

### V 模型

1. 需求分析 <---->  验收测试
2. 系统设计 <----> 系统测试
3. 详细功能设计 <----> 功能测试
4. 编码 <----> 单元测试

### 软件质量保证

是指通过对软件产品进行有计划的评审和审计，来确保软件开发按照产品质量过程标准实施项目的管理活动。

- 对软件过程各个阶段任务的完成质量及出现问题进行评审、跟踪。
- 审查和验证软件产品开发过程是否遵守适用的标准、规程和要求，并最终确保产品满足用户需求；
- 建立软件质量要素的度量机制，对软件开发的各种质量指标进行量化，为管理者提供软件开发的质量分析数据。

SQA 指导软件测试的计划与执行，监督测试工作结果的客观性、准确性与有效性，并协助软件测试的工作流程改进；

软件测试是 SQA 工作落实的重要手段，它为 SQA 提供所需的质量数据，作为软件质量评价的客观依据。

SQA 是一项软件质量管理性工作，侧重于对软件开发流程进行评审和监控。

软件测试是一项技术性工作，侧重于对软件质量特性进行检测与验证。

### 测试驱动开发

要求在编写某个功能的代码之前先编写测试代码，然后编写功能代码，通过测试来推动整个软件开发的进行。

### 习题

成功的软件测试是发现软件中的缺陷； 过程评审不是软件测试的范畴。

## 软件测试基本概念

### 缺陷

欠缺或不够完备的地方。因为缺陷是相对质量要求而存在的，任何违背了质量要求、违背了客户的志愿、不能满足用户的要求，都可以认为是缺陷。

软件缺陷指软件中存在的任何一种破坏正常运行能力的问题、错误、异常、失败等，导致软件产品在一定程度上不能满足用户的需要。

### 软件质量

质量是产品或服务满足所明示或隐含需求能力的固有特性集合；软件产品或服务满足用户需求的程度。具体地说，软件符合明确叙述的功能和性能需求、符合开发标准，具有专业软件都应满足的隐含特征和特性。

### 软件产品质量属性：

- 功能性
- 可靠性
- 可用性
- 效率
- 可移植性
- 可维护性
- 兼容性
- 可扩展性

使用质量

- 有效性
- 生产率
- 安全性
- 满意度
- 外部质量属性
- 功能性
- 可靠性
- 易用性
- 效率
- 维护性
- 可移植性

内部质量

- 代码耦合性
- 数据耦合性
- 程序规范性
- 需求可溯性
- 代码复杂度

![](/blog/static/boxcnjPqoLXj1eUnmMRW6LW5IAe.png)

![](/blog/static/boxcnMR4cokJPBIe6vye6I16fHe.png)

静态测试:指对系统需求规格说明书、系统设计规格说明书进行评审，对程序代码进行审查及静态分析等测试活动;

动态测试:指将被测软件程序进行运行，观察该程序运行过程中的系统行为、变量结果、内存、堆栈等运行数据，来判断软件系统是否存在缺陷的测试活动;

产品评审:可以及早发现需求分析、软件设计阶段等阶段的缺陷问题，是对软件开发文档或代码进行评估的一种手段，以判断是否与预期结果一致。

- 需求评审
- 设计评审
- 代码评审
- 文档评审
- 管理评审
- 流程评审

前四个软件测试，后两个软件质量保证

静态分析是对软件的源代码进行研读，查找错误或收集一些度量数据，并不需要对代码进行编译和仿真运行

![](/blog/static/boxcnXqgdXg132aP4dphi9R7Pre.png)

黑盒测试：不考虑内部结构和特性进行功能测试，是从用户观点出发开展的测试，目的是尽可能发现软件的外部行为错误

特点：与软件具体实现无关，用例设计可以和软件实现同时进行

白盒测试 了解被测程序内部逻辑结构对该程序的内部变量、逻辑结构、运行路径进行测试，检验被测程序的内部动或运行功能，是否符合设计规格要求。

原则：执行测试时先考虑各个分支被覆盖，考虑完成所有逻辑条件分别为真值和假值的测试 测试程序流程图中的独立路径。

局限：穷举路径测试不太可能 不能检测出程序违反设计规范，不能检测出编程遗漏路径，可能发现不了一些与数据相关的异常错误。

单元测试：单元测试针对软件测试中的最小功能单元代码进行测试（主要白盒），需要编写驱动模块和桩模块

### 系统测试

- 系统功能性测试：
- 系统非功能性测试：
- 性能测试（负载测试、压力测试）
- 等等

### 验收测试

- α 测试
- β 测试

### 测试用例

是指为特定测试目的送设计的测试条件测试数据以及测试规程的使用场景

### 课堂习题

![](/blog/static/boxcnNwdc4ym2faIGx0gL4N5Qzb.png)

DDB

![](/blog/static/boxcnfIvLNoFAwtUs6TulW3mkU4.png)

CBD

## 软件测试方法

1. Ad-hoc 测试方法：根据测试人员的应用知识和测试人员随机测试进行的，而不遵循规范/要求。因此，Adhoc 测试的成功取决于测试者进行测试的能力。测试人员必须找到缺陷，无需任何适当的规划和文档，仅基于测试人员的直觉。
2. ALAC，基于客户使用产品的经验知识所进行的测试方法
3. 错误推测法
4. 等价类
5. 边界值就是大于小于没有等于
6. 因果图（**使用形式化规格描述输入组合**）

![](/blog/static/boxcnsgTXv35vC0Qot4ZYwGXxXf.png)

![](/blog/static/boxcnGOlUdYVNdPNrp6GXjrMSNb.png)

7. 判定表

![](/blog/static/boxcnzgWiu43Rq9FRHVVnbPL0Og.png)

![](/blog/static/boxcnwOU5wlaLUAKqecc5cqEN3e.png)

8. 成对组合测试：每一列从上往下看排列
9. 正交实验法（**多因素多值域**） ：

![](/blog/static/boxcn1BYyIZRUjs8AvZERU5awOg.png)

```
 水平数等于输入取值数（有、无），因子数等于有多少种不同的输入（员工号，学号，邮箱），行数等于因字数*(水平数-1)+1
```

10. 语句覆盖：
11. 判定覆盖：大条件取值全
12. 条件覆盖：小条件取值全，（T1 F2 T3 F4；F1 T2  F3 T4）满足条件覆盖不一定满足判定覆盖
13. 判定-条件覆盖： 判定中每个条件子句的所有可能至少出现一次；同时每个判定分支也至少出现一次， 未考虑条件子句的组合情况。

例如 y>1 z=0

一组符合判定/条件覆盖的用例需要满足下面

- 使得判定为真、假
- 使得 y>1、y<=1
- 使得 z=0 && z!=0

14. 条件组合覆盖：满足“条件组合覆盖”的测试用例是一定满足 “判定覆盖”、“条件覆盖”和“判定-条件覆盖” 。所有子条件的组合情况

![](/blog/static/boxcnttKdhVgajqYESPtb96phDe.png)

15. 基本路径覆盖（数量等于基本路径数 +1），每个判定标准反转
16. 课后题目：

![](/blog/static/boxcn9xJXwP1YkfmEyqmPcFHlHB.png)

XDC

![](/blog/static/boxcnEKBtJn8xtK3MfMdVmIFdRe.png)

BBBA

![](/blog/static/boxcnhAbeFHCoWDHeTL1mcQsBlh.png)

BA

![](/blog/static/boxcnpa02W0SLBEAfzPiEvYiJNd.png)

BB

## 测试流程和规范

### 软件测试过程的活动

![](/blog/static/boxcnNaPcNfRLGlLEWgOV4dGPjb.png)

### 软件测试过程的活动

![](/blog/static/boxcnv4qPTI3trf5QIbrjkk5I5f.png)

### 测试阶段输入输出

![](/blog/static/boxcnr1M1tnLkKnMUXbEslcYPHg.png)

### 软件开发与软件测试的 W 模型关系

![](/blog/static/boxcnYqjJ6cuoSNHA17Ag24mygf.png)

![](/blog/static/boxcnk0XWM7kXxmvFjlwD0OM6Ke.png)

### TMAP 测试模型

业务驱动的、基于风险策略的、结构化的测试管理方法，其目标是尽早地发现缺陷，以最小的成本、有效地、彻底地完成测试任务。

![](/blog/static/boxcn0tPZRZSK01Z1FFKFlLaWwe.png)

![](/blog/static/boxcn5AJtxBeWMs3YB1W829qiCg.png)

三个基石 坚实的组织融合（O） 正确的基础设施和工具（I） 可用的技术（T）

### 敏捷测试

是一种遵从敏捷开发原则能够很好地版主敏捷软件开发实现对质量控制的测试实践。敏捷测试=持续的质量反馈

- 敏捷测试测试方法：
- 基于脚本测试：无论手工测试、自动化测试都需要先设计用例生成测试脚本然后执行脚本实施测试。
- 探索式测试：不需要设计测试用例，一边思考，一边测试。
- 在敏捷测试中主要采用探索式测试，基于脚本测试作补充。在传统测试中主要采用基于脚本测试，探索式测试作补充。

### 基于风险的测试策略

基于分概念的测试策略是指评估测试的优先级。先做高的。

### 测试过程改进

测试能力成熟度模型 TMM/TMMi

### 软件测试规范

是对软件测试每个流程元素进行明确的界定，形成一个系统的完整测试体系。

### 课堂练习

![](/blog/static/boxcnKoU9slqMGCPwqgozulzO0b.png)

C

1. 需求评审
2. 设计评审
3. 单元测试
4. 集成测试
5. 系统测试
6. 验收测试
7. 测试计划
8. 测试设计
9. 执行与监控
10. 结果分析与评估
11. 项目总结

ACBA

## 单元测试与集成测试

### 单元测试

- 路径测试
- 局部数据结构测试
- 单元接口测试
- 单元边界条件的测试
- 单元容错性测试
- 内存分析

### 集成测试

桩程序为模拟下层 的模块，驱动程序则为模拟上层模块，

- 非渐增式集成测试
- 渐增式集成测试
- 自顶向下增量集成测试

![](/blog/static/boxcn06dBU7f2MtGENm5lDLsvpq.png)

- 自底向上增量集成测试

![](/blog/static/boxcnwA2sAnT6dED1aG3gEQ0d3c.png)

- 三明治增量集成测试

![](/blog/static/boxcnpVG2olfsQe7t6BcXvqSMCf.png)

- 改进的三明治集成测试

![](/blog/static/boxcn70uK1vc2WPsOMuJChmDhge.png)

![](/blog/static/boxcn9av5sYQlyYf5VqPgecXNpg.png)

### 课堂练习

![](/blog/static/boxcnhI3SdJyFYvN8NdaeNfMgzb.png)

CADCD

![](/blog/static/boxcnyIm8I3l5Wkfn3gy5RPL1rd.png)

DDCDD

## 系统测试

![](/blog/static/boxcnlp1qF2dL9NKXXOCz49Tyle.png)

### 系统级功能测试

### 回归测试：修改代码后再次测试

### 性能测试

#### 目的

- 评估当前系统性能
- 寻找系统性能瓶颈
- 规划系统配置

#### 分类

- 性能验证测试
- 性能基准测试
- 性能规划测试
- 系统容量测试（确定最大容量）
- 系统压力测试（稳定性、压力性、更快发现内存泄漏、线程锁定）
- 系统负载测试（用于发现性能瓶颈、内存泄漏，施加不同负载）

### 系统安全测试

![](/blog/static/boxcngZr5jwz5mcnkSGRTV97eJe.png)

### 容错性测试

### 兼容性测试

### 可靠性测试

### 课堂练习

![](/blog/static/boxcnS4KimZht5fnMQ71bIhPQ4g.png)

CCCBB

![](/blog/static/boxcnc38gYye4magiH056bmvhkh.png)

D D D A C

## 验收测试

### 验收测试内容

![](/blog/static/boxcnum5q9VuZhAefElfl4UiVjh.png)

### 产品规格说明书验证

![](/blog/static/boxcnnTRinOIkB39x0xAZVeJiJf.png)

### 用户界面测试与可用性测试

- 好的用户界面：
- 规范性
- 直观性
- 一致性
- 灵活性
- 舒适性
- 正确性
- 实用性

### 安装测试和可恢复性测试

### 课堂练习

![](/blog/static/boxcnyjEWc5fz8PImCAzQpnveic.png)

ABDCD

![](/blog/static/boxcnN0lxZY07sJNLFWVCqMcVFh.png)

CBBDA

## 本地化测试

### 软件本地化

### 软件国际化

### 课堂练习

![](/blog/static/boxcnGJ0Ahzk5iWzf1dQoT3HJvb.png)

ADA

## 测试自动化及其框架

### 内涵

### 原理

![](/blog/static/boxcnGvdCLHAk5SSkEKNrjtlDCe.png)

### 功能测试工具特性要求

![](/blog/static/boxcnGu9lvvHLfwqM7rn6dtLZDb.png)

### 性能测试工具特性要求

![](/blog/static/boxcnk5nY5vgEVYRLjqXqel7lZc.png)

### 课堂练习

![](/blog/static/boxcn4Q08CHsDktwl1zOg4DBOCc.png)

DC**D**CB

![](/blog/static/boxcnnuPtnlmp4hxHAQVF8IusMg.png)

## 测试需求分析与测试计划

### 测试目标与准则

![](/blog/static/boxcnkV5SXbgnbUljjOUmUzr2Sc.png)

### 测试需求分析

![](/blog/static/boxcngEIEKRgIMdV2YSEAPnFyse.png)

![](/blog/static/boxcndKa2zuSmhptvR3IYdUYttf.png)

![](/blog/static/boxcnXTLscCvViYUKyegtPyQ9uc.png)

### 测试项目估算与进度安排

- 依据

![](/blog/static/boxcn1FWIoA2wI0PBoWeMqPCYQh.png)

- 甘特图（进度安排）

### 测试风险管理与策略

### 测试计划内容与编制

### 课堂练习

![](/blog/static/boxcnPVjqY1nI3N3hPKNG6pd4Fk.png)

DBDAC

## 软件质量保证

### 软件质量度量

### 软件质量保证

### 课堂练习

![](/blog/static/boxcn3R5Umqdau2SLEwdSjzEYQe.png)

DDDDC
