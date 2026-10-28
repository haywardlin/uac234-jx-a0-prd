# 12 输入输出交互矩阵

[返回完整PRD目录](../README.md) · [上一章](./11-custom-actions.md) · [下一章](./13-state-flows.md)

保留原始事件名称、触发阈值、候选配对及资料差异。

<table>
<thead>
<tr><th>规则</th><th>说明</th><th>来源</th></tr></thead>
<tbody>
<tr><td rowspan="1">映射依据</td><td rowspan="1">设备功能说明附录指定以初始成长表为准；本矩阵保留该表逐行配对。另一输入事件表的候选与 Beta 标记单列，未取并集。</td><td rowspan="1">设备功能说明.md：322–324 行；两份 Excel</td></tr>
<tr><td rowspan="1">候选选择</td><td rowspan="1">每个事件随机选一套“动作＋伴音＋部分震动”；App 可整体替换规则表。初始表 38 个事件为两套各 50%；充电、低电、呼吸、关机为单套 100%。</td><td rowspan="1">设备功能说明.md：297 行；初始成长表</td></tr>
<tr><td rowspan="1">拦截与记录</td><td rowspan="1">暗状态、行为静默、充电、睡眠时段：事件不执行动作，也不写事件记录。暗状态例外为变暗事件；充电例外为充电和开机事件；另两项无例外。被拦截的触摸、姿态等仍重置 2 小时／48 小时计时。</td><td rowspan="1">设备功能说明.md：193–204 行</td></tr>
<tr><td rowspan="1">浅睡与待机</td><td rowspan="1">浅睡：触摸、拿起／晃动、唤醒词、遇到 Beany 可完全唤醒；光感、呼吸、2／48 小时、低电只短暂上电约 6 秒。待机所有互动和唤醒均不响应，蓝牙仍可查询设置。</td><td rowspan="1">设备功能说明.md：148–183 行</td></tr>
<tr><td rowspan="1">事件去重</td><td rowspan="1">同一个事件 0.5 秒内只响应一次。姿态事件触发后约 1 秒不识别触摸。</td><td rowspan="1">设备功能说明.md：298–299 行</td></tr>
<tr><td rowspan="1">播放中仲裁</td><td rowspan="1">系统＞交友＞姿态＞触摸＞光感。新事件更高则打断当前动作；相同或更低直接丢弃、不排队。一个动作在伴音播完时算结束，最长按 5 秒计。唤醒提示归入系统事件。</td><td rowspan="1">设备功能说明.md：283–293、300–304行</td></tr>
<tr><td rowspan="1">触摸仲裁</td><td rowspan="1">手势：握持＞长时间抚摸＞撸一撸＞碰一碰；同手势区域：头顶＞肚子＞头左／头右＞后背＞身体两侧。</td><td rowspan="1">设备功能说明.md：231 行</td></tr>
<tr><td rowspan="1">IMU 仲裁</td><td rowspan="1">10ms 采样；Idle→Active（最长约 2.5 秒）→Parse→Cooldown 200ms。同次只报一个手势：旋转上抛＞上抛＞猛摇＞翻转＞倾倒＞轻摇。拿起／放下独立互锁；未命中事件无随机兜底。</td><td rowspan="1">八个IMU事件触发标准.md：3–9 行</td></tr>
<tr><td rowspan="1">空白及删除线</td><td rowspan="1">“原表空白”“原表空字符串”和“/”保留区别，不改写成“无输出”或 ANY。暗事件两处震动值保留原始删除线状态。</td><td rowspan="1">初始成长表；输入事件表</td></tr></tbody>
</table>

下表是初始模式的42个事件、80套原始候选。原表空白与“/”原样保留供核对；初始执行按ANY处理，不做情绪筛选。成长阶段沿用同一事件ID和输入条件，输出与概率见第07节。默认18个Beta Y事件开放；Beta N及划除事件不因表中有定义而自动启用。

<details>
<summary>触摸 · 原始输入及初始输出</summary>

