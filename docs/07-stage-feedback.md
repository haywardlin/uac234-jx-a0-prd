# 07 三个阶段的交互反馈

[返回完整PRD目录](../README.md) · [上一章](./06-growth.md) · [下一章](./08-sync.md)

事件ID保持1–42；每次只抽取一套动作、音频、震动组合。

<table>
<thead>
<tr><th>情绪ID</th><th>分组</th><th>具体情绪与匹配含义</th></tr></thead>
<tbody>
<tr><td rowspan="1">0</td><td rowspan="1">ANY</td><td rowspan="1">ANY；适用于任何情绪。适用于任何情绪；规则通配条件，不是设备的第四种实际情绪</td></tr>
<tr><td rowspan="1">1</td><td rowspan="1">开心</td><td rowspan="1">HAPPY / CLINGY / PROUD / COZY；开心 / 黏人 / 得意 / 惬意。同组具体情绪共用同一组反馈候选与概率</td></tr>
<tr><td rowspan="1">2</td><td rowspan="1">平静</td><td rowspan="1">CURIOUS / SPACED；好奇 / 发呆。同组具体情绪共用同一组反馈候选与概率</td></tr>
<tr><td rowspan="1">3</td><td rowspan="1">悲伤</td><td rowspan="1">SLEEPY / RESTLESS / ALERT / SHY；困倦 / 躁动 / 警觉 / 害羞。同组具体情绪共用同一组反馈候选与概率</td></tr></tbody>
</table>

每个阶段覆盖原42个事件和3个情绪组；固定反馈使用0 ANY。具体情绪只用于归组，同组共用候选与概率。例如“得意”和“惬意”都按ID 1查同一组；充电、低电等固定反馈按ANY匹配。默认只启用资料中18个Beta Y事件；预留及划除事件保留定义，不自动开放。

权重对同一组候选合计100%；一行是一整套输出。

## 初识 102组候选条件

