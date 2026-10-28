# 05 情绪算法与五维性格

[返回完整PRD目录](../README.md) · [上一章](./04-app-ux.md) · [下一章](./06-growth.md)

保留日运、时辰能量、原始情绪与升降缓冲；成长与情绪分开计算。

**情绪如何影响一次互动**

1. 已初始化的主五行＋本地日期/时辰
2. 日运×时辰能量→原始情绪
3. 与上次结果比较，执行缓冲
4. 最终具体情绪→1/2/3分组
5. 事件发生→阶段表选整套输出

<table>
<thead>
<tr><th>步骤</th><th>计算规则</th></tr></thead>
<tbody>
<tr><td rowspan="1">输入</td><td rowspan="1">仅在App初始化完成后计算：本地日期、当前小时、已生效主五行、上次最终情绪。首次未连接或初始化未完成时没有五行，不计算情绪；初始化主五行的产生规则见成长章节。</td></tr>
<tr><td rowspan="1">日运</td><td rowspan="1">以1900-01-01为起点计算日干五行。自己克当日=元吉；同五行=上吉；自己生当日=吉；当日生自己=平；当日克自己=小凶。</td></tr>
<tr><td rowspan="1">时辰能量</td><td rowspan="1">同五行或时辰生自己=旺；自己克时辰=平；自己生时辰或时辰克自己=弱。时辰映射见下表。</td></tr>
<tr><td rowspan="1">情绪查表</td><td rowspan="1">“日运×时辰能量”得到原始情绪，再按上一情绪缓冲；不是由某次触摸直接切换情绪。</td></tr>
<tr><td rowspan="1">降幅缓冲</td><td rowspan="1">上次层级－本次原始层级≥2：犯困/害羞改为发呆，警觉/焦躁改为好奇。其他结果保持。</td></tr>
<tr><td rowspan="1">升幅缓冲</td><td rowspan="1">本次原始层级－上次层级≥2：开心改为得意，撒娇改为惬意。其他结果保持。</td></tr>
<tr><td rowspan="1">同档连续</td><td rowspan="1">连续同一个0级情绪：焦躁→警觉；警觉→害羞；犯困→发呆；害羞不变。第一次计算直接使用原始情绪。</td></tr>
<tr><td rowspan="1">三类设备情绪</td><td rowspan="1">最终具体情绪映射为1开心、2平静、3悲伤，再匹配生效阶段的候选组。0 ANY是不限制情绪的规则；初始表使用ANY，成长中的固定事件也可使用ANY。</td></tr>
<tr><td rowspan="1">版本选用</td><td rowspan="1">PDF时辰表14个单元格与文字规则、Python不一致。本方案采用Python及一致的文字规则；原PDF差异留在附表。</td></tr></tbody>
</table>

<table>
<thead>
<tr><th>吉凶</th><th>旺</th><th>平</th><th>弱</th></tr></thead>
<tbody>
<tr><td rowspan="1">元吉</td><td rowspan="1">开心</td><td rowspan="1">撒娇</td><td rowspan="2">惬意</td></tr>
<tr><td rowspan="1">上吉</td><td rowspan="1">得意</td><td rowspan="1">开心</td></tr>
<tr><td rowspan="1">吉</td><td rowspan="1">撒娇</td><td rowspan="1">得意</td><td rowspan="1">好奇</td></tr>
<tr><td rowspan="1">平</td><td rowspan="1">好奇</td><td rowspan="1">发呆</td><td rowspan="1">犯困</td></tr>
<tr><td rowspan="1">小凶</td><td rowspan="1">RESTLESS（PDF：焦虑；Python：焦躁）</td><td rowspan="1">警觉</td><td rowspan="1">害羞</td></tr></tbody>
</table>

情绪算法/beany_emotion_machine.pdf p5；daily_emotion_liunian.py L69～94