<table>
<thead>
<tr><th>输入类型</th><th>事件 ID／输入区域</th><th>事件（原名称）</th><th>触发条件与状态限制</th><th>候选／概率／筛选条件</th><th>动作输出</th><th>音频输出</th><th>震动输出</th><th>版本与启用差异</th></tr></thead>
<tbody>
<tr><td rowspan="44">触摸</td><td rowspan="2">01<br>摸头顶</td><td rowspan="2">Headtouch(摸头顶/下巴/鼻子/后脑勺)</td><td rowspan="2">按下不到 1 秒松开，松手时触发。浅睡被触摸唤醒后补播本次反应。</td><td rowspan="1">候选 1｜50%<br>情绪：ANY<br>状态：ANY</td><td rowspan="1">ID 14｜低头躲闪</td><td rowspan="1">ID 13｜head_psr_shy_01.wav</td><td rowspan="5">原表空白</td><td rowspan="1"><strong>【待补/待确认】 输入事件表：Beta=Y；候选动作=10/11/14。<br>与初始成长表候选不同，未合并。</strong></td></tr>
<tr><td rowspan="1"><strong>【待补/待确认】 候选 2｜50%<br>情绪：原表空白<br>状态：原表空白</strong></td><td rowspan="1">ID 18｜单次轻触缓慢抬头观察</td><td rowspan="2">ID 17｜synth_aww_01.wav</td><td rowspan="1"><strong>【待补/待确认】 输入事件表：Beta=Y；候选动作=10/11/14。<br>与初始成长表候选不同，未合并。<br>本候选情绪／状态空白或“/”按原表保留，继承规则未给出。</strong></td></tr>
<tr><td rowspan="2">02<br>摸头顶</td><td rowspan="2">Headtouch—quickstroke(摸头顶/下巴/鼻子/后脑勺-快速撸)</td><td rowspan="2">按住满 1 秒、不到 3 秒时松开，松手时触发。浅睡被触摸唤醒后补播本次反应。</td><td rowspan="1">候选 1｜50%<br>情绪：ANY<br>状态：ANY</td><td rowspan="1">ID 39｜单侧轻碰头顶躲闪</td><td rowspan="1"><strong>【待补/待确认】 输入事件表：Beta=N；候选动作=10/11/14。<br>与初始成长表候选不同，未合并。<br>保留该表 N 标记，不据候选表改成已支持。<br>触摸分型表写 1–3 秒／&gt;3 秒；设备说明明确 3 秒立即触发长摸。</strong></td></tr>
<tr><td rowspan="1"><strong>【待补/待确认】 候选 2｜50%<br>情绪：原表空白<br>状态：原表空白</strong></td><td rowspan="1">ID 12｜正式的点头（抬头低头）</td><td rowspan="1">ID 11｜nod_psr_agree_01.wav</td><td rowspan="1"><strong>【待补/待确认】 输入事件表：Beta=N；候选动作=10/11/14。<br>与初始成长表候选不同，未合并。<br>保留该表 N 标记，不据候选表改成已支持。<br>触摸分型表写 1–3 秒／&gt;3 秒；设备说明明确 3 秒立即触发长摸。<br>本候选情绪／状态空白或“/”按原表保留，继承规则未给出。</strong></td></tr>
<tr><td rowspan="2">03<br>摸头顶</td><td rowspan="2">Headtouch—sustained(摸头顶/下巴/鼻子/后脑勺-长时间抚摸)</td><td rowspan="2">按住满 3 秒立即触发，之后松手不再触发。浅睡被触摸唤醒后补播本次反应。</td><td rowspan="1">候选 1｜50%<br>情绪：ANY<br>状态：ANY</td><td rowspan="1">ID 11｜快速上下点头（快速撸通用开心）</td><td rowspan="1">ID 10｜stroke_psr_joy_01.wav</td><td rowspan="1"><strong>【待补/待确认】 输入事件表：Beta=N；候选动作=10/11/14。<br>与初始成长表候选不同，未合并。<br>保留该表 N 标记，不据候选表改成已支持。<br>触摸分型表写 1–3 秒／&gt;3 秒；设备说明明确 3 秒立即触发长摸。</strong></td></tr>
<tr><td rowspan="1"><strong>【待补/待确认】 候选 2｜50%<br>情绪：/<br>状态：/</strong></td><td rowspan="1">ID 13｜抬头后快速点头（很乐意）</td><td rowspan="1">ID 12｜nod_psr_agree_03.wav</td><td rowspan="1">/</td><td rowspan="1"><strong>【待补/待确认】 输入事件表：Beta=N；候选动作=10/11/14。<br>与初始成长表候选不同，未合并。<br>保留该表 N 标记，不据候选表改成已支持。<br>触摸分型表写 1–3 秒／&gt;3 秒；设备说明明确 3 秒立即触发长摸。<br>本候选情绪／状态空白或“/”按原表保留，继承规则未给出。</strong></td></tr>
<tr><td rowspan="2">04<br>头左</td><td rowspan="2">Headtouch(摸头左边)</td><td rowspan="2">按下不到 1 秒松开，松手时触发。浅睡被触摸唤醒后补播本次反应。</td><td rowspan="1">候选 1｜50%<br>情绪：ANY<br>状态：ANY</td><td rowspan="1">ID 35｜单侧轻碰侧低头躲闪（摸头左，高速）</td><td rowspan="1">ID 13｜head_psr_shy_01.wav</td><td rowspan="5">原表空白</td><td rowspan="1"><strong>【待补/待确认】 输入事件表：Beta=Y；候选动作=2/11/35/37/41/42。<br>与初始成长表候选不同，未合并。<br>初始动作名含高速／中速；动作详情对应 35、37 均写低速。</strong></td></tr>
<tr><td rowspan="1"><strong>【待补/待确认】 候选 2｜50%<br>情绪：原表空白<br>状态：原表空白</strong></td><td rowspan="1">ID 24｜连续多次轻碰渐进抬头</td><td rowspan="1">ID 6｜back_psr_comforting_02.wav</td><td rowspan="1"><strong>【待补/待确认】 输入事件表：Beta=Y；候选动作=2/11/35/37/41/42。<br>与初始成长表候选不同，未合并。<br>初始动作名含高速／中速；动作详情对应 35、37 均写低速。<br>本候选情绪／状态空白或“/”按原表保留，继承规则未给出。</strong></td></tr>
<tr><td rowspan="2">05<br>头左</td><td rowspan="2">Headtouch—quickstroke(摸头左边-快速撸)</td><td rowspan="2">按住满 1 秒、不到 3 秒时松开，松手时触发。浅睡被触摸唤醒后补播本次反应。</td><td rowspan="1">候选 1｜50%<br>情绪：ANY<br>状态：ANY</td><td rowspan="1">ID 37｜单侧轻碰侧低头躲闪（摸头左, 中速，颤动）</td><td rowspan="1">ID 30｜head_psr_shy_02.wav</td><td rowspan="1"><strong>【待补/待确认】 输入事件表：Beta=N；候选动作=2/11/35/37/41/42。<br>与初始成长表候选不同，未合并。<br>保留该表 N 标记，不据候选表改成已支持。<br>触摸分型表写 1–3 秒／&gt;3 秒；设备说明明确 3 秒立即触发长摸。<br>初始动作名含高速／中速；动作详情对应 35、37 均写低速。</strong></td></tr>
<tr><td rowspan="1"><strong>【待补/待确认】 候选 2｜50%<br>情绪：原表空白<br>状态：原表空白</strong></td><td rowspan="1">ID 25｜快速撸过度刺激躲闪</td><td rowspan="1">ID 22｜hold_psr_afraid_01.wav</td><td rowspan="1"><strong>【待补/待确认】 输入事件表：Beta=N；候选动作=2/11/35/37/41/42。<br>与初始成长表候选不同，未合并。<br>保留该表 N 标记，不据候选表改成已支持。<br>触摸分型表写 1–3 秒／&gt;3 秒；设备说明明确 3 秒立即触发长摸。<br>初始动作名含高速／中速；动作详情对应 35、37 均写低速。<br>本候选情绪／状态空白或“/”按原表保留，继承规则未给出。</strong></td></tr>
<tr><td rowspan="2">06<br>头左</td><td rowspan="2">Headtouch—sustained(摸头左边-长时间抚摸)</td><td rowspan="2">按住满 3 秒立即触发，之后松手不再触发。浅睡被触摸唤醒后补播本次反应。</td><td rowspan="1">候选 1｜50%<br>情绪：ANY<br>状态：ANY</td><td rowspan="1">ID 41｜单侧慢偏头依赖（摸头左专用）</td><td rowspan="1">ID 33｜hold_dlm_clingy_01.wav</td><td rowspan="1"><strong>【待补/待确认】 输入事件表：Beta=N；候选动作=2/11/35/37/41/42。<br>与初始成长表候选不同，未合并。<br>保留该表 N 标记，不据候选表改成已支持。<br>触摸分型表写 1–3 秒／&gt;3 秒；设备说明明确 3 秒立即触发长摸。</strong></td></tr>
<tr><td rowspan="1"><strong>【待补/待确认】 候选 2｜50%<br>情绪：/<br>状态：/</strong></td><td rowspan="1">ID 42｜单侧快速偏头蹭手（摸头左快速撸）</td><td rowspan="1">ID 34｜hold_dlm_clingy_02.wav</td><td rowspan="1">/</td><td rowspan="1"><strong>【待补/待确认】 输入事件表：Beta=N；候选动作=2/11/35/37/41/42。<br>与初始成长表候选不同，未合并。<br>保留该表 N 标记，不据候选表改成已支持。<br>触摸分型表写 1–3 秒／&gt;3 秒；设备说明明确 3 秒立即触发长摸。<br>本候选情绪／状态空白或“/”按原表保留，继承规则未给出。</strong></td></tr>
<tr><td rowspan="2">07<br>头右</td><td rowspan="2">Headtouch(摸头右边)</td><td rowspan="2">按下不到 1 秒松开，松手时触发。浅睡被触摸唤醒后补播本次反应。</td><td rowspan="1">候选 1｜50%<br>情绪：ANY<br>状态：ANY</td><td rowspan="1">ID 38｜单侧轻碰侧低头躲闪（摸头右）</td><td rowspan="1">ID 16｜nose_dlm_shy_01.wav</td><td rowspan="5">原表空白</td><td rowspan="1"><strong>【待补/待确认】 输入事件表：Beta=Y；候选动作=2/11/38/44/61。<br>与初始成长表候选不同，未合并。</strong></td></tr>
<tr><td rowspan="1"><strong>【待补/待确认】 候选 2｜50%<br>情绪：原表空白<br>状态：原表空白</strong></td><td rowspan="1">ID 29｜遇见同类双向晃头（陌生Beany）</td><td rowspan="1">ID 25｜synth_emotion_grateful_01.wav</td><td rowspan="1"><strong>【待补/待确认】 输入事件表：Beta=Y；候选动作=2/11/38/44/61。<br>与初始成长表候选不同，未合并。<br>本候选情绪／状态空白或“/”按原表保留，继承规则未给出。</strong></td></tr>
<tr><td rowspan="2">08<br>头右</td><td rowspan="2">Headtouch—quickstroke(摸头右边-快速撸)</td><td rowspan="2">按住满 1 秒、不到 3 秒时松开，松手时触发。浅睡被触摸唤醒后补播本次反应。</td><td rowspan="1">候选 1｜50%<br>情绪：ANY<br>状态：ANY</td><td rowspan="1">ID 44｜单侧慢偏头依赖（摸头右专用）</td><td rowspan="1">ID 35｜hold_dlm_clingy_03.wav</td><td rowspan="1"><strong>【待补/待确认】 输入事件表：Beta=N；候选动作=2/11/38/44/61。<br>与初始成长表候选不同，未合并。<br>保留该表 N 标记，不据候选表改成已支持。<br>触摸分型表写 1–3 秒／&gt;3 秒；设备说明明确 3 秒立即触发长摸。</strong></td></tr>
<tr><td rowspan="1"><strong>【待补/待确认】 候选 2｜50%<br>情绪：原表空白<br>状态：原表空白</strong></td><td rowspan="1">ID 54｜长时间握持间断打量</td><td rowspan="1">ID 41｜sideright_psr_checkin_02.wav</td><td rowspan="1"><strong>【待补/待确认】 输入事件表：Beta=N；候选动作=2/11/38/44/61。<br>与初始成长表候选不同，未合并。<br>保留该表 N 标记，不据候选表改成已支持。<br>触摸分型表写 1–3 秒／&gt;3 秒；设备说明明确 3 秒立即触发长摸。<br>本候选情绪／状态空白或“/”按原表保留，继承规则未给出。</strong></td></tr>
<tr><td rowspan="2">09<br>头右</td><td rowspan="2">Headtouch—sustained(摸头右边-长时间抚摸)</td><td rowspan="2">按住满 3 秒立即触发，之后松手不再触发。浅睡被触摸唤醒后补播本次反应。</td><td rowspan="1">候选 1｜50%<br>情绪：ANY<br>状态：ANY</td><td rowspan="1">ID 61｜单侧快速偏头蹭手（摸头右快速撸）</td><td rowspan="1">ID 35｜hold_dlm_clingy_03.wav</td><td rowspan="1"><strong>【待补/待确认】 输入事件表：Beta=N；候选动作=2/11/38/44/61。<br>与初始成长表候选不同，未合并。<br>保留该表 N 标记，不据候选表改成已支持。<br>触摸分型表写 1–3 秒／&gt;3 秒；设备说明明确 3 秒立即触发长摸。</strong></td></tr>
<tr><td rowspan="1"><strong>【待补/待确认】 候选 2｜50%<br>情绪：/<br>状态：/</strong></td><td rowspan="1">ID 56｜暗光间断抬头观察</td><td rowspan="1">ID 43｜backhead_dlm_uneasy_01.wav</td><td rowspan="1">/</td><td rowspan="1"><strong>【待补/待确认】 输入事件表：Beta=N；候选动作=2/11/38/44/61。<br>与初始成长表候选不同，未合并。<br>保留该表 N 标记，不据候选表改成已支持。<br>触摸分型表写 1–3 秒／&gt;3 秒；设备说明明确 3 秒立即触发长摸。<br>本候选情绪／状态空白或“/”按原表保留，继承规则未给出。</strong></td></tr>
<tr><td rowspan="2">10<br>摸肚子</td><td rowspan="2">Bellytouch—tap(摸肚子-碰一碰)</td><td rowspan="2">按下不到 1 秒松开，松手时触发。浅睡被触摸唤醒后补播本次反应。</td><td rowspan="1">候选 1｜50%<br>情绪：ANY<br>状态：ANY</td><td rowspan="1">ID 5｜强行翻肚皮垂头</td><td rowspan="1">ID 5｜flip_psr_protest_01.wav</td><td rowspan="1">1｜弱震动</td><td rowspan="1"><strong>【待补/待确认】 输入事件表：Beta=Y；候选动作=2/10/11/20/27。<br>与初始成长表候选不同，未合并。</strong></td></tr>
<tr><td rowspan="1"><strong>【待补/待确认】 候选 2｜50%<br>情绪：原表空白<br>状态：原表空白</strong></td><td rowspan="1">ID 15｜高强度快速撸后垂头</td><td rowspan="1">ID 14｜flip_psr_protest_02.wav</td><td rowspan="1">原表空白</td><td rowspan="1"><strong>【待补/待确认】 输入事件表：Beta=Y；候选动作=2/10/11/20/27。<br>与初始成长表候选不同，未合并。<br>本候选情绪／状态空白或“/”按原表保留，继承规则未给出。</strong></td></tr>
<tr><td rowspan="2">11<br>摸肚子</td><td rowspan="2">Bellytouch—quickstroke(摸肚子-快速撸)</td><td rowspan="2">按住满 1 秒、不到 3 秒时松开，松手时触发。浅睡被触摸唤醒后补播本次反应。</td><td rowspan="1">候选 1｜50%<br>情绪：ANY<br>状态：ANY</td><td rowspan="1">ID 22｜翻转肚皮静态垂头</td><td rowspan="1">ID 20｜belly_bps_full_trust_02.wav</td><td rowspan="1">3｜强震动</td><td rowspan="1"><strong>【待补/待确认】 输入事件表：Beta=N；候选动作=2/10/11/20/27。<br>与初始成长表候选不同，未合并。<br>保留该表 N 标记，不据候选表改成已支持。<br>触摸分型表写 1–3 秒／&gt;3 秒；设备说明明确 3 秒立即触发长摸。</strong></td></tr>
<tr><td rowspan="1"><strong>【待补/待确认】 候选 2｜50%<br>情绪：原表空白<br>状态：原表空白</strong></td><td rowspan="1">ID 27｜肚皮触碰轻快垂点头（肚子快速撸）</td><td rowspan="1">ID 24｜social_psr_ecstatic_01.wav</td><td rowspan="2">原表空白</td><td rowspan="1"><strong>【待补/待确认】 输入事件表：Beta=N；候选动作=2/10/11/20/27。<br>与初始成长表候选不同，未合并。<br>保留该表 N 标记，不据候选表改成已支持。<br>触摸分型表写 1–3 秒／&gt;3 秒；设备说明明确 3 秒立即触发长摸。<br>本候选情绪／状态空白或“/”按原表保留，继承规则未给出。</strong></td></tr>
<tr><td rowspan="2">12<br>摸肚子</td><td rowspan="2">Bellytouch—sustained(摸肚子-长时间抚摸)</td><td rowspan="2">按住满 3 秒立即触发，之后松手不再触发。浅睡被触摸唤醒后补播本次反应。</td><td rowspan="1">候选 1｜50%<br>情绪：ANY<br>状态：ANY</td><td rowspan="1">ID 20｜肚子轻垂头软动（摸肚子专属）</td><td rowspan="1">ID 19｜belly_bps_full_trust_01.wav</td><td rowspan="1"><strong>【待补/待确认】 输入事件表：Beta=N；候选动作=2/10/11/20/27。<br>与初始成长表候选不同，未合并。<br>保留该表 N 标记，不据候选表改成已支持。<br>触摸分型表写 1–3 秒／&gt;3 秒；设备说明明确 3 秒立即触发长摸。</strong></td></tr>
<tr><td rowspan="1"><strong>【待补/待确认】 候选 2｜50%<br>情绪：/<br>状态：/</strong></td><td rowspan="1">ID 10｜上下微颤点头（满足惬意）</td><td rowspan="1">ID 9｜belly_psr_full_trust_01.wav</td><td rowspan="1">/</td><td rowspan="1"><strong>【待补/待确认】 输入事件表：Beta=N；候选动作=2/10/11/20/27。<br>与初始成长表候选不同，未合并。<br>保留该表 N 标记，不据候选表改成已支持。<br>触摸分型表写 1–3 秒／&gt;3 秒；设备说明明确 3 秒立即触发长摸。<br>本候选情绪／状态空白或“/”按原表保留，继承规则未给出。</strong></td></tr>
<tr><td rowspan="2">13<br>左侧面</td><td rowspan="2">Sidetouch—tap(摸左侧面-碰一碰)</td><td rowspan="2">按下不到 1 秒松开，松手时触发。浅睡被触摸唤醒后补播本次反应。</td><td rowspan="1">候选 1｜50%<br>情绪：ANY<br>状态：ANY</td><td rowspan="1">ID 43｜定点单侧观望（左）</td><td rowspan="1">ID 8｜headright_psr_alert_right_01.wav</td><td rowspan="5">原表空白</td><td rowspan="1"><strong>【待补/待确认】 输入事件表：Beta=Y；候选动作=2/11。<br>与初始成长表候选不同，未合并。</strong></td></tr>
<tr><td rowspan="1"><strong>【待补/待确认】 候选 2｜50%<br>情绪：原表空白<br>状态：原表空白</strong></td><td rowspan="1">ID 45｜定点单侧观望（右）</td><td rowspan="2">ID 2｜back_psr_comforting_01.wav</td><td rowspan="1"><strong>【待补/待确认】 输入事件表：Beta=Y；候选动作=2/11。<br>与初始成长表候选不同，未合并。<br>本候选情绪／状态空白或“/”按原表保留，继承规则未给出。</strong></td></tr>
<tr><td rowspan="2">14<br>左侧面</td><td rowspan="2">Sidetouch—quickstroke(摸左侧面-快速撸)</td><td rowspan="2">按住满 1 秒、不到 3 秒时松开，松手时触发。浅睡被触摸唤醒后补播本次反应。</td><td rowspan="1">候选 1｜50%<br>情绪：ANY<br>状态：ANY</td><td rowspan="1">ID 2｜轻抬慢回（温顺舒缓）</td><td rowspan="1"><strong>【待补/待确认】 输入事件表：Beta=N；候选动作=2/11。<br>与初始成长表候选不同，未合并。<br>保留该表 N 标记，不据候选表改成已支持。<br>触摸分型表写 1–3 秒／&gt;3 秒；设备说明明确 3 秒立即触发长摸。</strong></td></tr>
<tr><td rowspan="1"><strong>【待补/待确认】 候选 2｜50%<br>情绪：原表空白<br>状态：原表空白</strong></td><td rowspan="1">ID 12｜正式的点头（抬头低头）</td><td rowspan="1">ID 11｜nod_psr_agree_01.wav</td><td rowspan="1"><strong>【待补/待确认】 输入事件表：Beta=N；候选动作=2/11。<br>与初始成长表候选不同，未合并。<br>保留该表 N 标记，不据候选表改成已支持。<br>触摸分型表写 1–3 秒／&gt;3 秒；设备说明明确 3 秒立即触发长摸。<br>本候选情绪／状态空白或“/”按原表保留，继承规则未给出。</strong></td></tr>
<tr><td rowspan="2">15<br>左侧面</td><td rowspan="2">Sidetouch—sustained(摸左侧面-长时间抚摸)</td><td rowspan="2">按住满 3 秒立即触发，之后松手不再触发。浅睡被触摸唤醒后补播本次反应。</td><td rowspan="1">候选 1｜50%<br>情绪：ANY<br>状态：ANY</td><td rowspan="1">ID 11｜快速上下点头（快速撸通用开心）</td><td rowspan="1">ID 10｜stroke_psr_joy_01.wav</td><td rowspan="1"><strong>【待补/待确认】 输入事件表：Beta=N；候选动作=2/11。<br>与初始成长表候选不同，未合并。<br>保留该表 N 标记，不据候选表改成已支持。<br>触摸分型表写 1–3 秒／&gt;3 秒；设备说明明确 3 秒立即触发长摸。</strong></td></tr>
<tr><td rowspan="1"><strong>【待补/待确认】 候选 2｜50%<br>情绪：/<br>状态：/</strong></td><td rowspan="1">ID 30｜唤醒急促小颤头（唤醒词）</td><td rowspan="1">ID 26｜wakeup_psr_playful_01.wav</td><td rowspan="1">/</td><td rowspan="1"><strong>【待补/待确认】 输入事件表：Beta=N；候选动作=2/11。<br>与初始成长表候选不同，未合并。<br>保留该表 N 标记，不据候选表改成已支持。<br>触摸分型表写 1–3 秒／&gt;3 秒；设备说明明确 3 秒立即触发长摸。<br>本候选情绪／状态空白或“/”按原表保留，继承规则未给出。</strong></td></tr>
<tr><td rowspan="2">16<br>右侧面</td><td rowspan="2">Sidetouch—tap(摸右侧面-碰一碰)</td><td rowspan="2">按下不到 1 秒松开，松手时触发。浅睡被触摸唤醒后补播本次反应。</td><td rowspan="1">候选 1｜50%<br>情绪：ANY<br>状态：ANY</td><td rowspan="1">ID 45｜定点单侧观望（右）</td><td rowspan="1">ID 2｜back_psr_comforting_01.wav</td><td rowspan="5">原表空白</td><td rowspan="1"><strong>【待补/待确认】 输入事件表：Beta=Y；候选动作=2/11。<br>与初始成长表候选不同，未合并。</strong></td></tr>
<tr><td rowspan="1"><strong>【待补/待确认】 候选 2｜50%<br>情绪：原表空白<br>状态：原表空白</strong></td><td rowspan="1">ID 43｜定点单侧观望（左）</td><td rowspan="1">ID 8｜headright_psr_alert_right_01.wav</td><td rowspan="1"><strong>【待补/待确认】 输入事件表：Beta=Y；候选动作=2/11。<br>与初始成长表候选不同，未合并。<br>本候选情绪／状态空白或“/”按原表保留，继承规则未给出。</strong></td></tr>
<tr><td rowspan="2">17<br>右侧面</td><td rowspan="2">Sidetouch—quickstroke(摸右侧面-快速撸)</td><td rowspan="2">按住满 1 秒、不到 3 秒时松开，松手时触发。浅睡被触摸唤醒后补播本次反应。</td><td rowspan="1">候选 1｜50%<br>情绪：ANY<br>状态：ANY</td><td rowspan="1">ID 2｜轻抬慢回（温顺舒缓）</td><td rowspan="1">ID 2｜back_psr_comforting_01.wav</td><td rowspan="1"><strong>【待补/待确认】 输入事件表：Beta=N；候选动作=2/11。<br>与初始成长表候选不同，未合并。<br>保留该表 N 标记，不据候选表改成已支持。<br>触摸分型表写 1–3 秒／&gt;3 秒；设备说明明确 3 秒立即触发长摸。</strong></td></tr>
<tr><td rowspan="1"><strong>【待补/待确认】 候选 2｜50%<br>情绪：原表空白<br>状态：原表空白</strong></td><td rowspan="1">ID 6｜瞌睡</td><td rowspan="1">ID 3｜idle_dlm_lonely_01.wav</td><td rowspan="1"><strong>【待补/待确认】 输入事件表：Beta=N；候选动作=2/11。<br>与初始成长表候选不同，未合并。<br>保留该表 N 标记，不据候选表改成已支持。<br>触摸分型表写 1–3 秒／&gt;3 秒；设备说明明确 3 秒立即触发长摸。<br>本候选情绪／状态空白或“/”按原表保留，继承规则未给出。</strong></td></tr>
<tr><td rowspan="2">18<br>右侧面</td><td rowspan="2">Sidetouch—sustained(摸右侧面-长时间抚摸)</td><td rowspan="2">按住满 3 秒立即触发，之后松手不再触发。浅睡被触摸唤醒后补播本次反应。</td><td rowspan="1">候选 1｜50%<br>情绪：ANY<br>状态：ANY</td><td rowspan="1">ID 11｜快速上下点头（快速撸通用开心）</td><td rowspan="1">ID 10｜stroke_psr_joy_01.wav</td><td rowspan="1"><strong>【待补/待确认】 输入事件表：Beta=N；候选动作=2/11。<br>与初始成长表候选不同，未合并。<br>保留该表 N 标记，不据候选表改成已支持。<br>触摸分型表写 1–3 秒／&gt;3 秒；设备说明明确 3 秒立即触发长摸。</strong></td></tr>
<tr><td rowspan="1"><strong>【待补/待确认】 候选 2｜50%<br>情绪：/<br>状态：/</strong></td><td rowspan="1">ID 50｜间断定点侧头试探</td><td rowspan="1">ID 23｜synth_bps_soft_greeting_01.wav</td><td rowspan="1">/</td><td rowspan="1"><strong>【待补/待确认】 输入事件表：Beta=N；候选动作=2/11。<br>与初始成长表候选不同，未合并。<br>保留该表 N 标记，不据候选表改成已支持。<br>触摸分型表写 1–3 秒／&gt;3 秒；设备说明明确 3 秒立即触发长摸。<br>本候选情绪／状态空白或“/”按原表保留，继承规则未给出。</strong></td></tr>
<tr><td rowspan="2">19<br>摸后背</td><td rowspan="2">Backtouch—tap(摸后背-碰一碰)</td><td rowspan="2">按下不到 1 秒松开，松手时触发。浅睡被触摸唤醒后补播本次反应。</td><td rowspan="1">候选 1｜50%<br>情绪：ANY<br>状态：ANY</td><td rowspan="1">ID 16｜突发触碰单次躲闪</td><td rowspan="1">ID 31｜synth_oops_recovery_01.wav</td><td rowspan="8">原表空白</td><td rowspan="1"><strong>【待补/待确认】 输入事件表：Beta=Y；候选动作=2/7/10/11。<br>与初始成长表候选不同，未合并。</strong></td></tr>
<tr><td rowspan="1"><strong>【待补/待确认】 候选 2｜50%<br>情绪：原表空白<br>状态：原表空白</strong></td><td rowspan="1">ID 18｜单次轻触缓慢抬头观察</td><td rowspan="1">ID 17｜synth_aww_01.wav</td><td rowspan="1"><strong>【待补/待确认】 输入事件表：Beta=Y；候选动作=2/7/10/11。<br>与初始成长表候选不同，未合并。<br>本候选情绪／状态空白或“/”按原表保留，继承规则未给出。</strong></td></tr>
<tr><td rowspan="2">20<br>摸后背</td><td rowspan="2">Backtouch—quickstroke(摸后背-快速撸)</td><td rowspan="2">按住满 1 秒、不到 3 秒时松开，松手时触发。浅睡被触摸唤醒后补播本次反应。</td><td rowspan="1">候选 1｜50%<br>情绪：ANY<br>状态：ANY</td><td rowspan="1">ID 2｜轻抬慢回（温顺舒缓）</td><td rowspan="1">ID 2｜back_psr_comforting_01.wav</td><td rowspan="1"><strong>【待补/待确认】 输入事件表：Beta=N；候选动作=2/7/10/11。<br>与初始成长表候选不同，未合并。<br>保留该表 N 标记，不据候选表改成已支持。<br>触摸分型表写 1–3 秒／&gt;3 秒；设备说明明确 3 秒立即触发长摸。</strong></td></tr>
<tr><td rowspan="1"><strong>【待补/待确认】 候选 2｜50%<br>情绪：原表空白<br>状态：原表空白</strong></td><td rowspan="1">ID 12｜正式的点头（抬头低头）</td><td rowspan="1">ID 11｜nod_psr_agree_01.wav</td><td rowspan="1"><strong>【待补/待确认】 输入事件表：Beta=N；候选动作=2/7/10/11。<br>与初始成长表候选不同，未合并。<br>保留该表 N 标记，不据候选表改成已支持。<br>触摸分型表写 1–3 秒／&gt;3 秒；设备说明明确 3 秒立即触发长摸。<br>本候选情绪／状态空白或“/”按原表保留，继承规则未给出。</strong></td></tr>
<tr><td rowspan="2">21<br>摸后背</td><td rowspan="2">Backtouch—sustained(摸后背-长时间抚摸)</td><td rowspan="2">按住满 3 秒立即触发，之后松手不再触发。浅睡被触摸唤醒后补播本次反应。</td><td rowspan="1">候选 1｜50%<br>情绪：ANY<br>状态：ANY</td><td rowspan="1">ID 7｜摸后背匀速快点头（摸后背专属）</td><td rowspan="1">ID 6｜back_psr_comforting_02.wav</td><td rowspan="1"><strong>【待补/待确认】 输入事件表：Beta=N；候选动作=2/7/10/11。<br>与初始成长表候选不同，未合并。<br>保留该表 N 标记，不据候选表改成已支持。<br>触摸分型表写 1–3 秒／&gt;3 秒；设备说明明确 3 秒立即触发长摸。</strong></td></tr>
<tr><td rowspan="1"><strong>【待补/待确认】 候选 2｜50%<br>情绪：原表空白<br>状态：原表空白</strong></td><td rowspan="1">ID 13｜抬头后快速点头（很乐意）</td><td rowspan="1">ID 12｜nod_psr_agree_03.wav</td><td rowspan="1"><strong>【待补/待确认】 输入事件表：Beta=N；候选动作=2/7/10/11。<br>与初始成长表候选不同，未合并。<br>保留该表 N 标记，不据候选表改成已支持。<br>触摸分型表写 1–3 秒／&gt;3 秒；设备说明明确 3 秒立即触发长摸。<br>本候选情绪／状态空白或“/”按原表保留，继承规则未给出。</strong></td></tr>
<tr><td rowspan="2">22<br>长时间握持</td><td rowspan="2">Sustainedhold(长时间握持&lt;10S, 5 秒以上)</td><td rowspan="2">肚子＋背部任意两个区域，同时按住满 5 秒，松手触发。组合范围保留原文。</td><td rowspan="1">候选 1｜50%<br>情绪：ANY<br>状态：ANY</td><td rowspan="1">ID 46｜短时握持间断晃头（Sustainedhold）</td><td rowspan="1">ID 33｜hold_dlm_clingy_01.wav</td><td rowspan="1"><strong>【待补/待确认】 输入事件表：Beta=N；候选动作=31/46/52/54。<br>与初始成长表候选不同，未合并。<br>保留该表 N 标记，不据候选表改成已支持。<br>输入事件名写“&lt;10S, 5 秒以上”；设备说明未列 10 秒上限，区域组合与长摸冲突未说明。</strong></td></tr>
<tr><td rowspan="1"><strong>【待补/待确认】 候选 2｜50%<br>情绪：原表空白<br>状态：原表空白</strong></td><td rowspan="1">ID 52｜长时间握持静靠（Sustainedhold）</td><td rowspan="1">ID 35｜hold_dlm_clingy_03.wav</td><td rowspan="1"><strong>【待补/待确认】 输入事件表：Beta=N；候选动作=31/46/52/54。<br>与初始成长表候选不同，未合并。<br>保留该表 N 标记，不据候选表改成已支持。<br>输入事件名写“&lt;10S, 5 秒以上”；设备说明未列 10 秒上限，区域组合与长摸冲突未说明。<br>本候选情绪／状态空白或“/”按原表保留，继承规则未给出。</strong></td></tr></tbody>
</table>

