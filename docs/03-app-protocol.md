# 03 App通信协议

[返回完整PRD目录](../README.md) · [上一章](./02-firmware.md) · [下一章](./04-app-ux.md)

40项现有协议要求；新增业务所需接口单列，不视作已实现。

**【待补/待确认】 下表保留原协议。多步动作的输入能力、基础动作时长、完整规则原子启用/替换、按步按次调度及完成/停止回执为新增接口要求，见第11章，不能用0x51 OTA透传替代。**

<details>
<summary>连接与鉴权 · 3项</summary>

<table>
<thead>
<tr><th>编号</th><th>功能</th><th>需求</th><th>资料差异 / 缺项</th><th>依据</th></tr></thead>
<tbody>
<tr><td rowspan="1">AP-001</td><td rowspan="1">设备身份与KEY</td><td rowspan="1">App 按 MAC 识别设备。KEY 为 6 字节；App 首次连接默认 6 个 0x00，设备默认 6 个 0xFF。比对结果 0=失败、1=成功。</td><td rowspan="1"><strong>【待补/待确认】 密钥生成和更换规则未写明。</strong></td><td rowspan="1">通用BLE协议_V1_0_12.md，5.1</td></tr>
<tr><td rowspan="1">AP-002</td><td rowspan="1">绑定与保存KEY</td><td rowspan="1">App 发起绑定后，用户在 60 秒内单击设备按键确认；超时绑定失败。确认后 App 下发 6 字节 KEY，设备返回存储成功或失败。每次连接均需鉴权；连接后 65 秒内未完成鉴权，设备主动断开。</td><td rowspan="1"></td><td rowspan="1">通用BLE协议_V1_0_12.md §5.2～5.3、§8；设备功能说明.md §4.1</td></tr>
<tr><td rowspan="1">AP-003</td><td rowspan="1">解绑</td><td rowspan="1">App 下发解绑后，设备清除已保存的密钥，需要重新绑定。</td><td rowspan="1"><strong>【待补/待确认】 解绑清除其他用户数据的范围未写明。</strong></td><td rowspan="1">通用BLE协议_V1_0_12.md §5.4；设备功能说明.md §4.1</td></tr></tbody>
</table>

</details>

<details>
<summary>设置与状态 · 13项</summary>

