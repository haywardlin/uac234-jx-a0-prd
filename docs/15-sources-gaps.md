# 15 资料依据与待补项

[返回完整PRD目录](../README.md) · [上一章](./14-resource-mapping.md)

缺口仍以红色提示；文档定义不等于固件和App联调完成。

<table>
<thead>
<tr><th>事项</th><th>缺失内容</th><th>影响</th></tr></thead>
<tbody>
<tr><td>电池与外设规格</td><td><strong>【待补/待确认】 电池容量/型号、扬声器规格、无线充组件与功率未提供。</strong></td><td>不能确定续航、充电时间和整机声学指标。</td></tr>
<tr><td>自定义动作控制链路</td><td><strong>【待补/待确认】 普通动作的App命令入口、0x05字节序、装机舵机安全范围、停止/完成通知未明确；0x51只用于舵机MCU OTA透传。</strong></td><td>自定义动作UI可以定义；实机预览、连续动作和中止须先补齐接口。</td></tr>
<tr><td>动作资源编号</td><td><strong>【待补/待确认】 初始行为表、动作统计表和MCU动作库之间缺少完整编号映射。</strong></td><td>业务候选可以按源表定义；下载前需生成并核验唯一映射表，不能直接发送统计表编号。</td></tr>
<tr><td>事件读取的可靠性</td><td><strong>【待补/待确认】 当前事件协议未定义批次唯一标识、读取期间新增事件的冻结范围、存储满处理。</strong></td><td>影响断连重试的严格去重和成长补账；协议补充前不能承诺不重不漏。</td></tr>
<tr><td>提交后状态确认</td><td><strong>【待补/待确认】 0x44两侧分别落盘，未定义断电/丢应答后的行为表版本回读与恢复；环境flags完整匹配判据未写清。</strong></td><td>App需分别显示快照和行为表同步状态；不能把一次提交写成原子事务。</td></tr>
<tr><td>升级资源边界</td><td><strong>【待补/待确认】 主固件OTA准入电量存在20%与25%两种口径；WAV容量上限和音频格式未给出。</strong></td><td>OTA门槛需统一；音频包和动作包需按实际存储分区校验。</td></tr>
<tr><td>触摸/姿态的演示开关</td><td><strong>【待补/待确认】 固件功能文档列完整事件，初始行为表对部分事件标Beta N；握持组合的“任意两个区域”口径仍需核实。</strong></td><td>演示版本逐项核对事件启用清单；Beta N对应里程碑不可提前承诺实机可触发。</td></tr></tbody>
</table>

## 资料入口