</details>

<details>
<summary>IMU · 原始输入及初始输出</summary>

<table>
<thead>
<tr><th>输入类型</th><th>事件 ID／输入区域</th><th>事件（原名称）</th><th>触发条件与状态限制</th><th>候选／概率／筛选条件</th><th>动作输出</th><th>音频输出</th><th>震动输出</th><th>版本与启用差异</th></tr></thead>
<tbody>
<tr><td rowspan="16">IMU</td><td rowspan="2">23<br>轻摇</td><td rowspan="2">轻摇</td><td rowspan="2">约 2 秒内轻柔往复至少 2 次，有效半周均≥300ms；陀螺或加速度能量达到轻摇地板。停稳后响应；同段构成上抛或合格倾倒不报轻摇。</td><td rowspan="1">候选 1｜50%<br>情绪：ANY<br>状态：ANY</td><td rowspan="1">ID 49｜轻摇缓慢环视</td><td rowspan="1">ID 37｜tilt_psr_anxious_02.wav</td><td rowspan="16">原表空白</td><td rowspan="1"><strong>【待补/待确认】 输入事件表：Beta=N；候选动作=6/28/49。<br>与初始成长表候选不同，未合并。<br>保留该表 N 标记，不据候选表改成已支持。</strong></td></tr>
<tr><td rowspan="1"><strong>【待补/待确认】 候选 2｜50%<br>情绪：原表空白<br>状态：原表空白</strong></td><td rowspan="1">ID 28｜轻摇小幅快点头（Gentleshake）</td><td rowspan="1">ID 18｜wakeup_psr_playful_02.wav</td><td rowspan="1"><strong>【待补/待确认】 输入事件表：Beta=N；候选动作=6/28/49。<br>与初始成长表候选不同，未合并。<br>保留该表 N 标记，不据候选表改成已支持。<br>本候选情绪／状态空白或“/”按原表保留，继承规则未给出。</strong></td></tr>
<tr><td rowspan="2">24<br>猛摇</td><td rowspan="2">猛摇</td><td rowspan="2">手持快速剧烈往复至少 2 次；不要求半周时长，主要看能量。停稳后响应；同段已构成上抛链不报猛摇。</td><td rowspan="1">候选 1｜50%<br>情绪：ANY<br>状态：ANY</td><td rowspan="1">ID 31｜粗暴握持高频躲闪颤</td><td rowspan="1">ID 22｜hold_psr_afraid_01.wav</td><td rowspan="1"><strong>【待补/待确认】 输入事件表：Beta=N；候选动作=原表空字符串。<br>与初始成长表候选不同，未合并。<br>保留该表 N 标记，不据候选表改成已支持。</strong></td></tr>
<tr><td rowspan="1"><strong>【待补/待确认】 候选 2｜50%<br>情绪：原表空白<br>状态：原表空白</strong></td><td rowspan="1">ID 26｜强光急促低头躲闪</td><td rowspan="1">ID 23｜synth_bps_soft_greeting_01.wav</td><td rowspan="1"><strong>【待补/待确认】 输入事件表：Beta=N；候选动作=原表空字符串。<br>与初始成长表候选不同，未合并。<br>保留该表 N 标记，不据候选表改成已支持。<br>本候选情绪／状态空白或“/”按原表保留，继承规则未给出。</strong></td></tr>
<tr><td rowspan="2">25<br>翻转</td><td rowspan="2">翻转</td><td rowspan="2">先处于俯仰或横滚约 55°～125°侧躺带约 300ms，再绕竖直轴转约 150°以上；陀螺峰值≥约 50°/s。上抛链不报翻转；判成翻转后禁止倾倒。</td><td rowspan="1">候选 1｜50%<br>情绪：ANY<br>状态：ANY</td><td rowspan="1">ID 5｜强行翻肚皮垂头</td><td rowspan="1">ID 5｜flip_psr_protest_01.wav</td><td rowspan="1"><strong>【待补/待确认】 输入事件表：Beta=N；候选动作=5/47。<br>保留该表 N 标记，不据候选表改成已支持。<br>功能说明写“让肚皮朝上”；IMU 标准写“原朝上一面变朝下”，姿态口径待核对。</strong></td></tr>
<tr><td rowspan="1"><strong>【待补/待确认】 候选 2｜50%<br>情绪：原表空白<br>状态：原表空白</strong></td><td rowspan="1">ID 47｜翻转肚皮上扬晃头（Flipbelly-up）</td><td rowspan="1">ID 9｜belly_psr_full_trust_01.wav</td><td rowspan="1"><strong>【待补/待确认】 输入事件表：Beta=N；候选动作=5/47。<br>保留该表 N 标记，不据候选表改成已支持。<br>功能说明写“让肚皮朝上”；IMU 标准写“原朝上一面变朝下”，姿态口径待核对。<br>本候选情绪／状态空白或“/”按原表保留，继承规则未给出。</strong></td></tr>
<tr><td rowspan="2">26<br>原表空白</td><td rowspan="2">Pickedup(被拿起)</td><td rowspan="2">仅在“桌上”可报：有触摸（约 800ms 有效；浅睡 IMU 唤醒后约 3 秒可豁免）＋陀螺合速度≥45°/s 或合加速度偏离 1g≥0.25g，累计约 300ms，允许约 120ms 断帧。拿起／放下互锁。</td><td rowspan="1">候选 1｜50%<br>情绪：ANY<br>状态：ANY</td><td rowspan="1">ID 60｜被拿起上扬连续点头（Pickedup）</td><td rowspan="1">ID 34｜hold_dlm_clingy_02.wav</td><td rowspan="1"><strong>【待补/待确认】 输入事件表：Beta=N；候选动作=原表空白。<br>与初始成长表候选不同，未合并。<br>保留该表 N 标记，不据候选表改成已支持。<br>该表事件名称有删除线；功能说明／IMU 标准仍描述该事件。</strong></td></tr>
<tr><td rowspan="1"><strong>【待补/待确认】 候选 2｜50%<br>情绪：原表空白<br>状态：原表空白</strong></td><td rowspan="1">ID 9｜上下缓慢抬升打量</td><td rowspan="1">ID 8｜headright_psr_alert_right_01.wav</td><td rowspan="1"><strong>【待补/待确认】 输入事件表：Beta=N；候选动作=原表空白。<br>与初始成长表候选不同，未合并。<br>保留该表 N 标记，不据候选表改成已支持。<br>该表事件名称有删除线；功能说明／IMU 标准仍描述该事件。<br>本候选情绪／状态空白或“/”按原表保留，继承规则未给出。</strong></td></tr>
<tr><td rowspan="2">27<br>原表空白</td><td rowspan="2">Putdown(被放下)</td><td rowspan="2">仅在“手上”可报：坐姿（俯仰约 0°、横滚贴近±180°），陀螺&lt;35°/s、合加速度偏离 1g&lt;0.35g，最近约 800ms 无触摸，稳住约 2 秒。小晃／触摸毛刺暂停计时；明显离开坐姿或陀螺≥80°/s 清零。</td><td rowspan="1">候选 1｜50%<br>情绪：ANY<br>状态：ANY</td><td rowspan="1">ID 3｜放下后长期垂头</td><td rowspan="1">ID 3｜idle_dlm_lonely_01.wav</td><td rowspan="1"><strong>【待补/待确认】 输入事件表：Beta=N；候选动作=原表空白。<br>与初始成长表候选不同，未合并。<br>保留该表 N 标记，不据候选表改成已支持。<br>该表事件名称有删除线；功能说明／IMU 标准仍描述该事件。</strong></td></tr>
<tr><td rowspan="1"><strong>【待补/待确认】 候选 2｜50%<br>情绪：原表空白<br>状态：原表空白</strong></td><td rowspan="1">ID 50｜间断定点侧头试探</td><td rowspan="1">ID 23｜synth_bps_soft_greeting_01.wav</td><td rowspan="1"><strong>【待补/待确认】 输入事件表：Beta=N；候选动作=原表空白。<br>与初始成长表候选不同，未合并。<br>保留该表 N 标记，不据候选表改成已支持。<br>该表事件名称有删除线；功能说明／IMU 标准仍描述该事件。<br>本候选情绪／状态空白或“/”按原表保留，继承规则未给出。</strong></td></tr>
<tr><td rowspan="2">35<br>侧倒</td><td rowspan="2">侧倒</td><td rowspan="2">先正立且低角速度约 200ms，再推向前／后／左／右侧躺带约 55°～125°并静稳约 300ms。姿态变化至少约 30°；偏航峰峰值≤约 50°、偏航角速度&lt;约 120°/s，过程角速度约 55～750°/s。上抛、失重、翻转倾斜不报。</td><td rowspan="1">候选 1｜50%<br>情绪：ANY<br>状态：ANY</td><td rowspan="1">ID 36｜侧倒低头向内躲闪</td><td rowspan="1">ID 29｜sidefall_psr_guard_01.wav</td><td rowspan="1"><strong>【待补/待确认】 输入事件表：Beta=Y；候选动作=36。<br>与初始成长表候选不同，未合并。</strong></td></tr>
<tr><td rowspan="1"><strong>【待补/待确认】 候选 2｜50%<br>情绪：原表空白<br>状态：原表空白</strong></td><td rowspan="1">ID 40｜侧倒低头向内躲闪</td><td rowspan="1">ID 32｜sidefall_psr_guard_02.wav</td><td rowspan="1"><strong>【待补/待确认】 输入事件表：Beta=Y；候选动作=36。<br>与初始成长表候选不同，未合并。<br>本候选情绪／状态空白或“/”按原表保留，继承规则未给出。</strong></td></tr>
<tr><td rowspan="2">40<br>抛起</td><td rowspan="2">抛起</td><td rowspan="2">出手加速度≥约 1.5g→失重&lt;约 0.4g（约 150ms，短谷可约 70ms）→硬冲击约 1.8g／软接约 1.5g→约 80ms 无二次失重；空中体轴转角&lt;约 300°。落地或接住后报告。软链谷至冲击&gt;约 800ms 不认。</td><td rowspan="1">候选 1｜50%<br>情绪：ANY<br>状态：ANY</td><td rowspan="1">ID 32｜旋转抛起极速环绕头（旋转抛）</td><td rowspan="1">ID 27｜tossup_psr_frightened_01.wav</td><td rowspan="2"><strong>【待补/待确认】 输入事件表：Beta=Y；候选动作=32/58。<br>与初始成长表候选不同，未合并。</strong></td></tr>
<tr><td rowspan="1">候选 2｜50%<br>情绪：ANY<br>状态：ANY</td><td rowspan="1">ID 29｜遇见同类双向晃头（陌生Beany）</td><td rowspan="1">ID 25｜synth_emotion_grateful_01.wav</td></tr>
<tr><td rowspan="2">41<br>旋转抛起</td><td rowspan="2">旋转抛起</td><td rowspan="2">满足上抛同一空中链，空中绕体轴转过约 300°及以上（约 5/6 圈，两圈以上仍为本事件）。头尾翻滚／上下颠倒允许；起飞与落地姿态不限，落地确认后可提前收段。</td><td rowspan="1">候选 1｜50%<br>情绪：ANY<br>状态：ANY</td><td rowspan="1">ID 58｜抛起上扬晃头（抛起事件）</td><td rowspan="1">ID 27｜tossup_psr_frightened_01.wav</td><td rowspan="2"><strong>【待补/待确认】 输入事件表：Beta=N；候选动作=32。<br>与初始成长表候选不同，未合并。<br>保留该表 N 标记，不据候选表改成已支持。<br>该表事件名称有删除线；功能说明／IMU 标准仍描述该事件。</strong></td></tr>
<tr><td rowspan="1">候选 2｜50%<br>情绪：ANY<br>状态：ANY</td><td rowspan="1">ID 59｜左右快速摆头好奇（强光/唤醒）</td><td rowspan="1">ID 44｜wakeup_psr_playful_03.wav</td></tr></tbody>
</table>

