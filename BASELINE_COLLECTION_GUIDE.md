# 前沿对比方法检索与交付说明

## 1. 目标

为论文建立至少 6 种公开发表方法的正式对比。当前项目已经实现统一训练与评测接口，也包含固定惩罚、STL 奖励、Lagrangian、内部 MACPO 参考和物理 CBF-QP/SQP 等可训练参考实现。这些内部实现用于打通流程，不能全部替代第三方论文的官方复现。

建议先收集 7 至 9 个候选方法，经过代码完整性、任务相似度和许可证检查后，最终保留至少 6 个正式外部基线。不要为了凑数量选择与多智能体、安全约束或部分可观测决策无关的方法。

## 2. 建议检索的七类方法

| 优先级 | 类别 | 作用 | 最终要求 |
| --- | --- | --- | --- |
| P0 | MAPPO | 名义 MARL 主干和统一基础参照 | 需要官方或公认实现 |
| P0 | MACPO 或同等级约束 MARL | 代表显式安全成本约束 | 优先作者官方代码 |
| P0 | 多智能体 Lagrangian/CPO 类方法 | 代表原始-对偶约束学习 | 必须真正训练乘子或约束策略 |
| P0 | STL/时序逻辑引导 MARL | 代表逻辑奖励、鲁棒度或自动机方法 | 规则必须影响训练或决策 |
| P0 | CBF、shielding 或 runtime assurance MARL | 代表运行时动作修正 | 必须有明确安全过滤机制 |
| P1 | HAPPO | 代表异构/顺序更新的强 MARL 基线 | 官方实现优先 |
| P1 | MAT 或其他较新的 Transformer MARL | 代表非 MAPPO 的强策略学习器 | 需要能适配合作任务 |

如果某一类没有可复现代码，可以用同类、更新且代码完整的方法替代。最终组合中至少应有：

- 2 种普通强 MARL 方法；
- 3 种安全、约束、逻辑或运行时保障方法；
- 1 种与本文“时序规则或安全修正”最接近的方法。

固定惩罚和简单 STL 奖励可保留为经典机制基线，但不应把它们包装成前沿论文方法，也不应占满老师要求的 6 个外部方法名额。

## 3. 论文筛选硬条件

每个候选方法应尽量满足以下条件：

1. 论文发表于 2021 至 2026 年；经典必要基线可以稍早，但必须说明原因。
2. 论文来自正式期刊、会议或可信的最新预印本；优先 IEEE、Elsevier、Springer、AAMAS、NeurIPS、ICML、ICLR、AAAI、IJCAI、CoRL 等来源。
3. 研究对象是多智能体强化学习、约束决策、时序逻辑控制、安全屏蔽或运行时保障。
4. 有公开代码，最好是作者主页或论文链接的官方仓库。
5. 仓库能够找到训练入口，而不只是结果图片、演示脚本或伪代码。
6. 许可证允许研究使用和修改；没有许可证的仓库需要单独标记。
7. 方法能够在集中训练、分散执行或相近设置下运行。
8. 代码允许替换环境，或者环境接口足够清晰，不与某个专用仿真器完全绑定。
9. 执行阶段不能默认读取本项目不可获得的真值；如果必须读取，应作为 truth-informed 参考，而不是公平主基线。
10. 算法不能与本文方法实质相同后再改名，也不能只是同一算法的多个超参数版本。

## 4. 不建议选择的情况

- 只有论文，没有代码，且复现工作量明显超过一个完整算法开发周期；
- 只有单智能体实现，核心算法无法合理扩展到多智能体；
- 只适用于图像端到端飞控，与当前高层语义动作无法对接；
- 依赖商业软件、不可获得数据集或无法安装的私有组件；
- 仓库无法训练，只提供已经整理好的最终数字；
- 方法使用测试场景调参或依赖在线真值，而论文没有明确披露；
- 多个候选方法来自同一个算法，仅更换名称、网络宽度或奖励系数；
- 把博客实现、课程作业或无来源的二次转载当作官方实现。

## 5. 检索渠道与关键词

论文检索渠道：Google Scholar、Web of Science、Scopus、IEEE Xplore、ACM Digital Library、ScienceDirect、SpringerLink、OpenReview、arXiv。

代码检索渠道：论文项目主页、作者 GitHub、Papers With Code、OpenReview 附件。优先从论文中的链接进入仓库，避免下载同名非官方项目。

建议组合检索：

```text
safe multi-agent reinforcement learning constrained MAPPO code
multi-agent constrained policy optimization MACPO GitHub
multi-agent Lagrangian reinforcement learning safety constraints
multi-agent temporal logic reinforcement learning STL code
multi-agent control barrier function reinforcement learning shield
runtime assurance multi-agent reinforcement learning
partially observable safe multi-agent reinforcement learning
HAPPO official implementation
multi-agent transformer official implementation
```

检索时记录引用量只是辅助，代码可复现性和与论文问题的相似度更重要。最新方法如果引用量尚低，可以根据发表平台、实验完整性和官方代码质量判断。

## 6. 每种方法必须收集的材料

每个候选方法至少提供以下内容：