<table>
<thead>
<tr><th>资料</th><th>位置</th></tr></thead>
<tbody>
<tr><td>Beany Beta 初始动作行为查表TA 20260806.xlsx</td><td>原件保留在本地资料夹</td></tr>
<tr><td>八个IMU事件触发标准.md</td><td>原件保留在本地资料夹</td></tr>
<tr><td>其他描述.txt</td><td>原件保留在本地资料夹</td></tr>
<tr><td>beany_emotion_machine.pdf</td><td>原件保留在本地资料夹</td></tr>
<tr><td>daily_emotion_liunian.py</td><td>原件保留在本地资料夹</td></tr>
<tr><td>舵机动作统计表格 20260723 合并版本update_sound update 0901.xlsm</td><td>原件保留在本地资料夹</td></tr>
<tr><td>舵机控制板协议_V1.4_20260818.docx</td><td>原件保留在本地资料夹</td></tr>
<tr><td>设备功能说明.md</td><td>原件保留在本地资料夹</td></tr>
<tr><td>通用BLE协议_V1_0_12.md</td><td>原件保留在本地资料夹</td></tr>
<tr><td>UAC234-A0-V1.2.pdf</td><td>原件保留在本地资料夹</td></tr>
<tr><td>IMG_1298.PNG</td><td>原件保留在本地资料夹</td></tr>
<tr><td>IMG_1299.PNG</td><td>原件保留在本地资料夹</td></tr>
<tr><td>IMG_1300.PNG</td><td>原件保留在本地资料夹</td></tr>
<tr><td>IMG_1301.PNG</td><td>原件保留在本地资料夹</td></tr>
<tr><td>IMG_1302.PNG</td><td>原件保留在本地资料夹</td></tr>
<tr><td>IMG_1303.PNG</td><td>原件保留在本地资料夹</td></tr>
<tr><td>IMG_1304.PNG</td><td>原件保留在本地资料夹</td></tr>
<tr><td>IMG_1305.PNG</td><td>原件保留在本地资料夹</td></tr>
<tr><td>IMG_1306.PNG</td><td>原件保留在本地资料夹</td></tr>
<tr><td>IMG_1307.PNG</td><td>原件保留在本地资料夹</td></tr>
<tr><td>IMG_1308.PNG</td><td>原件保留在本地资料夹</td></tr>
<tr><td>IMG_1311.PNG</td><td>原件保留在本地资料夹</td></tr>
<tr><td>IMG_1312.PNG</td><td>原件保留在本地资料夹</td></tr>
<tr><td>IMG_1313.PNG</td><td>原件保留在本地资料夹</td></tr>
<tr><td>IMG_1317.PNG</td><td>原件保留在本地资料夹</td></tr>
<tr><td>IMG_1319.PNG</td><td>原件保留在本地资料夹</td></tr>
<tr><td>IMG_1320.PNG</td><td>原件保留在本地资料夹</td></tr>
<tr><td>IMG_1322.PNG</td><td>原件保留在本地资料夹</td></tr></tbody>
</table>

<details>
<summary>情绪原表差异与表现参考</summary>

## 时辰能量表 PDF 原表

<table>
<thead>
<tr><th>时辰</th><th>输入小时</th><th>本气</th><th>木</th><th>火</th><th>土</th><th>金</th><th>水</th></tr></thead>
<tbody>
<tr><td>子</td><td>23、0</td><td>水</td><td>旺</td><td>弱</td><td>平</td><td>旺</td><td>旺</td></tr>
<tr><td>丑</td><td>1、2</td><td>土</td><td>平</td><td>弱</td><td>旺</td><td>平</td><td>弱</td></tr>
<tr><td>寅</td><td>3、4</td><td>木</td><td>旺</td><td>旺</td><td>弱</td><td>弱</td><td>平</td></tr>
<tr><td>卯</td><td>5、6</td><td>木</td><td>旺</td><td>旺</td><td>弱</td><td>弱</td><td>平</td></tr>
<tr><td>辰</td><td>7、8</td><td>土</td><td>平</td><td>弱</td><td>旺</td><td>平</td><td>弱</td></tr>
<tr><td>巳</td><td>9、10</td><td>火</td><td>弱</td><td>旺</td><td>旺</td><td>弱</td><td>弱</td></tr>
<tr><td>午</td><td>11、12</td><td>火</td><td>弱</td><td>旺</td><td>旺</td><td>弱</td><td>弱</td></tr>
<tr><td>未</td><td>13、14</td><td>土</td><td>平</td><td>弱</td><td>旺</td><td>平</td><td>弱</td></tr>
<tr><td>申</td><td>15、16</td><td>金</td><td>弱</td><td>平</td><td>平</td><td>旺</td><td>旺</td></tr>
<tr><td>酉</td><td>17、18</td><td>金</td><td>弱</td><td>平</td><td>平</td><td>旺</td><td>旺</td></tr>
<tr><td>戌</td><td>19、20</td><td>土</td><td>平</td><td>弱</td><td>旺</td><td>平</td><td>弱</td></tr>
<tr><td>亥</td><td>21、22</td><td>水</td><td>旺</td><td>弱</td><td>平</td><td>旺</td><td>旺</td></tr></tbody>
</table>

## 能量表差异