</details>

<details>
<summary>语音唤醒 · 原始输入及初始输出</summary>

<table>
<thead>
<tr><th>输入类型</th><th>事件 ID／输入区域</th><th>事件（原名称）</th><th>触发条件与状态限制</th><th>候选／概率／筛选条件</th><th>动作输出</th><th>音频输出</th><th>震动输出</th><th>版本与启用差异</th></tr></thead>
<tbody>
<tr><td rowspan="2">语音唤醒</td><td rowspan="2">28<br>唤醒提示词</td><td rowspan="2">唤醒提示词</td><td rowspan="2">离线识别“Hello Beany”，播放唤醒提示；浅睡完全唤醒。待机无效；暗、充电、“静音”、睡眠时段内不出动作。</td><td rowspan="1">候选 1｜50%<br>情绪：ANY<br>状态：ANY</td><td rowspan="1">ID 59｜左右快速摆头好奇（强光/唤醒）</td><td rowspan="1">ID 44｜wakeup_psr_playful_03.wav</td><td rowspan="2">原表空白</td><td rowspan="2"><strong>【待补/待确认】 输入事件表：Beta=Y；候选动作=9/13/30/57/59。<br>与初始成长表候选不同，未合并。</strong></td></tr>
<tr><td rowspan="1">候选 2｜50%<br>情绪：ANY<br>状态：ANY</td><td rowspan="1">ID 13｜抬头后快速点头（很乐意）</td><td rowspan="1">ID 12｜nod_psr_agree_03.wav</td></tr></tbody>
</table>

