# 面向多机空战仿真的条令启发型候选时序知识库

构造一个“候选专家时序知识库”，覆盖物理安全、信息授权、故障处置、多机协同、任务连续性和效率偏好六个层级。

## 优先级
$$
P0 \succ P1 \succ P2 \succ P3 \succ P4 \succ P5.
$$

| 层级 | 内容                 | 松弛性           |
| ---- | -------------------- | ---------------- |
| P0   | 物理飞行安全         | 不可松弛         |
| P1   | 信息、识别与授权     | 原则上不可松弛   |
| P2   | 故障、风险与资源安全 | 高优先级条件规则 |
| P3   | 多机协同             | 可以有限松弛     |
| P4   | 任务连续性           | 可被P0～P3覆盖   |
| P5   | 效率与行为偏好       | 软规则           |

## 时间尺度
- $\Delta_0$：1～2个高层决策周期，立即响应；
- $\Delta_1$：3～5个周期，短时处置；
- $\Delta_2$：6～15个周期，协同调整；
- $\Delta_3$：一个任务阶段；
- $T_{\text{dwell}}$：模式最短保持时间。

所有数值均为仿真参数，不对应真实作战数据。

## 三、P0：物理安全层
### S01 飞行包线始终满足
$$
\phi_{S01}^i = \mathbf{G}\left[m_{\text{env}}^i \ge 0\right].
$$
- 来源：AV；
- 类型：绝对硬约束；
- 信号：速度、高度、过载、迎角、姿态和结构裕度的归一化组合；
- 规则含义：任何任务收益都不能补偿不可恢复的飞行状态。

### S02 己方成员保持安全间隔
$$
\phi_{S02}^{ij} = \mathbf{G}\left[d_{ij} \ge d_{\text{min}}\right].
$$
- 来源：AV；
- 类型：绝对硬约束；
- 冲突：协同支援、任务交接、集中覆盖。

### S03 预测到冲突后及时形成安全趋势
$$
\phi_{S03}^{ij} = \mathbf{G}\left[ TTC_{ij} < \tau_c \rightarrow \mathbf{F}_{[0,\Delta_0]} safe\_trend_{ij}\right].
$$
其中 $safe\_trend$ 表示相对距离增长、预计冲突时间恢复或进入其他安全状态。

S02检查“是否已经危险”，S03检查“是否提前处理未来危险”。

### S04 保持最低机动能量裕度
$$
\phi_{S04}^i = \mathbf{G}\left[m_E^i \ge m_{E,\text{min}}\right].
$$
- 来源：SIM‑M/SIM‑C；
- 类型：候选硬规则；
- 建议：只有当 $m_E < m_{E,\text{critical}}$ 会进入不可恢复状态时才列为P0；一般能量偏好应放入P2或P5。
它来源于DCS/BFM中常见的“不要把机动能量耗尽”，但应抽象为恢复能力，而不是某一机型的特定速度。

### S05 始终保留有限时域可恢复性
$$
\phi_{S05}^i = \mathbf{G}\left[\exists a_{t:t+H}^i: \mathbf{F}_{[0,H]} safe\_state_i\right].
$$
- 来源：AV + EXP；
- 类型：硬约束；
- 含义：当前即使没有违反包线，也不能进入未来已不存在安全恢复动作的状态。

### S06 危险解除后保持安全裕度
$$
\phi_{S06}^i = \mathbf{G}\left[ hazard\_resolved_i \rightarrow \mathbf{G}_{[0,T_{\text{dwell}}]} m_{\text{safe}}^i \ge m_{\text{hys}}\right].
$$
- 来源：AV + EXP；
- 作用：防止“脱离危险—立即重新进入危险”的振荡行为。

## 四、P1：信息识别与授权层
AFDP 3‑01将战斗识别描述为：对检测对象形成足以支持决策的准确表征，并强调识别、决策权限、程序和术语应预先标准化、明确和演练。条令同时强调ROE需要清晰传达，并与指挥意图和风险相平衡。AFDP 3‑01，战斗识别与ROE部分。

### I01 关键动作必须具备有效授权
$$
\phi_{I01}^i = \mathbf{G}\left[ critical\_action_i \rightarrow authorization\_valid_i\right].
$$
- 来源：D‑A；
- 类型：条件硬约束；
- 仿真时只使用抽象的“关键动作”，不建模真实ROE细节。