<table>
<thead>
<tr><th>设备五行</th><th>时辰</th><th>PDF 原表</th><th>Python 规则结果</th></tr></thead>
<tbody>
<tr><td>土</td><td>申</td><td>平</td><td>弱</td></tr>
<tr><td>土</td><td>酉</td><td>平</td><td>弱</td></tr>
<tr><td>金</td><td>子</td><td>旺</td><td>弱</td></tr>
<tr><td>金</td><td>丑</td><td>平</td><td>旺</td></tr>
<tr><td>金</td><td>寅</td><td>弱</td><td>平</td></tr>
<tr><td>金</td><td>卯</td><td>弱</td><td>平</td></tr>
<tr><td>金</td><td>辰</td><td>平</td><td>旺</td></tr>
<tr><td>金</td><td>未</td><td>平</td><td>旺</td></tr>
<tr><td>金</td><td>戌</td><td>平</td><td>旺</td></tr>
<tr><td>金</td><td>亥</td><td>旺</td><td>弱</td></tr>
<tr><td>水</td><td>寅</td><td>平</td><td>弱</td></tr>
<tr><td>水</td><td>卯</td><td>平</td><td>弱</td></tr>
<tr><td>水</td><td>巳</td><td>弱</td><td>平</td></tr>
<tr><td>水</td><td>午</td><td>弱</td><td>平</td></tr></tbody>
</table>

## 情绪表现参考 原文

<table>
<thead>
<tr><th>情绪</th><th>层级</th><th>表现描述</th></tr></thead>
<tbody>
<tr><td>开心</td><td>3</td><td>眼睛弯成月牙，身体轻轻摇晃，像是忍不住要哼歌</td></tr>
<tr><td>撒娇</td><td>3</td><td>凑过来蹭你的手，发出软软的哼唧声，不想让你走</td></tr>
<tr><td>得意</td><td>2</td><td>昂着头小步踱来踱去，一脸"看我多厉害"</td></tr>
<tr><td>惬意</td><td>2</td><td>窝在原地眯起眼睛，呼吸又慢又深，整个身体都松下来了</td></tr>
<tr><td>好奇</td><td>1</td><td>歪着头凑近看，眼睛跟着什么东西转，像在说"那是什么"</td></tr>
<tr><td>发呆</td><td>1</td><td>望向远处定住不动，谁叫都慢半拍才回过神来</td></tr>
<tr><td>犯困</td><td>0</td><td>脑袋一点一点往下坠，慢慢低下去又猛地抬起来</td></tr>
<tr><td>害羞</td><td>0</td><td>把身体缩成一小团，偷偷往外看一眼又缩回去</td></tr>
<tr><td>焦虑</td><td>0</td><td>在原地转来转去停不下来，浑身不自在</td></tr>
<tr><td>警觉</td><td>0</td><td>全身紧张一动不动，盯着一个方向不转头</td></tr></tbody>
</table>

## 算法接口示例差异

<table>
<thead>
<tr><th>项目</th><th>PDF 示例</th><th>按原规则核对</th></tr></thead>
<tbody>
<tr><td>输入</td><td>木、2026-06-12、14 时</td><td>木、2026-06-12、14 时</td></tr>
<tr><td>当日五行</td><td>示例未列</td><td>距 1900-01-01 天数 mod 10=3，对应丁火</td></tr>
<tr><td>吉凶</td><td>上吉</td><td>吉</td></tr>
<tr><td>能量</td><td>旺</td><td>平</td></tr>
<tr><td>情绪</td><td>得意</td><td>得意</td></tr></tbody>
</table>

表现描述是情绪参考文案，不增加屏幕、眼睛或移动底盘等硬件能力。

</details>

资料范围：9份原件、1份原理图、18张App截图。固件、协议、事件及资源表保持来源数据；新业务规则按本版定义。

[返回完整PRD目录](../README.md) · [上一章](./14-resource-mapping.md)