</details>

<details>
<summary>光感 · 原始输入及初始输出</summary>

<table>
<thead>
<tr><th>输入类型</th><th>事件 ID／输入区域</th><th>事件（原名称）</th><th>触发条件与状态限制</th><th>候选／概率／筛选条件</th><th>动作输出</th><th>音频输出</th><th>震动输出</th><th>版本与启用差异</th></tr></thead>
<tbody>
<tr><td rowspan="4">光感</td><td rowspan="2">29<br>变暗</td><td rowspan="2">光线变暗</td><td rowspan="2">光感原始值&lt;10 持续约 2.5 秒，触发变暗并进入暗状态；值&gt;950 解除暗状态，解除本身不触发事件。开机／退出待机后约 8 秒不触发光线事件。浅睡短暂唤醒约 6 秒。</td><td rowspan="1">候选 1｜50%<br>情绪：ANY<br>状态：ANY</td><td rowspan="1">ID 23｜暗光低头慢挪</td><td rowspan="1">ID 21｜lightdown_dlm_dreamy_02.wav</td><td rowspan="1"><strong>【待补/待确认】 1｜弱震动（原值已加删除线，不作为有效配置）</strong></td><td rowspan="2"><strong>【待补/待确认】 输入事件表：Beta=Y；候选动作=23/50/55/56/57。<br>与初始成长表候选不同，未合并。<br>状态表写暗时“不叫、不转、不震”；设备说明允许变暗事件。震动原值已加删除线。</strong></td></tr>
<tr><td rowspan="1">候选 2｜50%<br>情绪：ANY<br>状态：ANY</td><td rowspan="1">ID 55｜暗光慵懒垂头（Darkness）</td><td rowspan="1">ID 42｜lightdown_dlm_dreamy_01.wav</td><td rowspan="1"><strong>【待补/待确认】 3｜强震动（原值已加删除线，不作为有效配置）</strong></td></tr>
<tr><td rowspan="2">30<br>变亮</td><td rowspan="2">光线变亮</td><td rowspan="2">正常状态光感原始值&gt;1000 持续约 2.5 秒；回落到“60 以下”才可再次触发。开机／退出待机后约 8 秒不触发光线事件。光线不算互动；浅睡短暂唤醒约 6 秒。</td><td rowspan="1">候选 1｜50%<br>情绪：ANY<br>状态：ANY</td><td rowspan="1">ID 9｜上下缓慢抬升打量</td><td rowspan="1">ID 8｜headright_psr_alert_right_01.wav</td><td rowspan="2">原表空白</td><td rowspan="2"><strong>【待补/待确认】 输入事件表：Beta=Y；候选动作=9/50/57/59。<br>与初始成长表候选不同，未合并。</strong></td></tr>
<tr><td rowspan="1">候选 2｜50%<br>情绪：ANY<br>状态：ANY</td><td rowspan="1">ID 50｜间断定点侧头试探</td><td rowspan="1">ID 23｜synth_bps_soft_greeting_01.wav</td></tr></tbody>
</table>