### I02 关键动作必须满足识别置信度
$$
\phi_{I02}^i = \mathbf{G}\left[ critical\_action_i \rightarrow c_{ID}^i \ge c_{\text{min}}\right].
$$
- 来源：D‑A；
- 研究价值：区分“真实身份正确”和“智能体是否具有足够证据”。

### I03 使用的信息必须足够新鲜
$$
\phi_{I03}^i = \mathbf{G}\left[data\_age_i > \tau_{\text{fresh}} \rightarrow \left(\neg critical\_action_i \mathbf{U}_{[0,\Delta_2]} data\_updated_i\right)\right].
$$
如果在时间窗口内无法更新，则转入低风险或失联模式。

### I04 多源信息冲突时先复核或降级
$$
\phi_{I04}^i = \mathbf{G}\left[ source\_disagreement_i > \delta_c \rightarrow \mathbf{F}_{[0,\Delta_1]} \left(verified_i \lor lowrisk\_mode_i\right)\right].
$$
- 来源：D‑I；
- 冲突：任务时限；
- 优先级：高于P4任务期限。

### I05 威胁或安全告警必须及时传播
$$
\phi_{I05}^i = \mathbf{G}\left[ warning\_generated \rightarrow \mathbf{F}_{[0,\Delta_0]} warning\_received_{affected}\right].
$$

AFDP 3‑01强调及时探测和告警能为友方提供反应时间，并强调通信与传感器连接的可靠和冗余。

### I06 团队态势认知分歧过大时必须同步或解耦
$$
\phi_{I06}^{ij} = \mathbf{G}\left[ D(b_i,b_j) > \delta_b \rightarrow \mathbf{F}_{[0,\Delta_1]} \left(belief\_aligned_{ij} \lor task\_decoupled_{ij}\right)\right].
$$
- 来源：D‑I；
- 含义：如果无法统一态势认知，就不应继续执行高度耦合的协同任务。

## 五、P2：故障处置与风险层
AFDP 3‑01明确要求在信息降级或拒止情况下保持能力运行，并强调冗余、恢复和重构。AFDP 3‑01，任务式指挥及冗余恢复部分。

### F01 通信中断后切换为失联任务模式
$$
\phi_{F01}^i = \mathbf{G}\left[ C2\_lost_i \rightarrow \mathbf{F}_{[0,\Delta_1]} fallback_i\right].
$$
失联模式可以是：
- 继续最近一次有效任务意图；
- 降低任务耦合程度；
- 进入预设安全状态；
- 依据本地态势进行有限自治。

这直接对应条令中的“通信被拒止时仍依据指挥意图行动”，但具体动作是研究者设计的。

### F02 关键传感器退化后启用冗余来源或保守模式
$$
\phi_{F02}^i = \mathbf{G}\left[ sensor\_degraded_i \rightarrow \mathbf{F}_{[0,\Delta_1]} \left(backup\_source_i \lor conservative_i\right)\right].
$$
- 来源：D‑I；
- 可与I02识别置信度形成联动。

### F03 成员能力下降后重新配置团队
$$
\phi_{F03}^i = \mathbf{G}\left[ capability\_loss_i \rightarrow \mathbf{F}_{[0,\Delta_1]} team\_reconfigured\right].
$$
重新配置可以是任务接替、角色调整或任务降级，不规定具体战术。

### F04 资源低于安全阈值后及时进入恢复或退出状态
$$
\phi_{F04}^i = \mathbf{G}\left[ resource_i < r_{\text{low}} \rightarrow \mathbf{F}_{[0,\Delta_2]} \left(recovery_i \lor safe\_exit_i\right)\right].
$$
- 来源：SIM‑M + D‑I；
- 主要冲突：任务覆盖连续性。

### F05 安全层频繁干预时触发高层重规划
$$
\phi_{F05}^i = \mathbf{G}\left[ N_{\text{intervention}}^i(W) > N_{\text{max}} \rightarrow \mathbf{F}_{[0,\Delta_1]} replan_i\right].
$$
频繁干预说明不是单个动作有问题，而是当前计划或角色已经不再适用。

### F06 风险预算不足时必须降级或中止任务
$$
\phi_{F06}^i = \mathbf{G}\left[ B_{\text{risk}} < B_{\text{min}} \rightarrow \mathbf{F}_{[0,\Delta_1]} \left(mission\_degraded \lor valid\_abort \lor safe\_state\right)\right].
$$
AFDP 3‑01把可接受风险、威胁、时间和可用力量列为优先规划的重要因素，但这里的风险预算是研究用数学抽象。

