# 01 产品定义与硬件需求

[返回完整PRD目录](../README.md) · [下一章](./02-firmware.md)

只保留影响功能、交互和整机体验的硬件。

<table>
<thead>
<tr><th>项目</th><th>需求定义</th></tr></thead>
<tbody>
<tr><td rowspan="1">产品定位</td><td rowspan="1">通过触摸、姿态、光感和固定唤醒词互动的陪伴玩具，以动作、伴音和震动表达反馈；App负责设置、养成与动作编排。</td></tr>
<tr><td rowspan="1">设备职责</td><td rowspan="1">本地识别输入、执行状态和优先级限制，按已生效行为表反馈；断开App仍可互动并记录事件。</td></tr>
<tr><td rowspan="1">App职责</td><td rowspan="1">蓝牙绑定、设置、查询互动与好友、计算成长、更新规则、展示里程碑和故事、保存与绑定自定义动作。</td></tr>
<tr><td rowspan="1">运行模式</td><td rowspan="1">首次未初始化：无五行、无成长阶段，执行初始表。初始化成功：初识；10 XP可更新为熟悉；30 XP可更新为相伴。</td></tr>
<tr><td rowspan="1">情绪与性格</td><td rowspan="1">五维记录长期互动倾向，主五行参与日运/时辰情绪计算；情绪归为开心、平静、悲伤，再按阶段和事件选整套反馈。</td></tr>
<tr><td rowspan="1">资料范围</td><td rowspan="1">硬件、固件和App协议依据原资料；成长、里程碑、故事和自定义动作采用当前方案定义。红色表示尚缺资料或需要补齐的实现条件。</td></tr></tbody>
</table>

