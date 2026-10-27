> 上游历史资料：本项目已 fork 为叠意（dyth_homepage），当前入口说明见 [README.html](README.html)。本文中的原公司名称、CloudBase 环境、线上地址与回退路径属于上游项目，不是本项目的发布配置。

# 逸鸣山海公司官网开发与维护交接文档

> 交接对象：WorkBuddy / 后续网站维护人员  
> 项目名称：逸鸣山海公司官网（To C + To B）  
> 文档状态：当前有效  
> 最后核对日期：2026-10-20（Asia/Shanghai；浏览器标签页 Logo 发布后）

---

## 1. 这份文档解决什么问题

这份文档用于让新的开发者或 AI 助手在不了解历史对话的情况下，也能安全地继续修改、预览、发布和回退逸鸣山海公司官网。

接手后，请先完整阅读本文件，再阅读：

- `CURRENT_VERSION.md`：当前官方回退版本。
- `VERSIONS.md`：历史版本和每次重要线上更新记录。
- `dist/index.html`：当前 To C 正式首页。
- `dist/enterprise.html`：当前 To B 正式首页。
- `dist/*-greenbook.html`：四本已上线绿皮书的二级页面。
- `dist/assets/greenbook-site.css`：四本绿皮书共用的站点样式。

最重要的原则只有四条：

1. `dist/` 是唯一正式发布源。
2. 用户要求“先看本地效果”时只做预览；用户明确要求直接发布时，可在完成本地检查和备份后更新 `dist/` 并发布。
3. `versions/` 中的已批准版本是只读快照，不允许直接修改。
4. 发布前必须保存完整快照；发布后必须验证线上文件，而不是只相信命令显示“成功”。

---

## 2. 项目位置与线上地址

### 2.1 本地项目根目录

```text
/Users/xueming_1/Documents/ChatGPT/逸鸣山海公司网站/ymsh-lab
```

后续文档中出现的相对路径，均以该目录为基准。

### 2.2 正式线上地址

- To C 首页：<https://ymsh-team-d7ghsmmwt6c4e3b01-1301792998.tcloudbaseapp.com/>
- To C 显式首页：<https://ymsh-team-d7ghsmmwt6c4e3b01-1301792998.tcloudbaseapp.com/index.html>
- To B 企业服务页：<https://ymsh-team-d7ghsmmwt6c4e3b01-1301792998.tcloudbaseapp.com/enterprise.html>
- 课程页：<https://ymsh-team-d7ghsmmwt6c4e3b01-1301792998.tcloudbaseapp.com/course.html>
- 社群页：<https://ymsh-team-d7ghsmmwt6c4e3b01-1301792998.tcloudbaseapp.com/community.html>
- WorkBuddy 绿皮书：<https://ymsh-team-d7ghsmmwt6c4e3b01-1301792998.tcloudbaseapp.com/workbuddy-greenbook.html>
- Codex 绿皮书：<https://ymsh-team-d7ghsmmwt6c4e3b01-1301792998.tcloudbaseapp.com/codex-greenbook.html>
- TraeWork 绿皮书：<https://ymsh-team-d7ghsmmwt6c4e3b01-1301792998.tcloudbaseapp.com/traework-greenbook.html>
- Qoder 绿皮书：<https://ymsh-team-d7ghsmmwt6c4e3b01-1301792998.tcloudbaseapp.com/qoder-greenbook.html>

### 2.3 腾讯云 CloudBase 环境

```text
ymsh-team-d7ghsmmwt6c4e3b01
```

这是当前正式网站使用的 CloudBase 环境 ID。发布时必须核对完整字符串，不能凭记忆输入。

---

## 3. 当前技术形态

网站是一个无构建步骤的静态网站：

- HTML + CSS + 原生 JavaScript。
- 没有 React、Vue、Node 服务端或数据库。
- 没有 `package.json`，也不需要执行 `npm install` 或 `npm run build`。
- To C 和 To B 的主要样式、响应式规则及脚本，都直接写在各自 HTML 文件中。
- 课程页与社群页共用 `dist/assets/learn.css`。
- 四本绿皮书共用 `dist/assets/greenbook-site.css`，主体排版主要写在各自 HTML 中。
- 所有图片和二维码均为静态资源，位于 `dist/assets/`。
- 发布就是把 `dist/` 整个目录上传到 CloudBase 静态托管。

因此，修改后的 HTML 本身就是最终产物，不存在“修改源码后忘记重新构建”的步骤。但也正因为没有组件化，修改时要特别注意不要只改桌面样式而遗漏手机端媒体查询。

---

## 4. 目录结构与职责

```text
ymsh-lab/
├── WORKBUDDY_HANDOFF.md       # 本交接文档
├── CURRENT_VERSION.md         # 当前官方回退点
├── VERSIONS.md                # 版本历史、哈希和发布记录
├── dist/                      # 唯一正式发布目录
│   ├── index.html             # To C 正式首页
│   ├── enterprise.html        # To B 正式首页
│   ├── course.html            # AI 产品实战小课页
│   ├── community.html         # 小团队产品社群页
│   ├── workbuddy-greenbook.html # WorkBuddy 绿皮书
│   ├── codex-greenbook.html   # Codex 绿皮书
│   ├── traework-greenbook.html # TraeWork 绿皮书
│   ├── qoder-greenbook.html   # Qoder 绿皮书
│   └── assets/                # 正式图片、二维码、品牌 Logo、共用 CSS
├── previews/                  # 待确认方案和本地预览，不直接发布
├── versions/                  # 历史快照和正式回退版本，只读
├── output/                    # 浏览器检查截图等临时产物
└── .openai/hosting.json       # OpenAI Sites 元数据，不是 CloudBase 配置
```

### 4.1 `dist/`：正式源

如果用户要求先看预览，须等确认后再把改动写入这里；如果用户明确要求直接发布，完成核对、备份和本地检查后即可修改。CloudBase 发布命令始终指向 `./dist`。

### 4.2 `previews/`：预览方案

用于以下情况：

