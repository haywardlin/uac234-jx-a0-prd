# 02 固件需求

[返回完整PRD目录](../README.md) · [上一章](./01-product-hardware.md) · [下一章](./03-app-protocol.md)

73项原始功能要求，保留时间、数值、状态限制和来源。

## 关键时间与数值

<table>
<thead>
<tr><th>功能</th><th>明确值与边界</th><th>依据</th></tr></thead>
<tbody>
<tr><td>开机/关机</td><td>按住满3秒开机；长按4秒关机。开机震动约0.3秒，约3秒后传感器就绪；关机震动约1秒、关机动作约3秒。</td><td>设备功能说明.md §2</td></tr>
<tr><td>绑定/鉴权</td><td>发起绑定后60秒内单击确认；每次连接后65秒内完成鉴权。</td><td>设备功能说明.md §4.1</td></tr>
<tr><td>充电/拔出</td><td>插入5秒后待机；已有静默或睡眠条件时直接待机；连续约2秒检测不到充电才确认拔出。</td><td>设备功能说明.md §5.1</td></tr>
<tr><td>浅睡</td><td>连续1分钟无触摸或姿态事件进入；光感不重置；放下确认中不进入。</td><td>设备功能说明.md §6.1</td></tr>
<tr><td>深度待机</td><td>充电、行为静默、睡眠时段满足任一即进入；三项全部解除才退出；蓝牙仍可用。</td><td>设备功能说明.md §6.2</td></tr>
<tr><td>触摸</td><td>&lt;1秒松手=碰一碰；1～&lt;3秒松手=撸一撸；满3秒立即触发长抚；握持原文为“肚子+背部任意两个区域同时按住满5秒”，松手触发。</td><td>设备功能说明.md §8.1</td></tr>
<tr><td>光感</td><td>低于10持续约2.5秒变暗；高于950解除暗状态；高于1000持续约2.5秒变亮；回到60以下后可再次变亮。阈值均为原始值，不是lux。开机/退出待机约8秒内抑制光感事件。</td><td>设备功能说明.md §8.3</td></tr>
<tr><td>IMU</td><td>10ms采样；Active最长约2.5秒；200ms冷却；拿起累计约300ms、放下稳定约2秒；各姿态阈值完整保留在固件表。</td><td>八个IMU事件触发标准.md</td></tr>
<tr><td>优先级</td><td>系统&gt;交友&gt;姿态&gt;触摸&gt;光感；高优先级打断，同级或低级丢弃；同事件0.5秒去重；IMU后约1秒不识别触摸。</td><td>设备功能说明.md §8.7</td></tr>
<tr><td>名称/音量</td><td>名称最多25字节；音量6档0/20/40/60/80/100%，默认第4档60%，重启保留。</td><td>设备功能说明.md §4.2；BLE协议 §6</td></tr>
<tr><td>主导五行</td><td>dpID=8：1金、2木、3水、4火、5土。Python：0木、1火、2土、3金、4水。按名称转换。</td><td>BLE协议 §6；daily_emotion_liunian.py</td></tr>
<tr><td>成长快照/行为表</td><td>快照0&lt;长度≤2816字节；行为表7字节/行，≤256行、≤1792字节，整表替换。</td><td>BLE协议 §5.19～5.30</td></tr>
<tr><td>生效结果</td><td>0x44独立处理两侧：00两侧落盘；01行为表空、有快照则落快照；02快照空、有行为表则落行为表；03两侧都空。</td><td>BLE协议 §5.30</td></tr>
<tr><td>舵机编号</td><td>0x03传32项预置映射索引；0x04示例直接传动作号。不能互换，也不能直接等同动作统计表1～61编号。</td><td>舵机控制板协议 V1.4</td></tr>
<tr><td>WAV更新</td><td>全量清单；单包≤480字节；开始/信息/数据应答等3秒，提交等10秒；原帧最多重发3次；8秒无会话命令结束。</td><td>BLE协议 WAV总体说明、§5.32～5.35</td></tr></tbody>
</table>

<details>
<summary>开关机与充电 · 15项</summary>

