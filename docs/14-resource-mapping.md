# 14 资源映射与演示闭环

[返回完整PRD目录](../README.md) · [上一章](./13-state-flows.md) · [下一章](./15-sources-gaps.md)

事件、候选、逻辑资源和底层命令逐层对应。

<table>
<thead>
<tr><th>步骤</th><th>输入</th><th>处理</th></tr></thead>
<tbody>
<tr><td rowspan="1">1 输入识别</td><td rowspan="1">触摸、IMU、光感、唤醒、交友、系统条件</td><td rowspan="1">输出原事件ID。识别阈值与启用标记见固件及交互矩阵。</td></tr>
<tr><td rowspan="1">2 状态和优先级</td><td rowspan="1">工作状态、保护、去重、正在播放的事件</td><td rowspan="1">系统＞交友＞姿态＞触摸＞光感；ANY及用户动作均不能绕过保护。</td></tr>
<tr><td rowspan="1">3 用户绑定</td><td rowspan="1">七个普通轻触事件的当前已确认绑定</td><td rowspan="1">存在有效绑定时100%执行用户序列；仍按真实输入记成长。</td></tr>
<tr><td rowspan="1">4 模式与情绪</td><td rowspan="1">已生效阶段＋事件ID＋情绪组</td><td rowspan="1">未初始化用原表；成长使用本阶段候选。具体情绪只映射到1/2/3，不再叠加性格倍率。</td></tr>
<tr><td rowspan="1">5 一次抽取</td><td rowspan="1">同组候选及权重</td><td rowspan="1">合计100%；只抽一次，动作/音频/震动同属一行，不随机拼接。固定事件只使用ANY。</td></tr>
<tr><td rowspan="1">6 资源解析</td><td rowspan="1">逻辑ID→资源包→控制板命令/播放接口</td><td rowspan="1">动作逻辑ID不等于0x03的控制码。无震动逻辑0编译为0xFF。</td></tr>
<tr><td rowspan="1">7 执行与结束</td><td rowspan="1">完整输出或用户序列</td><td rowspan="1">保留原播放与打断规则；自定义序列等待完成/停止确认。缺必需资源则拒绝整包更新。</td></tr></tbody>
</table>

**【待补/待确认】 61个逻辑动作中，仅20个有当前控制板0x03映射。其余须补资源或确认库版本；App普通动作控制、序列停止/完成通知和装机安全范围仍需补齐。**

<details>
<summary>动作资源定义（61 项，原文）</summary>

