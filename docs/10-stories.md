# 10 故事与内容模板

[返回完整PRD目录](../README.md) · [上一章](./09-milestones.md) · [下一章](./11-custom-actions.md)

14篇固定模板；一次解锁对应一篇故事，支持列表和详情。

先保存解锁证据，再套用故事模板。故事是拟人化表达，不宣称识别人的真实情绪；已生成内容保留当时名称、日期与事实。

<details>
<summary>S01 你好，这一页从我们开始</summary>

关联 M01；事实字段：profile_id；first_applied_package_id；activation_confirmed_at

我是{pet_name}。我们的相处手册，从这一页正式开始。先留一点空白，给以后的招呼、触碰和小小相遇。接下来，就从一次轻轻的互动开始吧。

</details>

<details>
<summary>S02 一声招呼，一个开始</summary>

关联 M02；事实字段：event_record_ids；event_id=28；event_date

这一声招呼，给故事开了个头。我是{pet_name}，想把它夹成一枚小书签。以后再翻到这里，就能找到我们第一次留下招呼记录的这一页。

</details>

<details>
<summary>S03 第一枚摸头印章</summary>

关联 M03；事实字段：event_record_ids；head_event_id；event_date

头上的这次触碰，被我收进了故事里。我是{pet_name}，想把它叫作“第一枚摸头印章”。印章不用盖得很重，留住这次相处就够了。

</details>

<details>
<summary>S04 原来，招呼有这么多地方</summary>

关联 M04；事实字段：head_evidence；belly_evidence；back_side_evidence；event_date

头上、肚子和背侧，都留下了互动的小记号。原来，打招呼可以有这么多地方。我是{pet_name}，把它们放在同一张小地图上，不用按顺序，也不必赶在一起。

</details>

<details>
<summary>S05 把这一会儿留长一点</summary>

关联 M05；事实字段：event_record_ids；event_id=22；event_date

这次停留，比轻轻一碰更长一点。我把它折成书页的一角，放进相处手册。有些小故事不需要热闹，安安稳稳留住这一会儿，就很好。

</details>

<details>
<summary>S06 温柔，慢慢有了回声</summary>

关联 M06；事实字段：long_stroke_record_ids；confirmed_long_stroke_count>=3；event_date

三次停留久一点的抚摸，攒成了这页小故事。我是{pet_name}，把它们想象成三枚柔软的标点。不用急着添上下一枚，已经留下的这些，就值得好好收着。

</details>

<details>
<summary>S07 第三枚互动记号</summary>

关联 M07；事实字段：qualifying_event_record_ids；confirmed_interaction_count>=3；event_date

相处手册里，添上了第三枚互动记号。我是{pet_name}，负责把这些发生过的小事放在一起。它们不必相隔很久，也不用追赶下一页；这一页已经有了自己的内容。

</details>

<details>
<summary>S08 越来越熟悉的这一页</summary>

关联 M08；事实字段：applied_package_id；applied_xp>=10；applied_stage>=1；applied_confirmed_at

我们的相处，翻到了更熟悉的一页。我是{pet_name}，把之前的小记号一起带了过来。新的这一页，不用刻意安排；一次自然的招呼，就能接着往下写。

</details>

<details>
<summary>S09 慢慢成为日常</summary>

关联 M09；事实字段：applied_package_id；applied_xp>=30；applied_stage=2；applied_confirmed_at

这一页，想叫作“相伴”。我是{pet_name}，把一路留下的小互动收成一本薄薄的手册。后面仍有空白，留给接下来自然发生的小事；不用赶路，我们接着写。

</details>

<details>
<summary>S10 小世界，轻轻晃了一下</summary>

关联 M10；事实字段：event_record_ids；event_id=23；event_date

这次轻轻的摇动，像故事页边的一条小弧线。我是{pet_name}，把它留在这里。线不用画得很大，也不需要反复摇晃；记住这一次小变化，就够了。

</details>

<details>
<summary>S11 故事里，多了一个名字</summary>