- 用户说“先做一个本地 HTML 看看”。
- 页面结构、视觉风格或交互还没有确认。
- 需要比较两个或多个版本。

建议每个预览使用独立目录并复制完整页面依赖，例如：

```text
previews/to-c-feature-name-v1/
├── index.html
├── enterprise.html
├── course.html
├── community.html
└── assets/
```

只改某个单页且能安全引用正式资源时，也可以使用单个 HTML 文件，但完整目录更利于交接和回看。

### 4.3 `versions/`：回退快照

这里保存经过用户确认的重要版本和发布前快照。规则：

- 任何 `vN-approved-YYYYMMDD/` 都视为不可变的正式快照。
- `pre-功能名-YYYYMMDD/` 是某次修改前保存的完整现场。
- 不要在快照目录里继续开发。
- 不要为了“整理目录”删除旧版本。

### 4.4 `.openai/hosting.json`：不要和 CloudBase 混淆

当前内容指向 `dist`，但其中的 `project_id` 属于 OpenAI Sites/应用元数据，并不是腾讯云 CloudBase 环境 ID。

正式站的发布目标始终是：

```text
CloudBase env: ymsh-team-d7ghsmmwt6c4e3b01
```

不要根据 `.openai/hosting.json` 把网站发布到其他服务。

---

## 5. 当前线上基线

### 5.1 当前正式文件哈希

截至 2026-10-20，本地 `dist/` 中主要文件的 SHA-256 如下。这是浏览器标签页图标统一发布后的正式源，可用于核对线上内容：

```text
dist/index.html       f42268e84eee960bcb28d72858b9f8ba34d80fce2fb64a1944d1d81177956317
dist/enterprise.html  cf8ac3c24ee7c751e49417b6e93b012529480c09cbc36c3a0982b2f62ee35f9c
dist/course.html      43e48de3b7e67160426fc61f8e1561e7e821e694ee49c756264b975b96016d8b
dist/community.html   118c7d1091ea9bc2fd23fc985b87afbd6e5f449498789c778c7a5302dc5e91bc
dist/workbuddy-greenbook.html 066dacf607c838cfb25f710beba91158c871cc47d143bfffb7477ff228801536
dist/codex-greenbook.html     2d7936ff95aed2e063a41b19235aaa2fd12d3fed18d375e1695a58ad6387eee8
dist/traework-greenbook.html  293c604b2334352ee44789813b3cbf0034bd52e691a7be2b9700748acb98eb4e
dist/qoder-greenbook.html     085705d6d9038bdac976070d7a187412d2124ce1401e6a7b1f2e569a8fd8e6c2
dist/assets/greenbook-site.css b3879c992d33f526ccf5dbad787fc7b836667b4a7b0d811d4ec73e448ba2ffad
```

当线上内容看起来没有更新时，可用哈希辅助判断是发布失败还是浏览器/CDN 缓存。

### 5.2 当前批准回退版本

当前用户明确命名的正式回退点是：

```text
V9 → versions/v9-approved-20261015/
```

V9 之后已经上线但尚未重新命名版本号的内容包括：

- To C 全页统一为暖白、浅蓝灰、腾讯蓝的视觉体系。
- “正在做的产品”四张产品卡保留原本的蓝、橙、绿、黄差异色。
- Karmatang 形象替换为 3D IP 联合创始人形象。
- 新增五卡“绿皮书系列”：WorkBuddy、Codex、TraeWork、Qoder、更多筹备中。
- WorkBuddy、Codex、TraeWork、Qoder 四本绿皮书二级页已上线；四张卡片整卡可点击。
- 四本书的封面加入慢漫和小明同学 IP 形象、白色逸鸣山海标志；书内加入简短的版权与免责声明、致谢。
- “更多绿皮书”卡加入豆包工作、百度搭子、千问办公三个 Logo，标题改为“其他绿皮书正在筹备”。
- To C、To B 的页头改用蓝色逸鸣山海标志，页脚改用含文字的完整 Logo。
- 八个公开页面的浏览器标签页图标统一引用蓝色逸鸣山海 Logo；四本绿皮书不再依赖浏览器默认图标。

如需回退到 V9，这些 V9 后的内容都会被撤销，因此必须先向用户明确说明。

### 5.3 最近一次发布记录

- 日期：2026-10-20。
- 发布内容：八个公开页面的浏览器标签页图标统一为蓝色公司 Logo。
- 上传并校验：709/709 个文件；八个线上 HTML 和共用图标素材的 SHA-256 均与 `dist/` 一致。
- 发布前本地完整快照：`versions/pre-favicon-20261020/`，可用于恢复到本次图标更新之前的完整站点状态。
- 发布前 CloudBase 备份记录：`.cloudbase-backup/1792486206947/`。

CloudBase 的备份目录不一定长期存在于当前项目工作区，因此不能把它当作唯一回退手段。V9 是最后一个用户命名的正式回退版本，但不是最新线上内容；不要把“回到 V9”和“撤销最近一次修改”混为一谈。

---

## 6. 页面地图

### 6.1 To C：`dist/index.html`

To C 面向个人用户、学习者、内容读者和潜在产品用户。当前导航及模块顺序为：

1. `#top`：顶部 Hero。
2. `#about`：我们是谁。
3. `#products`：正在做的产品。
4. `#greenbooks`：绿皮书系列。
5. `#notes`：文章与实验。
6. `#services`：一起学习/服务。
7. `#contact`：联系方式。

顶部导航中的“企业服务”跳转到 `enterprise.html`。

### Hero 当前关键信息

- 主叙事：三个前腾讯 QQ 人正在做 AI 产品。
- 右上工作台图：`assets/studio-workbench-v4.png`。
- 右上悬浮能力文字共五组：
  - 学产品：AI 产品从 0 到 1。
  - 用工具：AI 工具 / 模型实测。
  - 做项目：小程序 / Web / Agent。
  - 提效率：工作流 / 内容创作。
  - 找同伴：课程 / 社群 / 一对一。
- 手机端必须同时保留五组悬浮文字，不要恢复为轮播。

