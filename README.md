# 灵析

> 面向风控建模的 Agentic 自主建模系统

**你定建模方案，它负责实现落地。**

传统风控建模需要分析师反复衔接数据分析、特征筛选、模型训练与报告生成；固定策略的超参数优化器只能在既定空间内搜索，何时停止、是否调整空间以及如何利用历史试验，仍依赖人工判断。灵析将这一过程重构为可规划、可执行、可观察、可纠错的多 Agent 长任务：自主组织分析步骤、调用建模工具并管理过程状态，最终交付高水准模型基线与完整过程产物。

## 系统框架

![灵析智能自主风险建模框架](media/LX_share_ZH.png)

全局规划 Agent 将目标拆解为任务链，执行 Agent 按状态调用代码、基础分析与风控建模工具；数据、Agent 记忆和中间结果持续沉淀在本地工作目录。训练观察者读取调参轨迹，将下一步动作路由给早停评估、搜索空间调整和参数推荐 Agent；执行结果再回流到规划与观察环节，形成从分析到模型、报告交付的闭环。

## 核心技术创新

- **工具运行时重构与动态绑定**：工具可按分析需求或失败反馈重构，通过运行时编译、依赖按需注入、延迟实例化和动态注册即时生效。工具与 Agent 共享本地工作路径，减少大文件跨服务传输及静态工具反复部署的开销。
- **有状态的自主建模闭环**：将全局规划、链式执行、结果观察和失败反思连接起来。遇到可修复问题时，Agent 可重新判断调用方式、执行代码纠错或重构工具；同时保留中间文件，使长流程可追踪、可复核。
- **Agentic HPO 分层元优化**：以内层贝叶斯优化、TPE 等算法承担可靠的数值搜索，外层观察者 Agent 决策“何时停、在哪搜、如何搜”。系统分离全局实验记忆与局部优化器状态，搜索空间变化后复用兼容历史，实现跨空间恢复，而非从零开始。
- **高价值调参记录筛选**：从长调参轨迹中挑选高价值、高增益试验，降低重复记录对上下文的干扰，使大模型能够有效识别收敛趋势、过拟合信号和参数交互，并据此调整后续策略。


## 主要能力与交付

灵析覆盖样本探查与 OOT 划分、单变量分析、特征筛选、多智能体 LightGBM 调参、模型选择和报告生成，也支持围绕中间结果进行按需分析。任务完成后保留分析明细、调参轨迹、模型文件、调参报告及模型开发与性能评估报告。

## 演示

<table>
  <tr>
    <td width="50%" align="center">
      <strong>工具按需重构、即时生效</strong><br />
      <img src="./media/tool-rebuild-demo.gif" alt="工具按需重构、即时生效演示" width="100%" />
    </td>
    <td width="50%" align="center">
      <strong>工具自我进化、智能纠错</strong><br />
      <img src="./media/tool-self-evolution-demo.gif" alt="工具自我进化、智能纠错演示" width="100%" />
    </td>
  </tr>
</table>

<table>
  <tr>
    <td width="75%" align="center" valign="top">
      <img src="https://alidocs.oss-cn-zhangjiakou.aliyuncs.com/res/Mp7ld7bQxLkapOBQ/img/1cb4a961-306e-4e6c-a176-678b0f3b30d4.png" alt="灵析对话主界面" width="100%" />
    </td>
    <td width="25%" align="center" valign="top">
      <img src="https://alidocs.oss-cn-zhangjiakou.aliyuncs.com/res/Mp7ld7bQxLkapOBQ/img/d59b1819-706c-453e-9249-e3d64ba7ac5a.png?x-oss-process=image/crop,x_1248,y_0,w_550,h_928/ignore-error,1" alt="灵析任务智能规划侧边栏" width="100%" />
    </td>
  </tr>
</table>

<table>
  <tr>
    <td width="60%" align="center" valign="top">
      <img src="https://alidocs.oss-cn-zhangjiakou.aliyuncs.com/res/Mp7ld7bQxLkapOBQ/img/04cef5c0-95ab-43f8-9d09-839a05acc9d4.png" alt="多智能体调参分析" width="100%" />
    </td>
    <td width="40%" align="center" valign="top">
      <img src="https://alidocs.oss-cn-zhangjiakou.aliyuncs.com/res/Mp7ld7bQxLkapOBQ/img/516ea468-37bb-4aac-8e20-7a2398830a38.png" alt="调参空间阶段变化" width="100%" />
    </td>
  </tr>
</table>

## 验证结果

在 10+ 个内部风控项目中，灵析交付模型的 KS 达到高级分析师方案的 99%～112%，可提供高水准建模基线；端到端建模耗时缩短 40% 以上。系统已在某企业内部上线。

## 相关专利申请

- 《智能体工具动态绑定方法及相关产品》｜CN202511286785.8
- 《结合多智能体的模型自动训练方法和相关产品》｜CN202511753369.4
- 《结合调参记录筛选和大模型的模型训练方法和相关产品》｜CN202610091929.2