<table>
<thead>
<tr><th>行为情绪ID</th><th>分组</th><th>匹配范围</th></tr></thead>
<tbody>
<tr><td rowspan="1">0</td><td rowspan="1">ANY</td><td rowspan="1">任意情绪；规则通配，不是第四种实际情绪</td></tr>
<tr><td rowspan="1">1</td><td rowspan="1">开心</td><td rowspan="1">HAPPY / CLINGY / PROUD / COZY：开心 / 黏人 / 得意 / 惬意</td></tr>
<tr><td rowspan="1">2</td><td rowspan="1">平静</td><td rowspan="1">CURIOUS / SPACED：好奇 / 发呆</td></tr>
<tr><td rowspan="1">3</td><td rowspan="1">悲伤</td><td rowspan="1">SLEEPY / RESTLESS / ALERT / SHY：困倦 / 躁动 / 警觉 / 害羞</td></tr></tbody>
</table>

<details>
<summary>时辰能量表 · 按Python及一致的文字规则</summary>

<table>
<thead>
<tr><th>时辰</th><th>输入小时</th><th>本气</th><th>木</th><th>火</th><th>土</th><th>金</th><th>水</th></tr></thead>
<tbody>
<tr><td rowspan="1">子</td><td rowspan="1">23、0</td><td rowspan="1">水</td><td rowspan="1">旺</td><td rowspan="2">弱</td><td rowspan="1">平</td><td rowspan="1">弱</td><td rowspan="1">旺</td></tr>
<tr><td rowspan="1">丑</td><td rowspan="1">1、2</td><td rowspan="1">土</td><td rowspan="1">平</td><td rowspan="1">旺</td><td rowspan="1">旺</td><td rowspan="4">弱</td></tr>
<tr><td rowspan="1">寅</td><td rowspan="1">3、4</td><td rowspan="2">木</td><td rowspan="2">旺</td><td rowspan="2">旺</td><td rowspan="2">弱</td><td rowspan="2">平</td></tr>
<tr><td rowspan="1">卯</td><td rowspan="1">5、6</td></tr>
<tr><td rowspan="1">辰</td><td rowspan="1">7、8</td><td rowspan="1">土</td><td rowspan="1">平</td><td rowspan="1">弱</td><td rowspan="4">旺</td><td rowspan="1">旺</td></tr>
<tr><td rowspan="1">巳</td><td rowspan="1">9、10</td><td rowspan="2">火</td><td rowspan="2">弱</td><td rowspan="2">旺</td><td rowspan="2">弱</td><td rowspan="2">平</td></tr>
<tr><td rowspan="1">午</td><td rowspan="1">11、12</td></tr>
<tr><td rowspan="1">未</td><td rowspan="1">13、14</td><td rowspan="1">土</td><td rowspan="1">平</td><td rowspan="1">弱</td><td rowspan="4">旺</td><td rowspan="1">弱</td></tr>
<tr><td rowspan="1">申</td><td rowspan="1">15、16</td><td rowspan="2">金</td><td rowspan="2">弱</td><td rowspan="2">平</td><td rowspan="2">弱</td><td rowspan="2">旺</td></tr>
<tr><td rowspan="1">酉</td><td rowspan="1">17、18</td></tr>
<tr><td rowspan="1">戌</td><td rowspan="1">19、20</td><td rowspan="1">土</td><td rowspan="1">平</td><td rowspan="2">弱</td><td rowspan="1">旺</td><td rowspan="1">弱</td></tr>
<tr><td rowspan="1">亥</td><td rowspan="1">21、22</td><td rowspan="1">水</td><td rowspan="1">旺</td><td rowspan="1">平</td><td rowspan="1">弱</td><td rowspan="1">旺</td></tr></tbody>
</table>

情绪算法/beany_emotion_machine.pdf p4；daily_emotion_liunian.py L151～159

</details>

<details>
<summary>算法内部层级与五行编码</summary>

下表0–9是源算法内部枚举，不是行为表的情绪ID。源文“撒娇/犯困/焦躁”分别归入用户定义的“黏人/困倦/躁动”。