### “我们是谁”当前人物素材

- Ever：`assets/founder-ever.jpg`。
- Karmatang：`assets/founder-karmatang-ip-20261016.png`。
- Wise：`assets/founder-wise-workbuddy-20261008.jpg`。

不要误用目录中保留的旧图 `founder-karmatang.jpg`、`founder-wise.png` 或 `founder-wise-wide.png`。

### “正在做的产品”当前四个产品

1. 没事哒充能站。
   - 类型：微信小程序、主播与粉丝经营工具。
   - 小程序文本链接：`#小程序://没事哒充能站/0r7FTp3nGyXj50b`。
   - 页面通过“复制小程序链接”按钮复制，不使用普通网页 `<a>` 跳转。
2. 一拍上身。
   - 类型：面向服装商户的 AI 上身展示工具。
   - 正式链接：<https://yipashangshen-318-d2d6p23645d706-1301792998.tcloudbaseapp.com/>。
   - 目前展示两组“服装图 → AI → 模特上身图”，并强调模特可选、场景可选、批量生成素材。
3. Color Work。
   - 类型：旅行灵感产品实验。
   - 当前没有产品跳转链接。
4. 跨境电商实验室。
   - 类型：自营真实业务，暂不对外。
   - 展示六步自动化闭环：自动选品、素材生成、自动上架、投流推广、数据回收、智能迭代。
   - 流程使用 SVG 粒子循环动画和简约手绘图标。

产品区是 To C 页面中有意保留明显差异色的区域。即使全站色调统一，也不要把四张产品卡全部改成相同颜色。

### “绿皮书系列”当前状态

五张卡片在桌面端保持一排：

1. WorkBuddy 绿皮书。
2. Codex 绿皮书。
3. TraeWork 绿皮书。
4. Qoder 绿皮书。
5. 其他绿皮书正在筹备。

前四张书卡均是指向站内二级页的 `<a>`，点击卡片任意区域或其中的“阅读当前版”文字，都在当前标签页打开对应页面。“更多绿皮书”仍是不可点击的 `<article>`。平板和手机端采用单行横向滑动，不允许因此产生整个页面的横向溢出。

四个二级页分别位于 `dist/workbuddy-greenbook.html`、`dist/codex-greenbook.html`、`dist/traework-greenbook.html`、`dist/qoder-greenbook.html`。页面顶部有返回 `index.html#greenbooks` 的链接，目录锚点在页内跳转。四页共用 `assets/greenbook-site.css`；配图分别位于 `assets/paths/`、`assets/codex-images/`、`assets/trae-images-opt/`、`assets/qoder-images/`。部分文件名及引用经过 URL 编码，改图或迁移时须逐项核对 HTML 中的真实路径，不能批量改名。

四本书按“指导与实践书”的口吻整理，封面使用慢漫和小明同学 IP 图，另有白色公司标志；正文开头设简短的“版权与免责声明”和“致谢”。书内涉及第三方产品时，应保留“独立整理、非官方文档”的界限，价格、功能、模型名称等会变化的信息需要重新核对。

对应 Logo：

```text
assets/greenbook-workbuddy-logo.png
assets/greenbook-codex-logo.png
assets/greenbook-traework-logo.png
assets/greenbook-qoder-logo.png
```

“更多绿皮书”卡目前展示三个筹备方向：豆包工作、百度搭子、千问办公。对应素材为 `assets/greenbook-more-doubao.jpg`、`assets/greenbook-more-baidu.png`、`assets/greenbook-more-qianwen.jpg`；三者目前都没有二级页或跳转链接。新增正式绿皮书时，再参照现有四页补齐正文、目录、图片、返回链接、卡片入口与移动端检查。

### “一起学习”及二级页

- `course.html`：AI 产品实战小课，价格文案目前为 388 元/季度。
- `community.html`：小团队产品社群，价格文案目前为 588 元/年。
- 两页共用 `assets/learn.css`。
- 两页的咨询/申请按钮返回 To C 首页的 `#contact`。

修改 `learn.css` 会同时影响课程页和社群页，必须两页一起检查。

---

### 6.2 To B：`dist/enterprise.html`

To B 面向企业客户，核心叙事不是“我们具备什么技术”，而是“客户遇到什么业务问题，可以找我们做什么”。当前模块顺序为：

1. `#top`：企业 Hero。
2. `#services`：服务能力。
3. `#scenario`：合作场景。
4. `#process`：交付方式。
5. `#proof`：真实实践。
6. 无 ID 的 `Why YMSH` 公司责任模块。
7. `#contact`：预约交流。

顶部“个人与学习”跳回 `index.html`。

### Hero 当前悬浮业务文字

- 找场景：AI 场景诊断。
- 做产品：AI Agent / 小程序 / 企业工具。
- 改流程：工作流自动化。
- 选模型：模型测评与选型。
- 带团队：AI 工作坊 / 岗位实训。

这五组文字是用户要求的“直观告诉 B 端客户什么事情可以找我们”。修改时应优先保持具体、简短、可理解，不要退回抽象能力名词堆叠。

### 服务能力

当前四项：

1. AI 产品与智能体开发。
2. 工作流自动化。
3. 模型测评与选型。
4. 企业 AI 工作坊。

默认第 1 项为腾讯蓝激活态；鼠标悬停或键盘聚焦其他卡片时，目标卡片轻微凸起并变为激活态；鼠标离开后回到第 1 项。

### 合作场景

这是原生 JavaScript 选项卡，共四种客户状态：

- 还没想清楚做什么 → 场景探索。
- 已有方向，想先验证 → 原型验证。
- 需要完整产品落地 → 产品交付。
- 想让团队用起来 → 组织赋能。

具体数据位于页面底部脚本中的 `scenarioData` 对象。修改按钮文案时，要同步检查 `data-scenario` 与对象键是否一致。

### 交付方式

四步流程：定义问题、原型验证、产品交付、持续迭代。

桌面端有企鹅沿流程线移动，经过某一步时该步骤凸显；手机端为了可读性，不应强行保留横向奔跑效果。脚本会根据 `.process-runner` 的位置同步 `.process-active`。

