# 09 里程碑

[返回完整PRD目录](../README.md) · [上一章](./08-sync.md) · [下一章](./10-stories.md)

14项里程碑；按真实、去重且属于当前养成档案的证据解锁。

<table>
<thead>
<tr><th>ID</th><th>名称</th><th>关联事件</th><th>解锁条件</th><th>故事ID</th><th>展示条件</th></tr></thead>
<tbody>
<tr><td rowspan="1">M01</td><td rowspan="1">初次见面</td><td rowspan="1"></td><td rowspan="1">首次成长包全部提交并核对成功，养成档案正式启用。仅绑定、仅查询或提交失败均不解锁。<br>证据来源：成长包生效回读。档案ID、成长启用起点、首个已生效包ID和确认时间</td><td rowspan="1">S01</td><td rowspan="1">已启用养成后显示；日期：首个成长包确认成功日期</td></tr>
<tr><td rowspan="1">M02</td><td rowspan="1">第一声招呼</td><td rowspan="1">28</td><td rowspan="1">本档案启用后，收到并去重保存第1次有效唤醒词事件。<br>证据来源：有效事件日志。事件28、稳定记录ID、首时间戳、已确认新增count</td><td rowspan="1">S02</td><td rowspan="2">已启用养成后显示；日期：事件记录日期</td></tr>
<tr><td rowspan="1">M03</td><td rowspan="1">摸摸头，就认识了</td><td rowspan="1">1；2；3；4；5；6；7；8；9</td><td rowspan="1">本档案启用后，头部任一区域累计1次有效触摸。<br>证据来源：有效事件日志。头部事件1–9的有效记录及新增count</td><td rowspan="1">S03</td></tr>
<tr><td rowspan="1">M04</td><td rowspan="1">每个角落都熟悉了</td><td rowspan="1">1；2；3；4；5；6；7；8；9；10；11；12；13；14；15；16；17；18；19；20；21</td><td rowspan="1">头部1–9、腹部10–12、背部及身体两侧13–21，各累计至少1次有效触摸；无顺序、同日或阶段要求。<br>证据来源：有效事件日志。三个区域的有效记录ID集合</td><td rowspan="1">S04</td><td rowspan="1">三个区域分别有至少一种已启用输入时显示；日期：首次凑齐三个区域的事件日期</td></tr>
<tr><td rowspan="1">M05</td><td rowspan="1">稳稳地抱一会儿</td><td rowspan="1">22</td><td rowspan="1">本档案启用后，累计1次有效长时间握持。<br>证据来源：有效事件日志。事件22、时间戳及新增count</td><td rowspan="1">S05</td><td rowspan="1">事件22验收启用后显示；日期：事件记录日期</td></tr>
<tr><td rowspan="1">M06</td><td rowspan="1">温柔有了回声</td><td rowspan="1">3；6；9；12；15；18；21</td><td rowspan="1">本档案启用后，累计3次有效长抚摸；不要求跨日，没有每日上限。<br>证据来源：有效事件日志。已启用长抚摸事件的去重新增count</td><td rowspan="1">S06</td><td rowspan="1">至少一种长抚摸事件验收启用后显示；日期：第3次有效长抚所在记录日期</td></tr>
<tr><td rowspan="1">M07</td><td rowspan="1">又见到你</td><td rowspan="1">1；2；3；4；5；6；7；8；9；10；11；12；13；14；15；16；17；18；19；20；21；22；23；28</td><td rowspan="1">本档案启用后，累计3次有效用户互动：已启用的触摸、握持、轻摇或唤醒。<br>证据来源：有效事件日志。事件1–23或28的去重新增count</td><td rowspan="1">S07</td><td rowspan="1">已启用养成后显示；日期：第3次有效互动所在记录日期</td></tr>
<tr><td rowspan="1">M08</td><td rowspan="1">越来越熟悉</td><td rowspan="1"></td><td rowspan="1">App确认完整成长包已生效，包内累计XP≥10且设备阶段为熟悉或相伴。<br>证据来源：成长包生效回读。已生效包ID、该包对应XP、设备读回阶段及确认时间</td><td rowspan="1">S08</td><td rowspan="1">已启用养成后显示；日期：首次满足条件的成长包确认成功日期</td></tr>
<tr><td rowspan="1">M09</td><td rowspan="1">慢慢成为日常</td><td rowspan="1"></td><td rowspan="1">App确认相伴成长包完整生效，包内累计XP≥30且设备阶段为相伴。<br>证据来源：成长包生效回读。相伴包ID、该包对应XP、设备读回阶段及确认时间</td><td rowspan="1">S09</td><td rowspan="1">已启用养成后显示；日期：首次相伴包确认成功日期</td></tr>
<tr><td rowspan="1">M10</td><td rowspan="1">轻轻晃动的小世界</td><td rowspan="1">23</td><td rowspan="1">本档案启用后，累计1次有效轻摇事件。<br>证据来源：有效事件日志。事件23及其有效记录</td><td rowspan="1">S10</td><td rowspan="1">事件23验收启用后显示；日期：首次有效轻摇记录日期</td></tr>
<tr><td rowspan="1">M11</td><td rowspan="1">第一次遇见同伴</td><td rowspan="1">33</td><td rowspan="1">好友表首次证实1位在本档案启用后新相遇、且历史从未认识的伙伴。<br>证据来源：好友表增量。伙伴ID、首次/最近相遇时间、count与启用基线</td><td rowspan="1">S11</td><td rowspan="1">交友功能及好友读取已启用时显示；日期：新伙伴首次相遇日期</td></tr>
<tr><td rowspan="1">M12</td><td rowspan="1">又遇见老朋友</td><td rowspan="1">34</td><td rowspan="1">同一伙伴在本档案启用后，已确认新增相遇累计达到3次。旧伙伴也可参加。<br>证据来源：好友表增量。伙伴ID、基线count、历次有效count正增量及已计last时间</td><td rowspan="1">S12</td><td rowspan="1">交友功能及好友读取已启用时显示；日期：首次确认达标时的最近相遇日期，标注同步确认</td></tr>
<tr><td rowspan="1">M13</td><td rowspan="1">一起认识新朋友</td><td rowspan="1">33</td><td rowspan="1">本档案启用后，累计认识3个不同的新伙伴ID。<br>证据来源：好友表增量。App保留的新伙伴ID集合及各自首次相遇时间</td><td rowspan="1">S13</td><td rowspan="1">交友功能及好友读取已启用时显示；日期：第3位新伙伴首次相遇日期</td></tr>
<tr><td rowspan="1">M14</td><td rowspan="1">三十次小回应</td><td rowspan="1">1；2；3；4；5；6；7；8；9；10；11；12；13；14；15；16；17；18；19；20；21</td><td rowspan="1">本档案启用后，有效触摸累计30次；无每日上限。<br>证据来源：有效事件日志。事件1–21的去重新增count</td><td rowspan="1">S14</td><td rowspan="1">已启用养成后显示；日期：第30次有效触摸所在记录日期</td></tr></tbody>
</table>