<table>
<thead>
<tr><th>动作 ID</th><th>动作名称</th><th>事件类型</th><th>事件情绪描述</th><th>最终效果</th><th>匹配情绪</th><th>声音 1：ID／原名称</th><th>声音 2：ID／原名称</th><th>声音 3：ID／原名称</th></tr></thead>
<tbody>
<tr><td rowspan="1">1</td><td rowspan="1">充电启动单次点头（充电专属）</td><td rowspan="1">充电</td><td rowspan="1">平稳休眠、补充能量</td><td rowspan="1">最终效果：低速微小幅度完成单次抬头回落，作为充电启动提示，动作结束后设备进入安静待机状态，状态识别清晰，风格沉稳，符合充电休养的松弛感</td><td rowspan="1">惬意、发呆</td><td rowspan="1">ID 61｜charge psr comforting 01.wav</td><td rowspan="1">ID /｜/</td><td rowspan="5">ID /｜/</td></tr>
<tr><td rowspan="1">2</td><td rowspan="1">轻抬慢回（温顺舒缓）</td><td rowspan="1">Headtouch/摸头左/摸头右/摸肚子/摸左侧面/摸右侧面/摸后背-轻碰</td><td rowspan="1">舒服、放松、温顺接纳</td><td rowspan="1">最终效果：低速轻柔完整抬头回落，全程无抖动，动作幅度偏小、节奏舒缓，展现温和接纳触碰的松弛状态，反应平缓，符合温顺基础性格（动作幅度柔和，速度缓慢，接纳度高）</td><td rowspan="1">惬意</td><td rowspan="1">ID 2｜back_psr_comforting_01.wav</td><td rowspan="1">ID 6｜back_psr_comforting_02.wav</td></tr>
<tr><td rowspan="1">3</td><td rowspan="1">放下后长期垂头</td><td rowspan="1">被放下</td><td rowspan="1">落地孤单</td><td rowspan="1">最终效果：低速大幅度抬头后垂落锁定，长时间静止，落地无人互动流露孤单低落</td><td rowspan="3">发呆、犯困</td><td rowspan="1">ID 3｜idle_dlm_lonely_01.wav</td><td rowspan="1">ID 21｜lightdown_dlm_dreamy_02.wav</td></tr>
<tr><td rowspan="1">4</td><td rowspan="1">关机缓慢垂头锁位</td><td rowspan="1">关机指令</td><td rowspan="1">彻底休眠</td><td rowspan="1">最终效果：超低速大幅度完整抬升至极限仰角，再平稳匀速垂落锁定最低位，全程无抖动，到位后彻底静止断电，放空深度休眠，反应沉稳无波动，适配关机收尾（全程匀速）</td><td rowspan="1">ID 4｜poweroff_dlm_sleep_01.wav</td><td rowspan="1">ID /｜/</td></tr>
<tr><td rowspan="1">5</td><td rowspan="1">强行翻肚皮垂头</td><td rowspan="1">强行翻肚皮/翻转</td><td rowspan="1">委屈不安，挣扎</td><td rowspan="1">最终效果：轻微紧绷颤动2次后垂落锁定，被强行翻肚皮后流露委屈不安，不耐烦，挣扎</td><td rowspan="1">ID 5｜flip_psr_protest_01.wav</td><td rowspan="1">ID 14｜flip_psr_protest_02.wav</td></tr>
<tr><td rowspan="1">6</td><td rowspan="1">瞌睡</td><td rowspan="1">呼吸/Idle&gt;2hours(长时间无互动)/Idle&gt;48hours(超长无互动)/Gentleshake(轻摇)</td><td rowspan="1">犯困</td><td rowspan="1">最终效果：2次慢速小幅抬头，快速低头，困倦打瞌睡的动作</td><td rowspan="1">犯困</td><td rowspan="1">ID 3｜idle_dlm_lonely_01.wav</td><td rowspan="1">ID 42｜lightdown_dlm_dreamy_01.wav</td><td rowspan="1">ID 1｜charge_dlm_resting_01.wav</td></tr>
<tr><td rowspan="1">7</td><td rowspan="1">摸后背匀速快点头（摸后背专属）</td><td rowspan="1">摸后背-轻碰/快速撸/长时间抚摸</td><td rowspan="1">安稳、踏实、放松</td><td rowspan="1">最终效果：低速标准幅度抬头回落匀速点头，节奏均匀平稳，展现后背被抚摸时踏实安稳的放松感，反应平缓，适配基础温顺性格（俯仰幅度标准，速度均匀，情绪平和无波动）</td><td rowspan="1">惬意</td><td rowspan="1">ID 6｜back_psr_comforting_02.wav</td><td rowspan="1">ID 2｜back_psr_comforting_01.wav</td><td rowspan="1">ID 60｜synth_dlm_content_hum_01.wav</td></tr>
<tr><td rowspan="1">8</td><td rowspan="1">开机上扬点头（开机启动）</td><td rowspan="1">开机上电</td><td rowspan="1">苏醒、精神、初次启动活力</td><td rowspan="1">最终效果：低速完整抬升至极限抬头仰角，随后切换中高速小幅连续点头，开机动作舒展精神，自带新生活力与小得意，先慢后快层次感强，反应循序渐进，适配标准青年性格（抬升段低速沉稳，点头段高速活泼，初始化仪式感充足）</td><td rowspan="1">开心、得意</td><td rowspan="1">ID 7｜poweron_psr_softwake_v01.wav</td><td rowspan="1">ID 39｜poweron_psr_softwake_v02.wav</td><td rowspan="8">ID /｜/</td></tr>
<tr><td rowspan="1">9</td><td rowspan="1">上下缓慢抬升打量</td><td rowspan="1">唤醒提示词/变亮/放下</td><td rowspan="1">上下打量</td><td rowspan="1">最终效果：低速标准幅度抬头回落匀速点头，节奏平稳舒缓，上下打量高低处环境，展现单纯的探索好奇，反应平缓，适配中性温和性格（纯粹探索）</td><td rowspan="1">好奇</td><td rowspan="1">ID 8｜headright_psr_alert_right_01.wav</td><td rowspan="1">ID 45｜headright_psr_alert_right_02.wav</td></tr>
<tr><td rowspan="1">10</td><td rowspan="1">上下微颤点头（满足惬意）</td><td rowspan="1">摸头顶/摸肚子/摸后背/长时间抚摸</td><td rowspan="1">满足、惬意、轻微开心</td><td rowspan="1">最终效果：低速小幅抬头回落连续点头，起伏柔和不急促，展现被长时间安抚后的满足惬意，轻微流露愉悦感，反应平缓温和，适配温顺慵懒性格（动作幅度轻微，速度舒缓，情绪内敛）</td><td rowspan="1">惬意、开心</td><td rowspan="1">ID 9｜belly_psr_full_trust_01.wav</td><td rowspan="1">ID 46｜chin_bps_trusting_01.wav</td></tr>
<tr><td rowspan="1">11</td><td rowspan="1">快速上下点头（快速撸通用开心）</td><td rowspan="1">摸头顶/摸头左/摸头右/摸肚子/摸左侧面/摸右侧面/摸后背</td><td rowspan="1">开心、兴奋、享受快速抚摸</td><td rowspan="1">最终效果：中高速标准幅度抬头回落连续快速点头，动作短促有力、节奏轻快，展现被快速抚摸时的愉悦开心，略带小得意，反应灵敏，适配活泼外向青年性格（俯仰幅度标准，速度快，情绪外放愉悦）</td><td rowspan="1">开心、得意</td><td rowspan="1">ID 10｜psr steady 02.wav</td><td rowspan="1">ID 47｜psr steady 03.wav</td></tr>
<tr><td rowspan="1">12</td><td rowspan="1">正式的点头（抬头低头）</td><td rowspan="1">触摸事件全场景</td><td rowspan="2">同意点头</td><td rowspan="1">最终效果：快速抬头 30° 定格约半秒后迅速回中，呈现标准「同意点头」；无左右偏移，态度明确、配合感强。</td><td rowspan="2">开心</td><td rowspan="1">ID 11｜nod_psr_agree_01.wav</td><td rowspan="1">ID 48｜nod_psr_agree_02.wav</td></tr>
<tr><td rowspan="1">13</td><td rowspan="1">抬头后快速点头（很乐意）</td><td rowspan="1">触摸事件全场景/唤醒提示词</td><td rowspan="1">最终效果：快速连点 3 次后停 500ms 再回中，呈现明确、热情的赞同姿态；无左右偏移，配合感强。</td><td rowspan="1">ID 12｜nod_psr_agree_03.wav</td><td rowspan="1">ID 49｜nod_psr_agree_04.wav</td></tr>
<tr><td rowspan="1">14</td><td rowspan="1">低头躲闪</td><td rowspan="1">摸头顶</td><td rowspan="1">躲闪</td><td rowspan="1">最终效果：感应到被摸头部后，快速低头，然后缓慢回正。害怕，害羞，躲闪</td><td rowspan="1">害羞、警觉</td><td rowspan="1">ID 13｜head_psr_shy_01.wav</td><td rowspan="1">ID 29｜sidefall_psr_guard_01.wav</td></tr>
<tr><td rowspan="1">15</td><td rowspan="1">高强度快速撸后垂头</td><td rowspan="1">高强度快速撸</td><td rowspan="1">委屈抗拒</td><td rowspan="1">最终效果：多次躲闪后垂落偏头锁定，长期静置，高强度抚摸后流露委屈厌烦</td><td rowspan="1">发呆、犯困</td><td rowspan="1">ID 14｜flip_psr_protest_02.wav</td><td rowspan="1">ID 50｜flip_psr_protest_03.wav</td></tr>
<tr><td rowspan="1">16</td><td rowspan="1">突发触碰单次躲闪</td><td rowspan="1">突然轻碰</td><td rowspan="1">猝不及防</td><td rowspan="1">最终效果：中高速标准幅度抬头后极速垂落低位，单次向触碰源反方向躲闪偏头，动作短促无循环，突然被碰产生轻微受惊的焦虑、瞬时警觉，反应急促内敛，适配中性敏感性格（单次动作）</td><td rowspan="1">焦虑、警觉</td><td rowspan="1">ID 31｜psr content sigh 01.wav</td><td rowspan="1">ID 17｜psr _clingy _mellow 01.wav</td><td rowspan="1">ID 15｜synth_emotion_worried_01.wav</td></tr>
<tr><td rowspan="1">17</td><td rowspan="1">初识同类慢偏头试探</td><td rowspan="1">遇到新Beany</td><td rowspan="1">害羞试探、不敢主动</td><td rowspan="1">最终效果：低速小幅抬头后垂至低位，缓慢向陌生同类单侧侧头长时间观望，全程低头内敛，腼腆胆小、充满谨慎好奇，反应迟缓克制，适配内向害羞性格（俯仰幅度微小，观望缓慢）</td><td rowspan="1">害羞、好奇</td><td rowspan="1">ID 16｜nose_dlm_shy_01.wav</td><td rowspan="1">ID 30｜head_psr_shy_02.wav</td><td rowspan="4">ID /｜/</td></tr>
<tr><td rowspan="1">18</td><td rowspan="1">单次轻触缓慢抬头观察</td><td rowspan="1">突发单次轻碰</td><td rowspan="1">猝不及防、轻微好奇</td><td rowspan="1">最终效果：轻柔小幅抬头短暂打量四周，随后安静回归水平，单次短暂反应，腼腆内敛，不会持续多动</td><td rowspan="1">好奇、害羞</td><td rowspan="1">ID 17｜psr _clingy _mellow 01</td><td rowspan="1">ID 25｜synth_emotion_grateful_01.wav</td></tr>
<tr><td rowspan="1">19</td><td rowspan="1">唤醒半睡慢抬</td><td rowspan="1">困倦状态唤醒</td><td rowspan="1">刚醒迷糊</td><td rowspan="1">最终效果：超低速先标准幅度抬头垂落低位，分段拖沓极慢抬升苏醒，半睡半醒迷糊放空，仅流露微弱好奇，反应极度迟缓，适配慵懒内向犯困性格（分段拖沓）</td><td rowspan="1">犯困、好奇</td><td rowspan="1">ID 18｜wakeup_psr_playful_02.wav</td><td rowspan="1">ID 44｜wakeup_psr_playful_03.wav</td></tr>
<tr><td rowspan="1">20</td><td rowspan="1">肚子轻垂头软动（摸肚子专属）</td><td rowspan="1">摸肚子-轻碰/快速撸/长时间抚摸</td><td rowspan="1">柔软、信任、毫无防备</td><td rowspan="1">最终效果：低速轻柔抬头后缓慢垂向低位，搭配同步小幅左右慢晃，姿态全程柔软松弛，毫无防备，流露腼腆惬意，反应平缓柔和，适配温顺胆小性格（俯仰落差柔和，摆动幅度极小，安全感拉满）</td><td rowspan="1">惬意、害羞</td><td rowspan="1">ID 19｜belly_bps_full_trust_01.wav</td><td rowspan="1">ID 46｜chin_bps_trusting_01.wav</td></tr>
<tr><td rowspan="1">21</td><td rowspan="1">陌生同类低头远离</td><td rowspan="1">遇到新Beany</td><td rowspan="1">自卑孤单</td><td rowspan="1">最终效果：多次试探躲闪后垂落偏头锁定，长期静止，陌生同类靠近后自卑孤单</td><td rowspan="1">发呆、犯困</td><td rowspan="1">ID 3｜idle_dlm_lonely_01.wav</td><td rowspan="1">ID 52｜nose_dlm_shy_02.wav</td><td rowspan="1">ID 51｜psr clingy mellow 02.wav</td></tr>
<tr><td rowspan="1">22</td><td rowspan="1">翻转肚皮静态垂头</td><td rowspan="1">翻肚皮朝上</td><td rowspan="1">慵懒放空</td><td rowspan="1">最终效果：低速标准小幅抬头垂落低位锁定，仅间隔很久才有极慢微小摆头，之后彻底静止躺平，慵懒放空安静发呆，反应平缓克制，适配高信任慵懒性格（摆动频次极低）</td><td rowspan="1">发呆、惬意</td><td rowspan="1">ID 20｜belly_bps_full_trust_02.wav</td><td rowspan="1">ID 53｜synth_content_sigh_01.wav</td><td rowspan="7">ID /｜/</td></tr>
<tr><td rowspan="1">23</td><td rowspan="1">暗光低头慢挪</td><td rowspan="1">环境变暗</td><td rowspan="1">胆小腼腆、躲起来犯困</td><td rowspan="1">最终效果：低速大幅度抬头后垂至极低位置锁定，仅间隔极久才有微不可察的头部挪动，昏暗环境下内敛胆小，慵懒犯困、安静蜷缩，反应极度迟缓，适配内向胆小慵懒性格（俯仰幅度大，挪动近乎消失）</td><td rowspan="1">害羞、犯困</td><td rowspan="1">ID 21｜lightdown_dlm_dreamy_02.wav</td><td rowspan="1">ID 13｜head_psr_shy_01.wav</td></tr>
<tr><td rowspan="1">24</td><td rowspan="1">连续多次轻碰渐进抬头</td><td rowspan="1">连续多次头部轻触</td><td rowspan="1">逐步放松、接纳互动</td><td rowspan="1">最终效果：循序渐进抬头环顾，动作柔和舒缓，多次触碰后慢慢放下防备，温顺接纳安抚</td><td rowspan="1">惬意、好奇</td><td rowspan="1">ID 6｜back_psr_comforting_02.wav</td><td rowspan="1">ID 52｜nose_dlm_shy_02.wav</td></tr>
<tr><td rowspan="1">25</td><td rowspan="1">快速撸过度刺激躲闪</td><td rowspan="1">高强度快速撸</td><td rowspan="1">抗拒害怕</td><td rowspan="1">最终效果：中高速标准幅度抬头后快速垂落低位，向抚摸源反方向躲闪偏头，动作短促克制，持续高强度抚摸产生轻微抗拒害怕的焦虑、警觉，反应急促内敛，适配敏感性格（轻度躲闪）</td><td rowspan="2">焦虑、警觉</td><td rowspan="1">ID 22｜hold_psr_afraid_01.wav</td><td rowspan="1">ID 50｜flip_psr_protest_03.wav</td></tr>
<tr><td rowspan="1">26</td><td rowspan="1">强光急促低头躲闪</td><td rowspan="1">突然强光</td><td rowspan="1">刺眼</td><td rowspan="1">最终效果：中高速标准幅度抬头后极速垂落低位，搭配小幅短促左右躲闪摆头，突然强光刺眼产生不安焦虑、警觉避光，反应急促内敛，适配胆小敏感性格（躲闪短促）</td><td rowspan="1">ID 23｜synth_bps_soft_greeting_01.wav</td><td rowspan="1">ID 37｜tilt_psr_anxious_02.wav</td></tr>
<tr><td rowspan="1">27</td><td rowspan="1">肚皮触碰轻快垂点头（肚子快速撸）</td><td rowspan="1">摸肚子-快速撸</td><td rowspan="1">放纵开心、毫无拘束</td><td rowspan="1">最终效果：中高速标准幅度抬头后快速垂向低位，搭配同步小幅快速左右晃头，姿态松弛无拘束，享受肚皮快速抚摸的放纵开心，软糯撒娇，反应灵敏，适配外向活泼性格（俯仰落差标准，摆动速度轻快，无紧绷拘束）</td><td rowspan="1">开心、撒娇</td><td rowspan="1">ID 24｜psr content sigh 02.wav</td><td rowspan="1">ID 18｜wakeup_psr_playful_02.wav</td></tr>
<tr><td rowspan="1">28</td><td rowspan="1">轻摇小幅快点头（Gentleshake）</td><td rowspan="1">轻摇</td><td rowspan="1">轻微兴奋、觉得好玩</td><td rowspan="1">最终效果：中速小幅抬头回落快速点头，搭配极微弱同步头部颤动，动作灵动轻快，对轻摇变化充满温和好奇，觉得趣味开心，反应适中灵敏，适配中性温和性格（俯仰幅度微小，颤动微弱，愉悦感克制）</td><td rowspan="1">开心、好奇</td><td rowspan="1">ID 18｜wakeup_psr_playful_02.wav</td><td rowspan="1">ID 47｜psr steady 03.wav</td></tr>
<tr><td rowspan="1">29</td><td rowspan="1">遇见同类双向晃头（陌生Beany）</td><td rowspan="1">遇到新Beany</td><td rowspan="1">好奇、新鲜、试探友好</td><td rowspan="1">最终效果：中低速小幅平缓抬头回落点头，搭配标准幅度温和左右摆头，节奏舒缓克制，试探性打量陌生同类，充满温和善意的好奇，反应适中，适配中性温和性格（双轴速度平缓，幅度标准，情绪克制友好）</td><td rowspan="1">好奇、开心</td><td rowspan="1">ID 25｜synth_emotion_grateful_01.wav</td><td rowspan="1">ID 23｜synth_bps_soft_greeting_01.wav</td><td rowspan="1">ID 38｜synth_emotion_mischievous_01.wav</td></tr>
<tr><td rowspan="1">30</td><td rowspan="1">唤醒急促小颤头（唤醒词）</td><td rowspan="1">唤醒提示词</td><td rowspan="1">立刻清醒、期待互动、开心</td><td rowspan="1">最终效果：超高速极小幅度抬头回落同步左右高频颤动，动作灵动急促，瞬间清醒，满怀期待互动的开心与好奇，反应极速灵敏，适配活泼青年性格（双轴幅度极小、频率极高，瞬间唤醒的灵动质感）</td><td rowspan="1">开心、好奇</td><td rowspan="1">ID 26｜wakeup_psr_playful_01.wav</td><td rowspan="1">ID 18｜wakeup_psr_playful_02.wav</td><td rowspan="1">ID /｜/</td></tr>
<tr><td rowspan="1">31</td><td rowspan="1">粗暴握持高频躲闪颤</td><td rowspan="1">粗暴长时间握持</td><td rowspan="1">拘束害怕</td><td rowspan="1">最终效果：超高速微小幅度抬头回落高频交替，搭配快速小幅左右躲闪颤动，动作急促紧绷，被粗暴握持产生拘束害怕的焦虑、高度警觉，适配胆小敏感性格（高频躲闪）</td><td rowspan="1">焦虑、警觉</td><td rowspan="1">ID 22｜hold_psr_afraid_01.wav</td><td rowspan="1">ID 31｜psr content sigh 01.wav</td><td rowspan="1">ID 15｜synth_emotion_worried_01.wav</td></tr>
<tr><td rowspan="1">32</td><td rowspan="1">旋转抛起极速环绕头（旋转抛）</td><td rowspan="1">旋转抛起</td><td rowspan="1">极度亢奋、刺激、欢快</td><td rowspan="1">最终效果：超高速标准幅度抬头回落交替，叠加极限大角度极速左右环绕，动作饱满紧凑，极致欢快亢奋，刺激感强烈，反应极其灵敏，适配极致活泼青年性格（双轴同步极限高速运动，幅度拉满，亢奋峰值）</td><td rowspan="1">开心、得意</td><td rowspan="1">ID 27｜tossup_psr_frightened_01.wav</td><td rowspan="1">ID 54｜synth_dlm_yawn_squeak_01.wav</td><td rowspan="4">ID /｜/</td></tr>
<tr><td rowspan="1">33</td><td rowspan="1">点头同步左右小幅颤（极致开心）</td><td rowspan="1">Headtouch全类型/遇到新Beany/遇到熟悉Beany</td><td rowspan="1">极度开心、雀跃、撒娇蹦跳感</td><td rowspan="1">最终效果：中高速小幅抬头回落点头叠加同步左右微颤，双轴联动灵动雀跃，极致外放开心，主动流露撒娇亲昵，反应极灵敏，适配高活泼青年性格（俯仰幅度偏小，双轴同步高速运动，亢奋感拉满）</td><td rowspan="2">开心、撒娇</td><td rowspan="1">ID 24｜psr content sigh 02.wav</td><td rowspan="1">ID 10｜psr steady 02.wav</td></tr>
<tr><td rowspan="1">34</td><td rowspan="1">遇见熟同类高频点头（熟悉Beany）</td><td rowspan="1">遇到熟悉Beany</td><td rowspan="1">狂喜、亲近、老友重逢</td><td rowspan="1">最终效果：高速标准幅度抬头回落高频点头，搭配极细微同步左右颤动，动作密集灵动，展现见到熟悉伙伴的狂喜亲昵撒娇，反应极灵敏，适配外向活泼性格（俯仰幅度偏大、高频循环，微颤烘托亲近亢奋感）</td><td rowspan="1">ID 28｜psr steady 01.wav</td><td rowspan="1">ID 33｜hold_dlm_clingy_01.wav</td></tr>
<tr><td rowspan="1">35</td><td rowspan="1"><strong>【待补/待确认】 单侧轻碰侧低头躲闪（摸头左）</strong></td><td rowspan="1">摸头左-轻碰</td><td rowspan="1">腼腆躲闪、慢慢适应</td><td rowspan="1"><strong>【待补/待确认】 最终效果：低速极小幅度抬头后垂向低位，同步向内侧缓慢躲闪偏头，静置许久才缓慢复位，被单侧触碰后腼腆羞涩，略带试探好奇，反应迟缓克制，适配胆小害羞性格（双轴幅度微小，全程低速，躲闪内敛）</strong></td><td rowspan="1">害羞、好奇</td><td rowspan="1">ID 13｜head_psr_shy_01.wav</td><td rowspan="1">ID 16｜nose_dlm_shy_01.wav</td></tr>
<tr><td rowspan="1">36</td><td rowspan="1">侧倒低头向内躲闪</td><td rowspan="1">侧倒（向左）</td><td rowspan="1">不安、自保</td><td rowspan="1">最终效果：高速大幅度抬头后极速垂落低位向内侧躲闪偏头，搭配短促颤动，身体侧倒失衡时流露不安害怕的焦虑警觉，反应急促紧绷，适配胆小敏感性格（向内躲闪自保）</td><td rowspan="1">焦虑、警觉</td><td rowspan="1">ID 29｜sidefall_psr_guard_01.wav</td><td rowspan="1">ID 31｜psr content sigh 01.wav</td><td rowspan="1">ID 15｜synth_emotion_worried_01.wav</td></tr>
<tr><td rowspan="1">37</td><td rowspan="1"><strong>【待补/待确认】 单侧轻碰侧低头躲闪（摸头左）</strong></td><td rowspan="1">摸头左-轻碰</td><td rowspan="2">腼腆躲闪、慢慢适应</td><td rowspan="2"><strong>【待补/待确认】 最终效果：低速极小幅度抬头后垂向低位，同步向内侧缓慢躲闪偏头，静置许久才缓慢复位，被单侧触碰后腼腆羞涩，略带试探好奇，反应迟缓克制，适配胆小害羞性格（双轴幅度微小，全程低速，躲闪内敛）</strong></td><td rowspan="2">害羞、好奇</td><td rowspan="1">ID 30｜head_psr_shy_02.wav</td><td rowspan="1">ID 52｜nose_dlm_shy_02.wav</td><td rowspan="11">ID /｜/</td></tr>
<tr><td rowspan="1">38</td><td rowspan="1">单侧轻碰侧低头躲闪（摸头右）</td><td rowspan="1">摸头右-轻碰</td><td rowspan="1">ID 16｜nose_dlm_shy_01.wav</td><td rowspan="1">ID 30｜head_psr_shy_02.wav</td></tr>
<tr><td rowspan="1">39</td><td rowspan="1">单侧轻碰头顶躲闪</td><td rowspan="1">摸头顶</td><td rowspan="1">惊吓躲闪</td><td rowspan="1">最终效果：直接高速低头后，缓慢犹豫抬头，怀有不确定迟疑</td><td rowspan="1">警觉</td><td rowspan="1">ID 17｜psr _clingy _mellow 01</td><td rowspan="1">ID 25｜synth_emotion_grateful_01.wav</td></tr>
<tr><td rowspan="1">40</td><td rowspan="1">侧倒低头向内躲闪</td><td rowspan="1">侧倒（向右）</td><td rowspan="1">不安、自保</td><td rowspan="1">最终效果：高速大幅度抬头后极速垂落低位向内侧躲闪偏头，搭配短促颤动，身体侧倒失衡时流露不安害怕的焦虑警觉，反应急促紧绷，适配胆小敏感性格（向内躲闪自保）</td><td rowspan="1">焦虑、警觉</td><td rowspan="1">ID 32｜sidefall_psr_guard_02.wav</td><td rowspan="1">ID 37｜tilt_psr_anxious_02.wav</td></tr>
<tr><td rowspan="1">41</td><td rowspan="1">单侧慢偏头依赖（摸头左专用）</td><td rowspan="1">摸头左-轻碰/长时间抚摸</td><td rowspan="1">依赖、撒娇、偏向抚摸源</td><td rowspan="1">最终效果：低速轻柔抬头后缓慢偏向左侧抚摸源长时间停留，再平缓回正，主动贴近触碰方向，流露软糯依赖的撒娇状态，反应迟缓温柔，适配内向温顺性格（动作幅度标准偏小，速度缓慢，依恋感突出）</td><td rowspan="1">撒娇、惬意</td><td rowspan="1">ID 33｜hold_dlm_clingy_01.wav</td><td rowspan="1">ID 34｜hold_dlm_clingy_02.wav</td></tr>
<tr><td rowspan="1">42</td><td rowspan="1">单侧快速偏头蹭手（摸头左快速撸）</td><td rowspan="1">摸头左-快速撸</td><td rowspan="1">兴奋撒娇、主动蹭抚摸手</td><td rowspan="1">最终效果：中高速轻柔抬头锁定高位，持续快速向左往返蹭向抚摸源，主动亲昵撒娇，情绪活泼外放，反应灵敏，适配外向活泼性格（抬头幅度微小，单侧偏航幅度适中，蹭动节奏轻快）</td><td rowspan="1">撒娇、开心</td><td rowspan="1">ID 34｜hold_dlm_clingy_02.wav</td><td rowspan="1">ID 47｜psr steady 03.wav</td></tr>
<tr><td rowspan="1">43</td><td rowspan="1">定点单侧观望（左）</td><td rowspan="1">全场景</td><td rowspan="1">好奇观察</td><td rowspan="1">最终效果：低速标准幅度抬头后缓慢向左侧大幅度侧转，长时间静置观察，动作平稳无抖动，展现单向留意事物的温和好奇，反应平缓，适配中性探索性格（观望久）</td><td rowspan="1">好奇</td><td rowspan="1">ID 8｜headright_psr_alert_right_01.wav</td><td rowspan="1">ID 45｜headright_psr_alert_right_02.wav</td></tr>
<tr><td rowspan="1">44</td><td rowspan="1">单侧慢偏头依赖（摸头右专用）</td><td rowspan="1">摸头右-轻碰/长时间抚摸</td><td rowspan="1">依赖、撒娇、偏向抚摸源</td><td rowspan="1">最终效果：低速轻柔抬头后缓慢偏向右侧抚摸源长时间停留，再平缓回正，主动贴近触碰方向，流露软糯依赖的撒娇状态，反应迟缓温柔，适配内向温顺性格（动作幅度标准偏小，速度缓慢，依恋感突出）</td><td rowspan="1">撒娇、惬意</td><td rowspan="1">ID 35｜hold_dlm_clingy_03.wav</td><td rowspan="1">ID 33｜hold_dlm_clingy_01.wav</td></tr>
<tr><td rowspan="1">45</td><td rowspan="1">定点单侧观望（右）</td><td rowspan="1">全场景</td><td rowspan="1">好奇观察</td><td rowspan="1">最终效果：低速标准幅度抬头后缓慢向右侧大幅度侧转，长时间静置观察，动作平稳无抖动，展现单向留意事物的温和好奇，反应平缓，适配中性探索性格（观望久）</td><td rowspan="1">好奇</td><td rowspan="1">ID 2｜back_psr_comforting_01.wav</td><td rowspan="1">ID 45｜headright_psr_alert_right_02.wav</td></tr>
<tr><td rowspan="1">46</td><td rowspan="1">短时握持间断晃头（Sustainedhold）</td><td rowspan="1">长时间握持/抬头抱持</td><td rowspan="1">黏人开心，舍不得放下</td><td rowspan="1">最终效果：低速轻柔抬头持续维持高位，间断穿插快速左右摆头，黏人不肯离开怀抱，撒娇卖萌、满心开心，反应快慢交替层次柔和，适配黏人温顺性格（抬头幅度微小，摆动间断克制，依恋撒娇感突出）</td><td rowspan="1">撒娇、开心</td><td rowspan="1">ID 33｜hold_dlm_clingy_01.wav</td><td rowspan="1">ID 35｜hold_dlm_clingy_03.wav</td></tr>
<tr><td rowspan="1">47</td><td rowspan="1">翻转肚皮上扬晃头（Flipbelly-up）</td><td rowspan="1">翻转肚皮朝上</td><td rowspan="1">信任、放肆、极度放松开心</td><td rowspan="1">最终效果：低速大幅度抬头舒展至高位，搭配标准大角度缓慢左右摆头，姿态完全放松无防备，尽显惬意安心的开心，反应平缓柔和，适配温顺高信任性格（俯仰幅度偏大，摆动速度缓慢，舒展松弛的安全感）</td><td rowspan="1">开心、惬意</td><td rowspan="1">ID 9｜belly_psr_full_trust_01.wav</td><td rowspan="1">ID 55｜belly_psr_full_trust_02.wav</td></tr>
<tr><td rowspan="1">48</td><td rowspan="1">待机呼吸间断侧头</td><td rowspan="1">呼吸</td><td rowspan="1">待机微探索</td><td rowspan="1">最终效果：超低速基础呼吸绑定间断单侧侧头，待机放空时偶尔好奇打量，不打断休眠，反应恒定缓慢</td><td rowspan="1">好奇、发呆</td><td rowspan="1">ID 36｜sideleft_psr_checkin_01.wav</td><td rowspan="1">ID 56｜sideright_psr_checkin_01.wav</td><td rowspan="1">ID 59｜synth_bps_steady_hum_01.wav</td></tr>
<tr><td rowspan="1">49</td><td rowspan="1">轻摇缓慢环视</td><td rowspan="1">轻摇</td><td rowspan="1">晃动观察</td><td rowspan="1">最终效果：低速微小幅度抬头锁定高位，搭配中等幅度缓慢小范围环绕摆头，动作平稳柔和，轻摇过程中平静打量四周，对晃动变化充满温和好奇，反应平缓，适配中性温和性格（范围小）</td><td rowspan="3">好奇</td><td rowspan="1">ID 37｜tilt_psr_anxious_02.wav</td><td rowspan="1">ID 31｜psr content sigh 01.wav</td><td rowspan="1">ID 15｜synth_emotion_worried_01.wav</td></tr>
<tr><td rowspan="1">50</td><td rowspan="1">间断定点侧头试探</td><td rowspan="1">遇到新Beany/变亮/变暗</td><td rowspan="1">试探观察</td><td rowspan="1">最终效果：低速小幅抬头锁定高位，间断向左右两侧定点侧头观望，交替试探陌生事物，动作谨慎克制，充满内敛的探索好奇，反应迟缓克制，适配内向探索性格（交替试探）</td><td rowspan="1">ID 23｜synth_bps_soft_greeting_01.wav</td><td rowspan="1">ID 52｜nose_dlm_shy_02.wav</td><td rowspan="1">ID 38｜synth_emotion_mischievous_01.wav</td></tr>
<tr><td rowspan="1">51</td><td rowspan="1">开机分段环视</td><td rowspan="1">开机</td><td rowspan="1">扫描环境</td><td rowspan="1">最终效果：低速大幅度完整抬升至极限仰角，搭配极限大角度缓慢完整左右环绕，开机后全面扫描初始化环境，充满初次探索好奇，反应沉稳有仪式感</td><td rowspan="1">ID 39｜poweron_psr_softwake_v02.wav</td><td rowspan="1">ID 45｜headright_psr_alert_right_02.wav</td><td rowspan="4">ID /｜/</td></tr>
<tr><td rowspan="1">52</td><td rowspan="1">长时间握持静靠（Sustainedhold）</td><td rowspan="1">长时间握持/抬头抱持</td><td rowspan="1">黏人、依赖、不愿被放下</td><td rowspan="1">最终效果：低速轻柔抬头锁定高位，持续缓慢小范围左右环绕摆头，姿态软糯黏人，流露不愿被放下的依赖撒娇，反应缓慢柔和，适配黏人温顺性格（抬头幅度微小，环绕速度极慢，依恋氛围浓厚）</td><td rowspan="1">撒娇、惬意</td><td rowspan="1">ID 35｜hold_dlm_clingy_03.wav</td><td rowspan="1">ID 34｜hold_dlm_clingy_02.wav</td></tr>
<tr><td rowspan="1">53</td><td rowspan="1">低电量间断抬头观望</td><td rowspan="1">低电量</td><td rowspan="1">虚弱观察</td><td rowspan="1">最终效果：超低速极小幅度无力抬头，搭配微弱缓慢左右摆动，电量不足时依旧流露微弱的探索好奇，反应极度迟缓乏力，适配低电量状态（动作无力）</td><td rowspan="1">好奇、犯困</td><td rowspan="1">ID 40｜psr content sigh 03.wav</td><td rowspan="1">ID /｜/</td></tr>
<tr><td rowspan="1">54</td><td rowspan="1">长时间握持间断打量</td><td rowspan="1">长时间握持</td><td rowspan="1">四处打量</td><td rowspan="1">最终效果：低速微小幅度抬头锁定高位，间断向左右两侧侧头观望，被抱在怀里时平静打量四周，充满安静的探索好奇，反应平缓克制，适配内向黏人探索性格（间断观望）</td><td rowspan="1">好奇</td><td rowspan="1">ID 41｜sideright_psr_checkin_02.wav</td><td rowspan="1">ID 57｜sideleft_psr_checkin_02.wav</td></tr>
<tr><td rowspan="1">55</td><td rowspan="1">暗光慵懒垂头（Darkness）</td><td rowspan="2">环境变暗</td><td rowspan="1">困倦、慵懒、昏昏欲睡</td><td rowspan="1">最终效果：低速大幅度抬头后垂至低位锁定，搭配超慢小幅左右晃动，动作全程慵懒迟缓，展现昏暗环境下昏昏犯困的放空状态，反应极度缓慢，适配慵懒内向性格（俯仰幅度大、低位停留久，摆动速度极慢，困倦感突出）</td><td rowspan="1">犯困、惬意</td><td rowspan="1">ID 42｜lightdown_dlm_dreamy_01.wav</td><td rowspan="1">ID 21｜lightdown_dlm_dreamy_02.wav</td><td rowspan="1">ID 1｜charge_dlm_resting_01.wav</td></tr>
<tr><td rowspan="1">56</td><td rowspan="1">暗光间断抬头观察</td><td rowspan="1">黑暗观察</td><td rowspan="1">最终效果：超低速间隔小幅抬头，单侧定点侧头观望，黑暗中谨慎打量周边，充满内敛的探索好奇，反应极度迟缓，适配内向胆小探索性格（间隔长）</td><td rowspan="2">好奇</td><td rowspan="1">ID 43｜backhead_dlm_uneasy_01.wav</td><td rowspan="1">ID 58｜backhead_dlm_uneasy_02.wav</td><td rowspan="6">ID /｜/</td></tr>
<tr><td rowspan="1">57</td><td rowspan="1">左右循环环视</td><td rowspan="1">唤醒提示词/遇到新Beany/变亮/变暗</td><td rowspan="1">四处打量</td><td rowspan="1">最终效果：中速小幅抬头锁定高位，搭配极限大角度缓慢完整左右环绕，动作平稳连贯，苏醒后全面扫描环境，四处打量充满新鲜感与探索欲，反应适中灵敏，适配活泼探索性格（环绕完整）</td><td rowspan="1">ID 18｜wakeup_psr_playful_02.wav</td><td rowspan="1">ID 41｜sideright_psr_checkin_02.wav</td></tr>
<tr><td rowspan="1">58</td><td rowspan="1">抛起上扬晃头（抛起事件）</td><td rowspan="1">抛起</td><td rowspan="1">刺激、兴奋、失重感雀跃</td><td rowspan="1">最终效果：高速大幅度抬头至极限仰角，搭配中幅快速左右摆头，动作舒展亢奋，展现被抛起时失重雀跃的小得意，反应极灵敏，适配高活泼青年性格（俯仰幅度拉满，偏航速度极快，亢奋刺激感强）</td><td rowspan="1">开心、得意</td><td rowspan="1">ID 27｜tossup_psr_frightened_01.wav</td><td rowspan="1">ID 54｜synth_dlm_yawn_squeak_01.wav</td></tr>
<tr><td rowspan="1">59</td><td rowspan="1">左右快速摆头好奇（强光/唤醒）</td><td rowspan="1">唤醒提示词/环境变亮</td><td rowspan="1">好奇、精神、苏醒兴奋</td><td rowspan="1">最终效果：高速小幅抬头锁定高位，搭配标准幅度快速左右往复摆头，动作轻快灵动，苏醒后快速扫描环境，满是新鲜感与愉悦好奇，反应灵敏，适配活泼青年性格（抬头幅度微小，偏航幅度标准，摆动速度快，探索欲强）</td><td rowspan="1">好奇、开心</td><td rowspan="1">ID 44｜wakeup_psr_playful_03.wav</td><td rowspan="1">ID 26｜wakeup_psr_playful_01.wav</td></tr>
<tr><td rowspan="1">60</td><td rowspan="1">被拿起上扬连续点头（Pickedup）</td><td rowspan="1">被拿起/抬头抱持</td><td rowspan="1">黏人、开心、喜欢被抱</td><td rowspan="1">最终效果：中速标准幅度抬头维持亲昵高位，不间断循环中等幅度左右摆头，被抱起时黏人撒娇，满心愉悦开心，反应持续灵敏，适配黏人活泼性格（抬头幅度适中，循环不间断，怀抱亲昵氛围浓厚）</td><td rowspan="1">开心、撒娇</td><td rowspan="1">ID 34｜hold_dlm_clingy_02.wav</td><td rowspan="1">ID 33｜hold_dlm_clingy_01.wav</td></tr>
<tr><td rowspan="1">61</td><td rowspan="1">单侧快速偏头蹭手（摸头右快速撸）</td><td rowspan="1">摸头右-快速撸</td><td rowspan="1">兴奋撒娇、主动蹭抚摸手</td><td rowspan="1">最终效果：中高速轻柔抬头锁定高位，持续快速向右往返蹭向抚摸手，主动亲昵撒娇，情绪活泼外放，反应灵敏，适配外向活泼性格（抬头幅度微小，单侧偏航幅度适中，蹭动节奏轻快）</td><td rowspan="1">撒娇、开心</td><td rowspan="1">ID 35｜hold_dlm_clingy_03.wav</td><td rowspan="1">ID 47｜psr steady 03.wav</td></tr></tbody>
</table>