### 真实实践

四张案例卡：

- 跨境电商 Agent。
- 一拍上身 AI 试衣。
- 主播粉丝与周边管理小程序。
- Color Work 旅行体验。

卡片支持悬停/聚焦轻微凸起。第四张必须保持 Color Work，不要误换成跨境电商或其他图文。

### Why YMSH

核心文案是：

> 以公司为责任主体，以结果建立长期合作。

右侧不是无关配图，而是“公司统一承接、核心团队直接参与、围绕业务结果迭代”的承诺板。这个模块的目标是建立企业合作信任，不要随意改成装饰性视觉。

### 预约交流

- 合作邮箱：`YmshTeam@126.com`。
- 微信二维码：`assets/wechat-contact-qr.png`。
- 飞书二维码：`assets/feishu-contact-qr.png`。
- 两个二维码并列，各自带一行说明文字。

---

## 7. 关键交互与脚本

### 7.1 To C 脚本

`dist/index.html` 底部原生 JavaScript 目前负责：

1. 手机导航展开、关闭和 `aria-expanded` 状态。
2. `.reveal` 元素进入视口后的渐入动画。
3. “没事哒充能站”小程序链接复制及失败回退方案。
4. “最近在做”企鹅位置与标签高亮同步。
5. “一起学习”服务卡悬停/聚焦激活状态。

小程序复制使用 Clipboard API；在权限不可用时，会临时创建隐藏的 `textarea` 回退复制。修改这部分时必须保留回退逻辑。

### 7.2 To B 脚本

`dist/enterprise.html` 底部原生 JavaScript 目前负责：

1. 手机导航展开与关闭。
2. 合作场景选项卡及动态内容切换。
3. 服务能力卡的默认和悬停激活状态。
4. 交付流程企鹅位置与步骤高亮同步。
5. `.reveal` 元素的入场动画。

### 7.3 减少动态效果的无障碍处理

两张主页均包含 `prefers-reduced-motion: reduce` 规则。用户系统选择减少动态效果时：

- 页面应直接显示内容。
- 企鹅或粒子动画可以停用。
- 不应因为动画停用而隐藏关键信息。

新增动画时也要补充对应的 reduced-motion 处理。

---

## 8. 视觉和响应式约束

### 8.1 To C 色彩

全页主体系：

- 暖白背景。
- 浅蓝灰区块。
- 腾讯蓝重点色。
- 少量橙色、黄色和绿色作提示。

产品区例外：四张产品卡保留原本的差异色，以避免全页过于素净。

`dist/index.html` 中存在 `<style id="unified-tone-preview">`。虽然 ID 中包含 `preview`，它目前已经是线上正式色调覆盖层，不要因为名字像预览就删除。若未来重构，可以在确认视觉无变化后把这部分合并进主样式。

### 8.2 To B 色彩

- 核心品牌色为腾讯蓝。
- 不使用大面积高饱和腾讯蓝铺满整个模块。
- 主要通过按钮、编号、激活卡片、边框、局部光晕和重点文字使用蓝色。
- 保证白底或浅底上的正文对比度。

### 8.3 手机端原则

至少检查以下宽度：

- 1440px 左右桌面端。
- 900px 左右平板端。
- 390 × 844 手机端。
- 360px 或 370px 的窄屏端。

当前关键断点：

- To C：900px、640px、370px。
- To B：920px、680px、370px。

手机端硬性要求：

- 页面不能整体左右滑动。
- 导航按钮可点击，菜单打开后项目不遮挡正文。
- Hero 五组悬浮能力文字全部可见，不使用自动轮播。
- 卡片不要保留过高的桌面固定高度。
- 二维码不被压扁或裁切。
- 绿皮书卡片内部可以横向滑动，但页面整体不能横向溢出。
- 一拍上身图片比例正常。
- 跨境电商六步流程的文字和图标不重叠。

可以在浏览器控制台检查：

```js
document.documentElement.scrollWidth === window.innerWidth
```

结果应为 `true`。如果为 `false`，要定位超宽元素，而不是简单给所有容器加 `overflow: hidden` 掩盖问题。

### 8.4 公司 Logo 的当前用法

用户提供了三款透明背景素材，页面已按背景亮度分工使用：

| 素材 | 当前用途 | 注意事项 |
| --- | --- | --- |
| `assets/ymsh-logo-blue.png` | To C、To B 页头的蓝色图形标志 | 图片没有公司中文字，邻近的页面文字仍需保留。 |
| `assets/ymsh-logo-full.png` | To C、To B 页脚的含文字完整 Logo | 文字颜色较深，应置于浅色底。 |
| `assets/ymsh-logo-white.png` | 四本绿皮书深色封面的白色图形标志 | 不要直接放在白底或浅底上。 |

绿皮书封面 Logo 和 IP 图的共用展示规则在 `assets/greenbook-site.css`；修改时要连四本书一起检查。不要把第三方工具 Logo 与逸鸣山海公司 Logo 混用。

八个公开 HTML 页面的 `<head>` 都使用 `assets/ymsh-logo-blue.png?v=20261020` 作为 `rel="icon"`。这里的版本参数用于绕开浏览器对旧标签页图标的缓存；后续换图时应同时更新八页的引用，并换一个新的版本参数。

---

## 9. 素材管理规则

### 9.1 正式素材目录

```text
dist/assets/
```

正式 HTML 中的图片路径统一使用相对路径：

```html
<img src="assets/example.png" alt="清楚描述图片内容" />
```

### 9.2 用户从聊天中上传图片时

聊天附件通常位于系统临时目录，后续可能被清理。收到确认使用的图片后，应立即：

1. 检查图片内容和方向。
2. 复制到当前预览目录的 `assets/`。
3. 用户确认发布时，再复制到 `dist/assets/`。
4. 使用含义清晰的英文小写文件名，必要时加日期。
5. 更新 HTML 的 `src` 和 `alt`。