<details>
<summary>解锁与保存规则</summary>

<table>
<thead>
<tr><th>项目</th><th>要求</th></tr></thead>
<tbody>
<tr><td rowspan="1">本版范围</td><td rowspan="1">保留M01–M14与S01–S14唯一ID和一对一关系；M06/M07/M08/M09/M14按本次快速演示规则调整。所有事件ID1–42保持原义，新增App业务条件不占用设备事件ID。</td></tr>
<tr><td rowspan="1">统计起点</td><td rowspan="1">首次成长包成功启用后建立档案统计起点。启用前事件和旧好友只建基线，不补分、不补发互动里程碑。仅绑定而未启用成长时，不开放本档案里程碑。</td></tr>
<tr><td rowspan="1">无日期配额</td><td rowspan="1">本版没有3/7/14互动日门槛，没有每日计数上限；按已确认新增count累计。设备既有识别去重与互斥仍生效，App不能把界面点击数当作设备有效事件。</td></tr>
<tr><td rowspan="1">事件准入</td><td rowspan="1">仅计当前档案起点后、时间有效、稳定ID可去重、已验收启用且来源为真实设备输入的记录。Beta=N及划除事件不因新规则自动启用；未启用项目在列表隐藏。</td></tr>
<tr><td rowspan="1">重复与聚合</td><td rowspan="1">按档案ID+设备ID+稳定记录ID去重。同记录count从3增至5只新增2次；整批重传不增加。源聚合只保留首时间戳时，按该记录日期展示，并注明设备汇总，不推算第n次的精确时间。</td></tr>
<tr><td rowspan="1">先保存后确认</td><td rowspan="1">事件/好友数据和增量台账保存成功后才确认接收。事件批次冻结、ACK只清已读批、稳定记录ID均属新增同步要求；现有0x12清空描述不足以保证并发不丢记录。</td></tr>
<tr><td rowspan="1">好友口径</td><td rowspan="1">相遇只依据好友表计一次，33/34日志不再重复累计。旧好友保存基线；正常count正增量累计。255饱和后，更新且未计过的last只确认至少1次。回退且新first晚于旧last，可计该新段count；否则只取可确认的新last记1次。设备名单淘汰不扣回App历史。</td></tr>
<tr><td rowspan="1">阶段门槛</td><td rowspan="1">M08/M09以完整包已确认生效为准。查询得到目标阶段或任一侧局部提交均不解锁；一次直接应用相伴包，可同时满足两项，不记录虚构的中间设备阶段。</td></tr>
<tr><td rowspan="1">查询与提交分开</td><td rowspan="1">互动类M02–M07/M10–M14在App保存有效证据后即可解锁；不必等新的成长包应用。M01/M08/M09必须等对应启用或阶段包核对成功。里程碑本身不额外增加XP或改变情绪。</td></tr>
<tr><td rowspan="1">唯一保存</td><td rowspan="1">同一档案每项仅解锁一次；用档案ID+里程碑ID作为唯一键。里程碑和唯一故事占位在同一笔本地保存中建立，正文失败不回退里程碑，也不另建第二篇。</td></tr>
<tr><td rowspan="1">日期与快照</td><td rowspan="1">互动项使用证据日期；阶段项使用包确认成功日期；M12使用首次确认达标的最近相遇日期并标同步确认。保存当次规则版本、名称、证据、已确认包、阶段/性格快照；后续阶段、名称或规则更新不追溯覆盖。</td></tr>
<tr><td rowspan="1">阶段标签含义</td><td rowspan="1">源事件没有成长包ID或阶段字段，不能把查询时阶段当作互动发生时阶段。首版标签统一写“记录生成时已确认阶段”，取最近核对成功的包；未知就隐藏。M08/M09单独展示本次已确认生效阶段。</td></tr>
<tr><td rowspan="1">列表与详情</td><td rowspan="1">列表显示名称、实际进度、未达成条件；已解锁显示日期。详情显示条件、证据摘要与关联故事。多项同时达成只弹一次汇总，不连续弹14次。未同步记录不显示已达成。</td></tr>
<tr><td rowspan="1">旧记录迁移</td><td rowspan="1">已解锁旧实例保留当时名称、规则和故事，不重新生成；可标“旧规则记录”。尚未解锁项目按新规则检查完整有效台账。缺历史就保留待核对，不从设备百分比或位图猜出事件明细。新档案从本次启用起重新计算。</td></tr></tbody>
</table>

</details>

[返回完整PRD目录](../README.md) · [上一章](./08-sync.md) · [下一章](./10-stories.md)