<table>
<thead>
<tr><th>编号</th><th>功能</th><th>需求</th><th>资料差异 / 缺项</th><th>依据</th></tr></thead>
<tbody>
<tr><td rowspan="1">FW-001</td><td rowspan="1">按键开机</td><td rowspan="1">关机状态下必须按住按键满 3 秒才开机；提前松手不开机。电压 ≤ 3.45V 时拒绝开机且无任何反应。</td><td rowspan="1"></td><td rowspan="4">设备功能说明.md｜2.1 开机</td></tr>
<tr><td rowspan="1">FW-002</td><td rowspan="1">首次接电与复位</td><td rowspan="1">电池首次接入或设备复位时，电压正常则自动开机。</td><td rowspan="1"></td></tr>
<tr><td rowspan="1">FW-003</td><td rowspan="1">关机状态充电</td><td rowspan="1">关机状态下插入充电不触发开机，只在后台充电；拔掉充电后继续保持关机。</td><td rowspan="1"></td></tr>
<tr><td rowspan="1">FW-004</td><td rowspan="1">开机过程</td><td rowspan="1">1、马达震动约 0.3 秒。<br>2、约 3 秒后传感器就绪，然后播放开机动作和伴音，蓝牙开始可被发现。</td><td rowspan="1"><strong>【待补/待确认】 “约 3 秒后”的计时起点及整机启动总耗时未写明。</strong></td></tr>
<tr><td rowspan="1">FW-005</td><td rowspan="1">正常关机</td><td rowspan="1">长按按键 4 秒关机；马达震动约 1 秒，播放关机动作约 3 秒，保存数据后关机。</td><td rowspan="1"></td><td rowspan="2">设备功能说明.md｜2.2 关机</td></tr>
<tr><td rowspan="1">FW-006</td><td rowspan="1">保护关机</td><td rowspan="1">低电保护、过温保护触发静默关机，不播放关机动作。</td><td rowspan="1"></td></tr>
<tr><td rowspan="1">FW-013</td><td rowspan="1">插入充电</td><td rowspan="1">1、开机状态下插入充电时播放充电动作，5 秒后进入待机；此后触摸、摇晃不再回应。<br>2、插入充电时如果已处于“静音”或睡眠时段，直接进入待机，不经过通常的插入反馈流程。</td><td rowspan="1"><strong>【待补/待确认】 “静音”与音量 0%／行为静默的对应关系未写明。</strong></td><td rowspan="3">设备功能说明.md｜5.1 开机状态下插拔充电</td></tr>
<tr><td rowspan="1">FW-014</td><td rowspan="1">拔出充电</td><td rowspan="1">连续约 2 秒检测不到充电才确认拔出；之后退出待机、恢复互动，拔出本身不播放动作。</td><td rowspan="1"><strong>【待补/待确认】 本节写拔出恢复互动；6.2 要求所有待机条件全部解除才恢复。静默或睡眠仍有效时按 6.2 保持待机，需核对两节口径。</strong></td></tr>
<tr><td rowspan="1">FW-015</td><td rowspan="1">充满电</td><td rowspan="1">充满电不播放“充电完成”动作；会通知无线充电座已经充满。</td><td rowspan="1"></td></tr>
<tr><td rowspan="1">FW-016</td><td rowspan="1">低电提示</td><td rowspan="1">电量第一次降到 20%、10%、0% 时，各播放一次低电动作；若处于浅睡，则短暂唤醒后播放。</td><td rowspan="1"><strong>【待补/待确认】 动作统计表“状态”页的低电备注末尾写“删掉”，删除范围未写明；此处保留设备说明的提示规则。</strong></td><td rowspan="1">设备功能说明.md｜5.2 低电提示</td></tr>
<tr><td rowspan="1">FW-017</td><td rowspan="1">低压保护</td><td rowspan="1">1、电压连续 3 次检测为 &lt; 3.40V 时静默关机；检测周期约 30 秒一次。<br>2、只有电压 &gt; 3.45V 才允许开机；电压 ≤ 3.45V 拒绝开机。</td><td rowspan="1"></td><td rowspan="1">设备功能说明.md｜5.3 低电保护</td></tr>
<tr><td rowspan="1">FW-018</td><td rowspan="1">温度保护生效范围</td><td rowspan="1">温度保护仅在充电时生效。</td><td rowspan="1"></td><td rowspan="4">设备功能说明.md｜5.4 温度保护（只在充电时生效）</td></tr>
<tr><td rowspan="1">FW-019</td><td rowspan="1">46℃充电保护</td><td rowspan="1">电池温度 ≥ 46°C 时降低充满电压；电压 ≥ 4.1V 时停止充电，电压降到 4.0V 以下后恢复充电。</td><td rowspan="1"><strong>【待补/待确认】 “4.0 V 以下”的等值边界未进一步定义。</strong></td></tr>
<tr><td rowspan="1">FW-020</td><td rowspan="1">57℃停充与恢复</td><td rowspan="1">电池温度 ≥ 57°C 时停止充电；温度降到 55°C 以下后恢复充电。</td><td rowspan="1"><strong>【待补/待确认】 “55℃以下”的等值边界未进一步定义。</strong></td></tr>
<tr><td rowspan="1">FW-021</td><td rowspan="1">60℃静默关机</td><td rowspan="1">电池温度 ≥ 60°C 时静默关机。</td><td rowspan="1"><strong>【待补/待确认】 46℃／57℃／60℃保护条件重叠时的执行与恢复次序未写明。</strong></td></tr></tbody>
</table>

</details>

<details>
<summary>按键操作 · 5项</summary>