不要让正式网页继续引用 `/var/folders/...`、`/tmp/...` 或其他本机绝对路径。

### 9.3 图片替换策略

如果只是替换同一素材，存在两种方案：

- 保留原文件名：HTML 无需改，但 CDN 和浏览器可能继续显示旧缓存。
- 使用新文件名：更容易触发更新，重要人物照和视觉素材更推荐这种方式。

过去 Wise 图片未及时显示，主要风险就是线上缓存或引用路径没有真正变化。因此重要图片更新建议使用带日期的新文件名，例如：

```text
founder-name-YYYYMMDD.jpg
```

### 9.4 图片体积

当前 `dist/assets/` 总体积较大，包含若干 1–2 MB 图片。新增图片时建议：

- 照片优先使用压缩后的 JPG/WebP。
- 透明 Logo、二维码和插画使用 PNG/WebP。
- 不要压缩二维码到影响扫码。
- 不要为了减小体积改变人物或产品图的宽高比。
- 优化旧素材前先做视觉对比，不要一次性批量重编码后直接发布。

### 9.5 公开性提醒

`dist/assets/` 中的一切都会被公开访问。禁止放入：

- API Key、CloudBase 密钥或账号凭证。
- 内部合同和未公开业务数据。
- 不希望公开的高清原图或个人资料。

### 9.6 近期新增的绿皮书素材

```text
assets/greenbook-manman-ip-sheet.png     # 慢漫封面 IP 图
assets/greenbook-xiaoming-ip-sheet.png   # 小明同学封面 IP 图
assets/greenbook-workbuddy-logo.png      # 首页书卡的 WorkBuddy 工具 Logo
assets/greenbook-codex-logo.png          # 首页书卡的 Codex 工具 Logo
assets/greenbook-traework-logo.png       # 首页书卡的 TraeWork 工具 Logo
assets/greenbook-qoder-logo.png          # 首页书卡的 Qoder 工具 Logo
assets/greenbook-more-doubao.jpg         # 筹备卡：豆包工作
assets/greenbook-more-baidu.png          # 筹备卡：百度搭子
assets/greenbook-more-qianwen.jpg        # 筹备卡：千问办公
```

这些工具图标仅用于说明绿皮书主题，并非公司标志。后续替换前，先检查透明度、裁切和小尺寸下的辨识度。

---

## 10. 标准修改流程

下面是后续每次修改都应遵循的流程。

### 第一步：确认范围

先明确是：

- 只改 To C。
- 只改 To B。
- 同时改两个主页。
- 改课程页/社群页。
- 只改素材，不改结构。

不要因为 To C 和 To B 在同一站点，就顺手修改用户没有要求的页面。

### 第二步：读取当前状态

至少检查：

```text
CURRENT_VERSION.md
VERSIONS.md
dist/目标页面
dist/assets/相关素材
```

同时查看工作区是否已有未完成改动。当前仓库中许多正式文件没有完整纳入 Git，因此不能假设 `git status` 干净，也不能通过 `git reset --hard` 恢复线上版本。

### 第三步：创建预览副本

用户要求“先看看效果”时，不要直接修改 `dist/`。建议命名：

```text
previews/to-c-功能名-v1/
previews/to-b-功能名-v1/
```

从 `dist/` 复制完整文件到新目录，然后只在该预览目录开发。不要覆盖已有预览，递增 `v1`、`v2`。

### 第四步：本地预览

预览 `dist/`：

```bash
python3 -m http.server 4180 --directory dist
```

预览独立方案目录：

```bash
python3 -m http.server 4180 --directory previews/to-c-功能名-v1
```

打开：

```text
http://127.0.0.1:4180/index.html
```

To B 则打开：

```text
http://127.0.0.1:4180/enterprise.html
```

如果 4180 端口已被占用，可以改用 4181、8080 等其他本地端口。

不要直接双击 `file://.../index.html` 作为唯一验收方式。本地 HTTP 服务更接近线上环境，也更容易发现路径和脚本问题。

### 第五步：按用户要求确定发布时机

如果用户要求“先做本地 HTML 看看”，在用户明确确认前只交付本地预览，不发布线上。如果用户一开始就明确要求“直接发布”，不必再为同一动作重复索要确认，但仍须完成备份、本地检查和线上验证。

如果用户对预览提出二次修改，应继续改预览版本；确认后再合入 `dist/`。

### 第六步：发布前保存快照

快照必须包含完整 `dist/`，而不是只备份一个 HTML。推荐目录名：

```text
versions/pre-功能名-YYYYMMDD/
```

创建前先确认目标目录不存在，再完整复制 `dist/`。如果用户明确把当前状态命名为 V10、V11 等，则使用：

```text
versions/v10-approved-YYYYMMDD/
```

并同步更新 `CURRENT_VERSION.md` 和 `VERSIONS.md`。

### 第七步：合入正式源

只把用户确认的改动和素材同步到 `dist/`。再次本地检查 `dist/`，不要只检查预览目录。

### 第八步：发布

在项目根目录执行：

```bash
npx --yes --package @cloudbase/cli tcb hosting deploy ./dist -e ymsh-team-d7ghsmmwt6c4e3b01 --safe --verify --ignore '.DS_Store'
```

参数说明：

- `./dist`：正式发布目录。
- `-e`：指定 CloudBase 环境。
- `--safe`：发布前执行安全备份流程。
- `--verify`：上传后进行远端一致性校验。
- `--ignore '.DS_Store'`：忽略 macOS 目录文件。

不要擅自加入 `--prune`。删除远端文件是高风险操作，只有在完整核对远端清单并获得用户确认后才能执行。

### 第九步：线上验证

至少验证：

- To C 首页能打开。
- To B 首页能打开。
- 本次修改模块正确。
- To C/To B 切换链接正常。
- 页面无控制台错误。
- 图片和二维码全部加载。
- 手机端没有横向溢出。

为绕过缓存，可在 URL 后增加查询参数：

```text
https://ymsh-team-d7ghsmmwt6c4e3b01-1301792998.tcloudbaseapp.com/index.html?verify=YYYYMMDDHHMM
```