<table>
<thead>
<tr><th>编号</th><th>功能</th><th>需求</th><th>资料差异 / 缺项</th><th>依据</th></tr></thead>
<tbody>
<tr><td rowspan="1">AP-004</td><td rowspan="1">设置确认和查询</td><td rowspan="1">每条下发命令只含 1 个功能点，异步执行。执行完成、状态变化或查询后上报状态；一次上报可含多个功能点。0xFF 用于查询全部功能点。</td><td rowspan="1"></td><td rowspan="1">通用BLE协议_V1_0_12.md，5.5–5.7</td></tr>
<tr><td rowspan="1">AP-005</td><td rowspan="1">时间和时区</td><td rowspan="1">App 同步 UTC Unix 秒时间及有符号时区偏移，偏移单位为分钟。RTC 和事件只存 UTC；当地情绪时辰按 UTC 加时区换算。默认东八区（+480 分钟）；设备时钟维持时间，时区不保存，重启恢复东八区。原文建议时区范围约 −720～+840 分钟；夏令时变化由 App 重新下发偏移。</td><td rowspan="1"><strong>【待补/待确认】 −720～+840 分钟为原文建议值；实际校验上下限未写明。</strong></td><td rowspan="5">通用BLE协议_V1_0_12.md §6；设备功能说明.md §4.2</td></tr>
<tr><td rowspan="1">AP-006</td><td rowspan="1">设备名称</td><td rowspan="1">宠物名称可设置和查询，最长 25 字节，重启后保留。</td><td rowspan="1"><strong>【待补/待确认】 名称编码、空名称处理及默认名称未写明。</strong></td></tr>
<tr><td rowspan="1">AP-007</td><td rowspan="1">电量和充电</td><td rowspan="1">电量只读，可查询，每 60 秒自动上报；协议分 0、25、50、75、100 五档，FF 表示无效。充电状态只读，可查询，状态变化时立即上报，值为 0/1。</td><td rowspan="1"><strong>【待补/待确认】 电量字段长度为 4 字节，而无效值仅写 FF；完整无效值编码待确认。</strong></td></tr>
<tr><td rowspan="1">AP-008</td><td rowspan="1">音量</td><td rowspan="1">音量可设置、查询和上报，共 1～6 档，依次对应 0%、20%、40%、60%、80%、100%，默认 4 档（60%）。重启后保留。</td><td rowspan="1"></td></tr>
<tr><td rowspan="1">AP-009</td><td rowspan="1">交友控制</td><td rowspan="1">交友开关可设置和查询，值为 0/1，重启后保留。附近有无好友（交友中状态）只读，由设备上报或供查询，值为 0/1。</td><td rowspan="1"><strong>【待补/待确认】 交友开关默认值未写明。</strong></td></tr>
<tr><td rowspan="1">AP-010</td><td rowspan="1">主导属性</td><td rowspan="1">App 主导五行取值为 1=金、2=木、3=水、4=火、5=土，可设置和查询，重启后保留；该属性影响情绪。</td><td rowspan="1"><strong>【待补/待确认】 Python 使用 0=木、1=火、2=土、3=金、4=水；两套编码按五行名称对应，实际对接调用方式未写明。</strong></td><td rowspan="1">通用BLE协议_V1_0_12.md §6；设备功能说明.md §4.2；情绪算法/daily_emotion_liunian.py L25～26</td></tr>
<tr><td rowspan="1">AP-011</td><td rowspan="1">一键演示</td><td rowspan="1">App 发起动作轮播演示，依次播放全部动作，每 5 秒一个；协议下发值为 0/1。</td><td rowspan="1"><strong>【待补/待确认】 0/1 的启动停止对应关系、完整播放顺序、循环及中断规则未写明。</strong></td><td rowspan="1">通用BLE协议_V1_0_12.md §6；设备功能说明.md §4.2</td></tr>
<tr><td rowspan="1">AP-012</td><td rowspan="1">行为静默</td><td rowspan="1">行为静默默认关闭（0）。开启（1）后不执行动作，也不写入事件记录，并进入待机；蓝牙仍可连接、查询和设置。该开关只存 RAM，重启自动关闭。</td><td rowspan="1"></td><td rowspan="1">通用BLE协议_V1_0_12.md §6；设备功能说明.md §4.2、设备功能说明.md §6.2、§7</td></tr>
<tr><td rowspan="1">AP-013</td><td rowspan="1">睡眠调度</td><td rowspan="1">睡眠时段按本地时间设置开始和结束时间，支持跨午夜，可关闭，重启后保留。起止分别为当日 00:00 起的分钟数，范围 0～1439，起止不允许相同，App 应拦截。处于睡眠时段时进入待机，所有互动和唤醒不响应。设置可查询，不主动上报；FF FF FF FF 表示关闭，从未设置时默认关闭。</td><td rowspan="1"><strong>【待补/待确认】 起止时间的等号边界未写明。</strong></td><td rowspan="1">通用BLE协议_V1_0_12.md §6；设备功能说明.md §4.2、设备功能说明.md §6.2</td></tr>
<tr><td rowspan="1">AP-014</td><td rowspan="1">重置</td><td rowspan="1">App 下发值 1 执行重置，清空事件记录和用户数据后重启。该控制值不保存，不主动上报。</td><td rowspan="1"><strong>【待补/待确认】 “用户数据”的逐项清除范围未列出。</strong></td><td rowspan="1">通用BLE协议_V1_0_12.md §6；设备功能说明.md §4.2</td></tr>
<tr><td rowspan="1">AP-015</td><td rowspan="1">充电温度</td><td rowspan="1">充电温度仅在充电中有效，只查询或上报，不可设置、不存 Flash；有效范围 −20～60℃。1 字节使用符号位加绝对值编码，FF 表示无效（未充电、拔线或采样失败），App 不得显示为 −127℃或 −1℃。0℃仅用 00 表示，禁止 80（−0）。</td><td rowspan="1"></td><td rowspan="1">通用BLE协议_V1_0_12.md，6，dpID=13</td></tr>
<tr><td rowspan="1">AP-016</td><td rowspan="1">WAV资源版本</td><td rowspan="1">资源版本独立于固件版本，主、次、修订共3段，仅查询或上报。无记录为00 00 00，上电读保存值，资源提交成功后更新，允许与旧版相同。</td><td rowspan="1"></td><td rowspan="1">通用BLE协议_V1_0_12.md，6，dpID=14</td></tr></tbody>
</table>