<table>
<thead>
<tr><th>事件ID</th><th>输入</th><th>启用</th><th>情绪ID / 分组</th><th>概率</th><th>动作ID</th><th>动作反馈</th><th>音频ID</th><th>伴音含义</th><th>震动ID</th><th>强度</th></tr></thead>
<tbody>
<tr><td rowspan="6">1</td><td rowspan="6">头顶轻触</td><td rowspan="6">Beta Y</td><td rowspan="2">1｜开心</td><td rowspan="1">65%</td><td rowspan="1">12</td><td rowspan="1">正式的点头（抬头低头）</td><td rowspan="1">11</td><td rowspan="1">表示认同、愿意配合；轻松的肯定；互动中的“好呀”式回应。</td><td rowspan="1">1</td><td rowspan="1">弱</td></tr>
<tr><td rowspan="1">35%</td><td rowspan="2">18</td><td rowspan="2">单次轻触缓慢抬头观察</td><td rowspan="2">17</td><td rowspan="2">软萌、轻微惊喜偏正向；轻碰或被注意到后的柔和回应。</td><td rowspan="3">0</td><td rowspan="3">关闭</td></tr>
<tr><td rowspan="2">2｜平静</td><td rowspan="1">55%</td></tr>
<tr><td rowspan="1">45%</td><td rowspan="2">16</td><td rowspan="2">突发触碰单次躲闪</td><td rowspan="1">31</td><td rowspan="1">惊吓或不安后的缓和；从紧张回到可互动；带一点不好意思的恢复声。</td></tr>
<tr><td rowspan="2">3｜悲伤</td><td rowspan="1">85%</td><td rowspan="1">15</td><td rowspan="1">不安、紧绷时的短反馈；安全感下降。</td><td rowspan="1">1</td><td rowspan="1">弱</td></tr>
<tr><td rowspan="1">15%</td><td rowspan="1">14</td><td rowspan="1">低头躲闪</td><td rowspan="1">13</td><td rowspan="1">略显腼腆、想躲一下；还不习惯被关注；害羞偏警觉的轻声。</td><td rowspan="1">0</td><td rowspan="1">关闭</td></tr>
<tr><td rowspan="6">2</td><td rowspan="6">头顶短抚</td><td rowspan="12">预留 Beta N</td><td rowspan="2">1｜开心</td><td rowspan="1">65%</td><td rowspan="1">12</td><td rowspan="1">正式的点头（抬头低头）</td><td rowspan="1">48</td><td rowspan="1">认同点头的第二条；轻松肯定；中等力度的配合感。</td><td rowspan="1">1</td><td rowspan="1">弱</td></tr>
<tr><td rowspan="1">35%</td><td rowspan="2">18</td><td rowspan="2">单次轻触缓慢抬头观察</td><td rowspan="2">17</td><td rowspan="2">软萌、轻微惊喜偏正向；轻碰或被注意到后的柔和回应。</td><td rowspan="3">0</td><td rowspan="3">关闭</td></tr>
<tr><td rowspan="2">2｜平静</td><td rowspan="1">55%</td></tr>
<tr><td rowspan="1">45%</td><td rowspan="1">16</td><td rowspan="1">突发触碰单次躲闪</td><td rowspan="1">31</td><td rowspan="1">惊吓或不安后的缓和；从紧张回到可互动；带一点不好意思的恢复声。</td></tr>
<tr><td rowspan="2">3｜悲伤</td><td rowspan="1">85%</td><td rowspan="1">25</td><td rowspan="1">快速撸过度刺激躲闪</td><td rowspan="1">15</td><td rowspan="1">不安、紧绷时的短反馈；安全感下降。</td><td rowspan="1">1</td><td rowspan="1">弱</td></tr>
<tr><td rowspan="1">15%</td><td rowspan="1">14</td><td rowspan="1">低头躲闪</td><td rowspan="1">13</td><td rowspan="1">略显腼腆、想躲一下；还不习惯被关注；害羞偏警觉的轻声。</td><td rowspan="1">0</td><td rowspan="1">关闭</td></tr>
<tr><td rowspan="6">3</td><td rowspan="6">头顶长抚</td><td rowspan="2">1｜开心</td><td rowspan="1">65%</td><td rowspan="1">12</td><td rowspan="1">正式的点头（抬头低头）</td><td rowspan="1">11</td><td rowspan="1">表示认同、愿意配合；轻松的肯定；互动中的“好呀”式回应。</td><td rowspan="1">1</td><td rowspan="1">弱</td></tr>
<tr><td rowspan="1">35%</td><td rowspan="2">18</td><td rowspan="2">单次轻触缓慢抬头观察</td><td rowspan="2">17</td><td rowspan="2">软萌、轻微惊喜偏正向；轻碰或被注意到后的柔和回应。</td><td rowspan="3">0</td><td rowspan="3">关闭</td></tr>
<tr><td rowspan="2">2｜平静</td><td rowspan="1">55%</td></tr>
<tr><td rowspan="1">45%</td><td rowspan="2">16</td><td rowspan="2">突发触碰单次躲闪</td><td rowspan="1">31</td><td rowspan="1">惊吓或不安后的缓和；从紧张回到可互动；带一点不好意思的恢复声。</td></tr>
<tr><td rowspan="2">3｜悲伤</td><td rowspan="1">85%</td><td rowspan="1">15</td><td rowspan="1">不安、紧绷时的短反馈；安全感下降。</td><td rowspan="1">1</td><td rowspan="1">弱</td></tr>
<tr><td rowspan="1">15%</td><td rowspan="1">14</td><td rowspan="1">低头躲闪</td><td rowspan="1">13</td><td rowspan="1">略显腼腆、想躲一下；还不习惯被关注；害羞偏警觉的轻声。</td><td rowspan="1">0</td><td rowspan="1">关闭</td></tr>
<tr><td rowspan="6">4</td><td rowspan="6">头左轻触</td><td rowspan="6">Beta Y</td><td rowspan="2">1｜开心</td><td rowspan="1">65%</td><td rowspan="1">12</td><td rowspan="1">正式的点头（抬头低头）</td><td rowspan="1">11</td><td rowspan="1">表示认同、愿意配合；轻松的肯定；互动中的“好呀”式回应。</td><td rowspan="1">1</td><td rowspan="1">弱</td></tr>
<tr><td rowspan="1">35%</td><td rowspan="1">18</td><td rowspan="1">单次轻触缓慢抬头观察</td><td rowspan="1">17</td><td rowspan="1">软萌、轻微惊喜偏正向；轻碰或被注意到后的柔和回应。</td><td rowspan="3">0</td><td rowspan="3">关闭</td></tr>
<tr><td rowspan="2">2｜平静</td><td rowspan="1">55%</td><td rowspan="1">35</td><td rowspan="1">单侧轻碰侧低头躲闪（摸头左）</td><td rowspan="1">16</td><td rowspan="1">距离突然很近；害羞又好奇；亲昵但还放不开。</td></tr>
<tr><td rowspan="1">45%</td><td rowspan="2">16</td><td rowspan="2">突发触碰单次躲闪</td><td rowspan="1">31</td><td rowspan="1">惊吓或不安后的缓和；从紧张回到可互动；带一点不好意思的恢复声。</td></tr>
<tr><td rowspan="2">3｜悲伤</td><td rowspan="1">85%</td><td rowspan="1">15</td><td rowspan="1">不安、紧绷时的短反馈；安全感下降。</td><td rowspan="1">1</td><td rowspan="1">弱</td></tr>
<tr><td rowspan="1">15%</td><td rowspan="1">18</td><td rowspan="1">单次轻触缓慢抬头观察</td><td rowspan="1">13</td><td rowspan="1">略显腼腆、想躲一下；还不习惯被关注；害羞偏警觉的轻声。</td><td rowspan="1">0</td><td rowspan="1">关闭</td></tr>
<tr><td rowspan="6">5</td><td rowspan="6">头左短抚</td><td rowspan="12">预留 Beta N</td><td rowspan="2">1｜开心</td><td rowspan="1">65%</td><td rowspan="1">12</td><td rowspan="1">正式的点头（抬头低头）</td><td rowspan="1">48</td><td rowspan="1">认同点头的第二条；轻松肯定；中等力度的配合感。</td><td rowspan="1">1</td><td rowspan="1">弱</td></tr>
<tr><td rowspan="1">35%</td><td rowspan="1">18</td><td rowspan="1">单次轻触缓慢抬头观察</td><td rowspan="1">17</td><td rowspan="1">软萌、轻微惊喜偏正向；轻碰或被注意到后的柔和回应。</td><td rowspan="3">0</td><td rowspan="3">关闭</td></tr>
<tr><td rowspan="2">2｜平静</td><td rowspan="1">55%</td><td rowspan="1">35</td><td rowspan="1">单侧轻碰侧低头躲闪（摸头左）</td><td rowspan="1">16</td><td rowspan="1">距离突然很近；害羞又好奇；亲昵但还放不开。</td></tr>
<tr><td rowspan="1">45%</td><td rowspan="1">16</td><td rowspan="1">突发触碰单次躲闪</td><td rowspan="1">31</td><td rowspan="1">惊吓或不安后的缓和；从紧张回到可互动；带一点不好意思的恢复声。</td></tr>
<tr><td rowspan="2">3｜悲伤</td><td rowspan="1">85%</td><td rowspan="1">25</td><td rowspan="1">快速撸过度刺激躲闪</td><td rowspan="1">15</td><td rowspan="1">不安、紧绷时的短反馈；安全感下降。</td><td rowspan="1">1</td><td rowspan="1">弱</td></tr>
<tr><td rowspan="1">15%</td><td rowspan="1">18</td><td rowspan="1">单次轻触缓慢抬头观察</td><td rowspan="1">13</td><td rowspan="1">略显腼腆、想躲一下；还不习惯被关注；害羞偏警觉的轻声。</td><td rowspan="1">0</td><td rowspan="1">关闭</td></tr>
<tr><td rowspan="6">6</td><td rowspan="6">头左长抚</td><td rowspan="2">1｜开心</td><td rowspan="1">65%</td><td rowspan="1">12</td><td rowspan="1">正式的点头（抬头低头）</td><td rowspan="1">11</td><td rowspan="1">表示认同、愿意配合；轻松的肯定；互动中的“好呀”式回应。</td><td rowspan="1">1</td><td rowspan="1">弱</td></tr>
<tr><td rowspan="1">35%</td><td rowspan="1">18</td><td rowspan="1">单次轻触缓慢抬头观察</td><td rowspan="1">17</td><td rowspan="1">软萌、轻微惊喜偏正向；轻碰或被注意到后的柔和回应。</td><td rowspan="3">0</td><td rowspan="3">关闭</td></tr>
<tr><td rowspan="2">2｜平静</td><td rowspan="1">55%</td><td rowspan="1">35</td><td rowspan="1">单侧轻碰侧低头躲闪（摸头左）</td><td rowspan="1">16</td><td rowspan="1">距离突然很近；害羞又好奇；亲昵但还放不开。</td></tr>
<tr><td rowspan="1">45%</td><td rowspan="2">16</td><td rowspan="2">突发触碰单次躲闪</td><td rowspan="1">31</td><td rowspan="1">惊吓或不安后的缓和；从紧张回到可互动；带一点不好意思的恢复声。</td></tr>
<tr><td rowspan="2">3｜悲伤</td><td rowspan="1">85%</td><td rowspan="1">15</td><td rowspan="1">不安、紧绷时的短反馈；安全感下降。</td><td rowspan="1">1</td><td rowspan="1">弱</td></tr>
<tr><td rowspan="1">15%</td><td rowspan="1">18</td><td rowspan="1">单次轻触缓慢抬头观察</td><td rowspan="1">13</td><td rowspan="1">略显腼腆、想躲一下；还不习惯被关注；害羞偏警觉的轻声。</td><td rowspan="1">0</td><td rowspan="1">关闭</td></tr>
<tr><td rowspan="6">7</td><td rowspan="6">头右轻触</td><td rowspan="6">Beta Y</td><td rowspan="2">1｜开心</td><td rowspan="1">65%</td><td rowspan="1">12</td><td rowspan="1">正式的点头（抬头低头）</td><td rowspan="1">11</td><td rowspan="1">表示认同、愿意配合；轻松的肯定；互动中的“好呀”式回应。</td><td rowspan="1">1</td><td rowspan="1">弱</td></tr>
<tr><td rowspan="1">35%</td><td rowspan="1">18</td><td rowspan="1">单次轻触缓慢抬头观察</td><td rowspan="1">17</td><td rowspan="1">软萌、轻微惊喜偏正向；轻碰或被注意到后的柔和回应。</td><td rowspan="3">0</td><td rowspan="3">关闭</td></tr>
<tr><td rowspan="2">2｜平静</td><td rowspan="1">55%</td><td rowspan="1">38</td><td rowspan="1">单侧轻碰侧低头躲闪（摸头右）</td><td rowspan="1">30</td><td rowspan="1">害羞躲闪的变体；慢慢适应被关注；比上一条略软一点。</td></tr>
<tr><td rowspan="1">45%</td><td rowspan="2">16</td><td rowspan="2">突发触碰单次躲闪</td><td rowspan="1">31</td><td rowspan="1">惊吓或不安后的缓和；从紧张回到可互动；带一点不好意思的恢复声。</td></tr>
<tr><td rowspan="2">3｜悲伤</td><td rowspan="1">85%</td><td rowspan="1">15</td><td rowspan="1">不安、紧绷时的短反馈；安全感下降。</td><td rowspan="1">1</td><td rowspan="1">弱</td></tr>
<tr><td rowspan="1">15%</td><td rowspan="1">18</td><td rowspan="1">单次轻触缓慢抬头观察</td><td rowspan="1">13</td><td rowspan="1">略显腼腆、想躲一下；还不习惯被关注；害羞偏警觉的轻声。</td><td rowspan="1">0</td><td rowspan="1">关闭</td></tr>
<tr><td rowspan="6">8</td><td rowspan="6">头右短抚</td><td rowspan="12">预留 Beta N</td><td rowspan="2">1｜开心</td><td rowspan="1">65%</td><td rowspan="1">12</td><td rowspan="1">正式的点头（抬头低头）</td><td rowspan="1">48</td><td rowspan="1">认同点头的第二条；轻松肯定；中等力度的配合感。</td><td rowspan="1">1</td><td rowspan="1">弱</td></tr>
<tr><td rowspan="1">35%</td><td rowspan="1">18</td><td rowspan="1">单次轻触缓慢抬头观察</td><td rowspan="1">17</td><td rowspan="1">软萌、轻微惊喜偏正向；轻碰或被注意到后的柔和回应。</td><td rowspan="3">0</td><td rowspan="3">关闭</td></tr>
<tr><td rowspan="2">2｜平静</td><td rowspan="1">55%</td><td rowspan="1">38</td><td rowspan="1">单侧轻碰侧低头躲闪（摸头右）</td><td rowspan="1">30</td><td rowspan="1">害羞躲闪的变体；慢慢适应被关注；比上一条略软一点。</td></tr>
<tr><td rowspan="1">45%</td><td rowspan="1">16</td><td rowspan="1">突发触碰单次躲闪</td><td rowspan="1">31</td><td rowspan="1">惊吓或不安后的缓和；从紧张回到可互动；带一点不好意思的恢复声。</td></tr>
<tr><td rowspan="2">3｜悲伤</td><td rowspan="1">85%</td><td rowspan="1">25</td><td rowspan="1">快速撸过度刺激躲闪</td><td rowspan="1">15</td><td rowspan="1">不安、紧绷时的短反馈；安全感下降。</td><td rowspan="1">1</td><td rowspan="1">弱</td></tr>
<tr><td rowspan="1">15%</td><td rowspan="1">18</td><td rowspan="1">单次轻触缓慢抬头观察</td><td rowspan="1">13</td><td rowspan="1">略显腼腆、想躲一下；还不习惯被关注；害羞偏警觉的轻声。</td><td rowspan="1">0</td><td rowspan="1">关闭</td></tr>
<tr><td rowspan="6">9</td><td rowspan="6">头右长抚</td><td rowspan="2">1｜开心</td><td rowspan="1">65%</td><td rowspan="1">12</td><td rowspan="1">正式的点头（抬头低头）</td><td rowspan="1">11</td><td rowspan="1">表示认同、愿意配合；轻松的肯定；互动中的“好呀”式回应。</td><td rowspan="1">1</td><td rowspan="1">弱</td></tr>
<tr><td rowspan="1">35%</td><td rowspan="1">18</td><td rowspan="1">单次轻触缓慢抬头观察</td><td rowspan="1">17</td><td rowspan="1">软萌、轻微惊喜偏正向；轻碰或被注意到后的柔和回应。</td><td rowspan="3">0</td><td rowspan="3">关闭</td></tr>
<tr><td rowspan="2">2｜平静</td><td rowspan="1">55%</td><td rowspan="1">38</td><td rowspan="1">单侧轻碰侧低头躲闪（摸头右）</td><td rowspan="1">30</td><td rowspan="1">害羞躲闪的变体；慢慢适应被关注；比上一条略软一点。</td></tr>
<tr><td rowspan="1">45%</td><td rowspan="2">16</td><td rowspan="2">突发触碰单次躲闪</td><td rowspan="1">31</td><td rowspan="1">惊吓或不安后的缓和；从紧张回到可互动；带一点不好意思的恢复声。</td></tr>
<tr><td rowspan="2">3｜悲伤</td><td rowspan="1">85%</td><td rowspan="1">15</td><td rowspan="1">不安、紧绷时的短反馈；安全感下降。</td><td rowspan="1">1</td><td rowspan="1">弱</td></tr>
<tr><td rowspan="1">15%</td><td rowspan="1">18</td><td rowspan="1">单次轻触缓慢抬头观察</td><td rowspan="1">13</td><td rowspan="1">略显腼腆、想躲一下；还不习惯被关注；害羞偏警觉的轻声。</td><td rowspan="1">0</td><td rowspan="1">关闭</td></tr>
<tr><td rowspan="6">10</td><td rowspan="6">腹部轻触</td><td rowspan="6">Beta Y</td><td rowspan="2">1｜开心</td><td rowspan="1">65%</td><td rowspan="1">12</td><td rowspan="1">正式的点头（抬头低头）</td><td rowspan="1">11</td><td rowspan="1">表示认同、愿意配合；轻松的肯定；互动中的“好呀”式回应。</td><td rowspan="1">1</td><td rowspan="1">弱</td></tr>
<tr><td rowspan="1">35%</td><td rowspan="1">18</td><td rowspan="1">单次轻触缓慢抬头观察</td><td rowspan="1">17</td><td rowspan="1">软萌、轻微惊喜偏正向；轻碰或被注意到后的柔和回应。</td><td rowspan="3">0</td><td rowspan="3">关闭</td></tr>
<tr><td rowspan="2">2｜平静</td><td rowspan="1">55%</td><td rowspan="1">20</td><td rowspan="1">肚子轻垂头软动（摸肚子专属）</td><td rowspan="1">19</td><td rowspan="1">高信任下的深度放松；完全卸下防备；绵长、温暖的安心声。</td></tr>
<tr><td rowspan="1">45%</td><td rowspan="2">16</td><td rowspan="2">突发触碰单次躲闪</td><td rowspan="1">31</td><td rowspan="1">惊吓或不安后的缓和；从紧张回到可互动；带一点不好意思的恢复声。</td></tr>
<tr><td rowspan="2">3｜悲伤</td><td rowspan="1">85%</td><td rowspan="1">15</td><td rowspan="1">不安、紧绷时的短反馈；安全感下降。</td><td rowspan="1">1</td><td rowspan="1">弱</td></tr>
<tr><td rowspan="1">15%</td><td rowspan="1">18</td><td rowspan="1">单次轻触缓慢抬头观察</td><td rowspan="1">13</td><td rowspan="1">略显腼腆、想躲一下；还不习惯被关注；害羞偏警觉的轻声。</td><td rowspan="1">0</td><td rowspan="1">关闭</td></tr>
<tr><td rowspan="6">11</td><td rowspan="6">腹部短抚</td><td rowspan="12">预留 Beta N</td><td rowspan="2">1｜开心</td><td rowspan="1">65%</td><td rowspan="1">12</td><td rowspan="1">正式的点头（抬头低头）</td><td rowspan="1">48</td><td rowspan="1">认同点头的第二条；轻松肯定；中等力度的配合感。</td><td rowspan="1">1</td><td rowspan="1">弱</td></tr>
<tr><td rowspan="1">35%</td><td rowspan="1">18</td><td rowspan="1">单次轻触缓慢抬头观察</td><td rowspan="1">17</td><td rowspan="1">软萌、轻微惊喜偏正向；轻碰或被注意到后的柔和回应。</td><td rowspan="3">0</td><td rowspan="3">关闭</td></tr>
<tr><td rowspan="2">2｜平静</td><td rowspan="1">55%</td><td rowspan="1">20</td><td rowspan="1">肚子轻垂头软动（摸肚子专属）</td><td rowspan="1">19</td><td rowspan="1">高信任下的深度放松；完全卸下防备；绵长、温暖的安心声。</td></tr>
<tr><td rowspan="1">45%</td><td rowspan="1">16</td><td rowspan="1">突发触碰单次躲闪</td><td rowspan="1">31</td><td rowspan="1">惊吓或不安后的缓和；从紧张回到可互动；带一点不好意思的恢复声。</td></tr>
<tr><td rowspan="2">3｜悲伤</td><td rowspan="1">85%</td><td rowspan="1">25</td><td rowspan="1">快速撸过度刺激躲闪</td><td rowspan="1">15</td><td rowspan="1">不安、紧绷时的短反馈；安全感下降。</td><td rowspan="1">1</td><td rowspan="1">弱</td></tr>
<tr><td rowspan="1">15%</td><td rowspan="1">18</td><td rowspan="1">单次轻触缓慢抬头观察</td><td rowspan="1">13</td><td rowspan="1">略显腼腆、想躲一下；还不习惯被关注；害羞偏警觉的轻声。</td><td rowspan="1">0</td><td rowspan="1">关闭</td></tr>
<tr><td rowspan="6">12</td><td rowspan="6">腹部长抚</td><td rowspan="2">1｜开心</td><td rowspan="1">65%</td><td rowspan="1">12</td><td rowspan="1">正式的点头（抬头低头）</td><td rowspan="1">11</td><td rowspan="1">表示认同、愿意配合；轻松的肯定；互动中的“好呀”式回应。</td><td rowspan="1">1</td><td rowspan="1">弱</td></tr>
<tr><td rowspan="1">35%</td><td rowspan="1">18</td><td rowspan="1">单次轻触缓慢抬头观察</td><td rowspan="1">17</td><td rowspan="1">软萌、轻微惊喜偏正向；轻碰或被注意到后的柔和回应。</td><td rowspan="3">0</td><td rowspan="3">关闭</td></tr>
<tr><td rowspan="2">2｜平静</td><td rowspan="1">55%</td><td rowspan="1">20</td><td rowspan="1">肚子轻垂头软动（摸肚子专属）</td><td rowspan="1">19</td><td rowspan="1">高信任下的深度放松；完全卸下防备；绵长、温暖的安心声。</td></tr>
<tr><td rowspan="1">45%</td><td rowspan="2">16</td><td rowspan="2">突发触碰单次躲闪</td><td rowspan="1">31</td><td rowspan="1">惊吓或不安后的缓和；从紧张回到可互动；带一点不好意思的恢复声。</td></tr>
<tr><td rowspan="2">3｜悲伤</td><td rowspan="1">85%</td><td rowspan="1">15</td><td rowspan="1">不安、紧绷时的短反馈；安全感下降。</td><td rowspan="1">1</td><td rowspan="1">弱</td></tr>
<tr><td rowspan="1">15%</td><td rowspan="1">18</td><td rowspan="1">单次轻触缓慢抬头观察</td><td rowspan="1">13</td><td rowspan="1">略显腼腆、想躲一下；还不习惯被关注；害羞偏警觉的轻声。</td><td rowspan="1">0</td><td rowspan="1">关闭</td></tr>
<tr><td rowspan="6">13</td><td rowspan="6">左侧轻触</td><td rowspan="6">Beta Y</td><td rowspan="2">1｜开心</td><td rowspan="1">65%</td><td rowspan="1">12</td><td rowspan="1">正式的点头（抬头低头）</td><td rowspan="1">11</td><td rowspan="1">表示认同、愿意配合；轻松的肯定；互动中的“好呀”式回应。</td><td rowspan="1">1</td><td rowspan="1">弱</td></tr>
<tr><td rowspan="1">35%</td><td rowspan="2">18</td><td rowspan="2">单次轻触缓慢抬头观察</td><td rowspan="2">17</td><td rowspan="2">软萌、轻微惊喜偏正向；轻碰或被注意到后的柔和回应。</td><td rowspan="3">0</td><td rowspan="3">关闭</td></tr>
<tr><td rowspan="2">2｜平静</td><td rowspan="1">55%</td></tr>
<tr><td rowspan="1">45%</td><td rowspan="2">16</td><td rowspan="2">突发触碰单次躲闪</td><td rowspan="1">31</td><td rowspan="1">惊吓或不安后的缓和；从紧张回到可互动；带一点不好意思的恢复声。</td></tr>
<tr><td rowspan="2">3｜悲伤</td><td rowspan="1">85%</td><td rowspan="1">15</td><td rowspan="1">不安、紧绷时的短反馈；安全感下降。</td><td rowspan="1">1</td><td rowspan="1">弱</td></tr>
<tr><td rowspan="1">15%</td><td rowspan="1">18</td><td rowspan="1">单次轻触缓慢抬头观察</td><td rowspan="1">13</td><td rowspan="1">略显腼腆、想躲一下；还不习惯被关注；害羞偏警觉的轻声。</td><td rowspan="1">0</td><td rowspan="1">关闭</td></tr>
<tr><td rowspan="6">14</td><td rowspan="6">左侧短抚</td><td rowspan="12">预留 Beta N</td><td rowspan="2">1｜开心</td><td rowspan="1">65%</td><td rowspan="1">12</td><td rowspan="1">正式的点头（抬头低头）</td><td rowspan="1">48</td><td rowspan="1">认同点头的第二条；轻松肯定；中等力度的配合感。</td><td rowspan="1">1</td><td rowspan="1">弱</td></tr>
<tr><td rowspan="1">35%</td><td rowspan="2">18</td><td rowspan="2">单次轻触缓慢抬头观察</td><td rowspan="2">17</td><td rowspan="2">软萌、轻微惊喜偏正向；轻碰或被注意到后的柔和回应。</td><td rowspan="3">0</td><td rowspan="3">关闭</td></tr>
<tr><td rowspan="2">2｜平静</td><td rowspan="1">55%</td></tr>
<tr><td rowspan="1">45%</td><td rowspan="1">16</td><td rowspan="1">突发触碰单次躲闪</td><td rowspan="1">31</td><td rowspan="1">惊吓或不安后的缓和；从紧张回到可互动；带一点不好意思的恢复声。</td></tr>
<tr><td rowspan="2">3｜悲伤</td><td rowspan="1">85%</td><td rowspan="1">25</td><td rowspan="1">快速撸过度刺激躲闪</td><td rowspan="1">15</td><td rowspan="1">不安、紧绷时的短反馈；安全感下降。</td><td rowspan="1">1</td><td rowspan="1">弱</td></tr>
<tr><td rowspan="1">15%</td><td rowspan="1">18</td><td rowspan="1">单次轻触缓慢抬头观察</td><td rowspan="1">13</td><td rowspan="1">略显腼腆、想躲一下；还不习惯被关注；害羞偏警觉的轻声。</td><td rowspan="1">0</td><td rowspan="1">关闭</td></tr>
<tr><td rowspan="6">15</td><td rowspan="6">左侧长抚</td><td rowspan="2">1｜开心</td><td rowspan="1">65%</td><td rowspan="1">12</td><td rowspan="1">正式的点头（抬头低头）</td><td rowspan="1">11</td><td rowspan="1">表示认同、愿意配合；轻松的肯定；互动中的“好呀”式回应。</td><td rowspan="1">1</td><td rowspan="1">弱</td></tr>
<tr><td rowspan="1">35%</td><td rowspan="2">18</td><td rowspan="2">单次轻触缓慢抬头观察</td><td rowspan="2">17</td><td rowspan="2">软萌、轻微惊喜偏正向；轻碰或被注意到后的柔和回应。</td><td rowspan="3">0</td><td rowspan="3">关闭</td></tr>
<tr><td rowspan="2">2｜平静</td><td rowspan="1">55%</td></tr>
<tr><td rowspan="1">45%</td><td rowspan="2">16</td><td rowspan="2">突发触碰单次躲闪</td><td rowspan="1">31</td><td rowspan="1">惊吓或不安后的缓和；从紧张回到可互动；带一点不好意思的恢复声。</td></tr>
<tr><td rowspan="2">3｜悲伤</td><td rowspan="1">85%</td><td rowspan="1">15</td><td rowspan="1">不安、紧绷时的短反馈；安全感下降。</td><td rowspan="1">1</td><td rowspan="1">弱</td></tr>
<tr><td rowspan="1">15%</td><td rowspan="1">18</td><td rowspan="1">单次轻触缓慢抬头观察</td><td rowspan="1">13</td><td rowspan="1">略显腼腆、想躲一下；还不习惯被关注；害羞偏警觉的轻声。</td><td rowspan="1">0</td><td rowspan="1">关闭</td></tr>
<tr><td rowspan="6">16</td><td rowspan="6">右侧轻触</td><td rowspan="6">Beta Y</td><td rowspan="2">1｜开心</td><td rowspan="1">65%</td><td rowspan="1">12</td><td rowspan="1">正式的点头（抬头低头）</td><td rowspan="1">11</td><td rowspan="1">表示认同、愿意配合；轻松的肯定；互动中的“好呀”式回应。</td><td rowspan="1">1</td><td rowspan="1">弱</td></tr>
<tr><td rowspan="1">35%</td><td rowspan="2">18</td><td rowspan="2">单次轻触缓慢抬头观察</td><td rowspan="2">17</td><td rowspan="2">软萌、轻微惊喜偏正向；轻碰或被注意到后的柔和回应。</td><td rowspan="3">0</td><td rowspan="3">关闭</td></tr>
<tr><td rowspan="2">2｜平静</td><td rowspan="1">55%</td></tr>
<tr><td rowspan="1">45%</td><td rowspan="2">16</td><td rowspan="2">突发触碰单次躲闪</td><td rowspan="1">31</td><td rowspan="1">惊吓或不安后的缓和；从紧张回到可互动；带一点不好意思的恢复声。</td></tr>
<tr><td rowspan="2">3｜悲伤</td><td rowspan="1">85%</td><td rowspan="1">15</td><td rowspan="1">不安、紧绷时的短反馈；安全感下降。</td><td rowspan="1">1</td><td rowspan="1">弱</td></tr>
<tr><td rowspan="1">15%</td><td rowspan="1">18</td><td rowspan="1">单次轻触缓慢抬头观察</td><td rowspan="1">13</td><td rowspan="1">略显腼腆、想躲一下；还不习惯被关注；害羞偏警觉的轻声。</td><td rowspan="1">0</td><td rowspan="1">关闭</td></tr>
<tr><td rowspan="6">17</td><td rowspan="6">右侧短抚</td><td rowspan="12">预留 Beta N</td><td rowspan="2">1｜开心</td><td rowspan="1">65%</td><td rowspan="1">12</td><td rowspan="1">正式的点头（抬头低头）</td><td rowspan="1">48</td><td rowspan="1">认同点头的第二条；轻松肯定；中等力度的配合感。</td><td rowspan="1">1</td><td rowspan="1">弱</td></tr>
<tr><td rowspan="1">35%</td><td rowspan="2">18</td><td rowspan="2">单次轻触缓慢抬头观察</td><td rowspan="2">17</td><td rowspan="2">软萌、轻微惊喜偏正向；轻碰或被注意到后的柔和回应。</td><td rowspan="3">0</td><td rowspan="3">关闭</td></tr>
<tr><td rowspan="2">2｜平静</td><td rowspan="1">55%</td></tr>
<tr><td rowspan="1">45%</td><td rowspan="1">16</td><td rowspan="1">突发触碰单次躲闪</td><td rowspan="1">31</td><td rowspan="1">惊吓或不安后的缓和；从紧张回到可互动；带一点不好意思的恢复声。</td></tr>
<tr><td rowspan="2">3｜悲伤</td><td rowspan="1">85%</td><td rowspan="1">25</td><td rowspan="1">快速撸过度刺激躲闪</td><td rowspan="1">15</td><td rowspan="1">不安、紧绷时的短反馈；安全感下降。</td><td rowspan="1">1</td><td rowspan="1">弱</td></tr>
<tr><td rowspan="1">15%</td><td rowspan="1">18</td><td rowspan="1">单次轻触缓慢抬头观察</td><td rowspan="1">13</td><td rowspan="1">略显腼腆、想躲一下；还不习惯被关注；害羞偏警觉的轻声。</td><td rowspan="1">0</td><td rowspan="1">关闭</td></tr>
<tr><td rowspan="6">18</td><td rowspan="6">右侧长抚</td><td rowspan="2">1｜开心</td><td rowspan="1">65%</td><td rowspan="1">12</td><td rowspan="1">正式的点头（抬头低头）</td><td rowspan="1">11</td><td rowspan="1">表示认同、愿意配合；轻松的肯定；互动中的“好呀”式回应。</td><td rowspan="1">1</td><td rowspan="1">弱</td></tr>
<tr><td rowspan="1">35%</td><td rowspan="2">18</td><td rowspan="2">单次轻触缓慢抬头观察</td><td rowspan="2">17</td><td rowspan="2">软萌、轻微惊喜偏正向；轻碰或被注意到后的柔和回应。</td><td rowspan="3">0</td><td rowspan="3">关闭</td></tr>
<tr><td rowspan="2">2｜平静</td><td rowspan="1">55%</td></tr>
<tr><td rowspan="1">45%</td><td rowspan="2">16</td><td rowspan="2">突发触碰单次躲闪</td><td rowspan="1">31</td><td rowspan="1">惊吓或不安后的缓和；从紧张回到可互动；带一点不好意思的恢复声。</td></tr>
<tr><td rowspan="2">3｜悲伤</td><td rowspan="1">85%</td><td rowspan="1">15</td><td rowspan="1">不安、紧绷时的短反馈；安全感下降。</td><td rowspan="1">1</td><td rowspan="1">弱</td></tr>
<tr><td rowspan="1">15%</td><td rowspan="1">18</td><td rowspan="1">单次轻触缓慢抬头观察</td><td rowspan="1">13</td><td rowspan="1">略显腼腆、想躲一下；还不习惯被关注；害羞偏警觉的轻声。</td><td rowspan="1">0</td><td rowspan="1">关闭</td></tr>
<tr><td rowspan="6">19</td><td rowspan="6">后背轻触</td><td rowspan="6">Beta Y</td><td rowspan="2">1｜开心</td><td rowspan="1">65%</td><td rowspan="1">12</td><td rowspan="1">正式的点头（抬头低头）</td><td rowspan="1">11</td><td rowspan="1">表示认同、愿意配合；轻松的肯定；互动中的“好呀”式回应。</td><td rowspan="1">1</td><td rowspan="1">弱</td></tr>
<tr><td rowspan="1">35%</td><td rowspan="2">18</td><td rowspan="2">单次轻触缓慢抬头观察</td><td rowspan="2">17</td><td rowspan="2">软萌、轻微惊喜偏正向；轻碰或被注意到后的柔和回应。</td><td rowspan="3">0</td><td rowspan="3">关闭</td></tr>
<tr><td rowspan="2">2｜平静</td><td rowspan="1">55%</td></tr>
<tr><td rowspan="1">45%</td><td rowspan="2">16</td><td rowspan="2">突发触碰单次躲闪</td><td rowspan="1">31</td><td rowspan="1">惊吓或不安后的缓和；从紧张回到可互动；带一点不好意思的恢复声。</td></tr>
<tr><td rowspan="2">3｜悲伤</td><td rowspan="1">85%</td><td rowspan="1">15</td><td rowspan="1">不安、紧绷时的短反馈；安全感下降。</td><td rowspan="1">1</td><td rowspan="1">弱</td></tr>
<tr><td rowspan="1">15%</td><td rowspan="1">18</td><td rowspan="1">单次轻触缓慢抬头观察</td><td rowspan="1">13</td><td rowspan="1">略显腼腆、想躲一下；还不习惯被关注；害羞偏警觉的轻声。</td><td rowspan="1">0</td><td rowspan="1">关闭</td></tr>
<tr><td rowspan="6">20</td><td rowspan="6">后背短抚</td><td rowspan="32">预留 Beta N</td><td rowspan="2">1｜开心</td><td rowspan="1">65%</td><td rowspan="1">12</td><td rowspan="1">正式的点头（抬头低头）</td><td rowspan="1">48</td><td rowspan="1">认同点头的第二条；轻松肯定；中等力度的配合感。</td><td rowspan="1">1</td><td rowspan="1">弱</td></tr>
<tr><td rowspan="1">35%</td><td rowspan="2">18</td><td rowspan="2">单次轻触缓慢抬头观察</td><td rowspan="2">17</td><td rowspan="2">软萌、轻微惊喜偏正向；轻碰或被注意到后的柔和回应。</td><td rowspan="3">0</td><td rowspan="3">关闭</td></tr>
<tr><td rowspan="2">2｜平静</td><td rowspan="1">55%</td></tr>
<tr><td rowspan="1">45%</td><td rowspan="1">16</td><td rowspan="1">突发触碰单次躲闪</td><td rowspan="1">31</td><td rowspan="1">惊吓或不安后的缓和；从紧张回到可互动；带一点不好意思的恢复声。</td></tr>
<tr><td rowspan="2">3｜悲伤</td><td rowspan="1">85%</td><td rowspan="1">25</td><td rowspan="1">快速撸过度刺激躲闪</td><td rowspan="1">15</td><td rowspan="1">不安、紧绷时的短反馈；安全感下降。</td><td rowspan="1">1</td><td rowspan="1">弱</td></tr>
<tr><td rowspan="1">15%</td><td rowspan="1">18</td><td rowspan="1">单次轻触缓慢抬头观察</td><td rowspan="1">13</td><td rowspan="1">略显腼腆、想躲一下；还不习惯被关注；害羞偏警觉的轻声。</td><td rowspan="1">0</td><td rowspan="1">关闭</td></tr>
<tr><td rowspan="6">21</td><td rowspan="6">后背长抚</td><td rowspan="2">1｜开心</td><td rowspan="1">65%</td><td rowspan="1">12</td><td rowspan="1">正式的点头（抬头低头）</td><td rowspan="1">11</td><td rowspan="1">表示认同、愿意配合；轻松的肯定；互动中的“好呀”式回应。</td><td rowspan="1">1</td><td rowspan="1">弱</td></tr>
<tr><td rowspan="1">35%</td><td rowspan="2">18</td><td rowspan="2">单次轻触缓慢抬头观察</td><td rowspan="2">17</td><td rowspan="2">软萌、轻微惊喜偏正向；轻碰或被注意到后的柔和回应。</td><td rowspan="3">0</td><td rowspan="3">关闭</td></tr>
<tr><td rowspan="2">2｜平静</td><td rowspan="1">55%</td></tr>
<tr><td rowspan="1">45%</td><td rowspan="2">16</td><td rowspan="2">突发触碰单次躲闪</td><td rowspan="1">31</td><td rowspan="1">惊吓或不安后的缓和；从紧张回到可互动；带一点不好意思的恢复声。</td></tr>
<tr><td rowspan="2">3｜悲伤</td><td rowspan="1">85%</td><td rowspan="1">15</td><td rowspan="1">不安、紧绷时的短反馈；安全感下降。</td><td rowspan="1">1</td><td rowspan="1">弱</td></tr>
<tr><td rowspan="1">15%</td><td rowspan="1">18</td><td rowspan="1">单次轻触缓慢抬头观察</td><td rowspan="1">13</td><td rowspan="1">略显腼腆、想躲一下；还不习惯被关注；害羞偏警觉的轻声。</td><td rowspan="2">0</td><td rowspan="2">关闭</td></tr>
<tr><td rowspan="6">22</td><td rowspan="6">长时间握持</td><td rowspan="2">1｜开心</td><td rowspan="1">65%</td><td rowspan="1">54</td><td rowspan="1">长时间握持间断打量</td><td rowspan="1">41</td><td rowspan="1">熟悉后的侧面短回声；亲昵互动中的二次确认；更松弛一点。</td></tr>
<tr><td rowspan="1">35%</td><td rowspan="1">46</td><td rowspan="1">短时握持间断晃头（Sustainedhold）</td><td rowspan="1">33</td><td rowspan="1">黏人、舍不得分开；被抱持时的依赖；温暖的撒娇贴近。</td><td rowspan="1">1</td><td rowspan="1">弱</td></tr>
<tr><td rowspan="2">2｜平静</td><td rowspan="1">55%</td><td rowspan="1">54</td><td rowspan="1">长时间握持间断打量</td><td rowspan="1">41</td><td rowspan="1">熟悉后的侧面短回声；亲昵互动中的二次确认；更松弛一点。</td><td rowspan="2">0</td><td rowspan="2">关闭</td></tr>
<tr><td rowspan="1">45%</td><td rowspan="1">46</td><td rowspan="1">短时握持间断晃头（Sustainedhold）</td><td rowspan="1">33</td><td rowspan="1">黏人、舍不得分开；被抱持时的依赖；温暖的撒娇贴近。</td></tr>
<tr><td rowspan="2">3｜悲伤</td><td rowspan="1">85%</td><td rowspan="1">31</td><td rowspan="1">粗暴握持高频躲闪颤</td><td rowspan="1">22</td><td rowspan="1">被拘束、不舒服；害怕但克制；需要不安的弱抗议。</td><td rowspan="1">1</td><td rowspan="1">弱</td></tr>
<tr><td rowspan="1">15%</td><td rowspan="1">54</td><td rowspan="1">长时间握持间断打量</td><td rowspan="1">41</td><td rowspan="1">熟悉后的侧面短回声；亲昵互动中的二次确认；更松弛一点。</td><td rowspan="2">0</td><td rowspan="2">关闭</td></tr>
<tr><td rowspan="6">23</td><td rowspan="6">轻摇</td><td rowspan="2">1｜开心</td><td rowspan="1">65%</td><td rowspan="1">49</td><td rowspan="1">轻摇缓慢环视</td><td rowspan="1">31</td><td rowspan="1">惊吓或不安后的缓和；从紧张回到可互动；带一点不好意思的恢复声。</td></tr>
<tr><td rowspan="1">35%</td><td rowspan="1">28</td><td rowspan="1">轻摇小幅快点头（Gentleshake）</td><td rowspan="1">18</td><td rowspan="1">熟悉的人唤醒；日常互动开始；比正式开机更轻快的起始。</td><td rowspan="1">1</td><td rowspan="1">弱</td></tr>
<tr><td rowspan="2">2｜平静</td><td rowspan="1">55%</td><td rowspan="1">49</td><td rowspan="1">轻摇缓慢环视</td><td rowspan="1">37</td><td rowspan="1">持续倾斜或多次晃动；不安累积；比更轻的不安反馈更紧一点。</td><td rowspan="2">0</td><td rowspan="2">关闭</td></tr>
<tr><td rowspan="1">45%</td><td rowspan="1">6</td><td rowspan="1">瞌睡</td><td rowspan="1">1</td><td rowspan="1">安静休息、低刺激存在感；长时间无互动或待机时的 resting 陪伴底。不用于充电提示。</td></tr>
<tr><td rowspan="2">3｜悲伤</td><td rowspan="1">85%</td><td rowspan="2">49</td><td rowspan="2">轻摇缓慢环视</td><td rowspan="1">37</td><td rowspan="1">持续倾斜或多次晃动；不安累积；比更轻的不安反馈更紧一点。</td><td rowspan="1">1</td><td rowspan="1">弱</td></tr>
<tr><td rowspan="1">15%</td><td rowspan="1">15</td><td rowspan="1">不安、紧绷时的短反馈；安全感下降。</td><td rowspan="1">0</td><td rowspan="1">关闭</td></tr>
<tr><td rowspan="2">24</td><td rowspan="2">猛摇</td><td rowspan="2">0｜ANY</td><td rowspan="1">70%</td><td rowspan="1">31</td><td rowspan="1">粗暴握持高频躲闪颤</td><td rowspan="1">22</td><td rowspan="1">被拘束、不舒服；害怕但克制；需要不安的弱抗议。</td><td rowspan="3">1</td><td rowspan="3">弱</td></tr>
<tr><td rowspan="1">30%</td><td rowspan="1">25</td><td rowspan="1">快速撸过度刺激躲闪</td><td rowspan="1">15</td><td rowspan="1">不安、紧绷时的短反馈；安全感下降。</td></tr>
<tr><td rowspan="6">25</td><td rowspan="6">翻转</td><td rowspan="2">1｜开心</td><td rowspan="1">65%</td><td rowspan="1">5</td><td rowspan="1">强行翻肚皮垂头</td><td rowspan="1">5</td><td rowspan="1">被强迫改变姿态；委屈并想挣脱；需要短促的抗拒反馈。</td></tr>
<tr><td rowspan="1">35%</td><td rowspan="1">22</td><td rowspan="1">翻转肚皮静态垂头</td><td rowspan="1">20</td><td rowspan="1">信任更深一层；安抚进入更浓的亲密；比上一条更持续、更沉。</td><td rowspan="1">0</td><td rowspan="1">关闭</td></tr>
<tr><td rowspan="2">2｜平静</td><td rowspan="1">55%</td><td rowspan="1">5</td><td rowspan="1">强行翻肚皮垂头</td><td rowspan="1">5</td><td rowspan="1">被强迫改变姿态；委屈并想挣脱；需要短促的抗拒反馈。</td><td rowspan="1">1</td><td rowspan="1">弱</td></tr>
<tr><td rowspan="1">45%</td><td rowspan="1">22</td><td rowspan="1">翻转肚皮静态垂头</td><td rowspan="1">20</td><td rowspan="1">信任更深一层；安抚进入更浓的亲密；比上一条更持续、更沉。</td><td rowspan="1">0</td><td rowspan="1">关闭</td></tr>
<tr><td rowspan="2">3｜悲伤</td><td rowspan="1">85%</td><td rowspan="1">5</td><td rowspan="1">强行翻肚皮垂头</td><td rowspan="1">5</td><td rowspan="1">被强迫改变姿态；委屈并想挣脱；需要短促的抗拒反馈。</td><td rowspan="1">1</td><td rowspan="1">弱</td></tr>
<tr><td rowspan="1">15%</td><td rowspan="1">22</td><td rowspan="1">翻转肚皮静态垂头</td><td rowspan="1">20</td><td rowspan="1">信任更深一层；安抚进入更浓的亲密；比上一条更持续、更沉。</td><td rowspan="2">0</td><td rowspan="2">关闭</td></tr>
<tr><td rowspan="6">26</td><td rowspan="6">被拿起</td><td rowspan="12">原表划除</td><td rowspan="2">1｜开心</td><td rowspan="1">65%</td><td rowspan="1">9</td><td rowspan="1">上下缓慢抬升打量</td><td rowspan="1">8</td><td rowspan="1">突然被从一侧接近；需要快速确认方位；短暂警觉后的注意。</td></tr>
<tr><td rowspan="1">35%</td><td rowspan="1">60</td><td rowspan="1">被拿起上扬连续点头（Pickedup）</td><td rowspan="1">34</td><td rowspan="1">黏人升级；主动蹭近；开心又舍不得被放下。</td><td rowspan="1">1</td><td rowspan="1">弱</td></tr>
<tr><td rowspan="2">2｜平静</td><td rowspan="1">55%</td><td rowspan="1">9</td><td rowspan="1">上下缓慢抬升打量</td><td rowspan="1">8</td><td rowspan="1">突然被从一侧接近；需要快速确认方位；短暂警觉后的注意。</td><td rowspan="1">0</td><td rowspan="1">关闭</td></tr>
<tr><td rowspan="1">45%</td><td rowspan="1">60</td><td rowspan="1">被拿起上扬连续点头（Pickedup）</td><td rowspan="1">34</td><td rowspan="1">黏人升级；主动蹭近；开心又舍不得被放下。</td><td rowspan="1">1</td><td rowspan="1">弱</td></tr>
<tr><td rowspan="2">3｜悲伤</td><td rowspan="1">85%</td><td rowspan="1">9</td><td rowspan="1">上下缓慢抬升打量</td><td rowspan="1">8</td><td rowspan="1">突然被从一侧接近；需要快速确认方位；短暂警觉后的注意。</td><td rowspan="9">0</td><td rowspan="9">关闭</td></tr>
<tr><td rowspan="1">15%</td><td rowspan="1">54</td><td rowspan="1">长时间握持间断打量</td><td rowspan="1">41</td><td rowspan="1">熟悉后的侧面短回声；亲昵互动中的二次确认；更松弛一点。</td></tr>
<tr><td rowspan="6">27</td><td rowspan="6">被放下</td><td rowspan="2">1｜开心</td><td rowspan="1">65%</td><td rowspan="1">9</td><td rowspan="1">上下缓慢抬升打量</td><td rowspan="1">8</td><td rowspan="1">突然被从一侧接近；需要快速确认方位；短暂警觉后的注意。</td></tr>
<tr><td rowspan="1">35%</td><td rowspan="1">3</td><td rowspan="1">放下后长期垂头</td><td rowspan="1">3</td><td rowspan="1">独处过久；被放下后的空落；需要稀疏、带着一点想念的低声。</td></tr>
<tr><td rowspan="2">2｜平静</td><td rowspan="1">55%</td><td rowspan="1">9</td><td rowspan="1">上下缓慢抬升打量</td><td rowspan="1">8</td><td rowspan="1">突然被从一侧接近；需要快速确认方位；短暂警觉后的注意。</td></tr>
<tr><td rowspan="1">45%</td><td rowspan="2">3</td><td rowspan="2">放下后长期垂头</td><td rowspan="2">3</td><td rowspan="2">独处过久；被放下后的空落；需要稀疏、带着一点想念的低声。</td></tr>
<tr><td rowspan="2">3｜悲伤</td><td rowspan="1">85%</td></tr>
<tr><td rowspan="1">15%</td><td rowspan="2">9</td><td rowspan="2">上下缓慢抬升打量</td><td rowspan="1">45</td><td rowspan="1">同一侧再次被注意；熟悉后的警觉确认；轻回头式的注意。</td></tr>
<tr><td rowspan="6">28</td><td rowspan="6">唤醒提示词</td><td rowspan="14">Beta Y</td><td rowspan="2">1｜开心</td><td rowspan="1">65%</td><td rowspan="1">8</td><td rowspan="1">突然被从一侧接近；需要快速确认方位；短暂警觉后的注意。</td></tr>
<tr><td rowspan="1">35%</td><td rowspan="1">13</td><td rowspan="1">抬头后快速点头（很乐意）</td><td rowspan="1">12</td><td rowspan="1">认同反馈的另一变体；避免与上一条完全重复；同样轻快的肯定感。</td><td rowspan="1">1</td><td rowspan="1">弱</td></tr>
<tr><td rowspan="2">2｜平静</td><td rowspan="1">55%</td><td rowspan="1">9</td><td rowspan="1">上下缓慢抬升打量</td><td rowspan="1">8</td><td rowspan="1">突然被从一侧接近；需要快速确认方位；短暂警觉后的注意。</td><td rowspan="1">0</td><td rowspan="1">关闭</td></tr>
<tr><td rowspan="1">45%</td><td rowspan="1">13</td><td rowspan="1">抬头后快速点头（很乐意）</td><td rowspan="1">12</td><td rowspan="1">认同反馈的另一变体；避免与上一条完全重复；同样轻快的肯定感。</td><td rowspan="1">1</td><td rowspan="1">弱</td></tr>
<tr><td rowspan="2">3｜悲伤</td><td rowspan="1">85%</td><td rowspan="1">9</td><td rowspan="1">上下缓慢抬升打量</td><td rowspan="1">8</td><td rowspan="1">突然被从一侧接近；需要快速确认方位；短暂警觉后的注意。</td><td rowspan="15">0</td><td rowspan="15">关闭</td></tr>
<tr><td rowspan="1">15%</td><td rowspan="1">19</td><td rowspan="1">唤醒半睡慢抬</td><td rowspan="1">18</td><td rowspan="1">熟悉的人唤醒；日常互动开始；比正式开机更轻快的起始。</td></tr>
<tr><td rowspan="2">29</td><td rowspan="2">光线变暗</td><td rowspan="2">0｜ANY</td><td rowspan="2">50%</td><td rowspan="1">23</td><td rowspan="1">暗光低头慢挪</td><td rowspan="1">21</td><td rowspan="1">夜间进一步安静；准备休息；需要更柔、更长的过渡。</td></tr>
<tr><td rowspan="1">55</td><td rowspan="1">暗光慵懒垂头（Darkness）</td><td rowspan="1">42</td><td rowspan="1">环境变暗；从活跃转入安静；准备进入低刺激状态。</td></tr>
<tr><td rowspan="6">30</td><td rowspan="6">光线变亮</td><td rowspan="2">1｜开心</td><td rowspan="1">65%</td><td rowspan="1">9</td><td rowspan="1">上下缓慢抬升打量</td><td rowspan="1">8</td><td rowspan="1">突然被从一侧接近；需要快速确认方位；短暂警觉后的注意。</td></tr>
<tr><td rowspan="1">35%</td><td rowspan="1">50</td><td rowspan="1">间断定点侧头试探</td><td rowspan="1">23</td><td rowspan="1">轻柔问候；关系刚开始或再次见面；低刺激的友好开场。</td></tr>
<tr><td rowspan="2">2｜平静</td><td rowspan="1">55%</td><td rowspan="1">9</td><td rowspan="1">上下缓慢抬升打量</td><td rowspan="1">8</td><td rowspan="1">突然被从一侧接近；需要快速确认方位；短暂警觉后的注意。</td></tr>
<tr><td rowspan="1">45%</td><td rowspan="1">50</td><td rowspan="1">间断定点侧头试探</td><td rowspan="1">23</td><td rowspan="1">轻柔问候；关系刚开始或再次见面；低刺激的友好开场。</td></tr>
<tr><td rowspan="2">3｜悲伤</td><td rowspan="1">85%</td><td rowspan="1">9</td><td rowspan="1">上下缓慢抬升打量</td><td rowspan="1">8</td><td rowspan="1">突然被从一侧接近；需要快速确认方位；短暂警觉后的注意。</td></tr>
<tr><td rowspan="1">15%</td><td rowspan="1">50</td><td rowspan="1">间断定点侧头试探</td><td rowspan="1">52</td><td rowspan="1">近距离逗弄后的二次害羞；熟人之间；比第一次更软。</td></tr>
<tr><td rowspan="2">31</td><td rowspan="2">2小时无互动</td><td rowspan="4">预留 Beta N</td><td rowspan="4">0｜ANY</td><td rowspan="1">70%</td><td rowspan="1">6</td><td rowspan="1">瞌睡</td><td rowspan="1">1</td><td rowspan="1">安静休息、低刺激存在感；长时间无互动或待机时的 resting 陪伴底。不用于充电提示。</td></tr>
<tr><td rowspan="1">30%</td><td rowspan="2">3</td><td rowspan="2">放下后长期垂头</td><td rowspan="2">3</td><td rowspan="2">独处过久；被放下后的空落；需要稀疏、带着一点想念的低声。</td></tr>
<tr><td rowspan="2">32</td><td rowspan="2">48小时无互动</td><td rowspan="1">60%</td></tr>
<tr><td rowspan="1">40%</td><td rowspan="1">6</td><td rowspan="1">瞌睡</td><td rowspan="1">1</td><td rowspan="1">安静休息、低刺激存在感；长时间无互动或待机时的 resting 陪伴底。不用于充电提示。</td></tr>
<tr><td rowspan="6">33</td><td rowspan="6">遇到新伙伴</td><td rowspan="18">Beta Y</td><td rowspan="2">1｜开心</td><td rowspan="1">65%</td><td rowspan="1">17</td><td rowspan="1">初识同类慢偏头试探</td><td rowspan="1">16</td><td rowspan="1">距离突然很近；害羞又好奇；亲昵但还放不开。</td></tr>
<tr><td rowspan="1">35%</td><td rowspan="1">29</td><td rowspan="1">遇见同类双向晃头（陌生Beany）</td><td rowspan="1">23</td><td rowspan="1">轻柔问候；关系刚开始或再次见面；低刺激的友好开场。</td><td rowspan="1">1</td><td rowspan="1">弱</td></tr>
<tr><td rowspan="2">2｜平静</td><td rowspan="1">55%</td><td rowspan="1">17</td><td rowspan="1">初识同类慢偏头试探</td><td rowspan="1">16</td><td rowspan="1">距离突然很近；害羞又好奇；亲昵但还放不开。</td><td rowspan="4">0</td><td rowspan="4">关闭</td></tr>
<tr><td rowspan="1">45%</td><td rowspan="1">50</td><td rowspan="1">间断定点侧头试探</td><td rowspan="1">23</td><td rowspan="1">轻柔问候；关系刚开始或再次见面；低刺激的友好开场。</td></tr>
<tr><td rowspan="2">3｜悲伤</td><td rowspan="1">85%</td><td rowspan="1">17</td><td rowspan="1">初识同类慢偏头试探</td><td rowspan="1">16</td><td rowspan="1">距离突然很近；害羞又好奇；亲昵但还放不开。</td></tr>
<tr><td rowspan="1">15%</td><td rowspan="1">21</td><td rowspan="1">陌生同类低头远离</td><td rowspan="1">3</td><td rowspan="1">独处过久；被放下后的空落；需要稀疏、带着一点想念的低声。</td></tr>
<tr><td rowspan="6">34</td><td rowspan="6">遇到熟悉伙伴</td><td rowspan="2">1｜开心</td><td rowspan="1">65%</td><td rowspan="1">29</td><td rowspan="1">遇见同类双向晃头（陌生Beany）</td><td rowspan="1">23</td><td rowspan="1">轻柔问候；关系刚开始或再次见面；低刺激的友好开场。</td><td rowspan="2">1</td><td rowspan="2">弱</td></tr>
<tr><td rowspan="1">35%</td><td rowspan="1">34</td><td rowspan="1">遇见熟同类高频点头（熟悉Beany）</td><td rowspan="1">28</td><td rowspan="1">极度开心的第二条；狂喜或重逢式雀跃；避免与上一条听感雷同。</td></tr>
<tr><td rowspan="2">2｜平静</td><td rowspan="1">55%</td><td rowspan="1">50</td><td rowspan="1">间断定点侧头试探</td><td rowspan="2">23</td><td rowspan="2">轻柔问候；关系刚开始或再次见面；低刺激的友好开场。</td><td rowspan="1">0</td><td rowspan="1">关闭</td></tr>
<tr><td rowspan="1">45%</td><td rowspan="1">29</td><td rowspan="1">遇见同类双向晃头（陌生Beany）</td><td rowspan="1">1</td><td rowspan="1">弱</td></tr>
<tr><td rowspan="2">3｜悲伤</td><td rowspan="1">85%</td><td rowspan="1">17</td><td rowspan="1">初识同类慢偏头试探</td><td rowspan="1">30</td><td rowspan="1">害羞躲闪的变体；慢慢适应被关注；比上一条略软一点。</td><td rowspan="2">0</td><td rowspan="2">关闭</td></tr>
<tr><td rowspan="1">15%</td><td rowspan="1">50</td><td rowspan="1">间断定点侧头试探</td><td rowspan="1">52</td><td rowspan="1">近距离逗弄后的二次害羞；熟人之间；比第一次更软。</td></tr>
<tr><td rowspan="2">35</td><td rowspan="2">侧倒</td><td rowspan="10">0｜ANY</td><td rowspan="2">50%</td><td rowspan="1">36</td><td rowspan="2">侧倒低头向内躲闪</td><td rowspan="1">29</td><td rowspan="1">失去平衡、需要自保；侧向不稳；戒备但不攻击。</td><td rowspan="2">1</td><td rowspan="2">弱</td></tr>
<tr><td rowspan="1">40</td><td rowspan="1">32</td><td rowspan="1">自保戒备的第二条；持续不稳时的重复；更明确一点的护住自己。</td></tr>
<tr><td rowspan="1">36</td><td rowspan="1">充电</td><td rowspan="2">100%</td><td rowspan="1">1</td><td rowspan="1">充电启动单次点头（充电专属）</td><td rowspan="1">61</td><td rowspan="1">插上充电器/开始充电时的固定提示。</td><td rowspan="2">0</td><td rowspan="2">关闭</td></tr>
<tr><td rowspan="1">37</td><td rowspan="1">低电量</td><td rowspan="1">53</td><td rowspan="1">低电量间断抬头观望</td><td rowspan="1">40</td><td rowspan="1">低电量固定提示；能量将尽、虚弱收束；偏困倦的告别感。</td></tr>
<tr><td rowspan="2">38</td><td rowspan="2">开机</td><td rowspan="2">50%</td><td rowspan="1">8</td><td rowspan="1">开机上扬点头（开机启动）</td><td rowspan="1">7</td><td rowspan="1">开机上电；第一次苏醒；需要柔和、有活力的启动感。</td><td rowspan="2">1</td><td rowspan="2">弱</td></tr>
<tr><td rowspan="1">51</td><td rowspan="1">开机分段环视</td><td rowspan="1">39</td><td rowspan="1">开机苏醒的另一音色；同样柔和启动；用于避免总播同一条。</td></tr>
<tr><td rowspan="1">39</td><td rowspan="1">呼吸</td><td rowspan="1">预留 Beta N</td><td rowspan="4">100%</td><td rowspan="1">48</td><td rowspan="1">待机呼吸间断侧头</td><td rowspan="1">59</td><td rowspan="1">平稳持续的轻哼；待机伴随；低刺激氛围底。</td><td rowspan="1">0</td><td rowspan="1">关闭</td></tr>
<tr><td rowspan="1">40</td><td rowspan="1">抛起</td><td rowspan="1">Beta Y</td><td rowspan="1">58</td><td rowspan="1">抛起上扬晃头（抛起事件）</td><td rowspan="2">27</td><td rowspan="2">明显失重、刺激偏强；短暂离开稳定支撑；需要高能量反馈。</td><td rowspan="2">1</td><td rowspan="2">弱</td></tr>
<tr><td rowspan="1">41</td><td rowspan="1">旋转抛起</td><td rowspan="1">原表划除</td><td rowspan="1">32</td><td rowspan="1">旋转抛起极速环绕头（旋转抛）</td></tr>
<tr><td rowspan="1">42</td><td rowspan="1">关机</td><td rowspan="1">Beta Y</td><td rowspan="1">4</td><td rowspan="1">关机缓慢垂头锁位</td><td rowspan="1">4</td><td rowspan="1">关机进入彻底休眠；一天结束；需要渐弱、收束的入睡感。</td><td rowspan="1">0</td><td rowspan="1">关闭</td></tr></tbody>
</table>