关联 M11；事实字段：peer_id；first_encounter；new_peer_evidence；event_date

这次相遇记录里，多了{friend_name}。我是{pet_name}，给这位新伙伴留了一个小小的位置。第一次见面不必写得很长，先收好这个开始，以后再慢慢添上新的记号。

</details>

<details>
<summary>S12 又在记录里碰见你</summary>

关联 M12；事实字段：peer_id；baseline_count；confirmed_encounter_delta>=3；last_encounter；confirmed_at

{friend_name}又出现在相遇这一页，已经攒下了三次新的见面记录。我是{pet_name}，把这些小记号排在一起。一个熟悉的名字，就这样有了更多可以回看的内容。

</details>

<details>
<summary>S13 一页放得下三个新伙伴</summary>

关联 M13；事实字段：three_distinct_new_peer_ids；first_encounter_times；event_date

相遇的小册子里，已经留过三个不同伙伴的记号。我是{pet_name}，把每次初见各自收好，再摆在同一页。它们不用同时出现，也能让这一页变得丰富一点。

</details>

<details>
<summary>S14 三十枚小小的记号</summary>

关联 M14；事实字段：touch_record_ids；confirmed_touch_count>=30；event_date

三十次小小的触碰，攒成了这一页记号。我是{pet_name}，把它们想象成纸上的圆点：一个接着一个，慢慢有了自己的形状。现在先收好这一页，下一次相处，照常发生就好。

</details>

<table>
<thead>
<tr><th>项目</th><th>要求</th></tr></thead>
<tbody>
<tr><td rowspan="1">生成方式</td><td rowspan="1">每项里程碑对应一篇预设短故事；首版由App模板填充，不调用大模型。故事ID保持S01–S14，实例唯一键使用档案ID+故事ID。</td></tr>
<tr><td rowspan="1">保存字段</td><td rowspan="1">保存实例ID、模板版本、关联里程碑、标题/摘要/完整正文、名称变量、证据ID、事件日期、生成时间、已确认包与阶段/性格快照、图片ID、生成状态、已读状态。名称≤25字节规则用于设备设置；正文使用已保存的显示名称。</td></tr>
<tr><td rowspan="1">事实与故事分开</td><td rowspan="1">详情上方展示可核对的“记录依据”，例如“设备记录：头部触摸1次”；下方显示拟人化故事。故事不宣称检测到人的情绪、理解自由对话、感知拥抱温度或确认动作执行成功。</td></tr>
<tr><td rowspan="1">变量缺失</td><td rowspan="1">宠物名缺失用“小伙伴”，好友备注缺失用“新伙伴”；无有效日期则正文保持准备中，等待证据补齐，不用今天补造历史日期。阶段/性格不可核实时隐藏该标签，不影响其他已具备证据的正文。</td></tr>
<tr><td rowspan="1">展示与已读</td><td rowspan="1">里程碑成立并保存故事占位后可显示“故事准备中”。标题、日期、正文准备成功后卡片显示摘要及未读。仅成功打开完整正文才标已读；列表曝光、加载失败或占位页不标已读。</td></tr>
<tr><td rowspan="1">重试与图片</td><td rowspan="1">正文失败重试同一实例并使用已冻结变量；不因重试改名或换故事。图片失败显示统一占位图，正文仍可读；后续补图不重置已读。</td></tr>
<tr><td rowspan="1">历史不覆盖</td><td rowspan="1">故事一经生成，后续改名、成长升级、关键词改名、模板升级和重复同步均不重写正文。旧性格标签可做显示映射，原值与正文保留。</td></tr>
<tr><td rowspan="1">阶段关系</td><td rowspan="1">S08/S09来自阶段包成功生效；其他故事来自已证实输入或相遇。故事不会反向加成长分、调反馈概率或改变情绪，也不因阶段升级批量编造未发生的互动故事。</td></tr></tbody>
</table>

[返回完整PRD目录](../README.md) · [上一章](./09-milestones.md) · [下一章](./11-custom-actions.md)