<table>
<thead>
<tr><th>编号</th><th>功能</th><th>需求</th><th>资料差异 / 缺项</th><th>依据</th></tr></thead>
<tbody>
<tr><td rowspan="1">FW-007</td><td rowspan="1">多击间隔</td><td rowspan="1">多次点击时，每两次点击之间的间隔必须 &lt; 0.4 秒。</td><td rowspan="1"></td><td rowspan="5">设备功能说明.md｜3. 按键操作</td></tr>
<tr><td rowspan="1">FW-008</td><td rowspan="1">单击与双击</td><td rowspan="1">1、只在 App 发起绑定后的 60 秒内，单击按键才执行绑定确认；其他时间单击无作用。<br>2、双击按键断开当前蓝牙连接，清除本次鉴权，重新进入可被发现状态。</td><td rowspan="1"></td></tr>
<tr><td rowspan="1">FW-009</td><td rowspan="1">三击与长按 2 秒</td><td rowspan="1">1、三击按键无功能。<br>2、长按 2 秒无功能。</td><td rowspan="1"></td></tr>
<tr><td rowspan="1">FW-010</td><td rowspan="1">四击 U 盘模式</td><td rowspan="1">四击按键进入 U 盘模式，属于临时调试功能；无法通过按键退出。</td><td rowspan="1"><strong>【待补/待确认】 退出方式未写明。</strong></td></tr>
<tr><td rowspan="1">FW-011</td><td rowspan="1">五击与六击</td><td rowspan="1">1、只有产线先开启该功能后，五击按键才可进入老化模式 3。<br>2、六击按键重启设备。</td><td rowspan="1"></td></tr></tbody>
</table>

</details>

<details>
<summary>蓝牙发现 · 1项</summary>

<table>
<thead>
<tr><th>编号</th><th>功能</th><th>需求</th><th>资料差异 / 缺项</th><th>依据</th></tr></thead>
<tbody>
<tr><td rowspan="1">FW-012</td><td rowspan="1">蓝牙发现</td><td rowspan="1">开机后蓝牙可被发现；连接断开后立刻重新进入可被发现状态。</td><td rowspan="1"></td><td rowspan="1">设备功能说明.md｜4.1 连接与绑定</td></tr></tbody>
</table>

</details>

<details>
<summary>工作状态与行为拦截 · 11项</summary>

<table>
<thead>
<tr><th>编号</th><th>功能</th><th>需求</th><th>资料差异 / 缺项</th><th>依据</th></tr></thead>
<tbody>
<tr><td rowspan="1">FW-022</td><td rowspan="1">浅睡进入条件</td><td rowspan="1">连续 1 分钟没有触摸或姿态事件时进入浅睡；光线变化不重置该计时；正在确认放下时不进入浅睡。</td><td rowspan="1"></td><td rowspan="6">设备功能说明.md｜6.1 浅睡</td></tr>
<tr><td rowspan="1">FW-023</td><td rowspan="1">浅睡硬件状态</td><td rowspan="1">浅睡时动作模块、马达和扬声器断电；触摸、姿态与光感继续检测。</td><td rowspan="1"><strong>【待补/待确认】 IMU 标准写“芯片深睡时摸不到”；与本节“触摸继续检测”的状态对应关系需确认。</strong></td></tr>
<tr><td rowspan="1">FW-024</td><td rowspan="1">浅睡完全唤醒</td><td rowspan="1">1、触摸、拿起或晃动、说出 Hello Beany、遇到其他 Beany 均可完全唤醒，回到正常状态。姿态传感器检测到运动即唤醒。<br>2、因触摸醒来后，补播本次触摸的反应。</td><td rowspan="1"></td></tr>
<tr><td rowspan="1">FW-025</td><td rowspan="1">浅睡短暂唤醒</td><td rowspan="1">光线变暗/变亮、呼吸、2 小时无互动、48 小时无互动和低电提示，可短暂唤醒：上电约 6 秒做一个动作，然后返回浅睡；该短暂唤醒不算作互动。</td><td rowspan="1"></td></tr>
<tr><td rowspan="1">FW-026</td><td rowspan="1">呼吸</td><td rowspan="1">距上次互动 10 分钟首次呼吸，其后每 10 分钟一次；距上次互动满 2 小时后停止呼吸。</td><td rowspan="1"><strong>【待补/待确认】 输入事件表写无互动 5 分钟～2 小时期间每 30 秒呼吸一次；状态页写“不要”。各版本规则并存，未统一。</strong></td></tr>
<tr><td rowspan="1">FW-027</td><td rowspan="1">2 小时与 48 小时无互动</td><td rowspan="1">2 小时无互动、48 小时无互动分别各触发一次；发生互动后重新计时。</td><td rowspan="1"><strong>【待补/待确认】 输入事件表名称使用 &gt;2 hours、&gt;48 hours，正好达到阈值时的边界需统一。</strong></td></tr>
<tr><td rowspan="1">FW-028</td><td rowspan="1">深度待机进入</td><td rowspan="1">以下条件满足任一项即进入待机：正在充电且插入已 5 秒；App 开启行为静默；当前处在 App 设置的睡眠时段。</td><td rowspan="1"></td><td rowspan="3">设备功能说明.md｜6.2 待机（深度省电）</td></tr>
<tr><td rowspan="1">FW-029</td><td rowspan="1">深度待机状态</td><td rowspan="1">待机时音频、语音识别、触摸与动作模块全部断电；所有互动和唤醒均不响应，唤醒词无效。蓝牙仍可用，App 可连接、查询和设置。</td><td rowspan="1"></td></tr>
<tr><td rowspan="1">FW-030</td><td rowspan="1">深度待机退出</td><td rowspan="1">进入待机的所有条件全部解除后自动恢复；恢复后约 8 秒内不触发光线事件。</td><td rowspan="1"></td></tr>
<tr><td rowspan="1">FW-031</td><td rowspan="1">行为拦截</td><td rowspan="1">1、环境处于“暗”状态时，事件不执行动作且不写入事件记录；“变暗”事件本身为例外，仍可执行。<br>2、App 开启行为静默时，事件不执行动作、不写入事件记录，无例外。<br>3、充电中事件不执行动作、不写入事件记录；充电事件、开机事件为例外，仍可执行。<br>4、睡眠时段内事件不执行动作、不写入事件记录，无例外。</td><td rowspan="1"><strong>【待补/待确认】 动作统计表“状态”页对暗状态写不发声、不动作、不震动；本节允许变暗事件本身执行，存在差异。</strong></td><td rowspan="2">设备功能说明.md｜7. 不响应的情况（行为拦截）</td></tr>
<tr><td rowspan="1">FW-032</td><td rowspan="1">拦截后的无互动计时</td><td rowspan="1">被拦截的触摸、姿态等互动仍会重置 2 小时/48 小时的无互动计时。</td><td rowspan="1"><strong>【待补/待确认】 待机部分输入断电。该规则对未采集到的触摸事件如何适用，原文未写明。</strong></td></tr></tbody>
</table>