也可以下载线上 HTML 后与本地核对：

```bash
curl -fsSL -H 'Cache-Control: no-cache' 'https://ymsh-team-d7ghsmmwt6c4e3b01-1301792998.tcloudbaseapp.com/index.html?verify=YYYYMMDDHHMM' -o /tmp/ymsh-live-index.html
shasum -a 256 /tmp/ymsh-live-index.html dist/index.html
```

两个哈希一致，才能证明 HTML 已更新。图片仍显示旧版本时，再分别检查资源 URL、文件名和 CDN 缓存。

### 第十步：记录版本

发布成功后更新 `VERSIONS.md`，至少记录：

- 发布日期。
- 修改范围。
- 是否影响 To C / To B。
- 页面哈希。
- 新增或替换的素材。
- 上传校验文件数。
- 发布前快照路径。
- 重要视觉和交互说明。

如果用户说“保存当前版本为 V10”，还必须更新 `CURRENT_VERSION.md` 并创建完整 `v10-approved-日期/` 快照。

---

## 11. 发布前 QA 检查清单

### 11.1 全站通用

- [ ] 页面标题、主文案和公司名没有错别字。
- [ ] 所有本地图片路径都能加载。
- [ ] 所有外链地址正确。
- [ ] 外部新窗口链接包含 `rel="noopener noreferrer"`。
- [ ] 邮箱链接仍为 `YmshTeam@126.com`。
- [ ] To C、To B 页头蓝色公司标志及页脚完整公司 Logo 均正常显示。
- [ ] To C、To B、课程、社群及四本绿皮书的浏览器标签页都显示蓝色公司 Logo。
- [ ] 锚点导航能定位到正确模块。
- [ ] 手机菜单可打开、可关闭，点击菜单项后自动收起。
- [ ] 页面控制台无红色错误。
- [ ] 无页面级横向滚动。
- [ ] 系统开启“减少动态效果”时仍可读、可操作。
- [ ] 没有把临时绝对路径写入正式 HTML。
- [ ] 没有把密钥、账号令牌或内部数据放进 `dist/`。

### 11.2 To C 专项

- [ ] Hero 五组悬浮文字桌面和手机端都可见。
- [ ] 三位联合创始人的图片没有拉伸。
- [ ] Karmatang 使用当前 IP 图，而不是旧真人图。
- [ ] Wise 使用当前 WorkBuddy 活动照片和已确认裁切。
- [ ] 四张产品卡保留差异色。
- [ ] 没事哒充能站复制按钮确实复制正确的小程序文本。
- [ ] 一拍上身两组服装图与上身图对应正确。
- [ ] 一拍上身外链可打开。
- [ ] 跨境电商六步流程动画正常，文字不重叠。
- [ ] 绿皮书桌面五卡一排。
- [ ] 绿皮书手机端只在卡片容器内部横滑。
- [ ] WorkBuddy、Codex、TraeWork、Qoder 四张卡片整卡和“阅读当前版”区域均可进入正确二级页。
- [ ] 四本书的返回入口、页内目录、正文配图、慢漫与小明同学 IP 图、白色公司 Logo、版权与免责声明及致谢均正常。
- [ ] “更多绿皮书”仍不可点击，豆包工作、百度搭子、千问办公三个图标和文字对应正确。
- [ ] 公众号文章链接和二维码正常。
- [ ] 课程、社群、企业服务入口正常。

### 11.3 To B 专项

- [ ] Hero 五组业务能力文字全部可见。
- [ ] Hero 中包含“小程序”字样。
- [ ] 服务能力默认第 1 卡激活。
- [ ] 鼠标悬停和键盘聚焦能切换服务卡状态。
- [ ] 四个合作场景选项卡内容正确切换。
- [ ] 交付流程桌面端企鹅移动和步骤高亮同步。
- [ ] 手机端流程不因横向动画破版。
- [ ] 四张真实实践卡有轻微凸起反馈。
- [ ] 第四张案例是 Color Work。
- [ ] Why YMSH 是公司承诺板，不是无关图片。
- [ ] 微信和飞书二维码并列、比例正常、说明文字正确。
- [ ] To B 到 To C 的“个人与学习”入口正常。

---

## 12. 常见修改操作

### 12.1 只改一段文案

1. 确认目标页面与模块 ID。
2. 在预览副本中修改。
3. 检查文字换行是否导致桌面/手机卡片高度异常。
4. 用户确认后合入 `dist/`。
5. 发布前做完整快照。

不要只在桌面宽度下看文字。中文文案多出 5–10 个字，手机端可能多换两行并造成按钮下沉。

### 12.2 替换联合创始人图片

1. 把新图放到预览目录 `assets/`。
2. 建议用新文件名，避免缓存。
3. 更新人物卡 `src` 和 `alt`。
4. 用人物卡当前的 `object-fit`、`object-position` 调整裁切，不要直接拉伸图片。
5. 同时检查 1440px 和 390px。
6. 用户确认后复制新图和 HTML 到 `dist/`。

### 12.3 新增产品卡

当前产品区使用两列网格，产品卡高度和展示内容较复杂。新增前先判断：

- 是否应该成为第 5 张卡，还是替换“介绍待补充”的产品。
- 是否需要产品链接。
- 是否有实图、流程图或动态图。
- 是否需要自己的卡片色调。

新增后必须检查 2 列桌面布局和单列手机布局，尤其避免只复制 HTML、不复制相关样式和素材。

### 12.4 新增或更新绿皮书

当前四本书已有站内页面，首页对应卡片是 `<a class="greenbook-card" href="书名-greenbook.html">`，整卡可点击。新增第五本时：

1. 先完成 `dist/书名-greenbook.html` 的内容、目录锚点、配图和返回 `index.html#greenbooks` 的链接。
2. 复用 `assets/greenbook-site.css` 的站点样式，并检查封面 IP、公司白色 Logo、版权与免责声明、致谢。
3. 将首页对应筹备卡改为完整的站内 `<a class="greenbook-card" href="书名-greenbook.html">`；站内链接默认在当前标签页打开，不必加 `target="_blank"`。
4. “阅读当前版”文字可放在整卡链接内部，但不要再嵌套一个 `<a>`。保留键盘焦点样式。
5. 更新书卡状态、素材路径、手机横滑布局和所有发布前检查。尚未上线的筹备主题保持不可点击。