<table>
<thead>
<tr><th>算法值</th><th>枚举</th><th>Python 中文</th><th>PDF 中文</th><th>层级</th></tr></thead>
<tbody>
<tr><td rowspan="1">0</td><td rowspan="1">HAPPY</td><td rowspan="1">开心</td><td rowspan="1">开心</td><td rowspan="2">3</td></tr>
<tr><td rowspan="1">1</td><td rowspan="1">CLINGY</td><td rowspan="1">撒娇</td><td rowspan="1">撒娇</td></tr>
<tr><td rowspan="1">2</td><td rowspan="1">PROUD</td><td rowspan="1">得意</td><td rowspan="1">得意</td><td rowspan="2">2</td></tr>
<tr><td rowspan="1">3</td><td rowspan="1">COZY</td><td rowspan="1">惬意</td><td rowspan="1">惬意</td></tr>
<tr><td rowspan="1">4</td><td rowspan="1">CURIOUS</td><td rowspan="1">好奇</td><td rowspan="1">好奇</td><td rowspan="2">1</td></tr>
<tr><td rowspan="1">5</td><td rowspan="1">SPACED</td><td rowspan="1">发呆</td><td rowspan="1">发呆</td></tr>
<tr><td rowspan="1">6</td><td rowspan="1">SLEEPY</td><td rowspan="1">犯困</td><td rowspan="1">犯困</td><td rowspan="4">0</td></tr>
<tr><td rowspan="1">7</td><td rowspan="1">SHY</td><td rowspan="1">害羞</td><td rowspan="1">害羞</td></tr>
<tr><td rowspan="1">8</td><td rowspan="1">RESTLESS</td><td rowspan="1">焦躁</td><td rowspan="1">焦虑</td></tr>
<tr><td rowspan="1">9</td><td rowspan="1">ALERT</td><td rowspan="1">警觉</td><td rowspan="1">警觉</td></tr></tbody>
</table>

情绪算法/beany_emotion_machine.pdf p5；daily_emotion_liunian.py L37～39、96～101、109～114

<table>
<thead>
<tr><th>五行</th><th>App 协议值</th><th>Python 值</th></tr></thead>
<tbody>
<tr><td rowspan="1">金</td><td rowspan="1">1</td><td rowspan="1">3</td></tr>
<tr><td rowspan="1">木</td><td rowspan="1">2</td><td rowspan="1">0</td></tr>
<tr><td rowspan="1">水</td><td rowspan="1">3</td><td rowspan="1">4</td></tr>
<tr><td rowspan="1">火</td><td rowspan="1">4</td><td rowspan="1">1</td></tr>
<tr><td rowspan="1">土</td><td rowspan="1">5</td><td rowspan="1">2</td></tr></tbody>
</table>

通用BLE协议_V1_0_12.md §6 dpID=8；daily_emotion_liunian.py L25～26

</details>

## 计算时机

<table>
<thead>
<tr><th>触发</th><th>执行要求</th></tr></thead>
<tbody>
<tr><td rowspan="1">首次有效校时 / 开机恢复</td><td rowspan="1">前提：已完成App初始化且时间有效。首次计算无历史则取原始结果；同周期重启恢复已保存结果，跨周期重启使用上次情绪缓冲一次。</td></tr>
<tr><td rowspan="1">正常运行</td><td rowspan="1">每日00:00跨日，以及01、03、05、07、09、11、13、15、17、19、21、23点进入新时辰时计算一次。</td></tr>
<tr><td rowspan="1">同一时段</td><td rowspan="1">不因App轮询、同一时段重复校时或重复写入相同五行而再次缓冲。</td></tr>
<tr><td rowspan="1">成长改变主五行</td><td rowspan="1">App通过dpID=8单独下发；确认后存为下一计算边界的输入。本时段不反复重算。</td></tr>
<tr><td rowspan="1">休眠 / 断电 / 改时</td><td rowspan="1">同周期恢复原结果，跨周期只计算当前时段，不回放错过时辰；可信校时改变当前周期后计算当前时段一次并重建标记，同一周期重复校时不重算。</td></tr>
<tr><td rowspan="1">计算与物理反馈</td><td rowspan="1">更新情绪不自动播放动作或音频。只有合法互动事件命中行为表才产生输出；深度待机不因此被唤醒。</td></tr></tbody>
</table>

[返回完整PRD目录](../README.md) · [上一章](./04-app-ux.md) · [下一章](./06-growth.md)