</details>

<details>
<summary>触摸、光感、唤醒与交友 · 12项</summary>

<table>
<thead>
<tr><th>编号</th><th>功能</th><th>需求</th><th>资料差异 / 缺项</th><th>依据</th></tr></thead>
<tbody>
<tr><td rowspan="1">FW-033</td><td rowspan="1">触摸区域</td><td rowspan="1">共 7 个触摸区域：头顶、头左侧、头右侧、后背、身体左侧、身体右侧、肚子；前 3 种触摸手势每区均可触发，7×3=21 种，加握持共 22 种触摸事件。</td><td rowspan="1"></td><td rowspan="6">设备功能说明.md｜8.1 触摸</td></tr>
<tr><td rowspan="1">FW-034</td><td rowspan="1">碰一碰</td><td rowspan="1">按下时长 &lt; 1 秒即松开，判定“碰一碰”，在松手时触发。</td><td rowspan="1"></td></tr>
<tr><td rowspan="1">FW-035</td><td rowspan="1">撸一撸</td><td rowspan="1">按住时长 ≥ 1 秒且 &lt; 3 秒时松开，判定“撸一撸”，在松手时触发。</td><td rowspan="1"></td></tr>
<tr><td rowspan="1">FW-036</td><td rowspan="1">长时间抚摸</td><td rowspan="1">按住满 3 秒立即触发“长时间抚摸”；之后松手不重复触发。</td><td rowspan="1"><strong>【待补/待确认】 输入事件表写 &gt;3 秒，设备说明写满 3 秒立即触发。输入表还列 &gt;10 秒校准，但未给出校准动作。</strong></td></tr>
<tr><td rowspan="1">FW-037</td><td rowspan="1">长时间握持</td><td rowspan="1">原文条件为“肚子 + 背部任意两个区域，同时按住满 5 秒”；在松手时触发握持。</td><td rowspan="1"><strong>【待补/待确认】 “肚子＋背部任意两个区域”的总区域数量不明确。输入事件表另写 5 秒以上、&lt;10 秒；与满 3 秒长抚摸的互斥时序未写明。</strong></td></tr>
<tr><td rowspan="1">FW-038</td><td rowspan="1">触摸竞争</td><td rowspan="1">1、多个手势同时成立时，优先级为：握持 &gt; 长时间抚摸 &gt; 撸一撸 &gt; 碰一碰。<br>2、手势相同时，区域优先级为：头顶 &gt; 肚子 &gt; 头左/头右 &gt; 后背 &gt; 身体两侧。</td><td rowspan="1"></td></tr>
<tr><td rowspan="1">FW-039</td><td rowspan="1">光感触发时长</td><td rowspan="1">1、光线降到接近全黑且连续约 2.5 秒时，触发变暗事件。<br>2、光线升到明亮水平且连续约 2.5 秒时，触发变亮事件。</td><td rowspan="1"></td><td rowspan="3">设备功能说明.md｜8.3 光感（变暗 / 变亮）</td></tr>
<tr><td rowspan="1">FW-040</td><td rowspan="1">光感阈值与再次触发</td><td rowspan="1">1、变暗后进入暗状态，普通互动不响应；直到光线恢复明亮才解除。解除暗状态本身不触发事件。<br>2、变暗事件后须先恢复明亮，才能再次触发变暗；变亮事件后须先回到较暗，才能再次触发变亮。<br>3、日志光感原始值 &lt; 10 判定变暗；&gt; 950 解除暗状态；从正常状态 &gt; 1000 判定变亮；回落到 60 以下后才允许再次触发变亮。以上是原始值，不是 lux。</td><td rowspan="1"><strong>【待补/待确认】 60 以下保留原文。暗状态解除后又满足变亮门槛的处理顺序未写明。</strong></td></tr>
<tr><td rowspan="1">FW-041</td><td rowspan="1">光感抑制与计时</td><td rowspan="1">1、开机或退出待机后约 8 秒内，仅记录亮暗状态，不触发光线事件。<br>2、光线事件不算作互动，不推迟浅睡。</td><td rowspan="1"></td></tr>
<tr><td rowspan="1">FW-042</td><td rowspan="1">语音唤醒</td><td rowspan="1">1、离线唤醒词为 Hello Beany；识别后播放“唤醒提示”动作；浅睡中会完全唤醒。<br>2、待机状态下语音识别断电，唤醒词无效。<br>3、环境暗、充电中、“静音”或睡眠时段内，唤醒词不产生动作。<br>4、唤醒提示在《设备功能说明》§8.6 列为系统事件，参与系统 &gt; 交友 &gt; 姿态 &gt; 触摸 &gt; 光感的优先级。</td><td rowspan="1"><strong>【待补/待确认】 设备功能说明 §8.6 已将唤醒提示归入系统事件；强制静音、自动静音及其他限制状态下的具体输出组合见本轮补充规则。</strong></td><td rowspan="1">设备功能说明.md｜8.4 唤醒词</td></tr>
<tr><td rowspan="1">FW-043</td><td rowspan="1">交友触发</td><td rowspan="1">1、必须已绑定 App 且交友开关打开，才启用遇到其他 Beany 的交友逻辑。<br>2、另一只 Beany 在约 5 米内持续 30 秒，首次见面触发“遇到新朋友”，此前见过则触发“遇到老朋友”。</td><td rowspan="1"></td><td rowspan="2">设备功能说明.md｜8.5 遇到其他 Beany（交友）</td></tr>
<tr><td rowspan="1">FW-044</td><td rowspan="1">好友离开</td><td rowspan="1">对方走远到约 10 米外或信号消失，累计 10 分钟后判定离开；离开不触发动作，只更新 App 好友状态。</td><td rowspan="1"></td></tr></tbody>
</table>

