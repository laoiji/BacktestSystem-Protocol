# BacktestSystem-Protocol
A股回测系统的核心接口定义和数据结构规范（Protocol Buffers）

#strategy_plugin.proto
策略插件（Strategy Plugin）核心接口定义
根据我们之前的规划，我们现在开始定义 策略插件的核心接口方法。这部分内容应该被记录为您 GitHub 仓库中的第一个 .proto 文件。

我们命名这个文件为 strategy_plugin.proto。

1. 编程专家：gRPC 服务定义
我们将策略插件抽象为一个名为 StrategyPluginService 的 gRPC 服务。核心引擎将通过这个服务与策略插件进行通信。

2. 数学家 & 通达信专家：核心方法职责
Initialize: 在此阶段，策略插件会从 StrategyConfiguration 中获取所有参数（例如：均线周期、止损比例），并通知核心引擎需要通达信函数服务提供的哪些指标数据。

OnBar: 这是实现所有交易算法和数学模型判断的地方。策略插件在这里调用通达信公式服务计算指标，并根据结果生成 TradeSignal。

#config.proto
策略配置结构：config.proto 文件内容
为了确保配置的灵活性和 UI 的易用性，我们不采用为每个策略硬编码参数的方式，而是设计一个通用的**键值对（Key-Value Pair）**配置框架，并加入配置元信息。
1. UI设计大师：参数类型与显示元数据
我们首先定义一个通用的参数结构 Parameter，它包含了参数的类型、数值范围和用户描述：
2. 编程专家 & 数学家：策略配置主结构
策略配置主结构采用 map，使配置可以灵活地扩展，并且包含策略的元信息：