</details>

<details>
<summary>事件同步 · 3项</summary>

<table>
<thead>
<tr><th>编号</th><th>功能</th><th>需求</th><th>资料差异 / 缺项</th><th>依据</th></tr></thead>
<tbody>
<tr><td rowspan="1">AP-017</td><td rowspan="1">读取和确认清空</td><td rowspan="1">设备本地保存事件，App 主动获取。单包有效数据最多480字节，逐包校验；可被App其他命令挂起后继续。App确认总长度及包数正确并回成功后，设备清空事件存储区。</td><td rowspan="1"><strong>【待补/待确认】 未写事件容量、满存储、读取时新增事件及App保存后再确认的顺序。</strong></td><td rowspan="1">通用BLE协议_V1_0_12.md，5.8–5.10</td></tr>
<tr><td rowspan="1">AP-018</td><td rowspan="1">连续事件合并</td><td rowspan="1">相邻两次事件的 ID、情绪、环境标记相同，且前后时间差 &lt;60 秒时合并、次数增加，保留首次时间。60 秒在原文标为暂定值。原例：1、40、99、140 秒合为一条（时间 1 秒、次数 4），210 秒单列。</td><td rowspan="1"><strong>【待补/待确认】 60 秒为暂定值；次数为 1 字节，溢出处理未写明。</strong></td><td rowspan="1">通用BLE协议_V1_0_12.md，核心思想一，事件交互表</td></tr>
<tr><td rowspan="1">AP-019</td><td rowspan="1">事件时间和统计口径</td><td rowspan="1">事件记录包含 UTC Unix 秒时间戳、次数、情绪和环境标记；合并记录保留首次时间。协议情绪取值：0=ANY；1=开心，对应 HAPPY／CLINGY／PROUD／COZY；2=平静，对应 CURIOUS／SPACED；3=悲伤，对应 SLEEPY／RESTLESS／ALERT／SHY。</td><td rowspan="1"><strong>【待补/待确认】 10 类算法情绪的分组已有原表定义；实际转换的运行端和接入时机未写明。跨午夜合并记录只保留首时刻，逐次日期不可还原。</strong></td><td rowspan="1">通用BLE协议_V1_0_12.md，核心思想一，EventContext_t及示例；舵机动作统计表格 20260723 合并版本update_sound update 0901.xlsm｜情绪表 A2:C5</td></tr></tbody>
</table>

</details>

<details>
<summary>好友记录 · 2项</summary>

<table>
<thead>
<tr><th>编号</th><th>功能</th><th>需求</th><th>资料差异 / 缺项</th><th>依据</th></tr></thead>
<tbody>
<tr><td rowspan="1">AP-020</td><td rowspan="1">容量与相遇计数</td><td rowspan="1">相遇30秒后计为一次，保存首次、最近相遇及次数。次数超过255按255处理。最多20个好友；第21个加入时，先移除最久未相遇者，再按首次相遇更早、设备标识字典序最小依次判定。</td><td rowspan="1"><strong>【待补/待确认】 “30秒后”的等号边界、同一好友再次计次间隔未写明。</strong></td><td rowspan="1">通用BLE协议_V1_0_12.md，核心思想一，好友列表</td></tr>
<tr><td rowspan="1">AP-021</td><td rowspan="1">读取列表</td><td rowspan="1">App 读取全部本地好友，单条27字节；没有好友时文件长度和总包数为0，直接结束。结束确认没有规定清空好友。</td><td rowspan="1"><strong>【待补/待确认】 不能套用事件同步的确认后清空。</strong></td><td rowspan="1">通用BLE协议_V1_0_12.md，5.11–5.13</td></tr></tbody>
</table>

</details>

<details>
<summary>成长与行为 · 9项</summary>

