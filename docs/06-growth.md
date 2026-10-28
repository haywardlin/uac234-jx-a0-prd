# 06 五维成长与阶段

[返回完整PRD目录](../README.md) · [上一章](./05-emotion.md) · [下一章](./07-stage-feedback.md)

初始模式独立于初识、熟悉、相伴；有效互动累计，App决定何时更新。

首次App初始化成功后，五维原始分各100；未初始化时不分配五行或五维分。每次有效温和互动增加1 XP。五维增量与XP分别累计，不能把五维增量总和当作XP。

<table>
<thead>
<tr><th>事件ID</th><th>输入事件</th><th>金·求知</th><th>木·沉稳</th><th>水·信赖</th><th>火·活力</th><th>土·依恋</th><th>XP</th><th>启用范围</th><th>计数要求</th></tr></thead>
<tbody>
<tr><td rowspan="1">1</td><td rowspan="1">头顶轻触</td><td rowspan="12">0</td><td rowspan="2">0</td><td rowspan="2">1</td><td rowspan="1">0</td><td rowspan="1">2</td><td rowspan="23">1</td><td rowspan="1">Beta Y</td><td rowspan="1">事件日志；仅有效真实输入；试玩、调试、被状态拦截的输入不计。</td></tr>
<tr><td rowspan="1">2</td><td rowspan="1">头顶短抚</td><td rowspan="1">1</td><td rowspan="2">1</td><td rowspan="2">预留 Beta N</td><td rowspan="2">事件日志；Beta N须本固件验收开放；存在映射不代表现成支持。</td></tr>
<tr><td rowspan="1">3</td><td rowspan="1">头顶长抚</td><td rowspan="1">1</td><td rowspan="1">2</td><td rowspan="2">0</td></tr>
<tr><td rowspan="1">4</td><td rowspan="1">头左轻触</td><td rowspan="2">0</td><td rowspan="2">1</td><td rowspan="1">2</td><td rowspan="1">Beta Y</td><td rowspan="1">事件日志；仅有效真实输入；试玩、调试、被状态拦截的输入不计。</td></tr>
<tr><td rowspan="1">5</td><td rowspan="1">头左短抚</td><td rowspan="1">1</td><td rowspan="2">1</td><td rowspan="2">预留 Beta N</td><td rowspan="2">事件日志；Beta N须本固件验收开放；存在映射不代表现成支持。</td></tr>
<tr><td rowspan="1">6</td><td rowspan="1">头左长抚</td><td rowspan="1">1</td><td rowspan="1">2</td><td rowspan="2">0</td></tr>
<tr><td rowspan="1">7</td><td rowspan="1">头右轻触</td><td rowspan="2">0</td><td rowspan="2">1</td><td rowspan="1">2</td><td rowspan="1">Beta Y</td><td rowspan="1">事件日志；仅有效真实输入；试玩、调试、被状态拦截的输入不计。</td></tr>
<tr><td rowspan="1">8</td><td rowspan="1">头右短抚</td><td rowspan="1">1</td><td rowspan="3">1</td><td rowspan="2">预留 Beta N</td><td rowspan="2">事件日志；Beta N须本固件验收开放；存在映射不代表现成支持。</td></tr>
<tr><td rowspan="1">9</td><td rowspan="1">头右长抚</td><td rowspan="1">1</td><td rowspan="2">2</td><td rowspan="2">0</td></tr>
<tr><td rowspan="1">10</td><td rowspan="1">腹部轻触</td><td rowspan="1">0</td><td rowspan="1">Beta Y</td><td rowspan="1">事件日志；仅有效真实输入；试玩、调试、被状态拦截的输入不计。</td></tr>
<tr><td rowspan="1">11</td><td rowspan="1">腹部短抚</td><td rowspan="8">1</td><td rowspan="1">1</td><td rowspan="1">1</td><td rowspan="1">0</td><td rowspan="2">预留 Beta N</td><td rowspan="2">事件日志；Beta N须本固件验收开放；存在映射不代表现成支持。</td></tr>
<tr><td rowspan="1">12</td><td rowspan="1">腹部长抚</td><td rowspan="1">2</td><td rowspan="11">0</td><td rowspan="2">1</td></tr>
<tr><td rowspan="1">13</td><td rowspan="1">左侧轻触</td><td rowspan="2">1</td><td rowspan="1">0</td><td rowspan="1">Beta Y</td><td rowspan="1">事件日志；仅有效真实输入；试玩、调试、被状态拦截的输入不计。</td></tr>
<tr><td rowspan="1">14</td><td rowspan="1">左侧短抚</td><td rowspan="1">1</td><td rowspan="1">0</td><td rowspan="2">预留 Beta N</td><td rowspan="2">事件日志；Beta N须本固件验收开放；存在映射不代表现成支持。</td></tr>
<tr><td rowspan="1">15</td><td rowspan="1">左侧长抚</td><td rowspan="1">0</td><td rowspan="1">2</td><td rowspan="2">1</td></tr>
<tr><td rowspan="1">16</td><td rowspan="1">右侧轻触</td><td rowspan="2">1</td><td rowspan="1">0</td><td rowspan="1">Beta Y</td><td rowspan="1">事件日志；仅有效真实输入；试玩、调试、被状态拦截的输入不计。</td></tr>
<tr><td rowspan="1">17</td><td rowspan="1">右侧短抚</td><td rowspan="1">1</td><td rowspan="1">0</td><td rowspan="2">预留 Beta N</td><td rowspan="2">事件日志；Beta N须本固件验收开放；存在映射不代表现成支持。</td></tr>
<tr><td rowspan="1">18</td><td rowspan="1">右侧长抚</td><td rowspan="5">0</td><td rowspan="1">2</td><td rowspan="1">1</td></tr>
<tr><td rowspan="1">19</td><td rowspan="1">后背轻触</td><td rowspan="2">2</td><td rowspan="2">1</td><td rowspan="2">0</td><td rowspan="1">Beta Y</td><td rowspan="1">事件日志；仅有效真实输入；试玩、调试、被状态拦截的输入不计。</td></tr>
<tr><td rowspan="1">20</td><td rowspan="1">后背短抚</td><td rowspan="6">预留 Beta N</td><td rowspan="4">事件日志；Beta N须本固件验收开放；存在映射不代表现成支持。</td></tr>
<tr><td rowspan="1">21</td><td rowspan="1">后背长抚</td><td rowspan="2">1</td><td rowspan="1">2</td><td rowspan="1">1</td></tr>
<tr><td rowspan="1">22</td><td rowspan="1">长时间握持</td><td rowspan="1">1</td><td rowspan="1">2</td></tr>
<tr><td rowspan="1">23</td><td rowspan="1">轻摇</td><td rowspan="1">1</td><td rowspan="20">0</td><td rowspan="10">0</td><td rowspan="1">2</td><td rowspan="11">0</td></tr>
<tr><td rowspan="1">24</td><td rowspan="1">猛摇</td><td rowspan="4">0</td><td rowspan="4">0</td><td rowspan="4">0</td><td rowspan="4">不计分；仅有效真实输入；试玩、调试、被状态拦截的输入不计。</td></tr>
<tr><td rowspan="1">25</td><td rowspan="1">翻转</td></tr>
<tr><td rowspan="1">26</td><td rowspan="1">被拿起</td><td rowspan="2">原表划除</td></tr>
<tr><td rowspan="1">27</td><td rowspan="1">被放下</td></tr>
<tr><td rowspan="1">28</td><td rowspan="1">唤醒提示词</td><td rowspan="1">2</td><td rowspan="1">1</td><td rowspan="1">1</td><td rowspan="3">Beta Y</td><td rowspan="1">事件日志；仅有效真实输入；试玩、调试、被状态拦截的输入不计。</td></tr>
<tr><td rowspan="1">29</td><td rowspan="1">光线变暗</td><td rowspan="4">0</td><td rowspan="4">0</td><td rowspan="4">0</td><td rowspan="4">不计分；仅有效真实输入；试玩、调试、被状态拦截的输入不计。</td></tr>
<tr><td rowspan="1">30</td><td rowspan="1">光线变亮</td></tr>
<tr><td rowspan="1">31</td><td rowspan="1">2小时无互动</td><td rowspan="2">预留 Beta N</td></tr>
<tr><td rowspan="1">32</td><td rowspan="1">48小时无互动</td></tr>
<tr><td rowspan="1">33</td><td rowspan="1">遇到新伙伴</td><td rowspan="1">2</td><td rowspan="2">1</td><td rowspan="2">1</td><td rowspan="2">1</td><td rowspan="6">Beta Y</td><td rowspan="1">好友表确认新增次数；事件33不重复计分；仅有效真实输入；试玩、调试、被状态拦截的输入不计。</td></tr>
<tr><td rowspan="1">34</td><td rowspan="1">遇到熟悉伙伴</td><td rowspan="1">1</td><td rowspan="1">1</td><td rowspan="1">好友表确认新增次数；事件34不重复计分；仅有效真实输入；试玩、调试、被状态拦截的输入不计。</td></tr>
<tr><td rowspan="1">35</td><td rowspan="1">侧倒</td><td rowspan="8">0</td><td rowspan="8">0</td><td rowspan="8">0</td><td rowspan="8">0</td><td rowspan="8">0</td><td rowspan="8">不计分；仅有效真实输入；试玩、调试、被状态拦截的输入不计。</td></tr>
<tr><td rowspan="1">36</td><td rowspan="1">充电</td></tr>
<tr><td rowspan="1">37</td><td rowspan="1">低电量</td></tr>
<tr><td rowspan="1">38</td><td rowspan="1">开机</td></tr>
<tr><td rowspan="1">39</td><td rowspan="1">呼吸</td><td rowspan="1">预留 Beta N</td></tr>
<tr><td rowspan="1">40</td><td rowspan="1">抛起</td><td rowspan="1">Beta Y</td></tr>
<tr><td rowspan="1">41</td><td rowspan="1">旋转抛起</td><td rowspan="1">原表划除</td></tr>
<tr><td rowspan="1">42</td><td rowspan="1">关机</td><td rowspan="1">Beta Y</td></tr></tbody>
</table>