</details>

<details>
<summary>音频资源（61 项，含原表建议替换列）</summary>

<table>
<thead>
<tr><th>ID</th><th>原音频文件名</th><th>Proposed replacement（原表建议）</th><th>适用场景</th></tr></thead>
<tbody>
<tr><td rowspan="1">1</td><td rowspan="1">charge_dlm_resting_01.wav</td><td rowspan="9">原表空白</td><td rowspan="1">安静休息、低刺激存在感；长时间无互动或待机时的 resting 陪伴底。不用于充电提示。</td></tr>
<tr><td rowspan="1">2</td><td rowspan="1">back_psr_comforting_01.wav</td><td rowspan="1">温和安抚刚开始；关系轻松、需要短而软的回应；安静陪伴中的轻确认。</td></tr>
<tr><td rowspan="1">3</td><td rowspan="1">idle_dlm_lonely_01.wav</td><td rowspan="1">独处过久；被放下后的空落；需要稀疏、带着一点想念的低声。</td></tr>
<tr><td rowspan="1">4</td><td rowspan="1">poweroff_dlm_sleep_01.wav</td><td rowspan="1">关机进入彻底休眠；一天结束；需要渐弱、收束的入睡感。</td></tr>
<tr><td rowspan="1">5</td><td rowspan="1">flip_psr_protest_01.wav</td><td rowspan="1">被强迫改变姿态；委屈并想挣脱；需要短促的抗拒反馈。</td></tr>
<tr><td rowspan="1">6</td><td rowspan="1">back_psr_comforting_02.wav</td><td rowspan="1">持续安抚中的重复回应；比第一条更柔；安静状态下的陪伴回声。</td></tr>
<tr><td rowspan="1">7</td><td rowspan="1">poweron_psr_softwake_v01.wav</td><td rowspan="1">开机上电；第一次苏醒；需要柔和、有活力的启动感。</td></tr>
<tr><td rowspan="1">8</td><td rowspan="1">headright_psr_alert_right_01.wav</td><td rowspan="1">突然被从一侧接近；需要快速确认方位；短暂警觉后的注意。</td></tr>
<tr><td rowspan="1">9</td><td rowspan="1">belly_psr_full_trust_01.wav</td><td rowspan="1">信任感较高时的满足回应；放松且开心一点；短时亲密反馈。</td></tr>
<tr><td rowspan="1">10</td><td rowspan="1">stroke_psr_joy_01.wav</td><td rowspan="1"><strong>【待补/待确认】 psr_steady_02.wav</strong></td><td rowspan="1">节奏偏快的愉快互动；兴奋且享受；需要明亮的开心短声。</td></tr>
<tr><td rowspan="1">11</td><td rowspan="1">nod_psr_agree_01.wav</td><td rowspan="6">原表空白</td><td rowspan="1">表示认同、愿意配合；轻松的肯定；互动中的“好呀”式回应。</td></tr>
<tr><td rowspan="1">12</td><td rowspan="1">nod_psr_agree_03.wav</td><td rowspan="1">认同反馈的另一变体；避免与上一条完全重复；同样轻快的肯定感。</td></tr>
<tr><td rowspan="1">13</td><td rowspan="1">head_psr_shy_01.wav</td><td rowspan="1">略显腼腆、想躲一下；还不习惯被关注；害羞偏警觉的轻声。</td></tr>
<tr><td rowspan="1">14</td><td rowspan="1">flip_psr_protest_02.wav</td><td rowspan="1">抗拒升级但仍克制；不想被继续折腾；委屈抗议的第二条。</td></tr>
<tr><td rowspan="1">15</td><td rowspan="1">synth_emotion_worried_01.wav</td><td rowspan="1">不安、紧绷时的短反馈；安全感下降。</td></tr>
<tr><td rowspan="1">16</td><td rowspan="1">nose_dlm_shy_01.wav</td><td rowspan="1">距离突然很近；害羞又好奇；亲昵但还放不开。</td></tr>
<tr><td rowspan="1">17</td><td rowspan="1">synth_aww_01.wav</td><td rowspan="1"><strong>【待补/待确认】 psr_clingy_mellow_01.wav</strong></td><td rowspan="1">软萌、轻微惊喜偏正向；轻碰或被注意到后的柔和回应。</td></tr>
<tr><td rowspan="1">18</td><td rowspan="1">wakeup_psr_playful_02.wav</td><td rowspan="6">原表空白</td><td rowspan="1">熟悉的人唤醒；日常互动开始；比正式开机更轻快的起始。</td></tr>
<tr><td rowspan="1">19</td><td rowspan="1">belly_bps_full_trust_01.wav</td><td rowspan="1">高信任下的深度放松；完全卸下防备；绵长、温暖的安心声。</td></tr>
<tr><td rowspan="1">20</td><td rowspan="1">belly_bps_full_trust_02.wav</td><td rowspan="1">信任更深一层；安抚进入更浓的亲密；比上一条更持续、更沉。</td></tr>
<tr><td rowspan="1">21</td><td rowspan="1">lightdown_dlm_dreamy_02.wav</td><td rowspan="1">夜间进一步安静；准备休息；需要更柔、更长的过渡。</td></tr>
<tr><td rowspan="1">22</td><td rowspan="1">hold_psr_afraid_01.wav</td><td rowspan="1">被拘束、不舒服；害怕但克制；需要不安的弱抗议。</td></tr>
<tr><td rowspan="1">23</td><td rowspan="1">synth_bps_soft_greeting_01.wav</td><td rowspan="1">轻柔问候；关系刚开始或再次见面；低刺激的友好开场。</td></tr>
<tr><td rowspan="1">24</td><td rowspan="1">social_psr_ecstatic_01.wav</td><td rowspan="1"><strong>【待补/待确认】 psr_content_sigh_02.wav</strong></td><td rowspan="1">情绪冲到很高的开心；雀跃、想撒娇蹦跳；社交或亲密高峰。</td></tr>
<tr><td rowspan="1">25</td><td rowspan="1">synth_emotion_grateful_01.wav</td><td rowspan="3">原表空白</td><td rowspan="1">温暖友好、被好好对待后的软回应；社交开场或亲密回馈。</td></tr>
<tr><td rowspan="1">26</td><td rowspan="1">wakeup_psr_playful_01.wav</td><td rowspan="1">被唤醒进入互动；从待机转到兴奋；期待被陪伴的第一声。</td></tr>
<tr><td rowspan="1">27</td><td rowspan="1">tossup_psr_frightened_01.wav</td><td rowspan="1">明显失重、刺激偏强；短暂离开稳定支撑；需要高能量反馈。</td></tr>
<tr><td rowspan="1">28</td><td rowspan="1">social_psr_ecstatic_02.wav</td><td rowspan="1"><strong>【待补/待确认】 psr_steady_01.wav</strong></td><td rowspan="1">极度开心的第二条；狂喜或重逢式雀跃；避免与上一条听感雷同。</td></tr>
<tr><td rowspan="1">29</td><td rowspan="1">sidefall_psr_guard_01.wav</td><td rowspan="2">原表空白</td><td rowspan="1">失去平衡、需要自保；侧向不稳；戒备但不攻击。</td></tr>
<tr><td rowspan="1">30</td><td rowspan="1">head_psr_shy_02.wav</td><td rowspan="1">害羞躲闪的变体；慢慢适应被关注；比上一条略软一点。</td></tr>
<tr><td rowspan="1">31</td><td rowspan="1">synth_oops_recovery_01.wav</td><td rowspan="1"><strong>【待补/待确认】 psr_content_sigh_01.wav</strong></td><td rowspan="1">惊吓或不安后的缓和；从紧张回到可互动；带一点不好意思的恢复声。</td></tr>
<tr><td rowspan="1">32</td><td rowspan="1">sidefall_psr_guard_02.wav</td><td rowspan="8">原表空白</td><td rowspan="1">自保戒备的第二条；持续不稳时的重复；更明确一点的护住自己。</td></tr>
<tr><td rowspan="1">33</td><td rowspan="1">hold_dlm_clingy_01.wav</td><td rowspan="1">黏人、舍不得分开；被抱持时的依赖；温暖的撒娇贴近。</td></tr>
<tr><td rowspan="1">34</td><td rowspan="1">hold_dlm_clingy_02.wav</td><td rowspan="1">黏人升级；主动蹭近；开心又舍不得被放下。</td></tr>
<tr><td rowspan="1">35</td><td rowspan="1">hold_dlm_clingy_03.wav</td><td rowspan="1">依赖感最浓的一版；长时间贴近；柔和持续的撒娇。</td></tr>
<tr><td rowspan="1">36</td><td rowspan="1">sideleft_psr_checkin_01.wav</td><td rowspan="1">侧面被轻触后的确认；友好探询；轻量互动中的“我在”。</td></tr>
<tr><td rowspan="1">37</td><td rowspan="1">tilt_psr_anxious_02.wav</td><td rowspan="1">持续倾斜或多次晃动；不安累积；比更轻的不安反馈更紧一点。</td></tr>
<tr><td rowspan="1">38</td><td rowspan="1">synth_emotion_mischievous_01.wav</td><td rowspan="1">调皮、小得意的短促 chirp；轻松逗弄。</td></tr>
<tr><td rowspan="1">39</td><td rowspan="1">poweron_psr_softwake_v02.wav</td><td rowspan="1">开机苏醒的另一音色；同样柔和启动；用于避免总播同一条。</td></tr>
<tr><td rowspan="1">40</td><td rowspan="1">synth_farewell_bye_01.wav</td><td rowspan="1"><strong>【待补/待确认】 psr_content_sigh_03.wav</strong></td><td rowspan="1">低电量固定提示；能量将尽、虚弱收束；偏困倦的告别感。</td></tr>
<tr><td rowspan="1">41</td><td rowspan="1">sideright_psr_checkin_02.wav</td><td rowspan="6">原表空白</td><td rowspan="1">熟悉后的侧面短回声；亲昵互动中的二次确认；更松弛一点。</td></tr>
<tr><td rowspan="1">42</td><td rowspan="1">lightdown_dlm_dreamy_01.wav</td><td rowspan="1">环境变暗；从活跃转入安静；准备进入低刺激状态。</td></tr>
<tr><td rowspan="1">43</td><td rowspan="1">backhead_dlm_uneasy_01.wav</td><td rowspan="1">视线外突然有动静；安静中被惊一下；柔和的不安。</td></tr>
<tr><td rowspan="1">44</td><td rowspan="1">wakeup_psr_playful_03.wav</td><td rowspan="1">唤醒/互动起始的第三条；轻快期待；用于轮换避免重复。</td></tr>
<tr><td rowspan="1">45</td><td rowspan="1">headright_psr_alert_right_02.wav</td><td rowspan="1">同一侧再次被注意；熟悉后的警觉确认；轻回头式的注意。</td></tr>
<tr><td rowspan="1">46</td><td rowspan="1">chin_bps_trusting_01.wav</td><td rowspan="1">深度亲密刚开始；被温柔对待；短而信任的贴近声。</td></tr>
<tr><td rowspan="1">47</td><td rowspan="1">stroke_psr_joy_02.wav</td><td rowspan="1"><strong>【待补/待确认】 psr_steady_03.wav</strong></td><td rowspan="1">愉快互动的第二条；同样偏快、偏亮；轮换用的开心反馈。</td></tr>
<tr><td rowspan="1">48</td><td rowspan="1">nod_psr_agree_02.wav</td><td rowspan="3">原表空白</td><td rowspan="1">认同点头的第二条；轻松肯定；中等力度的配合感。</td></tr>
<tr><td rowspan="1">49</td><td rowspan="1">nod_psr_agree_04.wav</td><td rowspan="1">认同反馈的第四条；保持轻快；批量互动时轮换。</td></tr>
<tr><td rowspan="1">50</td><td rowspan="1">flip_psr_protest_03.wav</td><td rowspan="1">抗议的第三条；仍委屈但不攻击；高强度不适时的备用。</td></tr>
<tr><td rowspan="1">51</td><td rowspan="1">synth_bored_psr_01.wav</td><td rowspan="1"><strong>【待补/待确认】 psr_clingy_mellow_02.wav</strong></td><td rowspan="1">无聊、提不起劲；长时间无趣等待；短促偏平的反馈。</td></tr>
<tr><td rowspan="1">52</td><td rowspan="1">nose_dlm_shy_02.wav</td><td rowspan="9">原表空白</td><td rowspan="1">近距离逗弄后的二次害羞；熟人之间；比第一次更软。</td></tr>
<tr><td rowspan="1">53</td><td rowspan="1">synth_content_sigh_01.wav</td><td rowspan="1">满足后的轻叹；放松惬意；亲密安抚后的绵长收束。</td></tr>
<tr><td rowspan="1">54</td><td rowspan="1">synth_dlm_yawn_squeak_01.wav</td><td rowspan="1">犯困时的哈欠式轻声；从活跃转入休息；带一点软萌收尾。</td></tr>
<tr><td rowspan="1">55</td><td rowspan="1">belly_psr_full_trust_02.wav</td><td rowspan="1">满足信任的第二条；放松开心；短时亲密反馈的轮换。</td></tr>
<tr><td rowspan="1">56</td><td rowspan="1">sideright_psr_checkin_01.wav</td><td rowspan="1">另一侧的轻量确认；友好接近；短促的“我知道你在”。</td></tr>
<tr><td rowspan="1">57</td><td rowspan="1">sideleft_psr_checkin_02.wav</td><td rowspan="1">侧面重复互动后的更友好回应；轻贴近；二级确认。</td></tr>
<tr><td rowspan="1">58</td><td rowspan="1">backhead_dlm_uneasy_02.wav</td><td rowspan="1">柔和不安的第二条；刺激不大但需表态；更轻的二级版本。</td></tr>
<tr><td rowspan="1">59</td><td rowspan="1">synth_bps_steady_hum_01.wav</td><td rowspan="1">平稳持续的轻哼；待机伴随；低刺激氛围底。</td></tr>
<tr><td rowspan="1">60</td><td rowspan="1">synth_dlm_content_hum_01.wav</td><td rowspan="1">起伏较多的合成低哼；安静陪伴备选。</td></tr>
<tr><td rowspan="1">61</td><td rowspan="1">synth_greeting_hello_01.wav</td><td rowspan="1"><strong>【待补/待确认】 charge_psr_comforting_01.wav</strong></td><td rowspan="1">插上充电器/开始充电时的固定提示。</td></tr></tbody>
</table>