<table>
<thead>
<tr><th>编号</th><th>功能</th><th>需求</th><th>资料差异 / 缺项</th><th>依据</th></tr></thead>
<tbody>
<tr><td rowspan="1">AP-022</td><td rowspan="1">实际成长分工</td><td rowspan="1">设备记录操作事件；App 获取事件集、计算成长特性，下发成长快照和行为查找表。设备存储和回传快照，不解析快照内容，按行为表执行。另一 App 可从设备读取成长快照。</td><td rowspan="1"><strong>【待补/待确认】 原流程标注“待优化”；成长计算公式和具体实现未提供。</strong></td><td rowspan="1">通用BLE协议_V1_0_12.md，7、5.19、5.23、核心思想一</td></tr>
<tr><td rowspan="1">AP-023</td><td rowspan="1">成长快照内容</td><td rowspan="1">成长快照草案包含格式版本、5 项五行数组（金木水火土）、阶段、阶段值（stage_grow_value，原注释“阶段正常值”）、状态序号和里程碑。</td><td rowspan="1"><strong>【待补/待确认】 字段含义及默认值、成长公式、阶段门槛和解锁条件未提供；字段类型位宽未定义业务取值范围。</strong></td><td rowspan="1">通用BLE协议_V1_0_12.md，核心思想二，Snapshot_t</td></tr>
<tr><td rowspan="1">AP-024</td><td rowspan="1">快照大小与保存</td><td rowspan="1">快照大小&gt;0且≤2816字节，单包有效数据≤480字节，每包及整文件CRC32校验。长度不必为11的整数倍。传完只暂存RAM，提交后才覆盖Flash原快照。读取只返回已落盘版本；无快照时长度和包数均为0。</td><td rowspan="1"><strong>【待补/待确认】 多 App 快照冲突处理、历史保留及回退规则未写明。</strong></td><td rowspan="1">通用BLE协议_V1_0_12.md，5.19–5.25、5.30</td></tr>
<tr><td rowspan="1">AP-025</td><td rowspan="1">规则表更新范围</td><td rowspan="1">规则表整表替换，不支持增量。每条7字节，最多256条，文件最大1792字节。空文件、超限或长度不是7的整数倍均拒绝。</td><td rowspan="1"></td><td rowspan="1">通用BLE协议_V1_0_12.md，5.26–5.29</td></tr>
<tr><td rowspan="1">AP-026</td><td rowspan="1">规则匹配与候选选择</td><td rowspan="1">条件中的事件值 0、情绪值 0、环境值 0，分别表示不比较该条件；非零事件和情绪要求相等，非零环境按位与规则匹配。多条命中时按 0～255 权重随机选一条，权重全为 0 时均匀随机。动作、声音、震动值 0xFF 分别表示该项不播放。</td><td rowspan="1"><strong>【待补/待确认】 环境按位与的完整判据、无效资源处理未写明。</strong></td><td rowspan="1">通用BLE协议_V1_0_12.md，核心思想一，BehaviorRule_t及匹配说明</td></tr>
<tr><td rowspan="1">AP-027</td><td rowspan="1">生效提交</td><td rowspan="1">行为表与快照传完只暂存 RAM，不立即生效、不写 Flash。App 提交生效后，已有暂存的两侧分别处理：行为表更新运行表并写 Flash；快照写 Flash。有则提交，无则跳过。提交前仍使用旧行为表，暂存快照不可读取。成功后清除待提交标记，防止重复擦写。</td><td rowspan="1"><strong>【待补/待确认】 两侧独立落盘；断电及部分提交后的恢复规则未写明。</strong></td><td rowspan="2">通用BLE协议_V1_0_12.md，5.30</td></tr>
<tr><td rowspan="1">AP-028</td><td rowspan="1">提交结果</td><td rowspan="1">只应答一次：0x00=两侧均有暂存且落盘；0x01=行为表空，有快照则提交快照；0x02=快照空，有行为表则提交行为表；0x03=两侧都空，不落盘。</td><td rowspan="1"><strong>【待补/待确认】 0x01和0x02不能一概显示全部失败。</strong></td></tr>
<tr><td rowspan="1">AP-029</td><td rowspan="1">重生转世续养</td><td rowspan="1">原文写：重生重置所有数据；转世不操作；续养停止成长算法。</td><td rowspan="1"><strong>【待补/待确认】 没有入口、清除范围、停止及恢复方式，也未说明与RESET的关系。</strong></td><td rowspan="1">通用BLE协议_V1_0_12.md，核心思想三</td></tr>
<tr><td rowspan="1">AP-040</td><td rowspan="1">喂食功能范围</td><td rowspan="1">取消喂食功能。</td><td rowspan="1"></td><td rowspan="1">通用BLE协议_V1_0_12.md 核心思想一 行为列表后说明</td></tr></tbody>
</table>