</details>

<details>
<summary>反馈选择与优先级 · 4项</summary>

<table>
<thead>
<tr><th>编号</th><th>功能</th><th>需求</th><th>资料差异 / 缺项</th><th>依据</th></tr></thead>
<tbody>
<tr><td rowspan="1">FW-045</td><td rowspan="1">行为候选选择</td><td rowspan="1">每个事件对应若干套候选动作，每套包括动作和伴音，部分带震动；随机选一套执行。App 可整体替换该规则表。</td><td rowspan="1"><strong>【待补/待确认】 初始映射按设备说明附录指定的初始成长表保留；其他表的候选差异在交互矩阵中单列。</strong></td><td rowspan="4">设备功能说明.md｜8.7 事件响应规则</td></tr>
<tr><td rowspan="1">FW-046</td><td rowspan="1">事件去重与触摸让路</td><td rowspan="1">1、同一个事件在 0.5 秒内只响应一次。<br>2、姿态事件触发后约 1 秒内不识别触摸。</td><td rowspan="1"></td></tr>
<tr><td rowspan="1">FW-047</td><td rowspan="1">事件优先级与抢占</td><td rowspan="1">1、事件类别优先级为：系统 &gt; 交友 &gt; 姿态 &gt; 触摸 &gt; 光感。<br>2、播放中收到更高类别事件时，打断当前动作并立即执行新事件。<br>3、播放中收到相同或更低类别事件时直接丢弃，不排队。</td><td rowspan="1"></td></tr>
<tr><td rowspan="1">FW-048</td><td rowspan="1">动作完成判定</td><td rowspan="1">伴音播放完毕视为动作结束，最长按 5 秒计。</td><td rowspan="1"><strong>【待补/待确认】 此处按伴音结束或最长 5 秒判定；舵机控制板的“命令接收成功”不是机械动作完成确认。</strong></td></tr></tbody>
</table>

</details>

<details>
<summary>IMU事件判定 · 15项</summary>