| 材料 | 必需 | 说明 |
| --- | --- | --- |
| 论文 PDF | 是 | 完整正文和附录 |
| DOI、arXiv 或正式论文链接 | 是 | 用于核对版本和引用信息 |
| 官方代码仓库链接 | 是 | 不要只给搜索结果页 |
| 仓库 commit、tag 或 release | 是 | 保证以后可以定位同一版本 |
| 源代码压缩包或完整 clone | 是 | 必须保留目录结构和配置文件 |
| README 和训练命令 | 是 | 要能找到从头训练入口 |
| 依赖文件 | 是 | 如 `requirements.txt`、`environment.yml`、Dockerfile |
| LICENSE | 是 | 缺失时明确写“未提供许可证” |
| 默认实验配置 | 是 | 包括网络、学习率、步数、约束阈值等 |
| 预训练模型 | 可选 | 有则下载，可用于验证安装是否正确 |
| 原论文结果表 | 建议 | 标记论文中最接近当前任务的指标 |
| issue 或复现说明 | 建议 | 记录已知安装问题和作者补丁 |

不要只提供论文名称、截图、零散 Python 文件或删除配置后的源码。GitHub 仓库后续可能变化，因此链接之外还要保留 commit 或下载时的完整压缩包。

## 7. 最终交付给我的目录格式

建议在项目外先完成下载和病毒检查，再将材料按以下格式放入项目：

```text
external_methods/
  inbox/
    method_short_name/
      PAPER.pdf
      SOURCE/
      REPO_INFO.md
      requirements.txt          # 如果原仓库提供
      environment.yml           # 如果原仓库提供
      LICENSE                    # 如果原仓库提供
      checkpoints/              # 可选
```

每个 `REPO_INFO.md` 至少填写：

```markdown
# Method information

- Method name:
- Paper title:
- Year and venue:
- DOI/arXiv URL:
- Official repository URL:
- Commit/tag/release:
- Download date:
- License:
- Official training command:
- Official evaluation command:
- Original environments:
- Observation space:
- Action space:
- Centralized information used during training:
- Information used during execution:
- Safety cost/constraint definition:
- Pretrained checkpoint included: yes/no
- Known installation problems:
- Why it is relevant to this paper:
```

如果不方便整理目录，最低限度可以先给我一个表格，包含方法名、论文链接、官方仓库链接、commit/tag、许可证、训练命令和下载状态。我核查后再决定是否下载完整代码。

## 8. 建议先提交的候选方法表

先整理一张候选表，不要看到代码就立即大规模下载：

| 方法 | 年份/平台 | 类别 | 论文链接 | 官方代码 | License | 可换环境 | 训练入口 | 预训练模型 | 初步结论 |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 示例 | 2024/期刊 | 约束 MARL | URL | URL | MIT | 是 | 有 | 有 | 待核查 |

建议先提交 7 至 9 个候选。我将其分为：

- A：适合正式公平对比；
- B：可作为补充或高保真验证参考；
- C：环境或信息假设不公平；
- D：代码、许可证或复现条件不完整。

确认 A 类名单后再下载大型模型和依赖，可以减少无效工作。

## 9. 接入后的公平比较要求

正式实验必须遵守以下规则：

1. 所有方法使用同一决策级环境版本和冻结测试库。
2. 训练、验证、测试种子族严格分开；测试集不得用于调参或选检查点。
3. 训练预算按环境交互步数统一，不能只比较含义不同的“更新次数”。
4. 每种方法获得相同的超参数搜索次数和验证场景预算。
5. 网络规模尽量接近；必须使用原论文特殊结构时记录参数量和计算量。
6. 所有分散执行策略使用相同的局部观测。额外使用真值或全局状态的方法单独标注。
7. 原方法需要安全成本、STL 鲁棒度或 CBF 约束时，统一从同一规则语义和环境状态构造，不改变测试判据。
8. 最终指标统一由项目的离线 truth-STL 评测器计算，不能直接采用各仓库自己的安全率定义。
9. 同一批随机种子做配对比较，报告均值、标准差、95% 置信区间和配对效应。
10. 同时报告任务回报、条件联合满足率、硬规则违反率、尾部风险、干预率、干预幅度、不可行率和在线时间。
11. 任何适配补丁都单独保存，不直接覆盖第三方原始源码，并记录修改理由。
12. 安装或训练失败也要记录，不能无说明地删除不利方法或随机种子。

## 10. 推荐实施顺序

1. 收集 7 至 9 个候选方法的论文和仓库信息。
2. 先提交候选表，由我筛选正式 6 至 7 种方法。
3. 下载确认后的源码、许可证、配置和可选检查点。
4. 我为每种方法制作独立环境适配器和统一动作转换层。
5. 对每种方法运行最小烟雾测试，确认能够训练、保存、加载和评测。
6. 用统一验证预算做有限调参，冻结配置和 commit。
7. 在决策级环境运行多种子正式对比和统计检验。
8. 根据安全性、任务性能、代表性和可迁移性选择 3 至 4 种方法。
9. 只对选中的方法进行 JSBSim 六自由度验证。
10. 整理论文主表、场景分表、Pareto 图、运行时间表和复现清单。

## 11. JSBSim 方法选择原则

进入 JSBSim 的 3 至 4 种方法建议包括：

- 本文完整方法；
- 决策级综合表现最好的普通 MARL 方法；
- 表现最好的安全/约束 MARL 方法；
- 与本文最接近的逻辑或安全屏蔽方法。

选择应在查看 JSBSim 结果前根据冻结的决策级结果确定，避免高保真测试后再挑方法。JSBSim 中统一报告直接迁移和必要的相同预算适配结果，不能只给本文方法额外微调。

## 12. 当前阶段不需要做的事情

- 暂时不需要运行大规模内部基线正式实验；官方代码接入后需要重新统一运行。
- 不需要一次下载所有候选方法的大型数据集和模型。
- 不需要修改第三方源码来迎合当前环境，先保持原始版本完整。
- 不需要优先寻找航空专用算法；算法机制相似、环境可替换比表面上的航空名称更重要。
- 不要把当前烟雾实验数字写进论文最终结果表。
