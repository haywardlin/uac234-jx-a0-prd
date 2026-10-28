# UAC234-JX-A0 完整产品需求

**公开网页，无需登录或下载：**

- [打开完整 PRD](https://haywardlin.github.io/uac234-jx-a0-prd/)
- [打开 App UI/UX 设计说明与可点击原型](https://haywardlin.github.io/uac234-jx-a0-prd/app-uiux.html)

可直接把上面两个网页链接发给同事，电脑和手机均可查看。

在手机上点击下方章节即可阅读。展开折叠明细，左右滑动查看宽表。阅读版保留完整需求和图片，三个成长阶段的反馈表已全部展开。

更新日期：2026-10-28。包含硬件、固件与 App 协议、App UI/UX、情绪算法、成长阶段、交互规则、里程碑与故事、自定义动作、状态流程和资源映射。

## GitHub 分章阅读目录

| 章节 |
|---|
| [01 产品定义与硬件需求](./docs/01-product-hardware.md) |
| [02 固件需求](./docs/02-firmware.md) |
| [03 App通信协议](./docs/03-app-protocol.md) |
| [04 App页面与体验](./docs/04-app-ux.md) |
| [05 情绪算法与五维性格](./docs/05-emotion.md) |
| [06 五维成长与阶段](./docs/06-growth.md) |
| [07 三个阶段的交互反馈](./docs/07-stage-feedback.md) |
| [08 App查询、下发与生效](./docs/08-sync.md) |
| [09 里程碑](./docs/09-milestones.md) |
| [10 故事与内容模板](./docs/10-stories.md) |
| [11 App自定义动作与舵机](./docs/11-custom-actions.md) |
| [12 输入输出交互矩阵](./docs/12-interaction-matrix.md) |
| [13 状态与功能流程](./docs/13-state-flows.md) |
| [14 资源映射与演示闭环](./docs/14-resource-mapping.md) |
| [15 资料依据与待补项](./docs/15-sources-gaps.md) |
| [16 App设计交接补充：23页功能与交互说明](./docs/16-app-uiux.md) |

## 完整文件

- [Excel 需求表（16 个 Sheet）](./UAC234-JX-A0_PRD.xlsx)
- [HTML 可视化版：在线浏览](https://haywardlin.github.io/uac234-jx-a0-prd/) / [源文件与下载](./index.html)
- [App UI/UX：在线浏览](https://haywardlin.github.io/uac234-jx-a0-prd/app-uiux.html) / [源文件与下载](./app-uiux.html)

推荐使用顶部网页链接查看原排版、筛选和交互原型。分章 Markdown 可在仓库内直接阅读；仓库文件列表中的 HTML 仍显示为源文件。

## 版本与待补项

硬件、固件及源协议依据现有资料；成长、里程碑、故事和自定义动作采用本版定义。HTML 和 Excel 中的红字在手机阅读版中以“【待补/待确认】”标识。原始资料文件仍保留在本地项目，仓库包含需求正文及正文所引用的图片。

资料核对不等于 App、固件和实机联调完成。电池与外设参数、资源实物及播放时长、可靠事件批次、首次激活、更新状态回读和自定义动作接口仍须补齐。


App设计交接为2026-10-28新增补充：23个主页面、4个子页面、7条核心流程。未改写情绪算法或成长阈值；原型使用示例数据，未连接真实设备。


2026-10-28动作编排修订：先选择一个触摸、IMU轻摇、唤醒或光感变亮事件，再编排“左右摇头5次 → 上下点头2次”等步骤。保存草稿与启用到设备分开；原型演示不代表原子动作资源和新增序列接口已经实机实现。
