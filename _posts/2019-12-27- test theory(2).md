---
layout: post
title: 测试理论（二）
date: 2019-12-27
tag: 学习笔记
---

# （一）软件质量度量指标及方法

|指标名称|定义|度量范围 |
|--|--|--|
|工作量偏差  | （（实际工作量-计划工作量）/计划工作量）*100% | 进度 |
|测试执行率  | （实际执行的测试用例数/测试用例总数）*100% | 测试进度 |
|测试通过率  | （（执行通过的测试用例数/测试用例总数）*100% | 开发质量 |
|测试覆盖率	 |（已设计测试用例的需求数/需求总数）*100% 	| |
|需求（测试用例）覆盖率|	（已设计测试用例的需求数/需求总数）*100%	| 测试设计质量 |
|需求通过率	|（已测试通过的需求数/需求总数）*100%	| 进度 |
|测试用例命中率	|（缺陷总数/测试用例数）*100%|	测试用例质量 |
|二次故障率	|（Reopen的缺陷/缺陷总数）*100%	| 开发质量 |
|NG率|	（验证不通过的缺陷/缺陷总数）*100%	| 开发质量 |
|缺陷有效率	|（无效的缺陷/缺陷总数）*100%	| 测试 |
|缺陷修复率|	（已解决的缺陷/缺陷总数）*100%	| 开发 |
|缺陷生存周期	|缺陷从提交到关闭的平均时间	| 开发、测试 |
|缺陷修复的平均时长|	缺陷从提交到修复的平均时间	| 开发 |
|缺陷关闭的平均时长|	缺陷从修复到关闭的平均时间	| 测试 |
|缺陷探测率|	（测试者发现的缺陷数/（测试者发现的缺陷+客户发现的缺陷））*100%	| 测试质量 |


# （二） 软件质量指标
软件内部/外部质量指标
外部质量因素影响用户，内部质量因素影响软件本身和它的开发者，外部质量取决于内部质量

## 1、外部质量

 1.  正确性(Correctness)：按照spec（规格）执行，得到正确的结果，软件的行为要严格符合规约中定义的行为
        保证正确性：测试和调适、防御式编程，形式化方法（形式化语言） encapsulation, decentralization
        封装、分散化
 2. 健壮性(Robustness)：针对异常情况的处理：出现规约定义之外的情形，软件做出恰当的反应（出现异常时不要崩  溃），未被spec覆盖的情况即为"异常情况"encapsulation, error handling封装、异常处理
 3.  可扩展性(Extendibility)：是否容易使软件适应规约的变化 提升可扩展性的两个原则：简约主义设计，分离主义设计 encapsulation, information hiding封装，信息隐蔽（结构良好的对象有简单的接口，并且不向外界显漏任何内部机制。）
 4. 可复用性(Reusability) ：一次开发，多次使用，发现共性
 modularity, component, models, patterns模块化、组件、模型、模式
 5. 兼容性(Compatibility )：不同软件系统之间相互可容易的集成 保持设计的同构性：标准化文件格式，标准化数据结构，标准化用户接口
    Efficient 性能
 6. 可移植性(Portability) ：软件可方便的在不同的技术环境之间移植：硬件、操作系统
 7. 易用性(Ease of use) ：易学、安装、操作、监控，给用户提供详细的指南，结构简单
 8. 及时性(Timeliness) ：及时发布等
其他质量： 可验证性(verifiability)，完整性(integrity)，可修复性(repairability)，经济性(economy)

## 2、内部质量
代码相关：lines of code（LOC）代码数量、cyclomatic complexity 循环复杂性
结构相关：coupling耦合度（多个模块间联系），cohesion聚合度（一个模块；高内聚，一个程序只执行一种功能） （应当 高内聚低耦合，单一责任原则）

Readability 可读性

Understandability 可理解性

Clearness

Size

最重要的几个质量因素：
Correctness and robustness: reliability（可靠性）

Extendibility and reusability: modularity（模块化）