</details>

<details>
<summary>系统 · 原始输入及初始输出</summary>

<table>
<thead>
<tr><th>输入类型</th><th>事件 ID／输入区域</th><th>事件（原名称）</th><th>触发条件与状态限制</th><th>候选／概率／筛选条件</th><th>动作输出</th><th>音频输出</th><th>震动输出</th><th>版本与启用差异</th></tr></thead>
<tbody>
<tr><td rowspan="10">系统</td><td rowspan="2">31<br>长时间无互动</td><td rowspan="2">Idle&gt;2hours(长时间无互动)</td><td rowspan="2">距离上次互动满 2 小时触发一次，互动后重新计时。浅睡短暂唤醒约 6 秒做动作，再回浅睡，不算互动。</td><td rowspan="1">候选 1｜50%<br>情绪：ANY<br>状态：ANY</td><td rowspan="1">ID 19｜唤醒半睡慢抬</td><td rowspan="1">ID 18｜wakeup_psr_playful_02.wav</td><td rowspan="10">原表空白</td><td rowspan="1"><strong>【待补/待确认】 输入事件表：Beta=N；候选动作=6。<br>与初始成长表候选不同，未合并。<br>保留该表 N 标记，不据候选表改成已支持。</strong></td></tr>
<tr><td rowspan="1"><strong>【待补/待确认】 候选 2｜50%<br>情绪：原表空白<br>状态：原表空白</strong></td><td rowspan="2">ID 9｜上下缓慢抬升打量</td><td rowspan="2">ID 8｜headright_psr_alert_right_01.wav</td><td rowspan="1"><strong>【待补/待确认】 输入事件表：Beta=N；候选动作=6。<br>与初始成长表候选不同，未合并。<br>保留该表 N 标记，不据候选表改成已支持。<br>本候选情绪／状态空白或“/”按原表保留，继承规则未给出。</strong></td></tr>
<tr><td rowspan="2">32<br>超长无互动</td><td rowspan="2">Idle&gt;48hours(超长无互动)</td><td rowspan="2">距离上次互动满 48 小时触发一次，互动后重新计时。浅睡短暂唤醒约 6 秒做动作，再回浅睡，不算互动。</td><td rowspan="1">候选 1｜50%<br>情绪：ANY<br>状态：ANY</td><td rowspan="1"><strong>【待补/待确认】 输入事件表：Beta=N；候选动作=6。<br>与初始成长表候选不同，未合并。<br>保留该表 N 标记，不据候选表改成已支持。</strong></td></tr>
<tr><td rowspan="1"><strong>【待补/待确认】 候选 2｜50%<br>情绪：原表空白<br>状态：原表空白</strong></td><td rowspan="1">ID 19｜唤醒半睡慢抬</td><td rowspan="1">ID 18｜wakeup_psr_playful_02.wav</td><td rowspan="1"><strong>【待补/待确认】 输入事件表：Beta=N；候选动作=6。<br>与初始成长表候选不同，未合并。<br>保留该表 N 标记，不据候选表改成已支持。<br>本候选情绪／状态空白或“/”按原表保留，继承规则未给出。</strong></td></tr>
<tr><td rowspan="1">36<br>充电</td><td rowspan="1">充电</td><td rowspan="1">开机状态插入充电，播放充电动作，5 秒后待机。插入时已处于“静音”或睡眠时段直接待机。关机插入充电不开机；充满无完成动作。</td><td rowspan="2">候选 1｜100%<br>情绪：ANY<br>状态：ANY</td><td rowspan="1">ID 1｜充电启动单次点头（充电专属）</td><td rowspan="1">ID 61｜synth_greeting_hello_01.wav</td><td rowspan="1">输入事件表：Beta=Y；候选动作=1。</td></tr>
<tr><td rowspan="1">37<br>低电量</td><td rowspan="1">低电量</td><td rowspan="1">电量第一次降到 20%、10%、0% 时各播放一次低电动作；浅睡短暂唤醒。连续 3 次电压&lt;3.40V（约每 30 秒检测）属于静默关机保护，不播动作。</td><td rowspan="1">ID 53｜低电量间断抬头观望</td><td rowspan="1">ID 40｜synth_farewell_bye_01.wav</td><td rowspan="1"><strong>【待补/待确认】 输入事件表：Beta=Y；候选动作=53。<br>状态表低电备注末尾写“删掉”；功能说明保留低电事件。</strong></td></tr>
<tr><td rowspan="2">38<br>开机</td><td rowspan="2">开机</td><td rowspan="2">关机长按满 3 秒；电压≤3.45V 拒绝开机。震动约 0.3 秒，约 3 秒后传感器就绪，播放开机动作伴音并可被蓝牙发现。首次接电池／复位且电压正常自动开机。</td><td rowspan="1">候选 1｜50%<br>情绪：ANY<br>状态：ANY</td><td rowspan="1">ID 8｜开机上扬点头（开机启动）</td><td rowspan="1">ID 7｜poweron_psr_softwake_v01.wav</td><td rowspan="2">输入事件表：Beta=Y；候选动作=8/51。</td></tr>
<tr><td rowspan="1">候选 2｜50%<br>情绪：ANY<br>状态：ANY</td><td rowspan="1">ID 51｜开机分段环视</td><td rowspan="1">ID 39｜poweron_psr_softwake_v02.wav</td></tr>
<tr><td rowspan="1">39<br>呼吸</td><td rowspan="1">呼吸（5分钟~2小时之间，如果没有互动就30S呼吸一次）</td><td rowspan="1">设备功能说明：距上次互动 10 分钟首次，之后每 10 分钟一次，满 2 小时不再呼吸；浅睡短暂唤醒约 6 秒后返回，不算互动。</td><td rowspan="2">候选 1｜100%<br>情绪：ANY<br>状态：ANY</td><td rowspan="1">ID 48｜待机呼吸间断侧头</td><td rowspan="1">ID 23｜synth_bps_soft_greeting_01.wav</td><td rowspan="1"><strong>【待补/待确认】 输入事件表：Beta=N；候选动作=6/48。<br>与初始成长表候选不同，未合并。<br>保留该表 N 标记，不据候选表改成已支持。<br>两份事件表均写“5 分钟～2 小时、每 30 秒”；状态表呼吸备注写“不要”。保留三处口径。</strong></td></tr>
<tr><td rowspan="1">42<br>关机</td><td rowspan="1">关机</td><td rowspan="1">按键长按满 4 秒；震动约 1 秒，播放关机动作约 3 秒，保存数据后关机。低电保护、过温保护静默关机，不播放本动作。</td><td rowspan="1">ID 4｜关机缓慢垂头锁位</td><td rowspan="1">ID 4｜poweroff_dlm_sleep_01.wav</td><td rowspan="1">输入事件表：Beta=Y；候选动作=4。</td></tr></tbody>
</table>