</details>

<details>
<summary>固件升级 · 3项</summary>

<table>
<thead>
<tr><th>编号</th><th>功能</th><th>需求</th><th>资料差异 / 缺项</th><th>依据</th></tr></thead>
<tbody>
<tr><td rowspan="1">AP-030</td><td rowspan="1">准入及版本</td><td rowspan="1">App 查询当前版本后申请升级；只接受高于当前版本的固件，相同或更低版本拒绝。BLE 协议写电量 &lt;25% 可拒绝，未鉴权、文件超限、单包长度异常也可拒绝；设备功能说明写电量 ≥20% 才允许升级。</td><td rowspan="1"><strong>【待补/待确认】 原资料存在 20% 与 25% 两种 OTA 电量门槛，待确认；固件文件大小上限未给出。</strong></td><td rowspan="1">通用BLE协议_V1_0_12.md §5.14～5.16；设备功能说明.md §4.3</td></tr>
<tr><td rowspan="1">AP-031</td><td rowspan="1">传输与安装</td><td rowspan="1">有效数据单包最多480字节，每包及整文件CRC32校验。总长度及校验正确后，结束应答成功，设备随后重启安装。</td><td rowspan="1"><strong>【待补/待确认】 结束应答不等于新固件已成功启动；安装后确认、断点续传和回滚未定义。</strong></td><td rowspan="1">通用BLE协议_V1_0_12.md，5.17–5.18</td></tr>
<tr><td rowspan="1">AP-032</td><td rowspan="1">超时与舵机升级</td><td rowspan="1">主固件OTA传输中8秒收不到数据即中止。BLE CMD-0x51被明确定义为“舵机MCU OTA数据透传”：主控不解析、不修改Data，舵机返回数据原样送回App；不能由该条推定已支持普通0x03/0x04/0x05动作控制的App透传入口。主固件OTA应答等待、重试及舵机OTA业务帧流程仍未完整提供。</td><td rowspan="1"><strong>【待补/待确认】 OTA 应答等待及重试次数未写明；舵机业务数据按舵机协议执行。</strong></td><td rowspan="1">设备功能说明.md §4.3；通用BLE协议_V1_0_12.md §5.31、WAV 文件传输总体说明</td></tr></tbody>
</table>

</details>

<details>
<summary>WAV资源更新 · 6项</summary>

<table>
<thead>
<tr><th>编号</th><th>功能</th><th>需求</th><th>资料差异 / 缺项</th><th>依据</th></tr></thead>
<tbody>
<tr><td rowspan="1">AP-033</td><td rowspan="1">全量模式及删除</td><td rowspan="1">当前仅支持0x00全量更新。App列出更新后全部WAV，提交成功后删除清单外WAV。0x01新增/替换和0x02删除均为预留，不支持。</td><td rowspan="1"></td><td rowspan="1">通用BLE协议_V1_0_12.md，WAV总体说明、5.32</td></tr>
<tr><td rowspan="1">AP-034</td><td rowspan="1">文件名与大小</td><td rowspan="1">文件名不含路径，只用小写a-z、0-9、下划线、连字符和点，后缀.wav。含后缀长5～128字节，同一会话不能重名。文件数≥1，每文件长度&gt;0，总大小为全部清单文件之和，含跳过的文件。</td><td rowspan="1"><strong>【待补/待确认】 单文件、个数和总大小上限原文待补充；10个文件及65536字节只是示例。</strong></td><td rowspan="2">通用BLE协议_V1_0_12.md，WAV总体说明、5.32–5.33</td></tr>
<tr><td rowspan="1">AP-035</td><td rowspan="1">准入和跳过</td><td rowspan="1">播放中或其他传输中返回忙；U盘模式先退出；非法参数不重试；存储未就绪或空间不足结束；未鉴权先鉴权。同名、同长度、同CRC32的文件无需重传，但仍须列在全量清单中。</td><td rowspan="1"></td></tr>
<tr><td rowspan="1">AP-036</td><td rowspan="1">顺序和分包确认</td><td rowspan="1">文件按0～个数−1顺序处理，前一文件完成才发下一文件。单包1～480字节，不得越过末尾。App按下一期望位置续传；丢弃不匹配当前包末尾位置的迟到成功应答。包成功不等于更新生效。</td><td rowspan="1"></td><td rowspan="1">通用BLE协议_V1_0_12.md，WAV总体说明、5.34</td></tr>
<tr><td rowspan="1">AP-037</td><td rowspan="1">超时重试和断连</td><td rowspan="1">App 等待开始、文件信息、数据应答为 3 秒，等待最终提交为 10 秒；超时或要求重发时，原帧最多重发 3 次。设备 8 秒无会话命令即结束会话，提交期间不计时。源协议规定更新失败、断连时保持原文件并恢复播放，App 重新从开始命令发起。</td><td rowspan="1"><strong>【待补/待确认】 “任何时候收到开始命令即重开”与“重复成功帧不重复处理”的优先关系未写明；最终提交成功但应答丢失时，结果确认方式未写明。</strong></td><td rowspan="1">通用BLE协议_V1_0_12.md，WAV总体说明</td></tr>
<tr><td rowspan="1">AP-038</td><td rowspan="1">提交播放和版本</td><td rowspan="1">只有最终提交成功才更新文件、删除清单外文件、记录新版本；失败保持原样。资源可同版或降版。会话期间禁播WAV，结束恢复。重复上一成功帧只重复应答，不重复执行。</td><td rowspan="1"><strong>【待补/待确认】 设备不解析WAV内容，素材采样率、位深、声道和编码未列。</strong></td><td rowspan="1">通用BLE协议_V1_0_12.md，WAV总体说明、5.35、6 dpID=14</td></tr></tbody>
</table>