<table>
<thead>
<tr><th>编号</th><th>功能</th><th>需求</th><th>资料差异 / 缺项</th><th>依据</th></tr></thead>
<tbody>
<tr><td rowspan="1">FW-049</td><td rowspan="1">IMU 采样与手势段</td><td rowspan="1">1、IMU 采样周期为 10ms。<br>2、手势段依次为 Idle → Active（最长约 2.5s）→ Parse → Cooldown（200ms）。<br>3、共 8 个 IMU 事件：拿起、放下、轻摇、猛摇、倾倒、翻转、上抛、旋转上抛；拿起/放下采用独立互锁状态机，不进入手势配方表。</td><td rowspan="1"></td><td rowspan="1">八个IMU事件触发标准.md</td></tr>
<tr><td rowspan="1">FW-050</td><td rowspan="1">IMU 互斥与未识别输入</td><td rowspan="1">1、同一次动作只报一个手势；优先级为旋转上抛 &gt; 上抛 &gt; 猛摇 &gt; 翻转 &gt; 倾倒 &gt; 轻摇。同事件 500ms 内去重，任意 IMU 事件上报后约 1s 内触摸解析让路。<br>2、大幅运动若未命中任一明确事件，则无互动反馈；当前没有“随机事件”兜底。</td><td rowspan="1"></td><td rowspan="1">八个IMU事件触发标准.md；八个IMU事件触发标准.md｜当前没有的项</td></tr>
<tr><td rowspan="1">FW-051</td><td rowspan="1">拿起：前置与门槛</td><td rowspan="1">1、玩具已在桌上：刚放下，或水平静置约 1 分钟进入浅睡后被 IMU 唤醒；再用手拎起。<br>2、拿起需有触摸，触摸有效约 800ms；浅睡被 IMU 唤醒后约 3s 内可豁免触摸条件。<br>3、离桌运动满足任一条件：陀螺合速度 ≥ 45°/s，或合加速度偏离 1g 的幅度 ≥ 0.25g。<br>4、触摸与离桌运动条件累计约 300ms；中间允许约 120ms 断帧，匀速稳拎不清零。</td><td rowspan="1"></td><td rowspan="2">八个IMU事件触发标准.md｜拿起 `EVENT_MOTION_PICKED_UP`</td></tr>
<tr><td rowspan="1">FW-052</td><td rowspan="1">拿起：互锁与排除</td><td rowspan="1">1、仅在“桌上”状态可上报拿起；上报后必须先放下或再次坐姿浅睡唤醒才能再报。上电时若为坐姿，初始化为桌上；非坐姿初始化为在手上，不上报拿起。<br>2、同一拍已上报轻摇、猛摇、翻转、倾倒、上抛或旋转上抛时，不再上报拿起，但物理状态记为“在手上”。<br>3、桌上微晃、未离桌触碰不算拿起；不触摸直接拎起也不算，浅睡 IMU 唤醒后约 3s 的豁免期除外。<br>4、旧口径“静置约 5s 后首次拿起”已不适用；当前桌上静置进入浅睡的门槛为约 1 分钟。</td><td rowspan="1"></td></tr>
<tr><td rowspan="1">FW-053</td><td rowspan="1">放下：姿态与时间</td><td rowspan="1">1、玩耍后坐姿平稳放下、手离开，连续稳定约 2 秒后触发放下。<br>2、坐姿指接近水平放置：俯仰约 0°，横滚贴近 ±180°。<br>3、平稳要求陀螺 &lt; 35°/s 且合加速度偏离 1g 的幅度 &lt; 0.35g；最近约 800ms 内没有触摸。</td><td rowspan="1"></td><td rowspan="3">八个IMU事件触发标准.md｜放下 `EVENT_MOTION_PUT_DOWN`</td></tr>
<tr><td rowspan="1">FW-054</td><td rowspan="1">放下：互锁与计时</td><td rowspan="1">1、仅“在手上”可上报放下；上报后必须先拿起或被其他手势改为在手上，才能再次上报。不支持连续放下。<br>2、宽坐姿内小晃、触摸毛刺只暂停放下计时，不清零。<br>3、明显离开坐姿，或陀螺 ≥ 80°/s 时退回“在手上”，放下计时清零。<br>4、轻摇、猛摇、翻转、倾倒、上抛、旋转上抛会打断放下，并记为“在手上”；放下确认期间不进入浅睡。</td><td rowspan="1"></td></tr>
<tr><td rowspan="1">FW-055</td><td rowspan="1">放下：排除与旧规则</td><td rowspan="1">1、倾斜、侧倒、倒立放下不属于放下事件；手仍放在玩具上的静置也不属于放下。<br>2、当前确认延时约 2s；旧规则“3 秒确认”及“最近 10 秒有其他 motion 则不报”已不存在。</td><td rowspan="1"></td></tr>
<tr><td rowspan="1">FW-056</td><td rowspan="1">轻摇</td><td rowspan="1">1、手持玩具在约 2s 观察窗内，轻柔往复至少 2 次，方向不限，可左右、上下或斜向。<br>2、往复次数 ≥ 2；有效半周（去、回各为一段）都 ≥ 300ms；陀螺或加速度能量达到轻摇地板。<br>3、同一段能量达到猛摇条件则报猛摇；可识别为摇但强度不足猛摇时，落入轻摇。已构成上抛链或合格倾倒时不报轻摇。<br>4、离手抛掷、快速剧烈甩动、翻面/侧倒中的单次摆动不属于轻摇。</td><td rowspan="1"><strong>【待补/待确认】 “轻摇地板”对应的能量阈值未写明。</strong></td><td rowspan="1">八个IMU事件触发标准.md｜轻摇 `EVENT_MOTION_GENTLE_SHAKE`</td></tr>
<tr><td rowspan="1">FW-057</td><td rowspan="1">猛摇</td><td rowspan="1">1、手持快速、连续、剧烈往复至少 2 次，方向不限；不要求半周时长，主要按能量判断。<br>2、猛摇优先级高于翻转、倾倒、轻摇，低于上抛和旋转上抛；同段已构成上抛链时不报猛摇。<br>3、已离手的空中运动、上抛动作不属于猛摇；能认出为摇但强度不足时归入轻摇。</td><td rowspan="1"><strong>【待补/待确认】 猛摇的能量阈值和观察窗未写明。</strong></td><td rowspan="1">八个IMU事件触发标准.md｜猛摇 `EVENT_MOTION_HARD_SHAKE`</td></tr>
<tr><td rowspan="1">FW-058</td><td rowspan="1">倾倒：姿态与角度</td><td rowspan="1">1、先在桌上坐稳：正立且低角速度约 200ms 后锁定正立基线，再由正立推倒。开段已经侧躺不算倾倒。<br>2、推倒到前、后、左、右任一侧躺带：俯仰或横滚约 55°～125°，侧躺后短时静稳约 300ms。<br>3、相对正立，横滚或俯仰变化至少约 30°；偏航峰峰值 ≤ 约 50°，偏航角速度 &lt; 约 120°/s；过程中角速度约 55～750°/s。</td><td rowspan="1"></td><td rowspan="2">八个IMU事件触发标准.md｜倾倒 `EVENT_MOTION_TILT_SIDE`</td></tr>
<tr><td rowspan="1">FW-059</td><td rowspan="1">倾倒：互斥与排除</td><td rowspan="1">1、上抛、失重、翻转过程中的倾斜不报倾倒；报过倾倒后清掉正立锁，必须重新坐稳才能再次倾倒。<br>2、摔落后已经侧躺但没有从正立推倒的过程、桌上微晃均不属于倾倒。推倒后应短暂停住，不立刻扶正或继续摇。</td><td rowspan="1"></td></tr>
<tr><td rowspan="1">FW-060</td><td rowspan="1">翻转</td><td rowspan="1">1、先明显侧躺，俯仰或横滚约 55°～125°并保持约 300ms；再绕竖直轴转过约 150°以上，使原来朝上的一面变为朝下（肚皮翻面）。<br>2、翻转过程中需有明显转动，陀螺峰值 ≥ 约 50°/s。<br>3、必须先进入侧带再翻，水平坐姿原地转身不算；本段已构成上抛链则不报翻转；判定翻转后禁止倾倒配方。<br>4、单纯侧倾 90°、水平放置下转身、头尾翻/上下颠倒，以及净转角不足约 150°的小幅来回摆，不属于翻转。</td><td rowspan="1"><strong>【待补/待确认】 设备说明写“侧躺后翻约半圈让肚皮朝上”；IMU 标准写绕竖直轴、原来朝上的面变朝下。终态与轴向需统一。</strong></td><td rowspan="1">八个IMU事件触发标准.md｜翻转 `EVENT_MOTION_FLIP_BELLY_UP`</td></tr>
<tr><td rowspan="1">FW-061</td><td rowspan="1">上抛：完整空中链</td><td rowspan="1">1、手持主动抛向空中，离手后完成空中过程，落地或接住后再上报；尽量在下降/落地确认后上报，不在出手瞬间上报。<br>2、出手加速要求合加速度 ≥ 约 1.5g；随后失重要求合加速度 &lt; 约 0.4g；原文失重时长为“严空挡约 150ms，短谷也可约 70ms”。<br>3、落地冲击原文给出硬冲击约 1.8g、软接约 1.5g；冲击后再确认约 80ms 无二次失重。</td><td rowspan="1"></td><td rowspan="2">八个IMU事件触发标准.md｜上抛 `EVENT_MOTION_TOSS_UP`</td></tr>
<tr><td rowspan="1">FW-062</td><td rowspan="1">上抛：圈量与收段</td><td rowspan="1">1、空中体轴转角 &lt; 约 300°（不到约 5/6 圈）报上抛；达到该角度则升格为旋转上抛。<br>2、允许竖着抛（Z）或侧着抛（X/Y）。普通上抛一般在段结束后上报：落地相对平稳，或 Active 超时约 2.5s；旋转上抛可在落地确认后提前收段。<br>3、失重谷到冲击间隔超过约 800ms 的软链不识别，避免长时间摇晃拼出错误包络。<br>4、未离手甩动（手里摇时合加速度仍贴近 1g）、倒着抛、原地快速翻面不属于普通上抛；空中明显连续旋转归入旋转上抛。</td><td rowspan="1"></td></tr>
<tr><td rowspan="1">FW-063</td><td rowspan="1">旋转上抛</td><td rowspan="1">1、满足普通上抛的完整空中链，同时空中绕体轴转过约 300°及以上（约 5/6 圈），判为旋转上抛；两圈以上仍报同一事件。<br>2、允许头尾翻滚、上下颠倒；只要属于同一次抛掷，起飞与落地姿态均不限。<br>3、旋转上抛优先级最高；圈量达到时可在落地确认后提前收段上报；圈量不够则仍报普通上抛且不提前收段。</td><td rowspan="1"></td><td rowspan="1">八个IMU事件触发标准.md｜旋转上抛 `EVENT_MOTION_SPIN_TOSS`</td></tr></tbody>
</table>