</details>

<details>
<summary>震动资源</summary>

<table>
<thead>
<tr><th>震动 ID</th><th>强度</th></tr></thead>
<tbody>
<tr><td rowspan="1">1</td><td rowspan="1">弱震动</td></tr>
<tr><td rowspan="1">2</td><td rowspan="1">中震动</td></tr>
<tr><td rowspan="1">3</td><td rowspan="1">强震动</td></tr></tbody>
</table>

</details>

<details>
<summary>情绪映射</summary>

<table>
<thead>
<tr><th>ID</th><th>情绪描述</th><th>原始对应值</th><th>对应具体情绪（原表D列）</th></tr></thead>
<tbody>
<tr><td rowspan="1">0</td><td rowspan="1">ANY</td><td rowspan="1">适用于任何情绪</td><td rowspan="1"></td></tr>
<tr><td rowspan="1">1</td><td rowspan="1">开心</td><td rowspan="1">HAPPY/CLINGY/PROUD/COZY</td><td rowspan="1">开心 / 黏人 / 得意 / 惬意</td></tr>
<tr><td rowspan="1">2</td><td rowspan="1">平静</td><td rowspan="1">CURIOUS/SPACED</td><td rowspan="1">好奇 / 发呆</td></tr>
<tr><td rowspan="1">3</td><td rowspan="1">悲伤</td><td rowspan="1">SLEEPY/RESTLESS/ALERT/SHY</td><td rowspan="1"></td></tr></tbody>
</table>