</details>

<details>
<summary>BLE 交友 · 原始输入及初始输出</summary>

<table>
<thead>
<tr><th>输入类型</th><th>事件 ID／输入区域</th><th>事件（原名称）</th><th>触发条件与状态限制</th><th>候选／概率／筛选条件</th><th>动作输出</th><th>音频输出</th><th>震动输出</th><th>版本与启用差异</th></tr></thead>
<tbody>
<tr><td rowspan="4">BLE 交友</td><td rowspan="2">33<br>遇到新Beany</td><td rowspan="2">NewBeanynearby(遇到新Beany)</td><td rowspan="2">已绑定 App 且交友开启；另一只 Beany 在约 5 米内持续 30 秒，第一次见。浅睡中完全唤醒；离开不触发动作。</td><td rowspan="1">候选 1｜50%<br>情绪：ANY<br>状态：ANY</td><td rowspan="1">ID 17｜初识同类慢偏头试探（左）</td><td rowspan="1">ID 16｜nose_dlm_shy_01.wav</td><td rowspan="4">原表空白</td><td rowspan="2"><strong>【待补/待确认】 输入事件表：Beta=Y；候选动作=17/21/29/33/50/57。<br>与初始成长表候选不同，未合并。</strong></td></tr>
<tr><td rowspan="1">候选 2｜50%<br>情绪：ANY<br>状态：ANY</td><td rowspan="1">ID 21｜陌生同类低头远离（左）</td><td rowspan="1">ID 3｜idle_dlm_lonely_01.wav</td></tr>
<tr><td rowspan="2">34<br>遇到熟悉Beany</td><td rowspan="2">FamiliarBeanynearby(遇到熟悉Beany)</td><td rowspan="2">已绑定 App 且交友开启；以前见过的 Beany 在约 5 米内持续 30 秒。浅睡中完全唤醒；离开不触发动作。</td><td rowspan="1">候选 1｜50%<br>情绪：ANY<br>状态：ANY</td><td rowspan="1">ID 33｜点头同步左右小幅颤（极致开心）</td><td rowspan="1">ID 24｜social_psr_ecstatic_01.wav</td><td rowspan="2">输入事件表：Beta=Y；候选动作=33/34。</td></tr>
<tr><td rowspan="1">候选 2｜50%<br>情绪：ANY<br>状态：ANY</td><td rowspan="1">ID 34｜遇见熟同类高频点头（熟悉Beany）</td><td rowspan="1">ID 28｜social_psr_ecstatic_02.wav</td></tr></tbody>
</table>

</details>

[返回完整PRD目录](../README.md) · [上一章](./11-custom-actions.md) · [下一章](./13-state-flows.md)