## 六、P3：多机协同层
### C01 同一任务只能存在一个有效任务权威来源
$$
\phi_{C01}^k = \mathbf{G}\left[ task_k \rightarrow N_{\text{active authority}}(k) = 1\right].
$$
- 来源：D‑A/D‑I；
- 对应统一指挥和明确责任；
- 不表示所有动作集中控制，执行仍可分散。

### C02 任务活动期间保持最低覆盖能力
$$
\phi_{C02} = \mathbf{G}\left[ mission\_active \rightarrow coverage\_capacity \ge c_{\text{min}}\right].
$$
覆盖能力不一定是固定飞机数量，也可以由成员能力加权求和。

### C03 高风险成员必须在期限内获得团队响应
$$
\phi_{C03}^i = \mathbf{G}\left[ risk_i > r_{\text{high}} \rightarrow \mathbf{F}_{[0,\Delta_2]} \left(support_i \lor declined\_and\_reassigned_i\right)\right].
$$
- 来源：D‑I + SIM‑C；
- “响应”可以是支援，也可以是明确拒绝并重新分配；
- 不要求固定某架飞机执行固定动作。

### C04 成员退出当前角色前必须完成交接
$$
\phi_{C04}^i = \mathbf{G}\left[ leave\_role_i \rightarrow handover\_confirmed_i\right].
$$
这条规则可以与F04资源退出形成冲突：资源安全要求退出，但协同规则要求先交接。

### C05 重大计划或角色变化必须及时共享意图
$$
\phi_{C05}^i = \mathbf{G}\left[ plan\_changed_i \rightarrow \mathbf{F}_{[0,\Delta_1]} \left(intent\_shared_i \lor lostlink\_mode_i\right)\right].
$$
- 来源：D‑I；
- 如果通信不可用，则切换失联模式，不能把无法通信判成永久违规。

### C06 团队始终保留最低未承诺能力
$$
\phi_{C06} = \mathbf{G}\left[ team\_active \rightarrow reserve\_capacity \ge r_{\text{reserve}}\right].
$$

## 七、P4：任务连续性层
AFDP 3‑01采用效果导向思路，强调把任务、效果和目标连接起来，在执行过程中持续评估并调整；同时把威胁、可用力量、时间和风险纳入优先级。AFDP 3‑01，规划与评估部分。

### M01 每项活动任务必须对应有效目标和评价指标
$$
\phi_{M01}^k = \mathbf{G}\left[ task\_active_k \rightarrow \left(objective\_active_{g(k)} \land indicator\_defined_k\right)\right].
$$
这是“任务—效果—目标”追踪规则，防止MARL只追求局部动作奖励。

### M02 分配任务必须在期限内完成、交接或有效中止
$$
\phi_{M02}^{ik} = \mathbf{G}\left[ assigned_{ik} \rightarrow \mathbf{F}_{[0,D_k]} \left(completed_{ik} \lor handover_{ik} \lor valid\_abort_{ik}\right)\right].
$$
任务不能在系统中无声消失。

### M03 关键任务动作后必须完成效果评估
$$
\phi_{M03}^k = \mathbf{G}\left[ task\_action_k \rightarrow \mathbf{F}_{[0,\Delta_2]} assessment_k\right].
$$
这里的评估只判断任务是否产生预期仿真效果，不涉及具体打击效果模型。

### M04 长时间无进展或动作—效果不一致时必须重规划
$$
\phi_{M04} = \mathbf{G}\left[ \left(no\_progress > T_{\text{stall}} \lor effect\_mismatch\right) \rightarrow \mathbf{F}_{[0,\Delta_1]} replan\right].
$$
这对应条令中“行动是否正确、是否在做正确的事”的持续评估思想。

### M05 失去上级连接后，在有效意图范围内保持任务连续性
$$
\phi_{M05}^i = \mathbf{G}\left[ C2\_lost_i \land intent\_valid_i \land risk\_acceptable_i \rightarrow \left(mission\_continuity_i \mathbf{U}\left(C2\_re\right)\right)\right].
$$
这条规则不能单独使用，必须与F01和F06共同作用。