原情绪表D5未填写；悲伤组中文映射按用户确认见第05节。

</details>

<details>
<summary>状态模式字</summary>

<table>
<thead>
<tr><th>ID（模式字）</th><th>描述</th><th>原始取值</th><th>原始备注</th></tr></thead>
<tbody>
<tr><td rowspan="1">0</td><td rowspan="1">ANY</td><td rowspan="1">适用于任何状态</td><td rowspan="1">原表空白</td></tr>
<tr><td rowspan="1">1</td><td rowspan="1">光线</td><td rowspan="1">0：暗；1：亮</td><td rowspan="1"><strong>【待补/待确认】 暗的情况下不做任何响应，动作设定为空（我们自己设好，不叫 不轉 不震）</strong></td></tr>
<tr><td rowspan="1">2</td><td rowspan="1">低电量</td><td rowspan="1">0：正常电量； 1：低电量</td><td rowspan="1"><strong>【待补/待确认】 低电量时候通过一个事件来表达，动作列表增加一个动作。删掉</strong></td></tr>
<tr><td rowspan="1">4</td><td rowspan="1">充电中</td><td rowspan="1">0：放电； 1：充电中</td><td rowspan="1"><strong>【待补/待确认】 隔多长时间没有互动，有个呼吸动作，不要</strong></td></tr>
<tr><td rowspan="1">8</td><td rowspan="1">饥饿</td><td rowspan="1">0：饥饿； 1：饱食</td><td rowspan="1">默认为0，占位</td></tr></tbody>
</table>