## 熟悉 102组候选条件

<table>
<thead>
<tr><th>事件ID</th><th>输入</th><th>启用</th><th>情绪ID / 分组</th><th>概率</th><th>动作ID</th><th>动作反馈</th><th>音频ID</th><th>伴音含义</th><th>震动ID</th><th>强度</th></tr></thead>
<tbody>
<tr><td rowspan="6">1</td><td rowspan="6">头顶轻触</td><td rowspan="6">Beta Y</td><td rowspan="2">1｜开心</td><td rowspan="1">70%</td><td rowspan="1">13</td><td rowspan="1">抬头后快速点头（很乐意）</td><td rowspan="1">12</td><td rowspan="1">认同反馈的另一变体；避免与上一条完全重复；同样轻快的肯定感。</td><td rowspan="1">2</td><td rowspan="1">中</td></tr>
<tr><td rowspan="1">30%</td><td rowspan="1">11</td><td rowspan="1">快速上下点头（快速撸通用开心）</td><td rowspan="1">47</td><td rowspan="1">愉快互动的第二条；同样偏快、偏亮；轮换用的开心反馈。</td><td rowspan="2">1</td><td rowspan="2">弱</td></tr>
<tr><td rowspan="2">2｜平静</td><td rowspan="1">70%</td><td rowspan="1">43</td><td rowspan="1">定点单侧观望（左）</td><td rowspan="1">8</td><td rowspan="1">突然被从一侧接近；需要快速确认方位；短暂警觉后的注意。</td></tr>
<tr><td rowspan="1">30%</td><td rowspan="1">18</td><td rowspan="1">单次轻触缓慢抬头观察</td><td rowspan="1">25</td><td rowspan="1">温暖友好、被好好对待后的软回应；社交开场或亲密回馈。</td><td rowspan="1">0</td><td rowspan="1">关闭</td></tr>
<tr><td rowspan="2">3｜悲伤</td><td rowspan="1">80%</td><td rowspan="1">16</td><td rowspan="1">突发触碰单次躲闪</td><td rowspan="1">31</td><td rowspan="1">惊吓或不安后的缓和；从紧张回到可互动；带一点不好意思的恢复声。</td><td rowspan="1">1</td><td rowspan="1">弱</td></tr>
<tr><td rowspan="1">20%</td><td rowspan="1">2</td><td rowspan="1">轻抬慢回（温顺舒缓）</td><td rowspan="1">6</td><td rowspan="1">持续安抚中的重复回应；比第一条更柔；安静状态下的陪伴回声。</td><td rowspan="1">0</td><td rowspan="1">关闭</td></tr>
<tr><td rowspan="6">2</td><td rowspan="6">头顶短抚</td><td rowspan="12">预留 Beta N</td><td rowspan="2">1｜开心</td><td rowspan="1">70%</td><td rowspan="1">11</td><td rowspan="1">快速上下点头（快速撸通用开心）</td><td rowspan="1">10</td><td rowspan="1">节奏偏快的愉快互动；兴奋且享受；需要明亮的开心短声。</td><td rowspan="1">2</td><td rowspan="1">中</td></tr>
<tr><td rowspan="1">30%</td><td rowspan="1">13</td><td rowspan="1">抬头后快速点头（很乐意）</td><td rowspan="1">49</td><td rowspan="1">认同反馈的第四条；保持轻快；批量互动时轮换。</td><td rowspan="2">1</td><td rowspan="2">弱</td></tr>
<tr><td rowspan="2">2｜平静</td><td rowspan="1">70%</td><td rowspan="1">43</td><td rowspan="1">定点单侧观望（左）</td><td rowspan="1">8</td><td rowspan="1">突然被从一侧接近；需要快速确认方位；短暂警觉后的注意。</td></tr>
<tr><td rowspan="1">30%</td><td rowspan="1">18</td><td rowspan="1">单次轻触缓慢抬头观察</td><td rowspan="1">25</td><td rowspan="1">温暖友好、被好好对待后的软回应；社交开场或亲密回馈。</td><td rowspan="1">0</td><td rowspan="1">关闭</td></tr>
<tr><td rowspan="2">3｜悲伤</td><td rowspan="1">80%</td><td rowspan="1">25</td><td rowspan="1">快速撸过度刺激躲闪</td><td rowspan="1">31</td><td rowspan="1">惊吓或不安后的缓和；从紧张回到可互动；带一点不好意思的恢复声。</td><td rowspan="1">1</td><td rowspan="1">弱</td></tr>
<tr><td rowspan="1">20%</td><td rowspan="1">2</td><td rowspan="1">轻抬慢回（温顺舒缓）</td><td rowspan="1">6</td><td rowspan="1">持续安抚中的重复回应；比第一条更柔；安静状态下的陪伴回声。</td><td rowspan="1">0</td><td rowspan="1">关闭</td></tr>
<tr><td rowspan="6">3</td><td rowspan="6">头顶长抚</td><td rowspan="2">1｜开心</td><td rowspan="1">70%</td><td rowspan="1">13</td><td rowspan="1">抬头后快速点头（很乐意）</td><td rowspan="1">12</td><td rowspan="1">认同反馈的另一变体；避免与上一条完全重复；同样轻快的肯定感。</td><td rowspan="1">2</td><td rowspan="1">中</td></tr>
<tr><td rowspan="1">30%</td><td rowspan="1">11</td><td rowspan="1">快速上下点头（快速撸通用开心）</td><td rowspan="1">47</td><td rowspan="1">愉快互动的第二条；同样偏快、偏亮；轮换用的开心反馈。</td><td rowspan="2">1</td><td rowspan="2">弱</td></tr>
<tr><td rowspan="2">2｜平静</td><td rowspan="1">70%</td><td rowspan="1">43</td><td rowspan="1">定点单侧观望（左）</td><td rowspan="1">8</td><td rowspan="1">突然被从一侧接近；需要快速确认方位；短暂警觉后的注意。</td></tr>
<tr><td rowspan="1">30%</td><td rowspan="1">18</td><td rowspan="1">单次轻触缓慢抬头观察</td><td rowspan="1">25</td><td rowspan="1">温暖友好、被好好对待后的软回应；社交开场或亲密回馈。</td><td rowspan="1">0</td><td rowspan="1">关闭</td></tr>
<tr><td rowspan="2">3｜悲伤</td><td rowspan="1">80%</td><td rowspan="1">16</td><td rowspan="1">突发触碰单次躲闪</td><td rowspan="1">31</td><td rowspan="1">惊吓或不安后的缓和；从紧张回到可互动；带一点不好意思的恢复声。</td><td rowspan="1">1</td><td rowspan="1">弱</td></tr>
<tr><td rowspan="1">20%</td><td rowspan="1">2</td><td rowspan="1">轻抬慢回（温顺舒缓）</td><td rowspan="1">6</td><td rowspan="1">持续安抚中的重复回应；比第一条更柔；安静状态下的陪伴回声。</td><td rowspan="1">0</td><td rowspan="1">关闭</td></tr>
<tr><td rowspan="6">4</td><td rowspan="6">头左轻触</td><td rowspan="6">Beta Y</td><td rowspan="2">1｜开心</td><td rowspan="1">70%</td><td rowspan="1">13</td><td rowspan="1">抬头后快速点头（很乐意）</td><td rowspan="1">12</td><td rowspan="1">认同反馈的另一变体；避免与上一条完全重复；同样轻快的肯定感。</td><td rowspan="1">2</td><td rowspan="1">中</td></tr>
<tr><td rowspan="1">30%</td><td rowspan="1">11</td><td rowspan="1">快速上下点头（快速撸通用开心）</td><td rowspan="1">47</td><td rowspan="1">愉快互动的第二条；同样偏快、偏亮；轮换用的开心反馈。</td><td rowspan="2">1</td><td rowspan="2">弱</td></tr>
<tr><td rowspan="2">2｜平静</td><td rowspan="1">70%</td><td rowspan="1">43</td><td rowspan="1">定点单侧观望（左）</td><td rowspan="1">8</td><td rowspan="1">突然被从一侧接近；需要快速确认方位；短暂警觉后的注意。</td></tr>
<tr><td rowspan="1">30%</td><td rowspan="1">18</td><td rowspan="1">单次轻触缓慢抬头观察</td><td rowspan="1">25</td><td rowspan="1">温暖友好、被好好对待后的软回应；社交开场或亲密回馈。</td><td rowspan="1">0</td><td rowspan="1">关闭</td></tr>
<tr><td rowspan="2">3｜悲伤</td><td rowspan="1">80%</td><td rowspan="1">16</td><td rowspan="1">突发触碰单次躲闪</td><td rowspan="1">31</td><td rowspan="1">惊吓或不安后的缓和；从紧张回到可互动；带一点不好意思的恢复声。</td><td rowspan="1">1</td><td rowspan="1">弱</td></tr>
<tr><td rowspan="1">20%</td><td rowspan="1">2</td><td rowspan="1">轻抬慢回（温顺舒缓）</td><td rowspan="1">6</td><td rowspan="1">持续安抚中的重复回应；比第一条更柔；安静状态下的陪伴回声。</td><td rowspan="1">0</td><td rowspan="1">关闭</td></tr>
<tr><td rowspan="6">5</td><td rowspan="6">头左短抚</td><td rowspan="12">预留 Beta N</td><td rowspan="2">1｜开心</td><td rowspan="1">70%</td><td rowspan="1">42</td><td rowspan="1">单侧快速偏头蹭手（摸头左快速撸）</td><td rowspan="1">34</td><td rowspan="1">黏人升级；主动蹭近；开心又舍不得被放下。</td><td rowspan="1">2</td><td rowspan="1">中</td></tr>
<tr><td rowspan="1">30%</td><td rowspan="1">13</td><td rowspan="1">抬头后快速点头（很乐意）</td><td rowspan="1">49</td><td rowspan="1">认同反馈的第四条；保持轻快；批量互动时轮换。</td><td rowspan="2">1</td><td rowspan="2">弱</td></tr>
<tr><td rowspan="2">2｜平静</td><td rowspan="1">70%</td><td rowspan="1">43</td><td rowspan="1">定点单侧观望（左）</td><td rowspan="1">8</td><td rowspan="1">突然被从一侧接近；需要快速确认方位；短暂警觉后的注意。</td></tr>
<tr><td rowspan="1">30%</td><td rowspan="1">18</td><td rowspan="1">单次轻触缓慢抬头观察</td><td rowspan="1">25</td><td rowspan="1">温暖友好、被好好对待后的软回应；社交开场或亲密回馈。</td><td rowspan="1">0</td><td rowspan="1">关闭</td></tr>
<tr><td rowspan="2">3｜悲伤</td><td rowspan="1">80%</td><td rowspan="1">25</td><td rowspan="1">快速撸过度刺激躲闪</td><td rowspan="1">31</td><td rowspan="1">惊吓或不安后的缓和；从紧张回到可互动；带一点不好意思的恢复声。</td><td rowspan="1">1</td><td rowspan="1">弱</td></tr>
<tr><td rowspan="1">20%</td><td rowspan="1">2</td><td rowspan="1">轻抬慢回（温顺舒缓）</td><td rowspan="1">6</td><td rowspan="1">持续安抚中的重复回应；比第一条更柔；安静状态下的陪伴回声。</td><td rowspan="1">0</td><td rowspan="1">关闭</td></tr>
<tr><td rowspan="6">6</td><td rowspan="6">头左长抚</td><td rowspan="2">1｜开心</td><td rowspan="1">70%</td><td rowspan="1">13</td><td rowspan="1">抬头后快速点头（很乐意）</td><td rowspan="1">12</td><td rowspan="1">认同反馈的另一变体；避免与上一条完全重复；同样轻快的肯定感。</td><td rowspan="1">2</td><td rowspan="1">中</td></tr>
<tr><td rowspan="1">30%</td><td rowspan="1">11</td><td rowspan="1">快速上下点头（快速撸通用开心）</td><td rowspan="1">47</td><td rowspan="1">愉快互动的第二条；同样偏快、偏亮；轮换用的开心反馈。</td><td rowspan="2">1</td><td rowspan="2">弱</td></tr>
<tr><td rowspan="2">2｜平静</td><td rowspan="1">70%</td><td rowspan="1">43</td><td rowspan="1">定点单侧观望（左）</td><td rowspan="1">8</td><td rowspan="1">突然被从一侧接近；需要快速确认方位；短暂警觉后的注意。</td></tr>
<tr><td rowspan="1">30%</td><td rowspan="1">18</td><td rowspan="1">单次轻触缓慢抬头观察</td><td rowspan="1">25</td><td rowspan="1">温暖友好、被好好对待后的软回应；社交开场或亲密回馈。</td><td rowspan="1">0</td><td rowspan="1">关闭</td></tr>
<tr><td rowspan="2">3｜悲伤</td><td rowspan="1">80%</td><td rowspan="1">16</td><td rowspan="1">突发触碰单次躲闪</td><td rowspan="1">31</td><td rowspan="1">惊吓或不安后的缓和；从紧张回到可互动；带一点不好意思的恢复声。</td><td rowspan="1">1</td><td rowspan="1">弱</td></tr>
<tr><td rowspan="1">20%</td><td rowspan="1">2</td><td rowspan="1">轻抬慢回（温顺舒缓）</td><td rowspan="1">6</td><td rowspan="1">持续安抚中的重复回应；比第一条更柔；安静状态下的陪伴回声。</td><td rowspan="1">0</td><td rowspan="1">关闭</td></tr>
<tr><td rowspan="6">7</td><td rowspan="6">头右轻触</td><td rowspan="6">Beta Y</td><td rowspan="2">1｜开心</td><td rowspan="1">70%</td><td rowspan="1">13</td><td rowspan="1">抬头后快速点头（很乐意）</td><td rowspan="1">12</td><td rowspan="1">认同反馈的另一变体；避免与上一条完全重复；同样轻快的肯定感。</td><td rowspan="1">2</td><td rowspan="1">中</td></tr>
<tr><td rowspan="1">30%</td><td rowspan="1">11</td><td rowspan="1">快速上下点头（快速撸通用开心）</td><td rowspan="1">47</td><td rowspan="1">愉快互动的第二条；同样偏快、偏亮；轮换用的开心反馈。</td><td rowspan="2">1</td><td rowspan="2">弱</td></tr>
<tr><td rowspan="2">2｜平静</td><td rowspan="1">70%</td><td rowspan="1">45</td><td rowspan="1">定点单侧观望（右）</td><td rowspan="1">8</td><td rowspan="1">突然被从一侧接近；需要快速确认方位；短暂警觉后的注意。</td></tr>
<tr><td rowspan="1">30%</td><td rowspan="1">18</td><td rowspan="1">单次轻触缓慢抬头观察</td><td rowspan="1">25</td><td rowspan="1">温暖友好、被好好对待后的软回应；社交开场或亲密回馈。</td><td rowspan="1">0</td><td rowspan="1">关闭</td></tr>
<tr><td rowspan="2">3｜悲伤</td><td rowspan="1">80%</td><td rowspan="1">16</td><td rowspan="1">突发触碰单次躲闪</td><td rowspan="1">31</td><td rowspan="1">惊吓或不安后的缓和；从紧张回到可互动；带一点不好意思的恢复声。</td><td rowspan="1">1</td><td rowspan="1">弱</td></tr>
<tr><td rowspan="1">20%</td><td rowspan="1">2</td><td rowspan="1">轻抬慢回（温顺舒缓）</td><td rowspan="1">6</td><td rowspan="1">持续安抚中的重复回应；比第一条更柔；安静状态下的陪伴回声。</td><td rowspan="1">0</td><td rowspan="1">关闭</td></tr>
<tr><td rowspan="6">8</td><td rowspan="6">头右短抚</td><td rowspan="12">预留 Beta N</td><td rowspan="2">1｜开心</td><td rowspan="1">70%</td><td rowspan="1">61</td><td rowspan="1">单侧快速偏头蹭手（摸头右快速撸）</td><td rowspan="1">35</td><td rowspan="1">依赖感最浓的一版；长时间贴近；柔和持续的撒娇。</td><td rowspan="1">2</td><td rowspan="1">中</td></tr>
<tr><td rowspan="1">30%</td><td rowspan="1">13</td><td rowspan="1">抬头后快速点头（很乐意）</td><td rowspan="1">49</td><td rowspan="1">认同反馈的第四条；保持轻快；批量互动时轮换。</td><td rowspan="2">1</td><td rowspan="2">弱</td></tr>
<tr><td rowspan="2">2｜平静</td><td rowspan="1">70%</td><td rowspan="1">45</td><td rowspan="1">定点单侧观望（右）</td><td rowspan="1">8</td><td rowspan="1">突然被从一侧接近；需要快速确认方位；短暂警觉后的注意。</td></tr>
<tr><td rowspan="1">30%</td><td rowspan="1">18</td><td rowspan="1">单次轻触缓慢抬头观察</td><td rowspan="1">25</td><td rowspan="1">温暖友好、被好好对待后的软回应；社交开场或亲密回馈。</td><td rowspan="1">0</td><td rowspan="1">关闭</td></tr>
<tr><td rowspan="2">3｜悲伤</td><td rowspan="1">80%</td><td rowspan="1">25</td><td rowspan="1">快速撸过度刺激躲闪</td><td rowspan="1">31</td><td rowspan="1">惊吓或不安后的缓和；从紧张回到可互动；带一点不好意思的恢复声。</td><td rowspan="1">1</td><td rowspan="1">弱</td></tr>
<tr><td rowspan="1">20%</td><td rowspan="1">2</td><td rowspan="1">轻抬慢回（温顺舒缓）</td><td rowspan="1">6</td><td rowspan="1">持续安抚中的重复回应；比第一条更柔；安静状态下的陪伴回声。</td><td rowspan="1">0</td><td rowspan="1">关闭</td></tr>
<tr><td rowspan="6">9</td><td rowspan="6">头右长抚</td><td rowspan="2">1｜开心</td><td rowspan="1">70%</td><td rowspan="1">13</td><td rowspan="1">抬头后快速点头（很乐意）</td><td rowspan="1">12</td><td rowspan="1">认同反馈的另一变体；避免与上一条完全重复；同样轻快的肯定感。</td><td rowspan="1">2</td><td rowspan="1">中</td></tr>
<tr><td rowspan="1">30%</td><td rowspan="1">11</td><td rowspan="1">快速上下点头（快速撸通用开心）</td><td rowspan="1">47</td><td rowspan="1">愉快互动的第二条；同样偏快、偏亮；轮换用的开心反馈。</td><td rowspan="2">1</td><td rowspan="2">弱</td></tr>
<tr><td rowspan="2">2｜平静</td><td rowspan="1">70%</td><td rowspan="1">45</td><td rowspan="1">定点单侧观望（右）</td><td rowspan="1">8</td><td rowspan="1">突然被从一侧接近；需要快速确认方位；短暂警觉后的注意。</td></tr>
<tr><td rowspan="1">30%</td><td rowspan="1">18</td><td rowspan="1">单次轻触缓慢抬头观察</td><td rowspan="1">25</td><td rowspan="1">温暖友好、被好好对待后的软回应；社交开场或亲密回馈。</td><td rowspan="1">0</td><td rowspan="1">关闭</td></tr>
<tr><td rowspan="2">3｜悲伤</td><td rowspan="1">80%</td><td rowspan="1">16</td><td rowspan="1">突发触碰单次躲闪</td><td rowspan="1">31</td><td rowspan="1">惊吓或不安后的缓和；从紧张回到可互动；带一点不好意思的恢复声。</td><td rowspan="1">1</td><td rowspan="1">弱</td></tr>
<tr><td rowspan="1">20%</td><td rowspan="1">2</td><td rowspan="1">轻抬慢回（温顺舒缓）</td><td rowspan="1">6</td><td rowspan="1">持续安抚中的重复回应；比第一条更柔；安静状态下的陪伴回声。</td><td rowspan="1">0</td><td rowspan="1">关闭</td></tr>
<tr><td rowspan="6">10</td><td rowspan="6">腹部轻触</td><td rowspan="6">Beta Y</td><td rowspan="2">1｜开心</td><td rowspan="1">70%</td><td rowspan="1">13</td><td rowspan="1">抬头后快速点头（很乐意）</td><td rowspan="1">12</td><td rowspan="1">认同反馈的另一变体；避免与上一条完全重复；同样轻快的肯定感。</td><td rowspan="1">2</td><td rowspan="1">中</td></tr>
<tr><td rowspan="1">30%</td><td rowspan="1">11</td><td rowspan="1">快速上下点头（快速撸通用开心）</td><td rowspan="1">47</td><td rowspan="1">愉快互动的第二条；同样偏快、偏亮；轮换用的开心反馈。</td><td rowspan="2">1</td><td rowspan="2">弱</td></tr>
<tr><td rowspan="2">2｜平静</td><td rowspan="1">70%</td><td rowspan="2">18</td><td rowspan="2">单次轻触缓慢抬头观察</td><td rowspan="2">25</td><td rowspan="2">温暖友好、被好好对待后的软回应；社交开场或亲密回馈。</td></tr>
<tr><td rowspan="1">30%</td><td rowspan="1">0</td><td rowspan="1">关闭</td></tr>
<tr><td rowspan="2">3｜悲伤</td><td rowspan="1">80%</td><td rowspan="1">16</td><td rowspan="1">突发触碰单次躲闪</td><td rowspan="1">31</td><td rowspan="1">惊吓或不安后的缓和；从紧张回到可互动；带一点不好意思的恢复声。</td><td rowspan="1">1</td><td rowspan="1">弱</td></tr>
<tr><td rowspan="1">20%</td><td rowspan="1">2</td><td rowspan="1">轻抬慢回（温顺舒缓）</td><td rowspan="1">6</td><td rowspan="1">持续安抚中的重复回应；比第一条更柔；安静状态下的陪伴回声。</td><td rowspan="1">0</td><td rowspan="1">关闭</td></tr>
<tr><td rowspan="6">11</td><td rowspan="6">腹部短抚</td><td rowspan="12">预留 Beta N</td><td rowspan="2">1｜开心</td><td rowspan="1">70%</td><td rowspan="1">27</td><td rowspan="1">肚皮触碰轻快垂点头（肚子快速撸）</td><td rowspan="1">24</td><td rowspan="1">情绪冲到很高的开心；雀跃、想撒娇蹦跳；社交或亲密高峰。</td><td rowspan="1">2</td><td rowspan="1">中</td></tr>
<tr><td rowspan="1">30%</td><td rowspan="1">13</td><td rowspan="1">抬头后快速点头（很乐意）</td><td rowspan="1">49</td><td rowspan="1">认同反馈的第四条；保持轻快；批量互动时轮换。</td><td rowspan="2">1</td><td rowspan="2">弱</td></tr>
<tr><td rowspan="2">2｜平静</td><td rowspan="1">70%</td><td rowspan="2">18</td><td rowspan="2">单次轻触缓慢抬头观察</td><td rowspan="2">25</td><td rowspan="2">温暖友好、被好好对待后的软回应；社交开场或亲密回馈。</td></tr>
<tr><td rowspan="1">30%</td><td rowspan="1">0</td><td rowspan="1">关闭</td></tr>
<tr><td rowspan="2">3｜悲伤</td><td rowspan="1">80%</td><td rowspan="1">25</td><td rowspan="1">快速撸过度刺激躲闪</td><td rowspan="1">31</td><td rowspan="1">惊吓或不安后的缓和；从紧张回到可互动；带一点不好意思的恢复声。</td><td rowspan="1">1</td><td rowspan="1">弱</td></tr>
<tr><td rowspan="1">20%</td><td rowspan="1">2</td><td rowspan="1">轻抬慢回（温顺舒缓）</td><td rowspan="1">6</td><td rowspan="1">持续安抚中的重复回应；比第一条更柔；安静状态下的陪伴回声。</td><td rowspan="1">0</td><td rowspan="1">关闭</td></tr>
<tr><td rowspan="6">12</td><td rowspan="6">腹部长抚</td><td rowspan="2">1｜开心</td><td rowspan="1">70%</td><td rowspan="1">13</td><td rowspan="1">抬头后快速点头（很乐意）</td><td rowspan="1">12</td><td rowspan="1">认同反馈的另一变体；避免与上一条完全重复；同样轻快的肯定感。</td><td rowspan="1">2</td><td rowspan="1">中</td></tr>
<tr><td rowspan="1">30%</td><td rowspan="1">11</td><td rowspan="1">快速上下点头（快速撸通用开心）</td><td rowspan="1">47</td><td rowspan="1">愉快互动的第二条；同样偏快、偏亮；轮换用的开心反馈。</td><td rowspan="2">1</td><td rowspan="2">弱</td></tr>
<tr><td rowspan="2">2｜平静</td><td rowspan="1">70%</td><td rowspan="2">18</td><td rowspan="2">单次轻触缓慢抬头观察</td><td rowspan="2">25</td><td rowspan="2">温暖友好、被好好对待后的软回应；社交开场或亲密回馈。</td></tr>
<tr><td rowspan="1">30%</td><td rowspan="1">0</td><td rowspan="1">关闭</td></tr>
<tr><td rowspan="2">3｜悲伤</td><td rowspan="1">80%</td><td rowspan="1">16</td><td rowspan="1">突发触碰单次躲闪</td><td rowspan="1">31</td><td rowspan="1">惊吓或不安后的缓和；从紧张回到可互动；带一点不好意思的恢复声。</td><td rowspan="1">1</td><td rowspan="1">弱</td></tr>
<tr><td rowspan="1">20%</td><td rowspan="1">2</td><td rowspan="1">轻抬慢回（温顺舒缓）</td><td rowspan="1">6</td><td rowspan="1">持续安抚中的重复回应；比第一条更柔；安静状态下的陪伴回声。</td><td rowspan="1">0</td><td rowspan="1">关闭</td></tr>
<tr><td rowspan="6">13</td><td rowspan="6">左侧轻触</td><td rowspan="6">Beta Y</td><td rowspan="2">1｜开心</td><td rowspan="1">70%</td><td rowspan="1">13</td><td rowspan="1">抬头后快速点头（很乐意）</td><td rowspan="1">12</td><td rowspan="1">认同反馈的另一变体；避免与上一条完全重复；同样轻快的肯定感。</td><td rowspan="1">2</td><td rowspan="1">中</td></tr>
<tr><td rowspan="1">30%</td><td rowspan="1">11</td><td rowspan="1">快速上下点头（快速撸通用开心）</td><td rowspan="1">47</td><td rowspan="1">愉快互动的第二条；同样偏快、偏亮；轮换用的开心反馈。</td><td rowspan="2">1</td><td rowspan="2">弱</td></tr>
<tr><td rowspan="2">2｜平静</td><td rowspan="1">70%</td><td rowspan="1">43</td><td rowspan="1">定点单侧观望（左）</td><td rowspan="1">36</td><td rowspan="1">侧面被轻触后的确认；友好探询；轻量互动中的“我在”。</td></tr>
<tr><td rowspan="1">30%</td><td rowspan="1">18</td><td rowspan="1">单次轻触缓慢抬头观察</td><td rowspan="1">25</td><td rowspan="1">温暖友好、被好好对待后的软回应；社交开场或亲密回馈。</td><td rowspan="1">0</td><td rowspan="1">关闭</td></tr>
<tr><td rowspan="2">3｜悲伤</td><td rowspan="1">80%</td><td rowspan="1">16</td><td rowspan="1">突发触碰单次躲闪</td><td rowspan="1">31</td><td rowspan="1">惊吓或不安后的缓和；从紧张回到可互动；带一点不好意思的恢复声。</td><td rowspan="1">1</td><td rowspan="1">弱</td></tr>
<tr><td rowspan="1">20%</td><td rowspan="1">2</td><td rowspan="1">轻抬慢回（温顺舒缓）</td><td rowspan="1">6</td><td rowspan="1">持续安抚中的重复回应；比第一条更柔；安静状态下的陪伴回声。</td><td rowspan="1">0</td><td rowspan="1">关闭</td></tr>
<tr><td rowspan="6">14</td><td rowspan="6">左侧短抚</td><td rowspan="12">预留 Beta N</td><td rowspan="2">1｜开心</td><td rowspan="1">70%</td><td rowspan="1">11</td><td rowspan="1">快速上下点头（快速撸通用开心）</td><td rowspan="1">10</td><td rowspan="1">节奏偏快的愉快互动；兴奋且享受；需要明亮的开心短声。</td><td rowspan="1">2</td><td rowspan="1">中</td></tr>
<tr><td rowspan="1">30%</td><td rowspan="1">13</td><td rowspan="1">抬头后快速点头（很乐意）</td><td rowspan="1">49</td><td rowspan="1">认同反馈的第四条；保持轻快；批量互动时轮换。</td><td rowspan="2">1</td><td rowspan="2">弱</td></tr>
<tr><td rowspan="2">2｜平静</td><td rowspan="1">70%</td><td rowspan="1">43</td><td rowspan="1">定点单侧观望（左）</td><td rowspan="1">36</td><td rowspan="1">侧面被轻触后的确认；友好探询；轻量互动中的“我在”。</td></tr>
<tr><td rowspan="1">30%</td><td rowspan="1">18</td><td rowspan="1">单次轻触缓慢抬头观察</td><td rowspan="1">25</td><td rowspan="1">温暖友好、被好好对待后的软回应；社交开场或亲密回馈。</td><td rowspan="1">0</td><td rowspan="1">关闭</td></tr>
<tr><td rowspan="2">3｜悲伤</td><td rowspan="1">80%</td><td rowspan="1">25</td><td rowspan="1">快速撸过度刺激躲闪</td><td rowspan="1">31</td><td rowspan="1">惊吓或不安后的缓和；从紧张回到可互动；带一点不好意思的恢复声。</td><td rowspan="1">1</td><td rowspan="1">弱</td></tr>
<tr><td rowspan="1">20%</td><td rowspan="1">2</td><td rowspan="1">轻抬慢回（温顺舒缓）</td><td rowspan="1">6</td><td rowspan="1">持续安抚中的重复回应；比第一条更柔；安静状态下的陪伴回声。</td><td rowspan="1">0</td><td rowspan="1">关闭</td></tr>
<tr><td rowspan="6">15</td><td rowspan="6">左侧长抚</td><td rowspan="2">1｜开心</td><td rowspan="1">70%</td><td rowspan="1">13</td><td rowspan="1">抬头后快速点头（很乐意）</td><td rowspan="1">12</td><td rowspan="1">认同反馈的另一变体；避免与上一条完全重复；同样轻快的肯定感。</td><td rowspan="1">2</td><td rowspan="1">中</td></tr>
<tr><td rowspan="1">30%</td><td rowspan="1">11</td><td rowspan="1">快速上下点头（快速撸通用开心）</td><td rowspan="1">47</td><td rowspan="1">愉快互动的第二条；同样偏快、偏亮；轮换用的开心反馈。</td><td rowspan="2">1</td><td rowspan="2">弱</td></tr>
<tr><td rowspan="2">2｜平静</td><td rowspan="1">70%</td><td rowspan="1">43</td><td rowspan="1">定点单侧观望（左）</td><td rowspan="1">36</td><td rowspan="1">侧面被轻触后的确认；友好探询；轻量互动中的“我在”。</td></tr>
<tr><td rowspan="1">30%</td><td rowspan="1">18</td><td rowspan="1">单次轻触缓慢抬头观察</td><td rowspan="1">25</td><td rowspan="1">温暖友好、被好好对待后的软回应；社交开场或亲密回馈。</td><td rowspan="1">0</td><td rowspan="1">关闭</td></tr>
<tr><td rowspan="2">3｜悲伤</td><td rowspan="1">80%</td><td rowspan="1">16</td><td rowspan="1">突发触碰单次躲闪</td><td rowspan="1">31</td><td rowspan="1">惊吓或不安后的缓和；从紧张回到可互动；带一点不好意思的恢复声。</td><td rowspan="1">1</td><td rowspan="1">弱</td></tr>
<tr><td rowspan="1">20%</td><td rowspan="1">2</td><td rowspan="1">轻抬慢回（温顺舒缓）</td><td rowspan="1">6</td><td rowspan="1">持续安抚中的重复回应；比第一条更柔；安静状态下的陪伴回声。</td><td rowspan="1">0</td><td rowspan="1">关闭</td></tr>
<tr><td rowspan="6">16</td><td rowspan="6">右侧轻触</td><td rowspan="6">Beta Y</td><td rowspan="2">1｜开心</td><td rowspan="1">70%</td><td rowspan="1">13</td><td rowspan="1">抬头后快速点头（很乐意）</td><td rowspan="1">12</td><td rowspan="1">认同反馈的另一变体；避免与上一条完全重复；同样轻快的肯定感。</td><td rowspan="1">2</td><td rowspan="1">中</td></tr>
<tr><td rowspan="1">30%</td><td rowspan="1">11</td><td rowspan="1">快速上下点头（快速撸通用开心）</td><td rowspan="1">47</td><td rowspan="1">愉快互动的第二条；同样偏快、偏亮；轮换用的开心反馈。</td><td rowspan="2">1</td><td rowspan="2">弱</td></tr>
<tr><td rowspan="2">2｜平静</td><td rowspan="1">70%</td><td rowspan="1">45</td><td rowspan="1">定点单侧观望（右）</td><td rowspan="1">56</td><td rowspan="1">另一侧的轻量确认；友好接近；短促的“我知道你在”。</td></tr>
<tr><td rowspan="1">30%</td><td rowspan="1">18</td><td rowspan="1">单次轻触缓慢抬头观察</td><td rowspan="1">25</td><td rowspan="1">温暖友好、被好好对待后的软回应；社交开场或亲密回馈。</td><td rowspan="1">0</td><td rowspan="1">关闭</td></tr>
<tr><td rowspan="2">3｜悲伤</td><td rowspan="1">80%</td><td rowspan="1">16</td><td rowspan="1">突发触碰单次躲闪</td><td rowspan="1">31</td><td rowspan="1">惊吓或不安后的缓和；从紧张回到可互动；带一点不好意思的恢复声。</td><td rowspan="1">1</td><td rowspan="1">弱</td></tr>
<tr><td rowspan="1">20%</td><td rowspan="1">2</td><td rowspan="1">轻抬慢回（温顺舒缓）</td><td rowspan="1">6</td><td rowspan="1">持续安抚中的重复回应；比第一条更柔；安静状态下的陪伴回声。</td><td rowspan="1">0</td><td rowspan="1">关闭</td></tr>
<tr><td rowspan="6">17</td><td rowspan="6">右侧短抚</td><td rowspan="12">预留 Beta N</td><td rowspan="2">1｜开心</td><td rowspan="1">70%</td><td rowspan="1">11</td><td rowspan="1">快速上下点头（快速撸通用开心）</td><td rowspan="1">10</td><td rowspan="1">节奏偏快的愉快互动；兴奋且享受；需要明亮的开心短声。</td><td rowspan="1">2</td><td rowspan="1">中</td></tr>
<tr><td rowspan="1">30%</td><td rowspan="1">13</td><td rowspan="1">抬头后快速点头（很乐意）</td><td rowspan="1">49</td><td rowspan="1">认同反馈的第四条；保持轻快；批量互动时轮换。</td><td rowspan="2">1</td><td rowspan="2">弱</td></tr>
<tr><td rowspan="2">2｜平静</td><td rowspan="1">70%</td><td rowspan="1">45</td><td rowspan="1">定点单侧观望（右）</td><td rowspan="1">56</td><td rowspan="1">另一侧的轻量确认；友好接近；短促的“我知道你在”。</td></tr>
<tr><td rowspan="1">30%</td><td rowspan="1">18</td><td rowspan="1">单次轻触缓慢抬头观察</td><td rowspan="1">25</td><td rowspan="1">温暖友好、被好好对待后的软回应；社交开场或亲密回馈。</td><td rowspan="1">0</td><td rowspan="1">关闭</td></tr>
<tr><td rowspan="2">3｜悲伤</td><td rowspan="1">80%</td><td rowspan="1">25</td><td rowspan="1">快速撸过度刺激躲闪</td><td rowspan="1">31</td><td rowspan="1">惊吓或不安后的缓和；从紧张回到可互动；带一点不好意思的恢复声。</td><td rowspan="1">1</td><td rowspan="1">弱</td></tr>
<tr><td rowspan="1">20%</td><td rowspan="1">2</td><td rowspan="1">轻抬慢回（温顺舒缓）</td><td rowspan="1">6</td><td rowspan="1">持续安抚中的重复回应；比第一条更柔；安静状态下的陪伴回声。</td><td rowspan="1">0</td><td rowspan="1">关闭</td></tr>
<tr><td rowspan="6">18</td><td rowspan="6">右侧长抚</td><td rowspan="2">1｜开心</td><td rowspan="1">70%</td><td rowspan="1">13</td><td rowspan="1">抬头后快速点头（很乐意）</td><td rowspan="1">12</td><td rowspan="1">认同反馈的另一变体；避免与上一条完全重复；同样轻快的肯定感。</td><td rowspan="1">2</td><td rowspan="1">中</td></tr>
<tr><td rowspan="1">30%</td><td rowspan="1">11</td><td rowspan="1">快速上下点头（快速撸通用开心）</td><td rowspan="1">47</td><td rowspan="1">愉快互动的第二条；同样偏快、偏亮；轮换用的开心反馈。</td><td rowspan="2">1</td><td rowspan="2">弱</td></tr>
<tr><td rowspan="2">2｜平静</td><td rowspan="1">70%</td><td rowspan="1">45</td><td rowspan="1">定点单侧观望（右）</td><td rowspan="1">56</td><td rowspan="1">另一侧的轻量确认；友好接近；短促的“我知道你在”。</td></tr>
<tr><td rowspan="1">30%</td><td rowspan="1">18</td><td rowspan="1">单次轻触缓慢抬头观察</td><td rowspan="1">25</td><td rowspan="1">温暖友好、被好好对待后的软回应；社交开场或亲密回馈。</td><td rowspan="1">0</td><td rowspan="1">关闭</td></tr>
<tr><td rowspan="2">3｜悲伤</td><td rowspan="1">80%</td><td rowspan="1">16</td><td rowspan="1">突发触碰单次躲闪</td><td rowspan="1">31</td><td rowspan="1">惊吓或不安后的缓和；从紧张回到可互动；带一点不好意思的恢复声。</td><td rowspan="1">1</td><td rowspan="1">弱</td></tr>
<tr><td rowspan="1">20%</td><td rowspan="1">2</td><td rowspan="1">轻抬慢回（温顺舒缓）</td><td rowspan="1">6</td><td rowspan="1">持续安抚中的重复回应；比第一条更柔；安静状态下的陪伴回声。</td><td rowspan="1">0</td><td rowspan="1">关闭</td></tr>
<tr><td rowspan="6">19</td><td rowspan="6">后背轻触</td><td rowspan="6">Beta Y</td><td rowspan="2">1｜开心</td><td rowspan="1">70%</td><td rowspan="1">13</td><td rowspan="1">抬头后快速点头（很乐意）</td><td rowspan="1">12</td><td rowspan="1">认同反馈的另一变体；避免与上一条完全重复；同样轻快的肯定感。</td><td rowspan="1">2</td><td rowspan="1">中</td></tr>
<tr><td rowspan="1">30%</td><td rowspan="1">11</td><td rowspan="1">快速上下点头（快速撸通用开心）</td><td rowspan="1">47</td><td rowspan="1">愉快互动的第二条；同样偏快、偏亮；轮换用的开心反馈。</td><td rowspan="2">1</td><td rowspan="2">弱</td></tr>
<tr><td rowspan="2">2｜平静</td><td rowspan="1">70%</td><td rowspan="1">43</td><td rowspan="1">定点单侧观望（左）</td><td rowspan="1">8</td><td rowspan="1">突然被从一侧接近；需要快速确认方位；短暂警觉后的注意。</td></tr>
<tr><td rowspan="1">30%</td><td rowspan="1">18</td><td rowspan="1">单次轻触缓慢抬头观察</td><td rowspan="1">25</td><td rowspan="1">温暖友好、被好好对待后的软回应；社交开场或亲密回馈。</td><td rowspan="1">0</td><td rowspan="1">关闭</td></tr>
<tr><td rowspan="2">3｜悲伤</td><td rowspan="1">80%</td><td rowspan="1">16</td><td rowspan="1">突发触碰单次躲闪</td><td rowspan="1">31</td><td rowspan="1">惊吓或不安后的缓和；从紧张回到可互动；带一点不好意思的恢复声。</td><td rowspan="1">1</td><td rowspan="1">弱</td></tr>
<tr><td rowspan="1">20%</td><td rowspan="1">2</td><td rowspan="1">轻抬慢回（温顺舒缓）</td><td rowspan="1">6</td><td rowspan="1">持续安抚中的重复回应；比第一条更柔；安静状态下的陪伴回声。</td><td rowspan="1">0</td><td rowspan="1">关闭</td></tr>
<tr><td rowspan="6">20</td><td rowspan="6">后背短抚</td><td rowspan="32">预留 Beta N</td><td rowspan="2">1｜开心</td><td rowspan="1">70%</td><td rowspan="1">11</td><td rowspan="1">快速上下点头（快速撸通用开心）</td><td rowspan="1">10</td><td rowspan="1">节奏偏快的愉快互动；兴奋且享受；需要明亮的开心短声。</td><td rowspan="1">2</td><td rowspan="1">中</td></tr>
<tr><td rowspan="1">30%</td><td rowspan="1">13</td><td rowspan="1">抬头后快速点头（很乐意）</td><td rowspan="1">49</td><td rowspan="1">认同反馈的第四条；保持轻快；批量互动时轮换。</td><td rowspan="2">1</td><td rowspan="2">弱</td></tr>
<tr><td rowspan="2">2｜平静</td><td rowspan="1">70%</td><td rowspan="1">43</td><td rowspan="1">定点单侧观望（左）</td><td rowspan="1">8</td><td rowspan="1">突然被从一侧接近；需要快速确认方位；短暂警觉后的注意。</td></tr>
<tr><td rowspan="1">30%</td><td rowspan="1">18</td><td rowspan="1">单次轻触缓慢抬头观察</td><td rowspan="1">25</td><td rowspan="1">温暖友好、被好好对待后的软回应；社交开场或亲密回馈。</td><td rowspan="1">0</td><td rowspan="1">关闭</td></tr>
<tr><td rowspan="2">3｜悲伤</td><td rowspan="1">80%</td><td rowspan="1">25</td><td rowspan="1">快速撸过度刺激躲闪</td><td rowspan="1">31</td><td rowspan="1">惊吓或不安后的缓和；从紧张回到可互动；带一点不好意思的恢复声。</td><td rowspan="1">1</td><td rowspan="1">弱</td></tr>
<tr><td rowspan="1">20%</td><td rowspan="1">2</td><td rowspan="1">轻抬慢回（温顺舒缓）</td><td rowspan="1">6</td><td rowspan="1">持续安抚中的重复回应；比第一条更柔；安静状态下的陪伴回声。</td><td rowspan="1">0</td><td rowspan="1">关闭</td></tr>
<tr><td rowspan="6">21</td><td rowspan="6">后背长抚</td><td rowspan="2">1｜开心</td><td rowspan="1">70%</td><td rowspan="1">13</td><td rowspan="1">抬头后快速点头（很乐意）</td><td rowspan="1">12</td><td rowspan="1">认同反馈的另一变体；避免与上一条完全重复；同样轻快的肯定感。</td><td rowspan="1">2</td><td rowspan="1">中</td></tr>
<tr><td rowspan="1">30%</td><td rowspan="1">11</td><td rowspan="1">快速上下点头（快速撸通用开心）</td><td rowspan="1">47</td><td rowspan="1">愉快互动的第二条；同样偏快、偏亮；轮换用的开心反馈。</td><td rowspan="2">1</td><td rowspan="2">弱</td></tr>
<tr><td rowspan="2">2｜平静</td><td rowspan="1">70%</td><td rowspan="1">43</td><td rowspan="1">定点单侧观望（左）</td><td rowspan="1">8</td><td rowspan="1">突然被从一侧接近；需要快速确认方位；短暂警觉后的注意。</td></tr>
<tr><td rowspan="1">30%</td><td rowspan="1">18</td><td rowspan="1">单次轻触缓慢抬头观察</td><td rowspan="1">25</td><td rowspan="1">温暖友好、被好好对待后的软回应；社交开场或亲密回馈。</td><td rowspan="1">0</td><td rowspan="1">关闭</td></tr>
<tr><td rowspan="2">3｜悲伤</td><td rowspan="1">80%</td><td rowspan="1">16</td><td rowspan="1">突发触碰单次躲闪</td><td rowspan="1">31</td><td rowspan="1">惊吓或不安后的缓和；从紧张回到可互动；带一点不好意思的恢复声。</td><td rowspan="1">1</td><td rowspan="1">弱</td></tr>
<tr><td rowspan="1">20%</td><td rowspan="1">2</td><td rowspan="1">轻抬慢回（温顺舒缓）</td><td rowspan="1">6</td><td rowspan="1">持续安抚中的重复回应；比第一条更柔；安静状态下的陪伴回声。</td><td rowspan="1">0</td><td rowspan="1">关闭</td></tr>
<tr><td rowspan="6">22</td><td rowspan="6">长时间握持</td><td rowspan="2">1｜开心</td><td rowspan="1">70%</td><td rowspan="1">46</td><td rowspan="1">短时握持间断晃头（Sustainedhold）</td><td rowspan="1">33</td><td rowspan="1">黏人、舍不得分开；被抱持时的依赖；温暖的撒娇贴近。</td><td rowspan="1">2</td><td rowspan="1">中</td></tr>
<tr><td rowspan="1">30%</td><td rowspan="1">60</td><td rowspan="1">被拿起上扬连续点头（Pickedup）</td><td rowspan="1">34</td><td rowspan="1">黏人升级；主动蹭近；开心又舍不得被放下。</td><td rowspan="3">1</td><td rowspan="3">弱</td></tr>
<tr><td rowspan="2">2｜平静</td><td rowspan="1">70%</td><td rowspan="1">54</td><td rowspan="1">长时间握持间断打量</td><td rowspan="1">57</td><td rowspan="1">侧面重复互动后的更友好回应；轻贴近；二级确认。</td></tr>
<tr><td rowspan="1">30%</td><td rowspan="1">60</td><td rowspan="1">被拿起上扬连续点头（Pickedup）</td><td rowspan="1">34</td><td rowspan="1">黏人升级；主动蹭近；开心又舍不得被放下。</td></tr>
<tr><td rowspan="2">3｜悲伤</td><td rowspan="1">80%</td><td rowspan="1">54</td><td rowspan="1">长时间握持间断打量</td><td rowspan="1">57</td><td rowspan="1">侧面重复互动后的更友好回应；轻贴近；二级确认。</td><td rowspan="2">0</td><td rowspan="2">关闭</td></tr>
<tr><td rowspan="1">20%</td><td rowspan="1">52</td><td rowspan="1">长时间握持静靠（Sustainedhold）</td><td rowspan="1">35</td><td rowspan="1">依赖感最浓的一版；长时间贴近；柔和持续的撒娇。</td></tr>
<tr><td rowspan="6">23</td><td rowspan="6">轻摇</td><td rowspan="2">1｜开心</td><td rowspan="1">70%</td><td rowspan="1">28</td><td rowspan="1">轻摇小幅快点头（Gentleshake）</td><td rowspan="1">18</td><td rowspan="1">熟悉的人唤醒；日常互动开始；比正式开机更轻快的起始。</td><td rowspan="1">2</td><td rowspan="1">中</td></tr>
<tr><td rowspan="1">30%</td><td rowspan="2">49</td><td rowspan="2">轻摇缓慢环视</td><td rowspan="1">25</td><td rowspan="1">温暖友好、被好好对待后的软回应；社交开场或亲密回馈。</td><td rowspan="3">1</td><td rowspan="3">弱</td></tr>
<tr><td rowspan="2">2｜平静</td><td rowspan="1">70%</td><td rowspan="1">41</td><td rowspan="1">熟悉后的侧面短回声；亲昵互动中的二次确认；更松弛一点。</td></tr>
<tr><td rowspan="1">30%</td><td rowspan="1">28</td><td rowspan="1">轻摇小幅快点头（Gentleshake）</td><td rowspan="1">18</td><td rowspan="1">熟悉的人唤醒；日常互动开始；比正式开机更轻快的起始。</td></tr>
<tr><td rowspan="2">3｜悲伤</td><td rowspan="1">80%</td><td rowspan="1">49</td><td rowspan="1">轻摇缓慢环视</td><td rowspan="1">31</td><td rowspan="1">惊吓或不安后的缓和；从紧张回到可互动；带一点不好意思的恢复声。</td><td rowspan="2">0</td><td rowspan="2">关闭</td></tr>
<tr><td rowspan="1">20%</td><td rowspan="1">2</td><td rowspan="1">轻抬慢回（温顺舒缓）</td><td rowspan="1">6</td><td rowspan="1">持续安抚中的重复回应；比第一条更柔；安静状态下的陪伴回声。</td></tr>
<tr><td rowspan="2">24</td><td rowspan="2">猛摇</td><td rowspan="2">0｜ANY</td><td rowspan="1">70%</td><td rowspan="1">31</td><td rowspan="1">粗暴握持高频躲闪颤</td><td rowspan="1">22</td><td rowspan="1">被拘束、不舒服；害怕但克制；需要不安的弱抗议。</td><td rowspan="3">1</td><td rowspan="3">弱</td></tr>
<tr><td rowspan="1">30%</td><td rowspan="1">25</td><td rowspan="1">快速撸过度刺激躲闪</td><td rowspan="1">15</td><td rowspan="1">不安、紧绷时的短反馈；安全感下降。</td></tr>
<tr><td rowspan="6">25</td><td rowspan="6">翻转</td><td rowspan="2">1｜开心</td><td rowspan="1">70%</td><td rowspan="1">47</td><td rowspan="1">翻转肚皮上扬晃头（Flipbelly-up）</td><td rowspan="1">9</td><td rowspan="1">信任感较高时的满足回应；放松且开心一点；短时亲密反馈。</td></tr>
<tr><td rowspan="1">30%</td><td rowspan="1">22</td><td rowspan="1">翻转肚皮静态垂头</td><td rowspan="1">53</td><td rowspan="1">满足后的轻叹；放松惬意；亲密安抚后的绵长收束。</td><td rowspan="1">0</td><td rowspan="1">关闭</td></tr>
<tr><td rowspan="2">2｜平静</td><td rowspan="1">70%</td><td rowspan="1">47</td><td rowspan="1">翻转肚皮上扬晃头（Flipbelly-up）</td><td rowspan="1">9</td><td rowspan="1">信任感较高时的满足回应；放松且开心一点；短时亲密反馈。</td><td rowspan="1">1</td><td rowspan="1">弱</td></tr>
<tr><td rowspan="1">30%</td><td rowspan="1">22</td><td rowspan="1">翻转肚皮静态垂头</td><td rowspan="1">53</td><td rowspan="1">满足后的轻叹；放松惬意；亲密安抚后的绵长收束。</td><td rowspan="1">0</td><td rowspan="1">关闭</td></tr>
<tr><td rowspan="2">3｜悲伤</td><td rowspan="1">80%</td><td rowspan="1">5</td><td rowspan="1">强行翻肚皮垂头</td><td rowspan="1">14</td><td rowspan="1">抗拒升级但仍克制；不想被继续折腾；委屈抗议的第二条。</td><td rowspan="1">1</td><td rowspan="1">弱</td></tr>
<tr><td rowspan="1">20%</td><td rowspan="1">22</td><td rowspan="1">翻转肚皮静态垂头</td><td rowspan="1">53</td><td rowspan="1">满足后的轻叹；放松惬意；亲密安抚后的绵长收束。</td><td rowspan="1">0</td><td rowspan="1">关闭</td></tr>
<tr><td rowspan="6">26</td><td rowspan="6">被拿起</td><td rowspan="12">原表划除</td><td rowspan="2">1｜开心</td><td rowspan="1">70%</td><td rowspan="1">60</td><td rowspan="1">被拿起上扬连续点头（Pickedup）</td><td rowspan="1">34</td><td rowspan="1">黏人升级；主动蹭近；开心又舍不得被放下。</td><td rowspan="1">2</td><td rowspan="1">中</td></tr>
<tr><td rowspan="1">30%</td><td rowspan="1">46</td><td rowspan="1">短时握持间断晃头（Sustainedhold）</td><td rowspan="1">33</td><td rowspan="1">黏人、舍不得分开；被抱持时的依赖；温暖的撒娇贴近。</td><td rowspan="1">1</td><td rowspan="1">弱</td></tr>
<tr><td rowspan="2">2｜平静</td><td rowspan="1">70%</td><td rowspan="1">60</td><td rowspan="1">被拿起上扬连续点头（Pickedup）</td><td rowspan="1">34</td><td rowspan="1">黏人升级；主动蹭近；开心又舍不得被放下。</td><td rowspan="1">2</td><td rowspan="1">中</td></tr>
<tr><td rowspan="1">30%</td><td rowspan="1">46</td><td rowspan="1">短时握持间断晃头（Sustainedhold）</td><td rowspan="1">33</td><td rowspan="1">黏人、舍不得分开；被抱持时的依赖；温暖的撒娇贴近。</td><td rowspan="1">1</td><td rowspan="1">弱</td></tr>
<tr><td rowspan="2">3｜悲伤</td><td rowspan="1">80%</td><td rowspan="1">54</td><td rowspan="1">长时间握持间断打量</td><td rowspan="1">57</td><td rowspan="1">侧面重复互动后的更友好回应；轻贴近；二级确认。</td><td rowspan="1">0</td><td rowspan="1">关闭</td></tr>
<tr><td rowspan="1">20%</td><td rowspan="1">46</td><td rowspan="1">短时握持间断晃头（Sustainedhold）</td><td rowspan="1">33</td><td rowspan="1">黏人、舍不得分开；被抱持时的依赖；温暖的撒娇贴近。</td><td rowspan="2">1</td><td rowspan="2">弱</td></tr>
<tr><td rowspan="6">27</td><td rowspan="6">被放下</td><td rowspan="2">1｜开心</td><td rowspan="1">70%</td><td rowspan="1">50</td><td rowspan="1">间断定点侧头试探</td><td rowspan="1">23</td><td rowspan="1">轻柔问候；关系刚开始或再次见面；低刺激的友好开场。</td></tr>
<tr><td rowspan="1">30%</td><td rowspan="1">9</td><td rowspan="1">上下缓慢抬升打量</td><td rowspan="1">25</td><td rowspan="1">温暖友好、被好好对待后的软回应；社交开场或亲密回馈。</td><td rowspan="1">0</td><td rowspan="1">关闭</td></tr>
<tr><td rowspan="2">2｜平静</td><td rowspan="1">70%</td><td rowspan="1">50</td><td rowspan="1">间断定点侧头试探</td><td rowspan="1">23</td><td rowspan="1">轻柔问候；关系刚开始或再次见面；低刺激的友好开场。</td><td rowspan="1">1</td><td rowspan="1">弱</td></tr>
<tr><td rowspan="1">30%</td><td rowspan="1">9</td><td rowspan="1">上下缓慢抬升打量</td><td rowspan="1">25</td><td rowspan="1">温暖友好、被好好对待后的软回应；社交开场或亲密回馈。</td><td rowspan="3">0</td><td rowspan="3">关闭</td></tr>
<tr><td rowspan="2">3｜悲伤</td><td rowspan="1">80%</td><td rowspan="1">3</td><td rowspan="1">放下后长期垂头</td><td rowspan="1">21</td><td rowspan="1">夜间进一步安静；准备休息；需要更柔、更长的过渡。</td></tr>
<tr><td rowspan="1">20%</td><td rowspan="1">50</td><td rowspan="1">间断定点侧头试探</td><td rowspan="1">23</td><td rowspan="1">轻柔问候；关系刚开始或再次见面；低刺激的友好开场。</td></tr>
<tr><td rowspan="6">28</td><td rowspan="6">唤醒提示词</td><td rowspan="14">Beta Y</td><td rowspan="2">1｜开心</td><td rowspan="1">70%</td><td rowspan="1">30</td><td rowspan="1">唤醒急促小颤头（唤醒词）</td><td rowspan="1">26</td><td rowspan="1">被唤醒进入互动；从待机转到兴奋；期待被陪伴的第一声。</td><td rowspan="1">2</td><td rowspan="1">中</td></tr>
<tr><td rowspan="1">30%</td><td rowspan="1">13</td><td rowspan="1">抬头后快速点头（很乐意）</td><td rowspan="1">49</td><td rowspan="1">认同反馈的第四条；保持轻快；批量互动时轮换。</td><td rowspan="1">1</td><td rowspan="1">弱</td></tr>
<tr><td rowspan="2">2｜平静</td><td rowspan="1">70%</td><td rowspan="1">30</td><td rowspan="1">唤醒急促小颤头（唤醒词）</td><td rowspan="1">26</td><td rowspan="1">被唤醒进入互动；从待机转到兴奋；期待被陪伴的第一声。</td><td rowspan="1">2</td><td rowspan="1">中</td></tr>
<tr><td rowspan="1">30%</td><td rowspan="1">13</td><td rowspan="1">抬头后快速点头（很乐意）</td><td rowspan="1">49</td><td rowspan="1">认同反馈的第四条；保持轻快；批量互动时轮换。</td><td rowspan="1">1</td><td rowspan="1">弱</td></tr>
<tr><td rowspan="2">3｜悲伤</td><td rowspan="1">80%</td><td rowspan="1">9</td><td rowspan="1">上下缓慢抬升打量</td><td rowspan="1">45</td><td rowspan="1">同一侧再次被注意；熟悉后的警觉确认；轻回头式的注意。</td><td rowspan="1">0</td><td rowspan="1">关闭</td></tr>
<tr><td rowspan="1">20%</td><td rowspan="1">57</td><td rowspan="1">左右循环环视</td><td rowspan="1">41</td><td rowspan="1">熟悉后的侧面短回声；亲昵互动中的二次确认；更松弛一点。</td><td rowspan="1">1</td><td rowspan="1">弱</td></tr>
<tr><td rowspan="2">29</td><td rowspan="2">光线变暗</td><td rowspan="2">0｜ANY</td><td rowspan="2">50%</td><td rowspan="1">23</td><td rowspan="1">暗光低头慢挪</td><td rowspan="1">21</td><td rowspan="1">夜间进一步安静；准备休息；需要更柔、更长的过渡。</td><td rowspan="2">0</td><td rowspan="2">关闭</td></tr>
<tr><td rowspan="1">55</td><td rowspan="1">暗光慵懒垂头（Darkness）</td><td rowspan="1">42</td><td rowspan="1">环境变暗；从活跃转入安静；准备进入低刺激状态。</td></tr>
<tr><td rowspan="6">30</td><td rowspan="6">光线变亮</td><td rowspan="2">1｜开心</td><td rowspan="1">70%</td><td rowspan="1">50</td><td rowspan="1">间断定点侧头试探</td><td rowspan="1">38</td><td rowspan="1">调皮、小得意的短促 chirp；轻松逗弄。</td><td rowspan="4">1</td><td rowspan="4">弱</td></tr>
<tr><td rowspan="1">30%</td><td rowspan="1">59</td><td rowspan="1">左右快速摆头好奇（强光/唤醒）</td><td rowspan="1">26</td><td rowspan="1">被唤醒进入互动；从待机转到兴奋；期待被陪伴的第一声。</td></tr>
<tr><td rowspan="2">2｜平静</td><td rowspan="1">70%</td><td rowspan="1">50</td><td rowspan="1">间断定点侧头试探</td><td rowspan="1">38</td><td rowspan="1">调皮、小得意的短促 chirp；轻松逗弄。</td></tr>
<tr><td rowspan="1">30%</td><td rowspan="1">59</td><td rowspan="1">左右快速摆头好奇（强光/唤醒）</td><td rowspan="1">26</td><td rowspan="1">被唤醒进入互动；从待机转到兴奋；期待被陪伴的第一声。</td></tr>
<tr><td rowspan="2">3｜悲伤</td><td rowspan="1">80%</td><td rowspan="1">50</td><td rowspan="1">间断定点侧头试探</td><td rowspan="1">52</td><td rowspan="1">近距离逗弄后的二次害羞；熟人之间；比第一次更软。</td><td rowspan="6">0</td><td rowspan="6">关闭</td></tr>
<tr><td rowspan="1">20%</td><td rowspan="1">9</td><td rowspan="1">上下缓慢抬升打量</td><td rowspan="1">45</td><td rowspan="1">同一侧再次被注意；熟悉后的警觉确认；轻回头式的注意。</td></tr>
<tr><td rowspan="2">31</td><td rowspan="2">2小时无互动</td><td rowspan="4">预留 Beta N</td><td rowspan="4">0｜ANY</td><td rowspan="1">70%</td><td rowspan="1">6</td><td rowspan="1">瞌睡</td><td rowspan="1">1</td><td rowspan="1">安静休息、低刺激存在感；长时间无互动或待机时的 resting 陪伴底。不用于充电提示。</td></tr>
<tr><td rowspan="1">30%</td><td rowspan="2">3</td><td rowspan="2">放下后长期垂头</td><td rowspan="2">3</td><td rowspan="2">独处过久；被放下后的空落；需要稀疏、带着一点想念的低声。</td></tr>
<tr><td rowspan="2">32</td><td rowspan="2">48小时无互动</td><td rowspan="1">60%</td></tr>
<tr><td rowspan="1">40%</td><td rowspan="1">6</td><td rowspan="1">瞌睡</td><td rowspan="1">1</td><td rowspan="1">安静休息、低刺激存在感；长时间无互动或待机时的 resting 陪伴底。不用于充电提示。</td></tr>
<tr><td rowspan="6">33</td><td rowspan="6">遇到新伙伴</td><td rowspan="18">Beta Y</td><td rowspan="2">1｜开心</td><td rowspan="1">70%</td><td rowspan="1">29</td><td rowspan="1">遇见同类双向晃头（陌生Beany）</td><td rowspan="1">25</td><td rowspan="1">温暖友好、被好好对待后的软回应；社交开场或亲密回馈。</td><td rowspan="1">2</td><td rowspan="1">中</td></tr>
<tr><td rowspan="1">30%</td><td rowspan="2">50</td><td rowspan="2">间断定点侧头试探</td><td rowspan="2">38</td><td rowspan="2">调皮、小得意的短促 chirp；轻松逗弄。</td><td rowspan="3">1</td><td rowspan="3">弱</td></tr>
<tr><td rowspan="2">2｜平静</td><td rowspan="1">70%</td></tr>
<tr><td rowspan="1">30%</td><td rowspan="1">29</td><td rowspan="1">遇见同类双向晃头（陌生Beany）</td><td rowspan="1">25</td><td rowspan="1">温暖友好、被好好对待后的软回应；社交开场或亲密回馈。</td></tr>
<tr><td rowspan="2">3｜悲伤</td><td rowspan="1">80%</td><td rowspan="1">17</td><td rowspan="1">初识同类慢偏头试探</td><td rowspan="1">30</td><td rowspan="1">害羞躲闪的变体；慢慢适应被关注；比上一条略软一点。</td><td rowspan="2">0</td><td rowspan="2">关闭</td></tr>
<tr><td rowspan="1">20%</td><td rowspan="1">50</td><td rowspan="1">间断定点侧头试探</td><td rowspan="1">52</td><td rowspan="1">近距离逗弄后的二次害羞；熟人之间；比第一次更软。</td></tr>
<tr><td rowspan="6">34</td><td rowspan="6">遇到熟悉伙伴</td><td rowspan="2">1｜开心</td><td rowspan="1">70%</td><td rowspan="1">34</td><td rowspan="1">遇见熟同类高频点头（熟悉Beany）</td><td rowspan="1">28</td><td rowspan="1">极度开心的第二条；狂喜或重逢式雀跃；避免与上一条听感雷同。</td><td rowspan="1">2</td><td rowspan="1">中</td></tr>
<tr><td rowspan="1">30%</td><td rowspan="1">33</td><td rowspan="1">点头同步左右小幅颤（极致开心）</td><td rowspan="1">10</td><td rowspan="1">节奏偏快的愉快互动；兴奋且享受；需要明亮的开心短声。</td><td rowspan="4">1</td><td rowspan="4">弱</td></tr>
<tr><td rowspan="2">2｜平静</td><td rowspan="1">70%</td><td rowspan="1">29</td><td rowspan="1">遇见同类双向晃头（陌生Beany）</td><td rowspan="1">38</td><td rowspan="1">调皮、小得意的短促 chirp；轻松逗弄。</td></tr>
<tr><td rowspan="1">30%</td><td rowspan="1">34</td><td rowspan="1">遇见熟同类高频点头（熟悉Beany）</td><td rowspan="1">33</td><td rowspan="1">黏人、舍不得分开；被抱持时的依赖；温暖的撒娇贴近。</td></tr>
<tr><td rowspan="2">3｜悲伤</td><td rowspan="1">80%</td><td rowspan="1">50</td><td rowspan="1">间断定点侧头试探</td><td rowspan="1">23</td><td rowspan="1">轻柔问候；关系刚开始或再次见面；低刺激的友好开场。</td></tr>
<tr><td rowspan="1">20%</td><td rowspan="1">17</td><td rowspan="1">初识同类慢偏头试探</td><td rowspan="1">30</td><td rowspan="1">害羞躲闪的变体；慢慢适应被关注；比上一条略软一点。</td><td rowspan="1">0</td><td rowspan="1">关闭</td></tr>
<tr><td rowspan="2">35</td><td rowspan="2">侧倒</td><td rowspan="10">0｜ANY</td><td rowspan="2">50%</td><td rowspan="1">36</td><td rowspan="2">侧倒低头向内躲闪</td><td rowspan="1">29</td><td rowspan="1">失去平衡、需要自保；侧向不稳；戒备但不攻击。</td><td rowspan="2">1</td><td rowspan="2">弱</td></tr>
<tr><td rowspan="1">40</td><td rowspan="1">32</td><td rowspan="1">自保戒备的第二条；持续不稳时的重复；更明确一点的护住自己。</td></tr>
<tr><td rowspan="1">36</td><td rowspan="1">充电</td><td rowspan="2">100%</td><td rowspan="1">1</td><td rowspan="1">充电启动单次点头（充电专属）</td><td rowspan="1">61</td><td rowspan="1">插上充电器/开始充电时的固定提示。</td><td rowspan="2">0</td><td rowspan="2">关闭</td></tr>
<tr><td rowspan="1">37</td><td rowspan="1">低电量</td><td rowspan="1">53</td><td rowspan="1">低电量间断抬头观望</td><td rowspan="1">40</td><td rowspan="1">低电量固定提示；能量将尽、虚弱收束；偏困倦的告别感。</td></tr>
<tr><td rowspan="2">38</td><td rowspan="2">开机</td><td rowspan="2">50%</td><td rowspan="1">8</td><td rowspan="1">开机上扬点头（开机启动）</td><td rowspan="1">7</td><td rowspan="1">开机上电；第一次苏醒；需要柔和、有活力的启动感。</td><td rowspan="2">1</td><td rowspan="2">弱</td></tr>
<tr><td rowspan="1">51</td><td rowspan="1">开机分段环视</td><td rowspan="1">39</td><td rowspan="1">开机苏醒的另一音色；同样柔和启动；用于避免总播同一条。</td></tr>
<tr><td rowspan="1">39</td><td rowspan="1">呼吸</td><td rowspan="1">预留 Beta N</td><td rowspan="4">100%</td><td rowspan="1">48</td><td rowspan="1">待机呼吸间断侧头</td><td rowspan="1">59</td><td rowspan="1">平稳持续的轻哼；待机伴随；低刺激氛围底。</td><td rowspan="1">0</td><td rowspan="1">关闭</td></tr>
<tr><td rowspan="1">40</td><td rowspan="1">抛起</td><td rowspan="1">Beta Y</td><td rowspan="1">58</td><td rowspan="1">抛起上扬晃头（抛起事件）</td><td rowspan="2">27</td><td rowspan="2">明显失重、刺激偏强；短暂离开稳定支撑；需要高能量反馈。</td><td rowspan="2">1</td><td rowspan="2">弱</td></tr>
<tr><td rowspan="1">41</td><td rowspan="1">旋转抛起</td><td rowspan="1">原表划除</td><td rowspan="1">32</td><td rowspan="1">旋转抛起极速环绕头（旋转抛）</td></tr>
<tr><td rowspan="1">42</td><td rowspan="1">关机</td><td rowspan="1">Beta Y</td><td rowspan="1">4</td><td rowspan="1">关机缓慢垂头锁位</td><td rowspan="1">4</td><td rowspan="1">关机进入彻底休眠；一天结束；需要渐弱、收束的入睡感。</td><td rowspan="1">0</td><td rowspan="1">关闭</td></tr></tbody>
</table>