### 12.5 替换二维码

1. 保持二维码完整正方形，不裁切定位角。
2. 尽量使用 PNG 原图。
3. 本地用手机实际扫码。
4. 检查桌面和手机显示尺寸。
5. 如果是同名替换，发布后用缓存参数验证；更推荐新文件名。

### 12.6 修改 To B 合作场景

合作场景由两部分共同组成：

- HTML 中的 `.scenario-tab` 按钮。
- JavaScript 中的 `scenarioData`。

新增或重命名时必须保证：

```text
button[data-scenario="键名"] ↔ scenarioData.键名
```

同时维护 `aria-selected`，并确保首个面板的初始 HTML 与首个数据对象一致。

---

## 13. 版本保存与回退

### 13.1 用户说“保存为 V10”时

必须同时完成：

1. 创建 `versions/v10-approved-YYYYMMDD/` 完整快照。
2. 快照中包含当时整个 `dist/`，目前至少有八个 HTML 页面和全部 `assets/`，不要只复制两个主页。
3. 计算 To C 与 To B 的 SHA-256。
4. 更新 `CURRENT_VERSION.md`。
5. 在 `VERSIONS.md` 顶部新增 V10 记录。
6. 明确这次版本包含哪些功能。

仅在文档中写“V10”而不复制完整文件，不算完成版本保存。

### 13.2 安全回退流程

回退会替换整个 `dist/`，属于高影响操作。执行前必须：

1. 明确用户要回退到哪个版本。
2. 告知该版本之后哪些功能会消失。
3. 先把当前 `dist/` 完整保存为新的 `pre-rollback-日期时间/` 快照。
4. 确认目标快照包含 HTML 和 `assets/`。
5. 用目标快照重建 `dist/`。
6. 本地预览并检查页面。
7. 获得用户确认后重新发布。
8. 发布后核对线上哈希。

推荐使用“移动当前目录到新快照，再复制目标版本”的可恢复方式。不要直接删除当前 `dist/`，也不要使用 `git reset --hard` 或 `git checkout -- dist`。

---

## 14. Git 状态特别说明

项目虽然有 `.git`，但当前生产站点的许多 HTML、图片、版本目录和文档没有完整纳入 Git 历史。

因此：

- Git 目前不能代替 `versions/` 快照。
- 不要把 `git status` 中的大量未跟踪素材当作垃圾清理。
- 不要在未核对前执行 `git clean`。
- 不要执行 `git reset --hard` 试图恢复线上状态。
- 如未来要规范 Git，应先把当前线上 `dist/` 和所有批准版本做一次独立备份，再制定忽略规则和首次基线提交。

如果后续决定正式 Git 化，建议至少跟踪：

```text
dist/
CURRENT_VERSION.md
VERSIONS.md
WORKBUDDY_HANDOFF.md
```

`output/`、`.DS_Store` 和临时浏览器截图通常可以忽略；`previews/`、`versions/` 是否纳入 Git 需要根据仓库体积和备份策略另行决定。

---

## 15. 常见问题与排查

### 15.1 本地已经换图，线上仍是旧图

依次检查：

1. 修改的是 `dist/` 还是只改了 `previews/`。
2. HTML 的 `src` 是否指向新文件。
3. 新文件是否真的位于 `dist/assets/`。
4. 发布日志是否包含该资源。
5. 使用 `?verify=时间戳` 绕过浏览器缓存。
6. 直接访问图片 URL 并加查询参数。
7. 重要图片是否应该换新文件名。

### 15.2 页面发布成功，但浏览器出现风险提示

当前使用 CloudBase 测试域名，某些浏览器或自动化环境可能显示测试域名风险提示。这不一定表示发布失败。

- 不要用自动化脚本绕过浏览器安全警告。
- 可以通过 `curl`、文件哈希和用户手动确认验证内容。
- 长期正式运营建议配置自有域名、HTTPS 和必要备案。

### 15.3 手机端布局与桌面差异很大

常见原因：

- 固定高度没有在媒体查询中重置。
- 绝对定位元素按桌面坐标保留。
- 字体换行导致卡片变高。
- 容器宽度加上 padding 超过视口。
- 横向滑动模块没有限制在自身容器内。

排查时从最外层超宽元素开始，不要只用 `body { overflow-x: hidden; }` 掩盖结构问题。

### 15.4 动画不运行

先检查：

- 系统是否启用“减少动态效果”。
- 元素是否因为手机端媒体查询被隐藏。
- 控制台是否有脚本错误。
- 类名是否被重命名但 JavaScript 查询仍使用旧类名。
- SVG `animateMotion` 是否被浏览器支持。

动画属于增强体验，任何情况下正文和关键信息都必须仍然可见。

### 15.5 本地双击能看，发布后图片丢失

通常是大小写或相对路径问题。CloudBase 路径区分大小写。检查：

- 文件名大小写是否完全一致。
- 是否误写成 `../assets/`。
- 是否引用本机绝对路径。
- 文件是否被漏复制到 `dist/assets/`。

绿皮书配图还要检查路径中的空格、中文和百分号编码。有些旧素材引用经过 URL 编码；不要只看文件管理器里的显示名，须核对浏览器实际请求地址与 HTML 的 `src`。

---

## 16. 可维护性改进建议

这些不是当前必须修改的任务，未经用户要求不要一次性重构，但后续可以逐步做：