</details>

<details>
<summary>输入事件原表（42 项）</summary>

<table>
<thead>
<tr><th>事件 ID</th><th>原事件名称</th><th>原事件来源</th><th>原区域</th><th>原候选动作 ID</th><th>Beta 支持</th><th>原表“没有用到的动作 ID，可自行设计”</th></tr></thead>
<tbody>
<tr><td rowspan="1">1</td><td rowspan="1">Headtouch(摸头顶/下巴/鼻子/后脑勺)</td><td rowspan="1">TOUCH </td><td rowspan="3">摸头顶</td><td rowspan="3">10/11/14</td><td rowspan="1">Y</td><td rowspan="1">3/6/15/16/18/19/20/24/25/26/29/31/32/38/39/43/45/60</td></tr>
<tr><td rowspan="1">2</td><td rowspan="1">Headtouch—quickstroke(摸头顶/下巴/鼻子/后脑勺-快速撸)</td><td rowspan="21">TOUCH</td><td rowspan="2">N</td><td rowspan="41">原表空白</td></tr>
<tr><td rowspan="1">3</td><td rowspan="1">Headtouch—sustained(摸头顶/下巴/鼻子/后脑勺-长时间抚摸)</td></tr>
<tr><td rowspan="1">4</td><td rowspan="1">Headtouch(摸头左边)</td><td rowspan="3">头左</td><td rowspan="3">2/11/35/37/41/42</td><td rowspan="1">Y</td></tr>
<tr><td rowspan="1">5</td><td rowspan="1">Headtouch—quickstroke(摸头左边-快速撸)</td><td rowspan="2">N</td></tr>
<tr><td rowspan="1">6</td><td rowspan="1">Headtouch—sustained(摸头左边-长时间抚摸)</td></tr>
<tr><td rowspan="1">7</td><td rowspan="1">Headtouch(摸头右边)</td><td rowspan="3">头右</td><td rowspan="3">2/11/38/44/61</td><td rowspan="1">Y</td></tr>
<tr><td rowspan="1">8</td><td rowspan="1">Headtouch—quickstroke(摸头右边-快速撸)</td><td rowspan="2">N</td></tr>
<tr><td rowspan="1">9</td><td rowspan="1">Headtouch—sustained(摸头右边-长时间抚摸)</td></tr>
<tr><td rowspan="1">10</td><td rowspan="1">Bellytouch—tap(摸肚子-碰一碰)</td><td rowspan="3">摸肚子</td><td rowspan="3">2/10/11/20/27</td><td rowspan="1">Y</td></tr>
<tr><td rowspan="1">11</td><td rowspan="1">Bellytouch—quickstroke(摸肚子-快速撸)</td><td rowspan="2">N</td></tr>
<tr><td rowspan="1">12</td><td rowspan="1">Bellytouch—sustained(摸肚子-长时间抚摸)</td></tr>
<tr><td rowspan="1">13</td><td rowspan="1">Sidetouch—tap(摸左侧面-碰一碰)</td><td rowspan="3">左侧面</td><td rowspan="6">2/11</td><td rowspan="1">Y</td></tr>
<tr><td rowspan="1">14</td><td rowspan="1">Sidetouch—quickstroke(摸左侧面-快速撸)</td><td rowspan="2">N</td></tr>
<tr><td rowspan="1">15</td><td rowspan="1">Sidetouch—sustained(摸左侧面-长时间抚摸)</td></tr>
<tr><td rowspan="1">16</td><td rowspan="1">Sidetouch—tap(摸右侧面-碰一碰)</td><td rowspan="3">右侧面</td><td rowspan="1">Y</td></tr>
<tr><td rowspan="1">17</td><td rowspan="1">Sidetouch—quickstroke(摸右侧面-快速撸)</td><td rowspan="2">N</td></tr>
<tr><td rowspan="1">18</td><td rowspan="1">Sidetouch—sustained(摸右侧面-长时间抚摸)</td></tr>
<tr><td rowspan="1">19</td><td rowspan="1">Backtouch—tap(摸后背-碰一碰)</td><td rowspan="3">摸后背</td><td rowspan="3">2/7/10/11</td><td rowspan="1">Y</td></tr>
<tr><td rowspan="1">20</td><td rowspan="1">Backtouch—quickstroke(摸后背-快速撸)</td><td rowspan="8">N</td></tr>
<tr><td rowspan="1">21</td><td rowspan="1">Backtouch—sustained(摸后背-长时间抚摸)</td></tr>
<tr><td rowspan="1">22</td><td rowspan="1">Sustainedhold(长时间握持&lt;10S, 5 秒以上)</td><td rowspan="1">长时间握持</td><td rowspan="1">31/46/52/54</td></tr>
<tr><td rowspan="1">23</td><td rowspan="1">Gentleshake(轻摇)</td><td rowspan="1">MOTION </td><td rowspan="1">轻摇</td><td rowspan="1">6/28/49</td></tr>
<tr><td rowspan="1">24</td><td rowspan="1">Hardshake(猛摇)</td><td rowspan="4">MOTION</td><td rowspan="1">猛摇</td><td rowspan="1">原表空字符串</td></tr>
<tr><td rowspan="1">25</td><td rowspan="1">Flipbelly-up(翻转)</td><td rowspan="1">翻转</td><td rowspan="1">5/47</td></tr>
<tr><td rowspan="1">26</td><td rowspan="1"><strong>【待补/待确认】 Pickedup(被拿起)（原表有删除线）</strong></td><td rowspan="2">原表空白</td><td rowspan="2">原表空白</td></tr>
<tr><td rowspan="1">27</td><td rowspan="1"><strong>【待补/待确认】 Putdown(被放下)（原表有删除线）</strong></td></tr>
<tr><td rowspan="1">28</td><td rowspan="1">唤醒提示词</td><td rowspan="1">VOICE</td><td rowspan="1">唤醒提示词</td><td rowspan="1">9/13/30/57/59</td><td rowspan="3">Y</td></tr>
<tr><td rowspan="1">29</td><td rowspan="1">Darkness(变暗)</td><td rowspan="2">LIGHT</td><td rowspan="1">变暗</td><td rowspan="1">23/50/55/56/57</td></tr>
<tr><td rowspan="1">30</td><td rowspan="1">Brightness(变亮)</td><td rowspan="1">变亮</td><td rowspan="1">9/50/57/59</td></tr>
<tr><td rowspan="1">31</td><td rowspan="1">Idle&gt;2hours(长时间无互动)</td><td rowspan="2">SYSTEM</td><td rowspan="1">长时间无互动</td><td rowspan="2">6</td><td rowspan="2">N</td></tr>
<tr><td rowspan="1">32</td><td rowspan="1">Idle&gt;48hours(超长无互动)</td><td rowspan="1">超长无互动</td></tr>
<tr><td rowspan="1">33</td><td rowspan="1">NewBeanynearby(遇到新Beany)</td><td rowspan="2">SOCIAL</td><td rowspan="1">遇到新Beany</td><td rowspan="1">17/21/29/33/50/57</td><td rowspan="6">Y</td></tr>
<tr><td rowspan="1">34</td><td rowspan="1">FamiliarBeanynearby(遇到熟悉Beany)</td><td rowspan="1">遇到熟悉Beany</td><td rowspan="1">33/34</td></tr>
<tr><td rowspan="1">35</td><td rowspan="1">侧倒</td><td rowspan="1">MOTION</td><td rowspan="1">侧倒</td><td rowspan="1">36</td></tr>
<tr><td rowspan="1">36</td><td rowspan="1">充电</td><td rowspan="4">SYSTEM</td><td rowspan="1">充电</td><td rowspan="1">1</td></tr>
<tr><td rowspan="1">37</td><td rowspan="1">低电量</td><td rowspan="1">低电量</td><td rowspan="1">53</td></tr>
<tr><td rowspan="1">38</td><td rowspan="1">开机</td><td rowspan="1">开机</td><td rowspan="1">8/51</td></tr>
<tr><td rowspan="1">39</td><td rowspan="1">呼吸（5分钟~2小时之间，如果没有互动就30S呼吸一次）</td><td rowspan="1">呼吸</td><td rowspan="1">6/48</td><td rowspan="1">N</td></tr>
<tr><td rowspan="1">40</td><td rowspan="1">抛起</td><td rowspan="2">MOTION</td><td rowspan="1">抛起</td><td rowspan="1">32/58</td><td rowspan="1">Y</td></tr>
<tr><td rowspan="1">41</td><td rowspan="1"><strong>【待补/待确认】 旋转抛起（原表有删除线）</strong></td><td rowspan="1">旋转抛起</td><td rowspan="1">32</td><td rowspan="1">N</td></tr>
<tr><td rowspan="1">42</td><td rowspan="1">关机</td><td rowspan="1">SYSTEM</td><td rowspan="1">关机</td><td rowspan="1">4</td><td rowspan="1">Y</td></tr></tbody>
</table>