</details>

<details>
<summary>传输能力 · 1项</summary>

<table>
<thead>
<tr><th>编号</th><th>功能</th><th>需求</th><th>资料差异 / 缺项</th><th>依据</th></tr></thead>
<tbody>
<tr><td rowspan="1">AP-039</td><td rowspan="1">包大小</td><td rowspan="1">MTU为512字节，文件分包有效数据上限480字节，不含包信息及帧头尾；文档列单帧最大498字节。</td><td rowspan="1"><strong>【待补/待确认】 手机无法达到该MTU时的协商或降包策略未写。</strong></td><td rowspan="1">通用BLE协议_V1_0_12.md，1</td></tr></tbody>
</table>

</details>

## 新增业务接口

情绪ID沿用原0/1/2/3，不新增情绪编码。基础动作映射、包状态回读、可靠事件批次及自定义控制链路仍需接通和联调。

<table>
<thead>
<tr><th>待补能力</th><th>产品要求</th><th>资料边界</th></tr></thead>
<tbody>
<tr><td rowspan="1">激活与模式查询</td><td rowspan="1">返回original/growth、实际生效stage、完整包ID、行为表校验值、摘要版本、主五行。首次包激活时切断旧批次/聚合，保存同刻好友计数基线，返回新记录边界与基线；之前增量只留历史，不计本档案成长。</td><td rowspan="1">新增产品定义；原快照不解析，不能以其stage字段直接当作设备完整包状态。</td></tr>
<tr><td rowspan="1">可靠事件批次</td><td rowspan="1">稳定记录/批次ID；查询时冻结批次；ACK只清已确认批，期间新事件写下一批；次数到255前拆新记录，避免回绕丢计数。</td><td rowspan="1">新增同步语义；原0x12成功说明为清空事件区，缺并发边界。</td></tr>
<tr><td rowspan="1">整包预检查</td><td rowspan="1">提交前检查当前包全部资源及版本；缺资源不进入提交；资源升级和成长包应用互斥。</td><td rowspan="1">新增产品要求；用来保证资源不全时旧包不变。</td></tr>
<tr><td rowspan="1">包读回与恢复</td><td rowspan="1">查询各侧实际生效版本/校验值。回滚重用当前档案内历史已确认成长基础规则，叠加当前绑定与当前摘要后形成新待应用包；不原样恢复旧绑定或旧里程碑位图。若要求断电后设备自动恢复完整上包，另需设备事务激活/双包保存能力。</td><td rowspan="1">行为版本查询、自动事务回滚均非现有协议已提供能力。</td></tr>
<tr><td rowspan="1">重置养成</td><td rowspan="1">恢复已验证原始行为表，清成长模式及摘要，解除自定义触摸绑定，确认结果后App再清对应账本。</td><td rowspan="1">新增业务范围；不能直接把现有恢复出厂指令当作等价实现。</td></tr>
<tr><td rowspan="1">自定义绑定</td><td rowspan="1">支持读取绑定版本、绑定/解绑与序列可用性；合成成长包前核对绑定仍有效。</td><td rowspan="1">现有资料未提供完整App动作业务接口。</td></tr>
<tr><td rowspan="1">无震动编译映射</td><td rowspan="1">业务逻辑0转换为wire 0xFF，1/2/3不变。</td><td rowspan="1">0xFF不输出来自原BehaviorRule_t；逻辑0只是产品表展示约定。</td></tr></tbody>
</table>