</details>

<details>
<summary>生产与维护 · 3项</summary>

<table>
<thead>
<tr><th>编号</th><th>功能</th><th>需求</th><th>资料差异 / 缺项</th><th>依据</th></tr></thead>
<tbody>
<tr><td rowspan="1">FW-064</td><td rowspan="1">产测模式</td><td rowspan="1">PCBA/整机产测模式不运行正常业务。</td><td rowspan="1"></td><td rowspan="1">设备功能说明.md｜9. 测试辅助模式</td></tr>
<tr><td rowspan="1">FW-065</td><td rowspan="1">老化模式</td><td rowspan="1">1、老化模式下不进入浅睡和待机。<br>2、整机老化不休眠，音量和亮度最大。<br>3、串口老化 1 用于长时间运行，最大音量，不进浅睡，正常响应互动。<br>4、串口老化 2 最大音量，不进浅睡，不响应传感器，按间隔自动轮播事件。<br>5、老化模式 3：先用串口开启，再五击进入；运行中再次五击会中止老化并重启设备。</td><td rowspan="1"><strong>【待补/待确认】 “亮度最大”对应的硬件未写明；不据此增加屏幕或灯光器件。串口老化 2 轮播间隔未写明。</strong></td><td rowspan="1">设备功能说明.md｜6.3 关机；设备功能说明.md｜9. 测试辅助模式</td></tr>
<tr><td rowspan="1">FW-066</td><td rowspan="1">边充边测</td><td rowspan="1">开启边充边测时，充电中仍执行互动动作；重启后该测试开关失效。</td><td rowspan="1"></td><td rowspan="1">设备功能说明.md｜9. 测试辅助模式</td></tr></tbody>
</table>