</details>

<details>
<summary>输入事件原表的触摸分型备注</summary>

<table>
<thead>
<tr><th>序号</th><th>Touch Type（原文）</th><th>Duration（原文）</th></tr></thead>
<tbody>
<tr><td rowspan="1">1</td><td rowspan="1">Tap (碰一碰)</td><td rowspan="1">&lt;1 sec</td></tr>
<tr><td rowspan="1">2</td><td rowspan="1">Quick stroke (快速撸一下)</td><td rowspan="1"><strong>【待补/待确认】 1-3 sec</strong></td></tr>
<tr><td rowspan="1">3</td><td rowspan="1">Sustained touch (长时间抚摸)</td><td rowspan="1"><strong>【待补/待确认】 &gt;3 sec</strong></td></tr>
<tr><td rowspan="1">4</td><td rowspan="1">超过10秒有校准动作</td><td rowspan="1">原表空白</td></tr></tbody>
</table>

</details>

<details>
<summary>控制板协议原动作 ID 与控制码</summary>

<table>
<thead>
<tr><th>原动作 ID</th><th>原控制码</th></tr></thead>
<tbody>
<tr><td rowspan="1">1</td><td rowspan="1">0x00</td></tr>
<tr><td rowspan="1">4</td><td rowspan="1">0x01</td></tr>
<tr><td rowspan="1">5</td><td rowspan="1">0x02</td></tr>
<tr><td rowspan="1">6</td><td rowspan="1">0x03</td></tr>
<tr><td rowspan="1">13</td><td rowspan="1">0x04</td></tr>
<tr><td rowspan="1">19</td><td rowspan="1">0x05</td></tr>
<tr><td rowspan="1">20</td><td rowspan="1">0x06</td></tr>
<tr><td rowspan="1">25</td><td rowspan="1">0x07</td></tr>
<tr><td rowspan="1">26</td><td rowspan="1">0x08</td></tr>
<tr><td rowspan="1">27</td><td rowspan="1">0x09</td></tr>
<tr><td rowspan="1">30</td><td rowspan="1">0x0A</td></tr>
<tr><td rowspan="1">32</td><td rowspan="1">0x0B</td></tr>
<tr><td rowspan="1">37</td><td rowspan="1">0x0C</td></tr>
<tr><td rowspan="1">45</td><td rowspan="1">0x0D</td></tr>
<tr><td rowspan="1">49</td><td rowspan="1">0x0E</td></tr>
<tr><td rowspan="1">50</td><td rowspan="1">0x0F</td></tr>
<tr><td rowspan="1">54</td><td rowspan="1">0x10</td></tr>
<tr><td rowspan="1">56</td><td rowspan="1">0x11</td></tr>
<tr><td rowspan="1">60</td><td rowspan="1">0x12</td></tr>
<tr><td rowspan="1">61</td><td rowspan="1">0x13</td></tr>
<tr><td rowspan="1">65</td><td rowspan="1">0x14</td></tr>
<tr><td rowspan="1">66</td><td rowspan="1">0x15</td></tr>
<tr><td rowspan="1">67</td><td rowspan="1">0x16</td></tr>
<tr><td rowspan="1">68</td><td rowspan="1">0x17</td></tr>
<tr><td rowspan="1">70</td><td rowspan="1">0x18</td></tr>
<tr><td rowspan="1">93</td><td rowspan="1">0x19</td></tr>
<tr><td rowspan="1">95</td><td rowspan="1">0x1A</td></tr>
<tr><td rowspan="1">96</td><td rowspan="1">0x1B</td></tr>
<tr><td rowspan="1">100</td><td rowspan="1">0x1C</td></tr>
<tr><td rowspan="1">101</td><td rowspan="1">0x1D</td></tr>
<tr><td rowspan="1">26+101</td><td rowspan="1">0x1E</td></tr>
<tr><td rowspan="1">20+101</td><td rowspan="1">0x1F</td></tr></tbody>
</table>