## App业务模块接口

<table>
<thead>
<tr><th>接口</th><th>产品要求</th><th>资料边界</th></tr></thead>
<tbody>
<tr><td rowspan="1">可靠事件批次</td><td rowspan="1">稳定记录/批次ID、冻结读取批次、ACK只清已保存记录、新事件写下一批；count满255前拆记录。</td><td rowspan="1">原0x10–0x12可复用，以上并发和去重字段尚未定义。</td></tr>
<tr><td rowspan="1">养成启用与整包确认</td><td rowspan="1">返回是否已启用、成长包ID、实际阶段、资源/行为/快照/主五行/绑定版本及启用序号边界；逐侧核对通过后才标整包成功。</td><td rowspan="1">原0x44两侧独立提交，不具备整包原子语义；新增字段/读回要求。</td></tr>
<tr><td rowspan="1">序列资源与时长</td><td rowspan="1">新增摇头一次/点头一次的真实ID、轴与零位、安全范围、周期、结束回执；规则含一个输入和有序步骤/次数。回读固件支持事件、正式步数/次数及安全总时长上限；完整规则按版本校验。</td><td rowspan="1">源13为连续点头3次；12/57/59未验证为本次单周期动作。原0x03只收令应答，0x04未定义串行/重复语义，0x05仍缺标定/字节序核对与App入口。</td></tr>
<tr><td rowspan="1">普通App预览控制</td><td rowspan="1">独立序列调度：任务ID、步骤进度、循环完成、整条完成/停止/中止/失败；停止取消余下。每步音频/震动各1次，全部结束才换步；禁止以串发0x03代替完成确认。</td><td rowspan="1">原普通反馈5秒机制继续有效；序列安全总时长与浅睡约6秒短唤醒协调待实现。0x51仅OTA透传；实际序列能力尚未验证。</td></tr>
<tr><td rowspan="1">震动档位</td><td rowspan="1">新步骤音频和震动默认关闭；可选验证配对，开始时各播放1次。0关闭、1弱、2中、3强到驱动/实际跨度/停止的映射按基础动作验证。</td><td rowspan="1">原资源表1–3有名称；控制板Moto命令缺完整强度/时长负载，0关闭为新增约定。</td></tr>
<tr><td rowspan="1">独立绑定层</td><td rowspan="1">一规则一输入，一输入一启用规则，最多8条已启用；完整传输后原子启用或替换输入，读回内容/版本；失败保留旧规则。轻摇23源Beta N须新增验收。屏蔽舵机自运动的普通IMU反触发，保护不中断检测。</td><td rowspan="1">源7字节规则只有单输出ID，不能直接表示有序步骤/次数；规则存储、事务替换、能力查询、IMU互锁和停止完成需新增。</td></tr>
<tr><td rowspan="1">重置范围</td><td rowspan="1">区分单输入恢复默认反馈（只解绑）、删除可编辑输入（先解绑再删资源）、重新开始养成（含全局恢复初始）与恢复出厂；每项明确清理范围和确认结果，不另设保留旧档案的全局恢复模式。</td><td rowspan="1">源“重生全重置/转世无操作/续养停成长”及dp12不足以代替这些细化业务，不能悄悄复用。</td></tr>
<tr><td rowspan="1">阶段历史证据</td><td rowspan="1">若后续需要显示互动发生时阶段，事件或激活历史须能关联包版本；首版只显示记录生成时已确认阶段。</td><td rowspan="1">现有事件只有ID/首UTC/count/emotion/flags，无成长阶段和包ID。</td></tr></tbody>
</table>

[返回完整PRD目录](../README.md) · [上一章](./02-firmware.md) · [下一章](./04-app-ux.md)