</details>

<details>
<summary>舵机控制板 · 7项</summary>

<table>
<thead>
<tr><th>编号</th><th>功能</th><th>需求</th><th>资料差异 / 缺项</th><th>依据</th></tr></thead>
<tbody>
<tr><td rowspan="1">FW-067</td><td rowspan="1">预置与组合动作</td><td rowspan="1">支持预置动作和组合控制。0x03 的数据字段是32项映射索引，依次为：00→1、01→4、02→5、03→6、04→13、05→19、06→20、07→25、08→26、09→27、0A→30、0B→32、0C→37、0D→45、0E→49、0F→50、10→54、11→56、12→60、13→61、14→65、15→66、16→67、17→68、18→70、19→93、1A→95、1B→96、1C→100、1D→101、1E→26+101、1F→20+101。0x04组合命令示例直接传动作号26和101（1A 65）、20和101（14 65）。上述两种编号不能混用；与动作统计表1～61编号的跨表映射仍缺失，组合执行顺序/并行方式及上限未写明。</td><td rowspan="1"><strong>【待补/待确认】 协议动作 ID 与动作统计表“舵机动作（new）”的 1～61 编号未建立映射；组合长度上限及组内执行时序未写明。</strong></td><td rowspan="7">舵机控制板协议_V1.4_20260818.docx</td></tr>
<tr><td rowspan="1">FW-068</td><td rowspan="1">自定义舵机控制</td><td rowspan="1">自定义命令0x05包含舵机ID（1～250）、角度Int16、转动时间Uint16、停顿时间Uint16；示例业务值为+30°、500ms、300ms。ID范围不代表实际舵机数，类型位宽不代表安全行程。协议正文写多字节数据为小端，但该示例的00 1E、01 F4、01 2C按大端表达上述数值，存在源内矛盾；不可把示例直接作为实机发送格式。物理行程和时间范围仍需从已装机舵机及结构标定取得。</td><td rowspan="1"><strong>【待补/待确认】 ID 范围不代表实际舵机数；字段范围不代表机械安全行程。物理角度与时间允许范围未写明。</strong></td></tr>
<tr><td rowspan="1">FW-069</td><td rowspan="1">应答状态</td><td rowspan="1">原文在0x03舵机动作控制之后定义：主设备主动读取5字节应答；同步字段AB，状态0=命令接收成功、1=接收失败、2=命令错误、3=校验错误、4=忙、5=设备异常、6=动作异常。命令接收成功不等于机械动作完成。表中命令字段注明基于主机命令，但0x04/0x05的独立应答细节、超时和完成通知未另行展开。</td><td rowspan="1"><strong>【待补/待确认】 应答超时、重试次数以及动作执行完成反馈未写明。</strong></td></tr>
<tr><td rowspan="1">FW-070</td><td rowspan="1">休眠与上电通知</td><td rowspan="1">支持控制 MCU 进入休眠；控制板上电后主动发送上电通知。</td><td rowspan="1"></td></tr>
<tr><td rowspan="1">FW-071</td><td rowspan="1">版本读取</td><td rowspan="1">支持查询控制板硬件大／小版本、软件大／中／小版本和动作库版本。动作库 0xFFFFFFFF 表示 NorFlash 未烧录；0x00000000 表示 NorFlash 硬件通信有问题，后者标注 McuAppV1.0.4 以上支持。</td><td rowspan="1"><strong>【待补/待确认】 文中硬件 V1.0、软件 V1.0.1、动作库 V1 为协议示例，未确定当前样机版本。</strong></td></tr>
<tr><td rowspan="1">FW-072</td><td rowspan="1">动作库升级</td><td rowspan="1">数据包最大 128 字节，包序号从 1 开始。应答区分 Flash 擦除完成、数据包接收正常、数据包请求重发、Flash 升级完成。</td><td rowspan="1"><strong>【待补/待确认】 开始和传输结束均列在包序号 0x0000 项下，区分方式未写明；总容量、超时和重试上限未写明。</strong></td></tr>
<tr><td rowspan="1">FW-073</td><td rowspan="1">鉴权与调试</td><td rowspan="1">提供 challenge/mac 交互。内部调试可拉低／拉高 NorFlash 的 CS，标注 McuAppV1.0.4 以上支持。</td><td rowspan="1"><strong>【待补/待确认】 鉴权算法和密钥规则未写明。命令列表另含 Light、Moto、Shaft 状态设置，但未给出详细功能定义。</strong></td></tr></tbody>
</table>

</details>

[返回完整PRD目录](../README.md) · [上一章](./01-product-hardware.md) · [下一章](./03-app-protocol.md)