<table>
<thead>
<tr><th>编号</th><th>模块</th><th>配置/数量</th><th>产品功能</th><th>待确认</th><th>依据</th></tr></thead>
<tbody>
<tr><td rowspan="1">H01</td><td rowspan="1">主控与动作控制</td><td rowspan="1">BK7258QN88616 主控 ×1；CIU32F003F5U6 舵机 MCU ×1</td><td rowspan="1">主控处理互动、蓝牙、声音与状态；舵机 MCU 执行动作库和舵机控制。</td><td rowspan="1"></td><td rowspan="1">UAC234-A0-V1.2.pdf 第2、5、11页；舵机控制板协议 V1.4</td></tr>
<tr><td rowspan="1">H02</td><td rowspan="1">触摸输入</td><td rowspan="1">3组、7个区域：头顶、头左、头右、后背、身体左、身体右、腹部</td><td rowspan="1">识别碰一碰、撸一撸、长时间抚摸和握持。</td><td rowspan="1"></td><td rowspan="1">设备功能说明.md §1、§8.1；UAC234-A0-V1.2.pdf 第9页</td></tr>
<tr><td rowspan="1">H03</td><td rowspan="1">姿态输入</td><td rowspan="1">SC7U22TH IMU ×1</td><td rowspan="1">识别拿起、放下、轻摇、猛摇、倾倒、翻转、上抛、旋转上抛；判定时间与阈值见固件需求。</td><td rowspan="1"></td><td rowspan="1">八个IMU事件触发标准.md；UAC234-A0-V1.2.pdf 第7页</td></tr>
<tr><td rowspan="1">H04</td><td rowspan="1">光感输入</td><td rowspan="1">光线传感器 ×1</td><td rowspan="1">识别环境变暗、变亮；暗环境抑制普通互动。</td><td rowspan="1"><strong>【待补/待确认】 需确认光感型号及装机后的原始值标定。</strong></td><td rowspan="1">设备功能说明.md §1、§8.3；UAC234-A0-V1.2.pdf 第9页</td></tr>
<tr><td rowspan="1">H05</td><td rowspan="1">按键输入</td><td rowspan="1">实体按键 ×1</td><td rowspan="1">长按开关机，单击确认绑定，双击重启蓝牙；其他维护操作见固件需求。</td><td rowspan="1"></td><td rowspan="1">设备功能说明.md §2、§3；UAC234-A0-V1.2.pdf 第9页</td></tr>
<tr><td rowspan="1">H06</td><td rowspan="1">语音输入</td><td rowspan="1">外接麦克风通路 ×1</td><td rowspan="1">识别固定离线唤醒词 Hello Beany。</td><td rowspan="1"></td><td rowspan="1">设备功能说明.md §8.4；UAC234-A0-V1.2.pdf 第5、6页</td></tr>
<tr><td rowspan="1">H07</td><td rowspan="1">声音输出</td><td rowspan="1">扬声器 ×1；AW8733ATQR 功放 ×1</td><td rowspan="1">播放动作伴音、开关机、充电及低电提示声音；App支持6档音量。</td><td rowspan="1"><strong>【待补/待确认】 扬声器型号、尺寸、阻抗、额定功率待确认。</strong></td><td rowspan="1">设备功能说明.md §1、§4.2；UAC234-A0-V1.2.pdf 第6页</td></tr>
<tr><td rowspan="1">H08</td><td rowspan="1">动作输出</td><td rowspan="1">X、Y 舵机接口各1路，共2路</td><td rowspan="1">执行预置肢体动作，供自定义动作调用已验证动作卡。</td><td rowspan="1"><strong>【待补/待确认】 已装舵机型号、X/Y对应部位、零位和安全角度/速度范围待确认。</strong></td><td rowspan="1">UAC234-A0-V1.2.pdf 第11页；舵机控制板协议 V1.4</td></tr>
<tr><td rowspan="1">H09</td><td rowspan="1">震动输出</td><td rowspan="1">震动马达 ×1</td><td rowspan="1">开关机震动；按行为资源表执行配对震动。</td><td rowspan="1"></td><td rowspan="1">设备功能说明.md §1、§2、§8.7；UAC234-A0-V1.2.pdf 第12页</td></tr>
<tr><td rowspan="1">H10</td><td rowspan="1">无线连接</td><td rowspan="1">蓝牙通信与附近同伴发现</td><td rowspan="1">连接App完成绑定、设置、事件/好友读取、成长规则同步和升级；支持附近同伴相遇反馈。</td><td rowspan="1"></td><td rowspan="1">设备功能说明.md §4、§8.5；通用BLE协议 V1.0.12；UAC234-A0-V1.2.pdf 第5页</td></tr>
<tr><td rowspan="1">H11</td><td rowspan="1">资源存储</td><td rowspan="1">SD NAND 1Gb；动作 NOR Flash 16MB</td><td rowspan="1">保存设备业务资源及动作库。1Gb是位容量，不能写为1GB。</td><td rowspan="1"><strong>【待补/待确认】 用户动作、音频、事件及升级区可用容量待分配。</strong></td><td rowspan="1">UAC234-A0-V1.2.pdf 第2、7、11页</td></tr>
<tr><td rowspan="1">H12</td><td rowspan="1">电池</td><td rowspan="1">锂电池 ×1</td><td rowspan="1">支持脱离电源后的便携互动；配合固件完成低电提示与保护。</td><td rowspan="1"><strong>【待补/待确认】 电池容量、型号及典型续航未提供；1000mAh仅为用户举例。</strong></td><td rowspan="1">设备功能说明.md §1、§5；UAC234-A0-V1.2.pdf 第8页</td></tr>
<tr><td rowspan="1">H13</td><td rowspan="1">有线充电</td><td rowspan="1">USB Type-C 接口 ×1</td><td rowspan="1">支持有线充电；充电后进入待机，拔线且其他待机条件解除后恢复互动。</td><td rowspan="1"><strong>【待补/待确认】 充电时间待电池规格和整机实测确定。</strong></td><td rowspan="1">设备功能说明.md §5；UAC234-A0-V1.2.pdf 第8、9页</td></tr>
<tr><td rowspan="1">H14</td><td rowspan="1">无线充电</td><td rowspan="1">无线充组件接口 ×1</td><td rowspan="1">支持无线充；充满后向充电座通知满电。</td><td rowspan="1"><strong>【待补/待确认】 无线充组件、充电座、功率和兼容规格待补充。</strong></td><td rowspan="1">设备功能说明.md §1、§5.1；UAC234-A0-V1.2.pdf 第1、8页</td></tr></tbody>
</table>

硬件具备检测通路不等于所有事件已开放。默认启用18个Beta Y事件，预留及划除事件见交互矩阵；电池容量尚无确认值。

[返回完整PRD目录](../README.md) · [下一章](./02-firmware.md)