## 相伴 102组候选条件

<table>
<thead>
<tr><th>事件ID</th><th>输入</th><th>启用</th><th>情绪ID / 分组</th><th>概率</th><th>动作ID</th><th>动作反馈</th><th>音频ID</th><th>伴音含义</th><th>震动ID</th><th>强度</th></tr></thead>
<tbody>
<tr><td rowspan="6">1</td><td rowspan="6">头顶轻触</td><td rowspan="6">Beta Y</td><td rowspan="2">1｜开心</td><td rowspan="1">75%</td><td rowspan="1">33</td><td rowspan="1">点头同步左右小幅颤（极致开心）</td><td rowspan="1">24</td><td rowspan="1">情绪冲到很高的开心；雀跃、想撒娇蹦跳；社交或亲密高峰。</td><td rowspan="1">2</td><td rowspan="1">中</td></tr>
<tr><td rowspan="1">25%</td><td rowspan="1">13</td><td rowspan="1">抬头后快速点头（很乐意）</td><td rowspan="1">49</td><td rowspan="1">认同反馈的第四条；保持轻快；批量互动时轮换。</td><td rowspan="3">1</td><td rowspan="3">弱</td></tr>
<tr><td rowspan="2">2｜平静</td><td rowspan="1">65%</td><td rowspan="1">45</td><td rowspan="1">定点单侧观望（右）</td><td rowspan="1">45</td><td rowspan="1">同一侧再次被注意；熟悉后的警觉确认；轻回头式的注意。</td></tr>
<tr><td rowspan="1">35%</td><td rowspan="1">13</td><td rowspan="1">抬头后快速点头（很乐意）</td><td rowspan="1">49</td><td rowspan="1">认同反馈的第四条；保持轻快；批量互动时轮换。</td></tr>
<tr><td rowspan="2">3｜悲伤</td><td rowspan="1">85%</td><td rowspan="1">2</td><td rowspan="1">轻抬慢回（温顺舒缓）</td><td rowspan="1">15</td><td rowspan="1">不安、紧绷时的短反馈；安全感下降。</td><td rowspan="2">0</td><td rowspan="2">关闭</td></tr>
<tr><td rowspan="1">15%</td><td rowspan="1">18</td><td rowspan="1">单次轻触缓慢抬头观察</td><td rowspan="1">31</td><td rowspan="1">惊吓或不安后的缓和；从紧张回到可互动；带一点不好意思的恢复声。</td></tr>
<tr><td rowspan="6">2</td><td rowspan="6">头顶短抚</td><td rowspan="12">预留 Beta N</td><td rowspan="2">1｜开心</td><td rowspan="1">75%</td><td rowspan="1">11</td><td rowspan="1">快速上下点头（快速撸通用开心）</td><td rowspan="1">10</td><td rowspan="1">节奏偏快的愉快互动；兴奋且享受；需要明亮的开心短声。</td><td rowspan="2">2</td><td rowspan="2">中</td></tr>
<tr><td rowspan="1">25%</td><td rowspan="1">33</td><td rowspan="1">点头同步左右小幅颤（极致开心）</td><td rowspan="1">24</td><td rowspan="1">情绪冲到很高的开心；雀跃、想撒娇蹦跳；社交或亲密高峰。</td></tr>
<tr><td rowspan="2">2｜平静</td><td rowspan="1">65%</td><td rowspan="1">45</td><td rowspan="1">定点单侧观望（右）</td><td rowspan="1">45</td><td rowspan="1">同一侧再次被注意；熟悉后的警觉确认；轻回头式的注意。</td><td rowspan="2">1</td><td rowspan="2">弱</td></tr>
<tr><td rowspan="1">35%</td><td rowspan="1">13</td><td rowspan="1">抬头后快速点头（很乐意）</td><td rowspan="1">49</td><td rowspan="1">认同反馈的第四条；保持轻快；批量互动时轮换。</td></tr>
<tr><td rowspan="2">3｜悲伤</td><td rowspan="1">85%</td><td rowspan="1">2</td><td rowspan="1">轻抬慢回（温顺舒缓）</td><td rowspan="1">15</td><td rowspan="1">不安、紧绷时的短反馈；安全感下降。</td><td rowspan="2">0</td><td rowspan="2">关闭</td></tr>
<tr><td rowspan="1">15%</td><td rowspan="1">18</td><td rowspan="1">单次轻触缓慢抬头观察</td><td rowspan="1">31</td><td rowspan="1">惊吓或不安后的缓和；从紧张回到可互动；带一点不好意思的恢复声。</td></tr>
<tr><td rowspan="6">3</td><td rowspan="6">头顶长抚</td><td rowspan="2">1｜开心</td><td rowspan="1">75%</td><td rowspan="1">33</td><td rowspan="1">点头同步左右小幅颤（极致开心）</td><td rowspan="1">24</td><td rowspan="1">情绪冲到很高的开心；雀跃、想撒娇蹦跳；社交或亲密高峰。</td><td rowspan="1">2</td><td rowspan="1">中</td></tr>
<tr><td rowspan="1">25%</td><td rowspan="1">13</td><td rowspan="1">抬头后快速点头（很乐意）</td><td rowspan="1">49</td><td rowspan="1">认同反馈的第四条；保持轻快；批量互动时轮换。</td><td rowspan="3">1</td><td rowspan="3">弱</td></tr>
<tr><td rowspan="2">2｜平静</td><td rowspan="1">65%</td><td rowspan="1">45</td><td rowspan="1">定点单侧观望（右）</td><td rowspan="1">45</td><td rowspan="1">同一侧再次被注意；熟悉后的警觉确认；轻回头式的注意。</td></tr>
<tr><td rowspan="1">35%</td><td rowspan="1">13</td><td rowspan="1">抬头后快速点头（很乐意）</td><td rowspan="1">49</td><td rowspan="1">认同反馈的第四条；保持轻快；批量互动时轮换。</td></tr>
<tr><td rowspan="2">3｜悲伤</td><td rowspan="1">85%</td><td rowspan="1">2</td><td rowspan="1">轻抬慢回（温顺舒缓）</td><td rowspan="1">15</td><td rowspan="1">不安、紧绷时的短反馈；安全感下降。</td><td rowspan="2">0</td><td rowspan="2">关闭</td></tr>
<tr><td rowspan="1">15%</td><td rowspan="1">18</td><td rowspan="1">单次轻触缓慢抬头观察</td><td rowspan="1">31</td><td rowspan="1">惊吓或不安后的缓和；从紧张回到可互动；带一点不好意思的恢复声。</td></tr>
<tr><td rowspan="6">4</td><td rowspan="6">头左轻触</td><td rowspan="6">Beta Y</td><td rowspan="2">1｜开心</td><td rowspan="1">75%</td><td rowspan="1">33</td><td rowspan="1">点头同步左右小幅颤（极致开心）</td><td rowspan="1">24</td><td rowspan="1">情绪冲到很高的开心；雀跃、想撒娇蹦跳；社交或亲密高峰。</td><td rowspan="1">2</td><td rowspan="1">中</td></tr>
<tr><td rowspan="1">25%</td><td rowspan="1">13</td><td rowspan="1">抬头后快速点头（很乐意）</td><td rowspan="1">49</td><td rowspan="1">认同反馈的第四条；保持轻快；批量互动时轮换。</td><td rowspan="3">1</td><td rowspan="3">弱</td></tr>
<tr><td rowspan="2">2｜平静</td><td rowspan="1">65%</td><td rowspan="1">43</td><td rowspan="1">定点单侧观望（左）</td><td rowspan="1">45</td><td rowspan="1">同一侧再次被注意；熟悉后的警觉确认；轻回头式的注意。</td></tr>
<tr><td rowspan="1">35%</td><td rowspan="1">13</td><td rowspan="1">抬头后快速点头（很乐意）</td><td rowspan="1">49</td><td rowspan="1">认同反馈的第四条；保持轻快；批量互动时轮换。</td></tr>
<tr><td rowspan="2">3｜悲伤</td><td rowspan="1">85%</td><td rowspan="1">2</td><td rowspan="1">轻抬慢回（温顺舒缓）</td><td rowspan="1">15</td><td rowspan="1">不安、紧绷时的短反馈；安全感下降。</td><td rowspan="2">0</td><td rowspan="2">关闭</td></tr>
<tr><td rowspan="1">15%</td><td rowspan="1">18</td><td rowspan="1">单次轻触缓慢抬头观察</td><td rowspan="1">31</td><td rowspan="1">惊吓或不安后的缓和；从紧张回到可互动；带一点不好意思的恢复声。</td></tr>
<tr><td rowspan="6">5</td><td rowspan="6">头左短抚</td><td rowspan="12">预留 Beta N</td><td rowspan="2">1｜开心</td><td rowspan="1">75%</td><td rowspan="1">42</td><td rowspan="1">单侧快速偏头蹭手（摸头左快速撸）</td><td rowspan="1">34</td><td rowspan="1">黏人升级；主动蹭近；开心又舍不得被放下。</td><td rowspan="2">2</td><td rowspan="2">中</td></tr>
<tr><td rowspan="1">25%</td><td rowspan="1">33</td><td rowspan="1">点头同步左右小幅颤（极致开心）</td><td rowspan="1">24</td><td rowspan="1">情绪冲到很高的开心；雀跃、想撒娇蹦跳；社交或亲密高峰。</td></tr>
<tr><td rowspan="2">2｜平静</td><td rowspan="1">65%</td><td rowspan="1">43</td><td rowspan="1">定点单侧观望（左）</td><td rowspan="1">45</td><td rowspan="1">同一侧再次被注意；熟悉后的警觉确认；轻回头式的注意。</td><td rowspan="2">1</td><td rowspan="2">弱</td></tr>
<tr><td rowspan="1">35%</td><td rowspan="1">13</td><td rowspan="1">抬头后快速点头（很乐意）</td><td rowspan="1">49</td><td rowspan="1">认同反馈的第四条；保持轻快；批量互动时轮换。</td></tr>
<tr><td rowspan="2">3｜悲伤</td><td rowspan="1">85%</td><td rowspan="1">2</td><td rowspan="1">轻抬慢回（温顺舒缓）</td><td rowspan="1">15</td><td rowspan="1">不安、紧绷时的短反馈；安全感下降。</td><td rowspan="2">0</td><td rowspan="2">关闭</td></tr>
<tr><td rowspan="1">15%</td><td rowspan="1">18</td><td rowspan="1">单次轻触缓慢抬头观察</td><td rowspan="1">31</td><td rowspan="1">惊吓或不安后的缓和；从紧张回到可互动；带一点不好意思的恢复声。</td></tr>
<tr><td rowspan="6">6</td><td rowspan="6">头左长抚</td><td rowspan="2">1｜开心</td><td rowspan="1">75%</td><td rowspan="1">33</td><td rowspan="1">点头同步左右小幅颤（极致开心）</td><td rowspan="1">24</td><td rowspan="1">情绪冲到很高的开心；雀跃、想撒娇蹦跳；社交或亲密高峰。</td><td rowspan="1">2</td><td rowspan="1">中</td></tr>
<tr><td rowspan="1">25%</td><td rowspan="1">13</td><td rowspan="1">抬头后快速点头（很乐意）</td><td rowspan="1">49</td><td rowspan="1">认同反馈的第四条；保持轻快；批量互动时轮换。</td><td rowspan="3">1</td><td rowspan="3">弱</td></tr>
<tr><td rowspan="2">2｜平静</td><td rowspan="1">65%</td><td rowspan="1">43</td><td rowspan="1">定点单侧观望（左）</td><td rowspan="1">45</td><td rowspan="1">同一侧再次被注意；熟悉后的警觉确认；轻回头式的注意。</td></tr>
<tr><td rowspan="1">35%</td><td rowspan="1">13</td><td rowspan="1">抬头后快速点头（很乐意）</td><td rowspan="1">49</td><td rowspan="1">认同反馈的第四条；保持轻快；批量互动时轮换。</td></tr>
<tr><td rowspan="2">3｜悲伤</td><td rowspan="1">85%</td><td rowspan="1">2</td><td rowspan="1">轻抬慢回（温顺舒缓）</td><td rowspan="1">15</td><td rowspan="1">不安、紧绷时的短反馈；安全感下降。</td><td rowspan="2">0</td><td rowspan="2">关闭</td></tr>
<tr><td rowspan="1">15%</td><td rowspan="1">18</td><td rowspan="1">单次轻触缓慢抬头观察</td><td rowspan="1">31</td><td rowspan="1">惊吓或不安后的缓和；从紧张回到可互动；带一点不好意思的恢复声。</td></tr>
<tr><td rowspan="6">7</td><td rowspan="6">头右轻触</td><td rowspan="6">Beta Y</td><td rowspan="2">1｜开心</td><td rowspan="1">75%</td><td rowspan="1">33</td><td rowspan="1">点头同步左右小幅颤（极致开心）</td><td rowspan="1">24</td><td rowspan="1">情绪冲到很高的开心；雀跃、想撒娇蹦跳；社交或亲密高峰。</td><td rowspan="1">2</td><td rowspan="1">中</td></tr>
<tr><td rowspan="1">25%</td><td rowspan="1">13</td><td rowspan="1">抬头后快速点头（很乐意）</td><td rowspan="1">49</td><td rowspan="1">认同反馈的第四条；保持轻快；批量互动时轮换。</td><td rowspan="3">1</td><td rowspan="3">弱</td></tr>
<tr><td rowspan="2">2｜平静</td><td rowspan="1">65%</td><td rowspan="1">45</td><td rowspan="1">定点单侧观望（右）</td><td rowspan="1">45</td><td rowspan="1">同一侧再次被注意；熟悉后的警觉确认；轻回头式的注意。</td></tr>
<tr><td rowspan="1">35%</td><td rowspan="1">13</td><td rowspan="1">抬头后快速点头（很乐意）</td><td rowspan="1">49</td><td rowspan="1">认同反馈的第四条；保持轻快；批量互动时轮换。</td></tr>
<tr><td rowspan="2">3｜悲伤</td><td rowspan="1">85%</td><td rowspan="1">2</td><td rowspan="1">轻抬慢回（温顺舒缓）</td><td rowspan="1">15</td><td rowspan="1">不安、紧绷时的短反馈；安全感下降。</td><td rowspan="2">0</td><td rowspan="2">关闭</td></tr>
<tr><td rowspan="1">15%</td><td rowspan="1">18</td><td rowspan="1">单次轻触缓慢抬头观察</td><td rowspan="1">31</td><td rowspan="1">惊吓或不安后的缓和；从紧张回到可互动；带一点不好意思的恢复声。</td></tr>
<tr><td rowspan="6">8</td><td rowspan="6">头右短抚</td><td rowspan="12">预留 Beta N</td><td rowspan="2">1｜开心</td><td rowspan="1">75%</td><td rowspan="1">61</td><td rowspan="1">单侧快速偏头蹭手（摸头右快速撸）</td><td rowspan="1">35</td><td rowspan="1">依赖感最浓的一版；长时间贴近；柔和持续的撒娇。</td><td rowspan="2">2</td><td rowspan="2">中</td></tr>
<tr><td rowspan="1">25%</td><td rowspan="1">33</td><td rowspan="1">点头同步左右小幅颤（极致开心）</td><td rowspan="1">24</td><td rowspan="1">情绪冲到很高的开心；雀跃、想撒娇蹦跳；社交或亲密高峰。</td></tr>
<tr><td rowspan="2">2｜平静</td><td rowspan="1">65%</td><td rowspan="1">45</td><td rowspan="1">定点单侧观望（右）</td><td rowspan="1">45</td><td rowspan="1">同一侧再次被注意；熟悉后的警觉确认；轻回头式的注意。</td><td rowspan="2">1</td><td rowspan="2">弱</td></tr>
<tr><td rowspan="1">35%</td><td rowspan="1">13</td><td rowspan="1">抬头后快速点头（很乐意）</td><td rowspan="1">49</td><td rowspan="1">认同反馈的第四条；保持轻快；批量互动时轮换。</td></tr>
<tr><td rowspan="2">3｜悲伤</td><td rowspan="1">85%</td><td rowspan="1">2</td><td rowspan="1">轻抬慢回（温顺舒缓）</td><td rowspan="1">15</td><td rowspan="1">不安、紧绷时的短反馈；安全感下降。</td><td rowspan="2">0</td><td rowspan="2">关闭</td></tr>
<tr><td rowspan="1">15%</td><td rowspan="1">18</td><td rowspan="1">单次轻触缓慢抬头观察</td><td rowspan="1">31</td><td rowspan="1">惊吓或不安后的缓和；从紧张回到可互动；带一点不好意思的恢复声。</td></tr>
<tr><td rowspan="6">9</td><td rowspan="6">头右长抚</td><td rowspan="2">1｜开心</td><td rowspan="1">75%</td><td rowspan="1">33</td><td rowspan="1">点头同步左右小幅颤（极致开心）</td><td rowspan="1">24</td><td rowspan="1">情绪冲到很高的开心；雀跃、想撒娇蹦跳；社交或亲密高峰。</td><td rowspan="1">2</td><td rowspan="1">中</td></tr>
<tr><td rowspan="1">25%</td><td rowspan="1">13</td><td rowspan="1">抬头后快速点头（很乐意）</td><td rowspan="1">49</td><td rowspan="1">认同反馈的第四条；保持轻快；批量互动时轮换。</td><td rowspan="3">1</td><td rowspan="3">弱</td></tr>
<tr><td rowspan="2">2｜平静</td><td rowspan="1">65%</td><td rowspan="1">45</td><td rowspan="1">定点单侧观望（右）</td><td rowspan="1">45</td><td rowspan="1">同一侧再次被注意；熟悉后的警觉确认；轻回头式的注意。</td></tr>
<tr><td rowspan="1">35%</td><td rowspan="1">13</td><td rowspan="1">抬头后快速点头（很乐意）</td><td rowspan="1">49</td><td rowspan="1">认同反馈的第四条；保持轻快；批量互动时轮换。</td></tr>
<tr><td rowspan="2">3｜悲伤</td><td rowspan="1">85%</td><td rowspan="1">2</td><td rowspan="1">轻抬慢回（温顺舒缓）</td><td rowspan="1">15</td><td rowspan="1">不安、紧绷时的短反馈；安全感下降。</td><td rowspan="2">0</td><td rowspan="2">关闭</td></tr>
<tr><td rowspan="1">15%</td><td rowspan="1">18</td><td rowspan="1">单次轻触缓慢抬头观察</td><td rowspan="1">31</td><td rowspan="1">惊吓或不安后的缓和；从紧张回到可互动；带一点不好意思的恢复声。</td></tr>
<tr><td rowspan="6">10</td><td rowspan="6">腹部轻触</td><td rowspan="6">Beta Y</td><td rowspan="2">1｜开心</td><td rowspan="1">75%</td><td rowspan="1">33</td><td rowspan="1">点头同步左右小幅颤（极致开心）</td><td rowspan="1">24</td><td rowspan="1">情绪冲到很高的开心；雀跃、想撒娇蹦跳；社交或亲密高峰。</td><td rowspan="1">2</td><td rowspan="1">中</td></tr>
<tr><td rowspan="1">25%</td><td rowspan="1">13</td><td rowspan="1">抬头后快速点头（很乐意）</td><td rowspan="1">49</td><td rowspan="1">认同反馈的第四条；保持轻快；批量互动时轮换。</td><td rowspan="3">1</td><td rowspan="3">弱</td></tr>
<tr><td rowspan="2">2｜平静</td><td rowspan="1">65%</td><td rowspan="1">43</td><td rowspan="1">定点单侧观望（左）</td><td rowspan="1">45</td><td rowspan="1">同一侧再次被注意；熟悉后的警觉确认；轻回头式的注意。</td></tr>
<tr><td rowspan="1">35%</td><td rowspan="1">13</td><td rowspan="1">抬头后快速点头（很乐意）</td><td rowspan="1">49</td><td rowspan="1">认同反馈的第四条；保持轻快；批量互动时轮换。</td></tr>
<tr><td rowspan="2">3｜悲伤</td><td rowspan="1">85%</td><td rowspan="1">2</td><td rowspan="1">轻抬慢回（温顺舒缓）</td><td rowspan="1">15</td><td rowspan="1">不安、紧绷时的短反馈；安全感下降。</td><td rowspan="2">0</td><td rowspan="2">关闭</td></tr>
<tr><td rowspan="1">15%</td><td rowspan="1">18</td><td rowspan="1">单次轻触缓慢抬头观察</td><td rowspan="1">31</td><td rowspan="1">惊吓或不安后的缓和；从紧张回到可互动；带一点不好意思的恢复声。</td></tr>
<tr><td rowspan="6">11</td><td rowspan="6">腹部短抚</td><td rowspan="12">预留 Beta N</td><td rowspan="2">1｜开心</td><td rowspan="1">75%</td><td rowspan="1">27</td><td rowspan="1">肚皮触碰轻快垂点头（肚子快速撸）</td><td rowspan="2">24</td><td rowspan="2">情绪冲到很高的开心；雀跃、想撒娇蹦跳；社交或亲密高峰。</td><td rowspan="2">2</td><td rowspan="2">中</td></tr>
<tr><td rowspan="1">25%</td><td rowspan="1">33</td><td rowspan="1">点头同步左右小幅颤（极致开心）</td></tr>
<tr><td rowspan="2">2｜平静</td><td rowspan="1">65%</td><td rowspan="1">43</td><td rowspan="1">定点单侧观望（左）</td><td rowspan="1">45</td><td rowspan="1">同一侧再次被注意；熟悉后的警觉确认；轻回头式的注意。</td><td rowspan="2">1</td><td rowspan="2">弱</td></tr>
<tr><td rowspan="1">35%</td><td rowspan="1">13</td><td rowspan="1">抬头后快速点头（很乐意）</td><td rowspan="1">49</td><td rowspan="1">认同反馈的第四条；保持轻快；批量互动时轮换。</td></tr>
<tr><td rowspan="2">3｜悲伤</td><td rowspan="1">85%</td><td rowspan="1">2</td><td rowspan="1">轻抬慢回（温顺舒缓）</td><td rowspan="1">15</td><td rowspan="1">不安、紧绷时的短反馈；安全感下降。</td><td rowspan="2">0</td><td rowspan="2">关闭</td></tr>
<tr><td rowspan="1">15%</td><td rowspan="1">18</td><td rowspan="1">单次轻触缓慢抬头观察</td><td rowspan="1">31</td><td rowspan="1">惊吓或不安后的缓和；从紧张回到可互动；带一点不好意思的恢复声。</td></tr>
<tr><td rowspan="6">12</td><td rowspan="6">腹部长抚</td><td rowspan="2">1｜开心</td><td rowspan="1">75%</td><td rowspan="1">33</td><td rowspan="1">点头同步左右小幅颤（极致开心）</td><td rowspan="1">24</td><td rowspan="1">情绪冲到很高的开心；雀跃、想撒娇蹦跳；社交或亲密高峰。</td><td rowspan="1">2</td><td rowspan="1">中</td></tr>
<tr><td rowspan="1">25%</td><td rowspan="1">13</td><td rowspan="1">抬头后快速点头（很乐意）</td><td rowspan="1">49</td><td rowspan="1">认同反馈的第四条；保持轻快；批量互动时轮换。</td><td rowspan="3">1</td><td rowspan="3">弱</td></tr>
<tr><td rowspan="2">2｜平静</td><td rowspan="1">65%</td><td rowspan="1">43</td><td rowspan="1">定点单侧观望（左）</td><td rowspan="1">45</td><td rowspan="1">同一侧再次被注意；熟悉后的警觉确认；轻回头式的注意。</td></tr>
<tr><td rowspan="1">35%</td><td rowspan="1">13</td><td rowspan="1">抬头后快速点头（很乐意）</td><td rowspan="1">49</td><td rowspan="1">认同反馈的第四条；保持轻快；批量互动时轮换。</td></tr>
<tr><td rowspan="2">3｜悲伤</td><td rowspan="1">85%</td><td rowspan="1">2</td><td rowspan="1">轻抬慢回（温顺舒缓）</td><td rowspan="1">15</td><td rowspan="1">不安、紧绷时的短反馈；安全感下降。</td><td rowspan="2">0</td><td rowspan="2">关闭</td></tr>
<tr><td rowspan="1">15%</td><td rowspan="1">18</td><td rowspan="1">单次轻触缓慢抬头观察</td><td rowspan="1">31</td><td rowspan="1">惊吓或不安后的缓和；从紧张回到可互动；带一点不好意思的恢复声。</td></tr>
<tr><td rowspan="6">13</td><td rowspan="6">左侧轻触</td><td rowspan="6">Beta Y</td><td rowspan="2">1｜开心</td><td rowspan="1">75%</td><td rowspan="1">33</td><td rowspan="1">点头同步左右小幅颤（极致开心）</td><td rowspan="1">24</td><td rowspan="1">情绪冲到很高的开心；雀跃、想撒娇蹦跳；社交或亲密高峰。</td><td rowspan="1">2</td><td rowspan="1">中</td></tr>
<tr><td rowspan="1">25%</td><td rowspan="1">13</td><td rowspan="1">抬头后快速点头（很乐意）</td><td rowspan="1">49</td><td rowspan="1">认同反馈的第四条；保持轻快；批量互动时轮换。</td><td rowspan="3">1</td><td rowspan="3">弱</td></tr>
<tr><td rowspan="2">2｜平静</td><td rowspan="1">65%</td><td rowspan="1">43</td><td rowspan="1">定点单侧观望（左）</td><td rowspan="1">57</td><td rowspan="1">侧面重复互动后的更友好回应；轻贴近；二级确认。</td></tr>
<tr><td rowspan="1">35%</td><td rowspan="1">13</td><td rowspan="1">抬头后快速点头（很乐意）</td><td rowspan="1">49</td><td rowspan="1">认同反馈的第四条；保持轻快；批量互动时轮换。</td></tr>
<tr><td rowspan="2">3｜悲伤</td><td rowspan="1">85%</td><td rowspan="1">2</td><td rowspan="1">轻抬慢回（温顺舒缓）</td><td rowspan="1">15</td><td rowspan="1">不安、紧绷时的短反馈；安全感下降。</td><td rowspan="2">0</td><td rowspan="2">关闭</td></tr>
<tr><td rowspan="1">15%</td><td rowspan="1">18</td><td rowspan="1">单次轻触缓慢抬头观察</td><td rowspan="1">31</td><td rowspan="1">惊吓或不安后的缓和；从紧张回到可互动；带一点不好意思的恢复声。</td></tr>
<tr><td rowspan="6">14</td><td rowspan="6">左侧短抚</td><td rowspan="12">预留 Beta N</td><td rowspan="2">1｜开心</td><td rowspan="1">75%</td><td rowspan="1">11</td><td rowspan="1">快速上下点头（快速撸通用开心）</td><td rowspan="1">10</td><td rowspan="1">节奏偏快的愉快互动；兴奋且享受；需要明亮的开心短声。</td><td rowspan="2">2</td><td rowspan="2">中</td></tr>
<tr><td rowspan="1">25%</td><td rowspan="1">33</td><td rowspan="1">点头同步左右小幅颤（极致开心）</td><td rowspan="1">24</td><td rowspan="1">情绪冲到很高的开心；雀跃、想撒娇蹦跳；社交或亲密高峰。</td></tr>
<tr><td rowspan="2">2｜平静</td><td rowspan="1">65%</td><td rowspan="1">43</td><td rowspan="1">定点单侧观望（左）</td><td rowspan="1">57</td><td rowspan="1">侧面重复互动后的更友好回应；轻贴近；二级确认。</td><td rowspan="2">1</td><td rowspan="2">弱</td></tr>
<tr><td rowspan="1">35%</td><td rowspan="1">13</td><td rowspan="1">抬头后快速点头（很乐意）</td><td rowspan="1">49</td><td rowspan="1">认同反馈的第四条；保持轻快；批量互动时轮换。</td></tr>
<tr><td rowspan="2">3｜悲伤</td><td rowspan="1">85%</td><td rowspan="1">2</td><td rowspan="1">轻抬慢回（温顺舒缓）</td><td rowspan="1">15</td><td rowspan="1">不安、紧绷时的短反馈；安全感下降。</td><td rowspan="2">0</td><td rowspan="2">关闭</td></tr>
<tr><td rowspan="1">15%</td><td rowspan="1">18</td><td rowspan="1">单次轻触缓慢抬头观察</td><td rowspan="1">31</td><td rowspan="1">惊吓或不安后的缓和；从紧张回到可互动；带一点不好意思的恢复声。</td></tr>
<tr><td rowspan="6">15</td><td rowspan="6">左侧长抚</td><td rowspan="2">1｜开心</td><td rowspan="1">75%</td><td rowspan="1">33</td><td rowspan="1">点头同步左右小幅颤（极致开心）</td><td rowspan="1">24</td><td rowspan="1">情绪冲到很高的开心；雀跃、想撒娇蹦跳；社交或亲密高峰。</td><td rowspan="1">2</td><td rowspan="1">中</td></tr>
<tr><td rowspan="1">25%</td><td rowspan="1">13</td><td rowspan="1">抬头后快速点头（很乐意）</td><td rowspan="1">49</td><td rowspan="1">认同反馈的第四条；保持轻快；批量互动时轮换。</td><td rowspan="3">1</td><td rowspan="3">弱</td></tr>
<tr><td rowspan="2">2｜平静</td><td rowspan="1">65%</td><td rowspan="1">43</td><td rowspan="1">定点单侧观望（左）</td><td rowspan="1">57</td><td rowspan="1">侧面重复互动后的更友好回应；轻贴近；二级确认。</td></tr>
<tr><td rowspan="1">35%</td><td rowspan="1">13</td><td rowspan="1">抬头后快速点头（很乐意）</td><td rowspan="1">49</td><td rowspan="1">认同反馈的第四条；保持轻快；批量互动时轮换。</td></tr>
<tr><td rowspan="2">3｜悲伤</td><td rowspan="1">85%</td><td rowspan="1">2</td><td rowspan="1">轻抬慢回（温顺舒缓）</td><td rowspan="1">15</td><td rowspan="1">不安、紧绷时的短反馈；安全感下降。</td><td rowspan="2">0</td><td rowspan="2">关闭</td></tr>
<tr><td rowspan="1">15%</td><td rowspan="1">18</td><td rowspan="1">单次轻触缓慢抬头观察</td><td rowspan="1">31</td><td rowspan="1">惊吓或不安后的缓和；从紧张回到可互动；带一点不好意思的恢复声。</td></tr>
<tr><td rowspan="6">16</td><td rowspan="6">右侧轻触</td><td rowspan="6">Beta Y</td><td rowspan="2">1｜开心</td><td rowspan="1">75%</td><td rowspan="1">33</td><td rowspan="1">点头同步左右小幅颤（极致开心）</td><td rowspan="1">24</td><td rowspan="1">情绪冲到很高的开心；雀跃、想撒娇蹦跳；社交或亲密高峰。</td><td rowspan="1">2</td><td rowspan="1">中</td></tr>
<tr><td rowspan="1">25%</td><td rowspan="1">13</td><td rowspan="1">抬头后快速点头（很乐意）</td><td rowspan="1">49</td><td rowspan="1">认同反馈的第四条；保持轻快；批量互动时轮换。</td><td rowspan="3">1</td><td rowspan="3">弱</td></tr>
<tr><td rowspan="2">2｜平静</td><td rowspan="1">65%</td><td rowspan="1">45</td><td rowspan="1">定点单侧观望（右）</td><td rowspan="1">41</td><td rowspan="1">熟悉后的侧面短回声；亲昵互动中的二次确认；更松弛一点。</td></tr>
<tr><td rowspan="1">35%</td><td rowspan="1">13</td><td rowspan="1">抬头后快速点头（很乐意）</td><td rowspan="1">49</td><td rowspan="1">认同反馈的第四条；保持轻快；批量互动时轮换。</td></tr>
<tr><td rowspan="2">3｜悲伤</td><td rowspan="1">85%</td><td rowspan="1">2</td><td rowspan="1">轻抬慢回（温顺舒缓）</td><td rowspan="1">15</td><td rowspan="1">不安、紧绷时的短反馈；安全感下降。</td><td rowspan="2">0</td><td rowspan="2">关闭</td></tr>
<tr><td rowspan="1">15%</td><td rowspan="1">18</td><td rowspan="1">单次轻触缓慢抬头观察</td><td rowspan="1">31</td><td rowspan="1">惊吓或不安后的缓和；从紧张回到可互动；带一点不好意思的恢复声。</td></tr>
<tr><td rowspan="6">17</td><td rowspan="6">右侧短抚</td><td rowspan="12">预留 Beta N</td><td rowspan="2">1｜开心</td><td rowspan="1">75%</td><td rowspan="1">11</td><td rowspan="1">快速上下点头（快速撸通用开心）</td><td rowspan="1">10</td><td rowspan="1">节奏偏快的愉快互动；兴奋且享受；需要明亮的开心短声。</td><td rowspan="2">2</td><td rowspan="2">中</td></tr>
<tr><td rowspan="1">25%</td><td rowspan="1">33</td><td rowspan="1">点头同步左右小幅颤（极致开心）</td><td rowspan="1">24</td><td rowspan="1">情绪冲到很高的开心；雀跃、想撒娇蹦跳；社交或亲密高峰。</td></tr>
<tr><td rowspan="2">2｜平静</td><td rowspan="1">65%</td><td rowspan="1">45</td><td rowspan="1">定点单侧观望（右）</td><td rowspan="1">41</td><td rowspan="1">熟悉后的侧面短回声；亲昵互动中的二次确认；更松弛一点。</td><td rowspan="2">1</td><td rowspan="2">弱</td></tr>
<tr><td rowspan="1">35%</td><td rowspan="1">13</td><td rowspan="1">抬头后快速点头（很乐意）</td><td rowspan="1">49</td><td rowspan="1">认同反馈的第四条；保持轻快；批量互动时轮换。</td></tr>
<tr><td rowspan="2">3｜悲伤</td><td rowspan="1">85%</td><td rowspan="1">2</td><td rowspan="1">轻抬慢回（温顺舒缓）</td><td rowspan="1">15</td><td rowspan="1">不安、紧绷时的短反馈；安全感下降。</td><td rowspan="2">0</td><td rowspan="2">关闭</td></tr>
<tr><td rowspan="1">15%</td><td rowspan="1">18</td><td rowspan="1">单次轻触缓慢抬头观察</td><td rowspan="1">31</td><td rowspan="1">惊吓或不安后的缓和；从紧张回到可互动；带一点不好意思的恢复声。</td></tr>
<tr><td rowspan="6">18</td><td rowspan="6">右侧长抚</td><td rowspan="2">1｜开心</td><td rowspan="1">75%</td><td rowspan="1">33</td><td rowspan="1">点头同步左右小幅颤（极致开心）</td><td rowspan="1">24</td><td rowspan="1">情绪冲到很高的开心；雀跃、想撒娇蹦跳；社交或亲密高峰。</td><td rowspan="1">2</td><td rowspan="1">中</td></tr>
<tr><td rowspan="1">25%</td><td rowspan="1">13</td><td rowspan="1">抬头后快速点头（很乐意）</td><td rowspan="1">49</td><td rowspan="1">认同反馈的第四条；保持轻快；批量互动时轮换。</td><td rowspan="3">1</td><td rowspan="3">弱</td></tr>
<tr><td rowspan="2">2｜平静</td><td rowspan="1">65%</td><td rowspan="1">45</td><td rowspan="1">定点单侧观望（右）</td><td rowspan="1">41</td><td rowspan="1">熟悉后的侧面短回声；亲昵互动中的二次确认；更松弛一点。</td></tr>
<tr><td rowspan="1">35%</td><td rowspan="1">13</td><td rowspan="1">抬头后快速点头（很乐意）</td><td rowspan="1">49</td><td rowspan="1">认同反馈的第四条；保持轻快；批量互动时轮换。</td></tr>
<tr><td rowspan="2">3｜悲伤</td><td rowspan="1">85%</td><td rowspan="1">2</td><td rowspan="1">轻抬慢回（温顺舒缓）</td><td rowspan="1">15</td><td rowspan="1">不安、紧绷时的短反馈；安全感下降。</td><td rowspan="2">0</td><td rowspan="2">关闭</td></tr>
<tr><td rowspan="1">15%</td><td rowspan="1">18</td><td rowspan="1">单次轻触缓慢抬头观察</td><td rowspan="1">31</td><td rowspan="1">惊吓或不安后的缓和；从紧张回到可互动；带一点不好意思的恢复声。</td></tr>
<tr><td rowspan="6">19</td><td rowspan="6">后背轻触</td><td rowspan="6">Beta Y</td><td rowspan="2">1｜开心</td><td rowspan="1">75%</td><td rowspan="1">33</td><td rowspan="1">点头同步左右小幅颤（极致开心）</td><td rowspan="1">24</td><td rowspan="1">情绪冲到很高的开心；雀跃、想撒娇蹦跳；社交或亲密高峰。</td><td rowspan="1">2</td><td rowspan="1">中</td></tr>
<tr><td rowspan="1">25%</td><td rowspan="1">13</td><td rowspan="1">抬头后快速点头（很乐意）</td><td rowspan="1">49</td><td rowspan="1">认同反馈的第四条；保持轻快；批量互动时轮换。</td><td rowspan="3">1</td><td rowspan="3">弱</td></tr>
<tr><td rowspan="2">2｜平静</td><td rowspan="1">65%</td><td rowspan="1">45</td><td rowspan="1">定点单侧观望（右）</td><td rowspan="1">45</td><td rowspan="1">同一侧再次被注意；熟悉后的警觉确认；轻回头式的注意。</td></tr>
<tr><td rowspan="1">35%</td><td rowspan="1">13</td><td rowspan="1">抬头后快速点头（很乐意）</td><td rowspan="1">49</td><td rowspan="1">认同反馈的第四条；保持轻快；批量互动时轮换。</td></tr>
<tr><td rowspan="2">3｜悲伤</td><td rowspan="1">85%</td><td rowspan="1">2</td><td rowspan="1">轻抬慢回（温顺舒缓）</td><td rowspan="1">15</td><td rowspan="1">不安、紧绷时的短反馈；安全感下降。</td><td rowspan="2">0</td><td rowspan="2">关闭</td></tr>
<tr><td rowspan="1">15%</td><td rowspan="1">18</td><td rowspan="1">单次轻触缓慢抬头观察</td><td rowspan="1">31</td><td rowspan="1">惊吓或不安后的缓和；从紧张回到可互动；带一点不好意思的恢复声。</td></tr>
<tr><td rowspan="6">20</td><td rowspan="6">后背短抚</td><td rowspan="32">预留 Beta N</td><td rowspan="2">1｜开心</td><td rowspan="1">75%</td><td rowspan="1">11</td><td rowspan="1">快速上下点头（快速撸通用开心）</td><td rowspan="1">10</td><td rowspan="1">节奏偏快的愉快互动；兴奋且享受；需要明亮的开心短声。</td><td rowspan="2">2</td><td rowspan="2">中</td></tr>
<tr><td rowspan="1">25%</td><td rowspan="1">33</td><td rowspan="1">点头同步左右小幅颤（极致开心）</td><td rowspan="1">24</td><td rowspan="1">情绪冲到很高的开心；雀跃、想撒娇蹦跳；社交或亲密高峰。</td></tr>
<tr><td rowspan="2">2｜平静</td><td rowspan="1">65%</td><td rowspan="1">45</td><td rowspan="1">定点单侧观望（右）</td><td rowspan="1">45</td><td rowspan="1">同一侧再次被注意；熟悉后的警觉确认；轻回头式的注意。</td><td rowspan="2">1</td><td rowspan="2">弱</td></tr>
<tr><td rowspan="1">35%</td><td rowspan="1">13</td><td rowspan="1">抬头后快速点头（很乐意）</td><td rowspan="1">49</td><td rowspan="1">认同反馈的第四条；保持轻快；批量互动时轮换。</td></tr>
<tr><td rowspan="2">3｜悲伤</td><td rowspan="1">85%</td><td rowspan="1">2</td><td rowspan="1">轻抬慢回（温顺舒缓）</td><td rowspan="1">15</td><td rowspan="1">不安、紧绷时的短反馈；安全感下降。</td><td rowspan="2">0</td><td rowspan="2">关闭</td></tr>
<tr><td rowspan="1">15%</td><td rowspan="1">18</td><td rowspan="1">单次轻触缓慢抬头观察</td><td rowspan="1">31</td><td rowspan="1">惊吓或不安后的缓和；从紧张回到可互动；带一点不好意思的恢复声。</td></tr>
<tr><td rowspan="6">21</td><td rowspan="6">后背长抚</td><td rowspan="2">1｜开心</td><td rowspan="1">75%</td><td rowspan="1">33</td><td rowspan="1">点头同步左右小幅颤（极致开心）</td><td rowspan="1">24</td><td rowspan="1">情绪冲到很高的开心；雀跃、想撒娇蹦跳；社交或亲密高峰。</td><td rowspan="1">2</td><td rowspan="1">中</td></tr>
<tr><td rowspan="1">25%</td><td rowspan="1">13</td><td rowspan="1">抬头后快速点头（很乐意）</td><td rowspan="1">49</td><td rowspan="1">认同反馈的第四条；保持轻快；批量互动时轮换。</td><td rowspan="3">1</td><td rowspan="3">弱</td></tr>
<tr><td rowspan="2">2｜平静</td><td rowspan="1">65%</td><td rowspan="1">45</td><td rowspan="1">定点单侧观望（右）</td><td rowspan="1">45</td><td rowspan="1">同一侧再次被注意；熟悉后的警觉确认；轻回头式的注意。</td></tr>
<tr><td rowspan="1">35%</td><td rowspan="1">13</td><td rowspan="1">抬头后快速点头（很乐意）</td><td rowspan="1">49</td><td rowspan="1">认同反馈的第四条；保持轻快；批量互动时轮换。</td></tr>
<tr><td rowspan="2">3｜悲伤</td><td rowspan="1">85%</td><td rowspan="1">2</td><td rowspan="1">轻抬慢回（温顺舒缓）</td><td rowspan="1">15</td><td rowspan="1">不安、紧绷时的短反馈；安全感下降。</td><td rowspan="2">0</td><td rowspan="2">关闭</td></tr>
<tr><td rowspan="1">15%</td><td rowspan="1">18</td><td rowspan="1">单次轻触缓慢抬头观察</td><td rowspan="1">31</td><td rowspan="1">惊吓或不安后的缓和；从紧张回到可互动；带一点不好意思的恢复声。</td></tr>
<tr><td rowspan="6">22</td><td rowspan="6">长时间握持</td><td rowspan="2">1｜开心</td><td rowspan="1">75%</td><td rowspan="1">52</td><td rowspan="1">长时间握持静靠（Sustainedhold）</td><td rowspan="1">35</td><td rowspan="1">依赖感最浓的一版；长时间贴近；柔和持续的撒娇。</td><td rowspan="1">2</td><td rowspan="1">中</td></tr>
<tr><td rowspan="1">25%</td><td rowspan="2">46</td><td rowspan="2">短时握持间断晃头（Sustainedhold）</td><td rowspan="1">34</td><td rowspan="1">黏人升级；主动蹭近；开心又舍不得被放下。</td><td rowspan="2">1</td><td rowspan="2">弱</td></tr>
<tr><td rowspan="2">2｜平静</td><td rowspan="1">65%</td><td rowspan="1">35</td><td rowspan="1">依赖感最浓的一版；长时间贴近；柔和持续的撒娇。</td></tr>
<tr><td rowspan="1">35%</td><td rowspan="1">54</td><td rowspan="1">长时间握持间断打量</td><td rowspan="1">57</td><td rowspan="1">侧面重复互动后的更友好回应；轻贴近；二级确认。</td><td rowspan="3">0</td><td rowspan="3">关闭</td></tr>
<tr><td rowspan="2">3｜悲伤</td><td rowspan="1">85%</td><td rowspan="1">52</td><td rowspan="1">长时间握持静靠（Sustainedhold）</td><td rowspan="1">35</td><td rowspan="1">依赖感最浓的一版；长时间贴近；柔和持续的撒娇。</td></tr>
<tr><td rowspan="1">15%</td><td rowspan="1">54</td><td rowspan="1">长时间握持间断打量</td><td rowspan="1">41</td><td rowspan="1">熟悉后的侧面短回声；亲昵互动中的二次确认；更松弛一点。</td></tr>
<tr><td rowspan="6">23</td><td rowspan="6">轻摇</td><td rowspan="2">1｜开心</td><td rowspan="1">75%</td><td rowspan="1">28</td><td rowspan="1">轻摇小幅快点头（Gentleshake）</td><td rowspan="1">47</td><td rowspan="1">愉快互动的第二条；同样偏快、偏亮；轮换用的开心反馈。</td><td rowspan="1">2</td><td rowspan="1">中</td></tr>
<tr><td rowspan="1">25%</td><td rowspan="1">13</td><td rowspan="1">抬头后快速点头（很乐意）</td><td rowspan="1">49</td><td rowspan="1">认同反馈的第四条；保持轻快；批量互动时轮换。</td><td rowspan="3">1</td><td rowspan="3">弱</td></tr>
<tr><td rowspan="2">2｜平静</td><td rowspan="1">65%</td><td rowspan="1">49</td><td rowspan="1">轻摇缓慢环视</td><td rowspan="1">25</td><td rowspan="1">温暖友好、被好好对待后的软回应；社交开场或亲密回馈。</td></tr>
<tr><td rowspan="1">35%</td><td rowspan="1">28</td><td rowspan="1">轻摇小幅快点头（Gentleshake）</td><td rowspan="1">47</td><td rowspan="1">愉快互动的第二条；同样偏快、偏亮；轮换用的开心反馈。</td></tr>
<tr><td rowspan="2">3｜悲伤</td><td rowspan="1">85%</td><td rowspan="1">49</td><td rowspan="1">轻摇缓慢环视</td><td rowspan="1">15</td><td rowspan="1">不安、紧绷时的短反馈；安全感下降。</td><td rowspan="2">0</td><td rowspan="2">关闭</td></tr>
<tr><td rowspan="1">15%</td><td rowspan="1">2</td><td rowspan="1">轻抬慢回（温顺舒缓）</td><td rowspan="1">53</td><td rowspan="1">满足后的轻叹；放松惬意；亲密安抚后的绵长收束。</td></tr>
<tr><td rowspan="2">24</td><td rowspan="2">猛摇</td><td rowspan="2">0｜ANY</td><td rowspan="1">70%</td><td rowspan="1">31</td><td rowspan="1">粗暴握持高频躲闪颤</td><td rowspan="1">22</td><td rowspan="1">被拘束、不舒服；害怕但克制；需要不安的弱抗议。</td><td rowspan="2">1</td><td rowspan="2">弱</td></tr>
<tr><td rowspan="1">30%</td><td rowspan="1">25</td><td rowspan="1">快速撸过度刺激躲闪</td><td rowspan="1">15</td><td rowspan="1">不安、紧绷时的短反馈；安全感下降。</td></tr>
<tr><td rowspan="6">25</td><td rowspan="6">翻转</td><td rowspan="2">1｜开心</td><td rowspan="1">75%</td><td rowspan="1">47</td><td rowspan="1">翻转肚皮上扬晃头（Flipbelly-up）</td><td rowspan="1">55</td><td rowspan="1">满足信任的第二条；放松开心；短时亲密反馈的轮换。</td><td rowspan="1">2</td><td rowspan="1">中</td></tr>
<tr><td rowspan="1">25%</td><td rowspan="1">22</td><td rowspan="1">翻转肚皮静态垂头</td><td rowspan="1">53</td><td rowspan="1">满足后的轻叹；放松惬意；亲密安抚后的绵长收束。</td><td rowspan="1">1</td><td rowspan="1">弱</td></tr>
<tr><td rowspan="2">2｜平静</td><td rowspan="1">65%</td><td rowspan="1">47</td><td rowspan="1">翻转肚皮上扬晃头（Flipbelly-up）</td><td rowspan="1">55</td><td rowspan="1">满足信任的第二条；放松开心；短时亲密反馈的轮换。</td><td rowspan="1">2</td><td rowspan="1">中</td></tr>
<tr><td rowspan="1">35%</td><td rowspan="2">22</td><td rowspan="2">翻转肚皮静态垂头</td><td rowspan="2">53</td><td rowspan="2">满足后的轻叹；放松惬意；亲密安抚后的绵长收束。</td><td rowspan="1">1</td><td rowspan="1">弱</td></tr>
<tr><td rowspan="2">3｜悲伤</td><td rowspan="1">85%</td><td rowspan="1">0</td><td rowspan="1">关闭</td></tr>
<tr><td rowspan="1">15%</td><td rowspan="1">5</td><td rowspan="1">强行翻肚皮垂头</td><td rowspan="1">50</td><td rowspan="1">抗议的第三条；仍委屈但不攻击；高强度不适时的备用。</td><td rowspan="1">1</td><td rowspan="1">弱</td></tr>
<tr><td rowspan="6">26</td><td rowspan="6">被拿起</td><td rowspan="12">原表划除</td><td rowspan="2">1｜开心</td><td rowspan="1">75%</td><td rowspan="1">46</td><td rowspan="1">短时握持间断晃头（Sustainedhold）</td><td rowspan="1">35</td><td rowspan="1">依赖感最浓的一版；长时间贴近；柔和持续的撒娇。</td><td rowspan="1">2</td><td rowspan="1">中</td></tr>
<tr><td rowspan="1">25%</td><td rowspan="1">60</td><td rowspan="1">被拿起上扬连续点头（Pickedup）</td><td rowspan="1">33</td><td rowspan="1">黏人、舍不得分开；被抱持时的依赖；温暖的撒娇贴近。</td><td rowspan="1">1</td><td rowspan="1">弱</td></tr>
<tr><td rowspan="2">2｜平静</td><td rowspan="1">65%</td><td rowspan="1">46</td><td rowspan="1">短时握持间断晃头（Sustainedhold）</td><td rowspan="1">35</td><td rowspan="1">依赖感最浓的一版；长时间贴近；柔和持续的撒娇。</td><td rowspan="1">2</td><td rowspan="1">中</td></tr>
<tr><td rowspan="1">35%</td><td rowspan="1">60</td><td rowspan="1">被拿起上扬连续点头（Pickedup）</td><td rowspan="1">33</td><td rowspan="1">黏人、舍不得分开；被抱持时的依赖；温暖的撒娇贴近。</td><td rowspan="2">1</td><td rowspan="2">弱</td></tr>
<tr><td rowspan="2">3｜悲伤</td><td rowspan="1">85%</td><td rowspan="1">52</td><td rowspan="1">长时间握持静靠（Sustainedhold）</td><td rowspan="1">35</td><td rowspan="1">依赖感最浓的一版；长时间贴近；柔和持续的撒娇。</td></tr>
<tr><td rowspan="1">15%</td><td rowspan="1">54</td><td rowspan="1">长时间握持间断打量</td><td rowspan="1">41</td><td rowspan="1">熟悉后的侧面短回声；亲昵互动中的二次确认；更松弛一点。</td><td rowspan="1">0</td><td rowspan="1">关闭</td></tr>
<tr><td rowspan="6">27</td><td rowspan="6">被放下</td><td rowspan="2">1｜开心</td><td rowspan="1">75%</td><td rowspan="1">43</td><td rowspan="1">定点单侧观望（左）</td><td rowspan="1">45</td><td rowspan="1">同一侧再次被注意；熟悉后的警觉确认；轻回头式的注意。</td><td rowspan="1">1</td><td rowspan="1">弱</td></tr>
<tr><td rowspan="1">25%</td><td rowspan="1">9</td><td rowspan="1">上下缓慢抬升打量</td><td rowspan="1">25</td><td rowspan="1">温暖友好、被好好对待后的软回应；社交开场或亲密回馈。</td><td rowspan="1">0</td><td rowspan="1">关闭</td></tr>
<tr><td rowspan="2">2｜平静</td><td rowspan="1">65%</td><td rowspan="1">43</td><td rowspan="1">定点单侧观望（左）</td><td rowspan="1">45</td><td rowspan="1">同一侧再次被注意；熟悉后的警觉确认；轻回头式的注意。</td><td rowspan="1">1</td><td rowspan="1">弱</td></tr>
<tr><td rowspan="1">35%</td><td rowspan="1">9</td><td rowspan="1">上下缓慢抬升打量</td><td rowspan="1">25</td><td rowspan="1">温暖友好、被好好对待后的软回应；社交开场或亲密回馈。</td><td rowspan="3">0</td><td rowspan="3">关闭</td></tr>
<tr><td rowspan="2">3｜悲伤</td><td rowspan="1">85%</td><td rowspan="1">3</td><td rowspan="1">放下后长期垂头</td><td rowspan="1">3</td><td rowspan="1">独处过久；被放下后的空落；需要稀疏、带着一点想念的低声。</td></tr>
<tr><td rowspan="1">15%</td><td rowspan="1">43</td><td rowspan="1">定点单侧观望（左）</td><td rowspan="1">45</td><td rowspan="1">同一侧再次被注意；熟悉后的警觉确认；轻回头式的注意。</td></tr>
<tr><td rowspan="6">28</td><td rowspan="6">唤醒提示词</td><td rowspan="14">Beta Y</td><td rowspan="2">1｜开心</td><td rowspan="1">75%</td><td rowspan="1">59</td><td rowspan="1">左右快速摆头好奇（强光/唤醒）</td><td rowspan="1">44</td><td rowspan="1">唤醒/互动起始的第三条；轻快期待；用于轮换避免重复。</td><td rowspan="1">2</td><td rowspan="1">中</td></tr>
<tr><td rowspan="1">25%</td><td rowspan="1">57</td><td rowspan="1">左右循环环视</td><td rowspan="1">18</td><td rowspan="1">熟悉的人唤醒；日常互动开始；比正式开机更轻快的起始。</td><td rowspan="1">1</td><td rowspan="1">弱</td></tr>
<tr><td rowspan="2">2｜平静</td><td rowspan="1">65%</td><td rowspan="1">59</td><td rowspan="1">左右快速摆头好奇（强光/唤醒）</td><td rowspan="1">44</td><td rowspan="1">唤醒/互动起始的第三条；轻快期待；用于轮换避免重复。</td><td rowspan="1">2</td><td rowspan="1">中</td></tr>
<tr><td rowspan="1">35%</td><td rowspan="2">57</td><td rowspan="2">左右循环环视</td><td rowspan="1">18</td><td rowspan="1">熟悉的人唤醒；日常互动开始；比正式开机更轻快的起始。</td><td rowspan="2">1</td><td rowspan="2">弱</td></tr>
<tr><td rowspan="2">3｜悲伤</td><td rowspan="1">85%</td><td rowspan="1">41</td><td rowspan="1">熟悉后的侧面短回声；亲昵互动中的二次确认；更松弛一点。</td></tr>
<tr><td rowspan="1">15%</td><td rowspan="1">13</td><td rowspan="1">抬头后快速点头（很乐意）</td><td rowspan="1">49</td><td rowspan="1">认同反馈的第四条；保持轻快；批量互动时轮换。</td><td rowspan="3">0</td><td rowspan="3">关闭</td></tr>
<tr><td rowspan="2">29</td><td rowspan="2">光线变暗</td><td rowspan="2">0｜ANY</td><td rowspan="2">50%</td><td rowspan="1">23</td><td rowspan="1">暗光低头慢挪</td><td rowspan="1">21</td><td rowspan="1">夜间进一步安静；准备休息；需要更柔、更长的过渡。</td></tr>
<tr><td rowspan="1">55</td><td rowspan="1">暗光慵懒垂头（Darkness）</td><td rowspan="1">42</td><td rowspan="1">环境变暗；从活跃转入安静；准备进入低刺激状态。</td></tr>
<tr><td rowspan="6">30</td><td rowspan="6">光线变亮</td><td rowspan="2">1｜开心</td><td rowspan="1">75%</td><td rowspan="1">57</td><td rowspan="1">左右循环环视</td><td rowspan="1">18</td><td rowspan="1">熟悉的人唤醒；日常互动开始；比正式开机更轻快的起始。</td><td rowspan="1">1</td><td rowspan="1">弱</td></tr>
<tr><td rowspan="1">25%</td><td rowspan="1">59</td><td rowspan="1">左右快速摆头好奇（强光/唤醒）</td><td rowspan="1">44</td><td rowspan="1">唤醒/互动起始的第三条；轻快期待；用于轮换避免重复。</td><td rowspan="1">2</td><td rowspan="1">中</td></tr>
<tr><td rowspan="2">2｜平静</td><td rowspan="1">65%</td><td rowspan="1">57</td><td rowspan="1">左右循环环视</td><td rowspan="1">18</td><td rowspan="1">熟悉的人唤醒；日常互动开始；比正式开机更轻快的起始。</td><td rowspan="1">1</td><td rowspan="1">弱</td></tr>
<tr><td rowspan="1">35%</td><td rowspan="1">59</td><td rowspan="1">左右快速摆头好奇（强光/唤醒）</td><td rowspan="1">44</td><td rowspan="1">唤醒/互动起始的第三条；轻快期待；用于轮换避免重复。</td><td rowspan="1">2</td><td rowspan="1">中</td></tr>
<tr><td rowspan="2">3｜悲伤</td><td rowspan="1">85%</td><td rowspan="1">9</td><td rowspan="1">上下缓慢抬升打量</td><td rowspan="1">45</td><td rowspan="1">同一侧再次被注意；熟悉后的警觉确认；轻回头式的注意。</td><td rowspan="6">0</td><td rowspan="6">关闭</td></tr>
<tr><td rowspan="1">15%</td><td rowspan="1">50</td><td rowspan="1">间断定点侧头试探</td><td rowspan="1">23</td><td rowspan="1">轻柔问候；关系刚开始或再次见面；低刺激的友好开场。</td></tr>
<tr><td rowspan="2">31</td><td rowspan="2">2小时无互动</td><td rowspan="4">预留 Beta N</td><td rowspan="4">0｜ANY</td><td rowspan="1">70%</td><td rowspan="1">6</td><td rowspan="1">瞌睡</td><td rowspan="1">1</td><td rowspan="1">安静休息、低刺激存在感；长时间无互动或待机时的 resting 陪伴底。不用于充电提示。</td></tr>
<tr><td rowspan="1">30%</td><td rowspan="2">3</td><td rowspan="2">放下后长期垂头</td><td rowspan="2">3</td><td rowspan="2">独处过久；被放下后的空落；需要稀疏、带着一点想念的低声。</td></tr>
<tr><td rowspan="2">32</td><td rowspan="2">48小时无互动</td><td rowspan="1">60%</td></tr>
<tr><td rowspan="1">40%</td><td rowspan="1">6</td><td rowspan="1">瞌睡</td><td rowspan="1">1</td><td rowspan="1">安静休息、低刺激存在感；长时间无互动或待机时的 resting 陪伴底。不用于充电提示。</td></tr>
<tr><td rowspan="6">33</td><td rowspan="6">遇到新伙伴</td><td rowspan="18">Beta Y</td><td rowspan="2">1｜开心</td><td rowspan="1">75%</td><td rowspan="1">33</td><td rowspan="1">点头同步左右小幅颤（极致开心）</td><td rowspan="1">24</td><td rowspan="1">情绪冲到很高的开心；雀跃、想撒娇蹦跳；社交或亲密高峰。</td><td rowspan="1">2</td><td rowspan="1">中</td></tr>
<tr><td rowspan="1">25%</td><td rowspan="2">29</td><td rowspan="2">遇见同类双向晃头（陌生Beany）</td><td rowspan="1">25</td><td rowspan="1">温暖友好、被好好对待后的软回应；社交开场或亲密回馈。</td><td rowspan="4">1</td><td rowspan="4">弱</td></tr>
<tr><td rowspan="2">2｜平静</td><td rowspan="1">65%</td><td rowspan="1">23</td><td rowspan="1">轻柔问候；关系刚开始或再次见面；低刺激的友好开场。</td></tr>
<tr><td rowspan="1">35%</td><td rowspan="1">57</td><td rowspan="1">左右循环环视</td><td rowspan="1">41</td><td rowspan="1">熟悉后的侧面短回声；亲昵互动中的二次确认；更松弛一点。</td></tr>
<tr><td rowspan="2">3｜悲伤</td><td rowspan="1">85%</td><td rowspan="1">50</td><td rowspan="1">间断定点侧头试探</td><td rowspan="1">52</td><td rowspan="1">近距离逗弄后的二次害羞；熟人之间；比第一次更软。</td></tr>
<tr><td rowspan="1">15%</td><td rowspan="1">17</td><td rowspan="1">初识同类慢偏头试探</td><td rowspan="1">30</td><td rowspan="1">害羞躲闪的变体；慢慢适应被关注；比上一条略软一点。</td><td rowspan="1">0</td><td rowspan="1">关闭</td></tr>
<tr><td rowspan="6">34</td><td rowspan="6">遇到熟悉伙伴</td><td rowspan="2">1｜开心</td><td rowspan="1">75%</td><td rowspan="1">33</td><td rowspan="1">点头同步左右小幅颤（极致开心）</td><td rowspan="1">24</td><td rowspan="1">情绪冲到很高的开心；雀跃、想撒娇蹦跳；社交或亲密高峰。</td><td rowspan="1">3</td><td rowspan="1">强</td></tr>
<tr><td rowspan="1">25%</td><td rowspan="2">34</td><td rowspan="2">遇见熟同类高频点头（熟悉Beany）</td><td rowspan="2">33</td><td rowspan="2">黏人、舍不得分开；被抱持时的依赖；温暖的撒娇贴近。</td><td rowspan="2">2</td><td rowspan="2">中</td></tr>
<tr><td rowspan="2">2｜平静</td><td rowspan="1">65%</td></tr>
<tr><td rowspan="1">35%</td><td rowspan="1">57</td><td rowspan="1">左右循环环视</td><td rowspan="1">41</td><td rowspan="1">熟悉后的侧面短回声；亲昵互动中的二次确认；更松弛一点。</td><td rowspan="2">1</td><td rowspan="2">弱</td></tr>
<tr><td rowspan="2">3｜悲伤</td><td rowspan="1">85%</td><td rowspan="1">29</td><td rowspan="1">遇见同类双向晃头（陌生Beany）</td><td rowspan="1">25</td><td rowspan="1">温暖友好、被好好对待后的软回应；社交开场或亲密回馈。</td></tr>
<tr><td rowspan="1">15%</td><td rowspan="1">50</td><td rowspan="1">间断定点侧头试探</td><td rowspan="1">52</td><td rowspan="1">近距离逗弄后的二次害羞；熟人之间；比第一次更软。</td><td rowspan="1">0</td><td rowspan="1">关闭</td></tr>
<tr><td rowspan="2">35</td><td rowspan="2">侧倒</td><td rowspan="10">0｜ANY</td><td rowspan="2">50%</td><td rowspan="1">36</td><td rowspan="2">侧倒低头向内躲闪</td><td rowspan="1">29</td><td rowspan="1">失去平衡、需要自保；侧向不稳；戒备但不攻击。</td><td rowspan="2">1</td><td rowspan="2">弱</td></tr>
<tr><td rowspan="1">40</td><td rowspan="1">32</td><td rowspan="1">自保戒备的第二条；持续不稳时的重复；更明确一点的护住自己。</td></tr>
<tr><td rowspan="1">36</td><td rowspan="1">充电</td><td rowspan="2">100%</td><td rowspan="1">1</td><td rowspan="1">充电启动单次点头（充电专属）</td><td rowspan="1">61</td><td rowspan="1">插上充电器/开始充电时的固定提示。</td><td rowspan="2">0</td><td rowspan="2">关闭</td></tr>
<tr><td rowspan="1">37</td><td rowspan="1">低电量</td><td rowspan="1">53</td><td rowspan="1">低电量间断抬头观望</td><td rowspan="1">40</td><td rowspan="1">低电量固定提示；能量将尽、虚弱收束；偏困倦的告别感。</td></tr>
<tr><td rowspan="2">38</td><td rowspan="2">开机</td><td rowspan="2">50%</td><td rowspan="1">8</td><td rowspan="1">开机上扬点头（开机启动）</td><td rowspan="1">7</td><td rowspan="1">开机上电；第一次苏醒；需要柔和、有活力的启动感。</td><td rowspan="2">1</td><td rowspan="2">弱</td></tr>
<tr><td rowspan="1">51</td><td rowspan="1">开机分段环视</td><td rowspan="1">39</td><td rowspan="1">开机苏醒的另一音色；同样柔和启动；用于避免总播同一条。</td></tr>
<tr><td rowspan="1">39</td><td rowspan="1">呼吸</td><td rowspan="1">预留 Beta N</td><td rowspan="4">100%</td><td rowspan="1">48</td><td rowspan="1">待机呼吸间断侧头</td><td rowspan="1">59</td><td rowspan="1">平稳持续的轻哼；待机伴随；低刺激氛围底。</td><td rowspan="1">0</td><td rowspan="1">关闭</td></tr>
<tr><td rowspan="1">40</td><td rowspan="1">抛起</td><td rowspan="1">Beta Y</td><td rowspan="1">58</td><td rowspan="1">抛起上扬晃头（抛起事件）</td><td rowspan="2">27</td><td rowspan="2">明显失重、刺激偏强；短暂离开稳定支撑；需要高能量反馈。</td><td rowspan="2">1</td><td rowspan="2">弱</td></tr>
<tr><td rowspan="1">41</td><td rowspan="1">旋转抛起</td><td rowspan="1">原表划除</td><td rowspan="1">32</td><td rowspan="1">旋转抛起极速环绕头（旋转抛）</td></tr>
<tr><td rowspan="1">42</td><td rowspan="1">关机</td><td rowspan="1">Beta Y</td><td rowspan="1">4</td><td rowspan="1">关机缓慢垂头锁位</td><td rowspan="1">4</td><td rowspan="1">关机进入彻底休眠；一天结束；需要渐弱、收束的入睡感。</td><td rowspan="1">0</td><td rowspan="1">关闭</td></tr></tbody>
</table>

[返回完整PRD目录](../README.md) · [上一章](./06-growth.md) · [下一章](./08-sync.md)