1. 把 `index.html` 和 `enterprise.html` 的内联 CSS 拆成独立样式文件。
2. 把两页共用的导航、按钮、响应式变量整理成公共 CSS。
3. 把底部原生脚本拆成 `assets/site.js` 和 `assets/enterprise.js`。
4. 为 `dist/` 建立正式 Git 基线提交。
5. 增加 `.gitignore`，忽略 `.DS_Store`、浏览器输出和临时文件。
6. 压缩大图片并转换为 WebP，同时保留二维码清晰度。
7. 配置自有域名，减少 CloudBase 测试域名提示。
8. 增加自动化静态检查：断链、缺失图片、HTML 语法和手机端横向溢出。
9. 给重要图片加入明确尺寸，减少加载时布局跳动。
10. 如果产品/文章数量继续增长，再考虑数据化或组件化，而不是继续复制长 HTML。

重构原则：每次只做一个小范围，并用当前线上截图做视觉对照，避免“代码更整洁但页面变样”。

---

## 17. 当前已知边界

- 网站目前没有后台内容管理系统；文章、产品和绿皮书都需要改 HTML。
- 没有自动发布流水线；发布依赖本机 CloudBase CLI 登录状态。
- 没有表单后端；联系入口主要是邮箱和二维码。
- 没有线上监控和错误上报。
- 四本绿皮书已经有二级页；豆包工作、百度搭子和千问办公仍只是筹备展示，没有正文页与入口。
- Color Work 当前为概念介绍，产品详情待补充。
- CloudBase 测试域名可能有缓存或风险提示。
- 当前 Git 历史不能完整恢复线上生产文件。

这些边界不是 bug，但在新增功能前应判断是否需要补齐。

---

## 18. 完成交付的定义

一次网站改动只有同时满足以下条件，才算真正完成：

1. 改动范围符合用户要求，没有顺手改动其他模块。
2. 本地预览通过，桌面和手机均检查。
3. 如果用户要求先看预览，已获得最终确认；如果用户明确要求直接发布，已按要求完成发布前检查。
4. 发布前完整快照已保存。
5. 确认版已合入 `dist/`。
6. CloudBase 发布成功并完成远端校验。
7. 线上页面和资源已实际检查。
8. 哈希或内容标记证明线上是新版本。
9. `VERSIONS.md` 已记录。
10. 如用户命名了新版本，`CURRENT_VERSION.md` 和批准快照均已更新。

---

## 19. 给 WorkBuddy 的建议首条任务指令

把下面这段连同本项目目录一起提供给 WorkBuddy，可以减少误操作：

```text
请先完整阅读 ymsh-lab/WORKBUDDY_HANDOFF.md、CURRENT_VERSION.md 和 VERSIONS.md，再开始工作。

正式发布源只有 ymsh-lab/dist/。如果我说“先看看效果”，请从 dist 创建新的 previews 预览副本，不要直接修改 dist，也不要发布。versions 里的 approved 目录都是只读回退快照，不允许在里面开发。

每次改动都要同时检查桌面端和 390px 手机端，尤其检查页面横向溢出、Hero 悬浮文字、图片比例、二维码、To C/To B 切换和动态效果。当前四本绿皮书都有站内二级页；改动绿皮书时也要检查整卡入口、返回链接、目录、封面 IP 与公司 Logo。

如果我要求先预览，请等我确认后再发布；如果我明确要求直接发布，可以在完成检查和备份后进行。发布到 CloudBase 环境 ymsh-team-d7ghsmmwt6c4e3b01，命令必须使用 --safe、--verify，并在发布后核对线上内容或哈希。当前最新现场是 dist，V9 是最后一个由我命名的正式回退版本，不等于最新线上版本。

不要使用 git reset --hard、git clean 或直接删除 dist；当前生产文件没有完整纳入 Git。
```

---

## 20. 2026-10-17 至 10-19 增量发布记录

以下变更均晚于用户命名的 V9，属于已上线但尚未命名为 V10 的更新；详细哈希与发布记录以 `VERSIONS.md` 为准。

| 日期 | 更新 | 已知发布前备份 |
| --- | --- | --- |
| 10 月 17 日 | WorkBuddy、Codex、Qoder 三本绿皮书二级页上线，首页书卡接入阅读入口；442/442 文件校验。 | 本地 `versions/pre-greenbook-pages-20261017/`；CloudBase `.cloudbase-backup/1792227323473/` |
| 10 月 19 日 | 前三本书补封面 IP、版权与免责声明、致谢；444/444 文件校验。 | 本地 `versions/pre-greenbook-frontmatter-ip-20261019/`；CloudBase `.cloudbase-backup/1792396809076/` |
| 10 月 19 日 | TraeWork 绿皮书二级页上线，第四张卡整卡可点击；703/703 文件校验。 | 本地 `versions/pre-traework-greenbook-20261019/`；CloudBase `.cloudbase-backup/1792409274468/` |
| 10 月 19 日 | “更多绿皮书”加入豆包工作、百度搭子、千问办公三个图标及名称；706/706 文件校验。 | CloudBase `.cloudbase-backup/1792412346711/` |
| 10 月 19 日 | To C、To B 页头和页脚加入公司 Logo，四本书封面加入白色公司标志；709/709 文件校验。 | CloudBase `.cloudbase-backup/1792420793925/` |
| 10 月 20 日 | 八个公开页面统一为逸鸣山海蓝色 Logo 标签页图标；709/709 文件校验。 | 本地 `versions/pre-favicon-20261020/`；CloudBase `.cloudbase-backup/1792486206947/` |

当前 `pre-favicon` 快照完整保存了 10 月 19 日公司 Logo 发布后的站点，适合撤销本次标签页图标更新；它不包含 10 月 20 日的图标改动。V9 则是更早、由用户命名的正式回退版本。下一次发布仍应先为当时的完整 `dist/` 另存快照。

---

## 21. 最后提醒

这个项目最容易发生的三类事故是：

1. 只改了预览文件，以为线上源也改了。
2. 发布成功但被缓存误导，以为素材没有更新。
3. 在没有完整快照的情况下回退或清理，导致新版内容无法恢复。

用户要先看效果时，坚持“预览 → 确认 → 完整快照 → 合入 `dist/` → 安全发布 → 线上验证 → 版本记录”；用户明确要求直接发布时，可省去等待预览确认，但不能省去快照、检查和线上核验。