<details>
<summary>累计、比例、主五行与去重规则</summary>

<table>
<thead>
<tr><th>项目</th><th>要求</th></tr></thead>
<tbody>
<tr><td rowspan="1">五维累计</td><td rowspan="1">金木水火土初值各100，总分500。每个获准真实互动按下表增加五维；每次增加1 XP。五维分数与XP分开保存，不以五维增量之和作为XP。</td></tr>
<tr><td rowspan="1">五维比例</td><td rowspan="1">各维占比=原始分/五维总分×100。先取整数，再按小数余数由大到小补足100；同余数按金木水火土顺序。原始分保存在App，百分比只是摘要。</td></tr>
<tr><td rowspan="1">主五行</td><td rowspan="1">首次由App初始化配置明确给出主五行并下发，不从未初始化设备读取一个默认属性。App生成初始值时沿用源算法的生产日期规则；生产日期或初始化配置缺失则待补，保持未初始化。后续取最高原始分；并列保留原主五行，若原主不在并列项中按金木水火土顺序选。</td></tr>
<tr><td rowspan="1">计分起点</td><td rowspan="1">首次成长包真正激活时，设备结束旧事件批次和旧聚合，建立新记录边界，并保存同一时刻的好友计数基线；返回包ID、激活时间、新记录边界及好友基线。只计算该边界之后的增量，不能把传包前读取的旧基线当成激活基线。此为新增同步要求，源资料未定义。</td></tr>
<tr><td rowspan="1">事件去重</td><td rowspan="1">整批校验且持久保存后才ACK。按档案+设备+稳定记录ID去重；同一记录次数增长只计正增量；整批重传不重复加XP。设备按原0.5秒去重及播放互斥识别事件，App不把手指点击次数当设备有效事件。</td></tr>
<tr><td rowspan="1">聚合次数</td><td rowspan="1">源协议把相邻间隔小于60秒且ID/emotion/flags相同的事件聚合。真实新增count=n时，获准n次、XP+n、各维+n×向量；这里的60秒是设备记录聚合窗口，不是App更新周期。</td></tr>
<tr><td rowspan="1">数据不足</td><td rowspan="1">无稳定ID时暂用设备+档案+事件ID+首UTC+emotion+flags与最大已见count兼容去重；不能保证同秒独立事件无歧义。时间不可信、发生于启用前或所属档案不明的记录不计，保留待核对。</td></tr>
<tr><td rowspan="1">社交统计</td><td rowspan="1">只以好友表作为相遇计分来源，33/34日志不再加分。初次启用保存每个伙伴的历史计数基线；以后正常count正增量每次+1 XP。新伙伴首条记初次相遇，剩余已确认次数记再次相遇。</td></tr>
<tr><td rowspan="1">好友计数边界</td><td rowspan="1">count=255饱和后，每个比上次更新且尚未计过的last相遇时间只确认至少1次；不虚构其间次数。计数因淘汰重建回退时，若新的first时间晚于上次已知last，可将该新段count计入；否则只用可确认的新增last计1次。已累计次数不扣回、不把旧伙伴再次当新伙伴。</td></tr></tbody>
</table>

</details>

演示路线：App启用初识 → 完成10次有效互动 → App查询并更新熟悉 → 再完成20次 → App查询并更新相伴。反复查询同一批记录不会重复加分。

[返回完整PRD目录](../README.md) · [上一章](./05-emotion.md) · [下一章](./07-stage-feedback.md)