</details>

<details>
<summary>控制板动作命令应答</summary>

<table>
<thead>
<tr><th>应答含义</th><th>原数据值</th></tr></thead>
<tbody>
<tr><td rowspan="1">命令接收成功</td><td rowspan="1">0x00</td></tr>
<tr><td rowspan="1">命令接收失败</td><td rowspan="1">0x01</td></tr>
<tr><td rowspan="1">命令错误</td><td rowspan="1">0x02</td></tr>
<tr><td rowspan="1">校验错误</td><td rowspan="1">0x03</td></tr>
<tr><td rowspan="1">设备在忙</td><td rowspan="1">0x04</td></tr>
<tr><td rowspan="1">设备异常</td><td rowspan="1">0x05</td></tr>
<tr><td rowspan="1">动作异常</td><td rowspan="1">0x06</td></tr></tbody>
</table>

</details>

## 对外演示闭环

<table>
<thead>
<tr><th>场景</th><th>操作与预期</th></tr></thead>
<tbody>
<tr><td rowspan="1">未启用时保持初始</td><td rowspan="1">设备未装成长包，发生30次普通触摸<br>App仅连接或读取<br>设备仍为初始模式，不产生本档案成长里程碑<br>用户首次启用并确认包成功后，初识XP0，生成M01/S01</td></tr>
<tr><td rowspan="1">一次摸头留下故事</td><td rowspan="1">初识包已生效，M03未达成<br>真人触发头顶轻触1，App查询并去重保存<br>五维与XP累计；M03/S03生成，设备阶段仍按原已确认包<br>打开M03详情进入S03全文，已读状态更新<br>重读同一条记录，无新增分/第二篇故事</td></tr>
<tr><td rowspan="1">熟悉与相伴需要应用</td><td rowspan="1">查询累计10XP，显示待更新熟悉，M08尚未解锁<br>应用熟悉包并核对成功，M08/S08出现<br>查询到30XP，待更新相伴，M09仍未解锁<br>应用相伴包成功，M09/S09出现<br>若直接提交≥30XP相伴包，可一次解锁M08和M09，不伪造中间运行</td></tr>
<tr><td rowspan="1">自定义动作与成长共存</td><td rowspan="1">初始模式保存作品并绑定头顶轻触<br>该输入100%执行用户序列，界面仍是初始模式<br>App首次启用成长后，绑定保留<br>真人再次触摸按事件1计成长；App预览不计<br>更新熟悉/相伴包后绑定仍在；取消绑定恢复当前阶段默认概率</td></tr>
<tr><td rowspan="1">故事失败和删除异常</td><td rowspan="1">里程碑达成时正文生成失败，保留唯一故事占位<br>重试同一实例，按冻结变量生成正文<br>删除绑定作品时先解绑<br>资源清理失败显示未绑定/待清理，不恢复旧绑定<br>重试清理成功后才释放作品槽位</td></tr></tbody>
</table>

[返回完整PRD目录](../README.md) · [上一章](./13-state-flows.md) · [下一章](./15-sources-gaps.md)