### M06 能力受损后应在一个任务阶段内恢复或正式降级
$$
\phi_{M06}^i = \mathbf{G}\left[ capability < c_{\text{desired}} \rightarrow \mathbf{F}_{[0,\Delta_3]} \left(reconstituted \lor mission\_formally\_degraded\right)\right].
$$
- 来源：D‑A；
- 对应条令中的恢复、重构与冗余思想。

## 八、P5：效率偏好层
### E01 避免对同一任务投入明显过量能力
$$
\phi_{E01}^k = \mathbf{G}\left[ allocated\_capacity_k \le required\_capacity_k + \epsilon_k\right].
$$
- 来源：D‑I；
- 对应“力量经济性”抽象；
- 必须作为软规则，因为高风险任务可能需要冗余。

### E02 角色和模式变化后保持最短驻留时间
$$
\phi_{E02}^i = \mathbf{G}\left[ mode\_changed_i \land \neg emergency_i \rightarrow \mathbf{G}_{[0,T_{\text{dwell}}]} mode\_stable_i\right].
$$
- 来源：SIM‑C + EXP；
- 防止MARL角色振荡。

### E03 无安全风险时避免不必要的安全干预
$$
\phi_{E03}^i = \mathbf{G}\left[ risk_i < r_{\text{low}} \rightarrow d(a_i^{nom},a_i^{safe}) \le \epsilon_a\right].
$$
这是“最小安全残差”最重要的效率偏好。

### E04 通信负载过高时转为压缩信息模式
$$
\phi_{E04} = \mathbf{G}\left[ comm\_load > C_{\text{max}} \rightarrow \mathbf{F}_{[0,\Delta_1]} compressed\_mode\right].
$$
- 来源：D‑I + EXP；
- 用于防止算法依赖无限通信。

### E05 安全事件解除后及时恢复可行任务
$$
\phi_{E05}^i = \mathbf{G}\left[ hazard\_resolved_i \land mission\_feasible_i \rightarrow \mathbf{F}_{[0,\Delta_2]} mission\_resumed_i\right].
$$
用于衡量安全层是否过度保守。

### E06 一个任务阶段内逐步平衡团队负载
$$
\phi_{E06} = \mathbf{F}_{[0,\Delta_3]} \left[\max_i load_i - \min_i load_i \le \delta_l\right].
$$
它不要求每时每刻平均，而要求团队有时间尺度地消除长期负载失衡。

## 经验转成时序知识的方法
建议按下表抽象，而不要把具体动作照搬进知识库。

| 非正式仿真经验               | 不应如何写           | 推荐抽象                       |
| ---------------------------- | -------------------- | ------------------------------ |
| “不要把能量打光”             | 固定某速度或机型参数 | S04机动能量裕度、S05可恢复性   |
| “不要丢失态势感知”           | 强制永远保持目标可见 | I03信息新鲜度、I06认知分歧协调 |
| “两机不要都陷入同一局部任务” | 固定一架必须做某角色 | C06最低未承诺能力              |
| “队友遇险应响应”             | 指定固定支援动作     | C03限时响应或重新分配          |
| “脱离前通知队友”             | 固定通信口令         | C04交接、C05意图共享           |
| “情况不对及时退出”           | 单一距离阈值退出     | F06风险预算、M04无进展重规划   |
| “危险解除后重新组织”         | 固定队形动作         | M06恢复重构、E05任务恢复       |
| “不要频繁改变打法”           | 禁止策略变化         | E02带紧急例外的驻留时间        |

## 十、最有论文价值的冲突场景

| 冲突                         | 高优先规则 | 低优先规则 | 预期仲裁                   |
| ---------------------------- | ---------- | ---------- | -------------------------- |
| 限时团队响应与安全间隔冲突   | S02/S03    | C03        | 更换响应成员或延迟响应     |
| 资源退出与任务覆盖冲突       | F04        | C02        | 先交接，必要时任务降级     |
| 识别置信度与任务截止时间冲突 | I02        | M02        | 不得用任务收益突破识别要求 |
| 通信中断与意图共享冲突       | F01        | C05        | 转入失联模式               |
| 能力下降与角色驻留冲突       | F03        | E02        | 紧急情况允许提前切换       |
| 风险预算与任务连续性冲突     | F06        | M05        | 降级或中止任务             |
| 任务覆盖与未承诺能力冲突     | C02        | C06        | 根据威胁紧迫度动态分配     |
| 最小安全干预与飞行安全冲突   | S01～S05   | E03        | 必要时允许大幅修正         |
