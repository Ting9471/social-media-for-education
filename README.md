# Social Media for Education

教育社媒赛道分析报告：儿童教育类目、教育学习达人竞争、账号候选、分区/领域 Top20、K12 低粉热门笔记。

- 交付文件：[`index.html`](index.html)。本目录可以独立作为静态站点发布目录。
- 交付运行 ID：`RUN-20261115-social-media-education-handoff-001`。
- 数据采集：2026-11-12 至 2026-11-14；交付整理：2026-11-15。
- 访问范围：内部研究资料，仅限有权限的同事在私有仓库使用；外部发布前需另行审核第三方内容授权及隐私边界。
- 这是**静态数据快照，不是实时看板，也不是完整离线媒体包**。

## 1. 同事如何打开

### 直接打开

下载本目录的 `index.html`，用 Chrome、Edge 或 Safari 打开。报告的文字、数据、图表、筛选、排序和导出不需要后端。视频、在线正文图片、外部来源链接需要联网；有些来源页面需要同事自己的平台登录权限。

仓库的 HTML 文件预览通常显示代码，并不等于运行报告。需要下载 HTML、本地起服务，或部署到静态托管后查看。

### 本地起服务（推荐）

在增长仓库根目录执行以下命令；需有 Python 3。只监听本机，不对局域网开放。

```bash
python3 -m http.server 8766 --bind 127.0.0.1 --directory social-media-for-education
```

打开 `http://127.0.0.1:8766/`。按 `Ctrl+C` 停止服务。不需要 npm 安装、构建或数据库，也不需要下载几 GB 的素材包。

## 2. HTML 是怎样制作的

这份报告是逐次整理和扩展的**单文件静态网页**，不是 React/Vue 项目：

1. 从已授权访问的灰豚页面收集当前列表、图表和筛选结果，保存 JSON 及相关证据；具体阶段见下一节。
2. 整理类目、达人、笔记及指标定义，保留来源文件、采集时间、原始分子分母和异常口径。
3. 使用原生 HTML/CSS/JavaScript 编排报告，将数据写入七个 `type="application/json"` 的 `<script>` 数据块。
4. 页面打开时，JavaScript 用 `JSON.parse()` 读取内嵌数据，生成表格、SVG 图表、排序筛选和 CSV/JSON 下载。
5. 标题、结论、部分候选卡片、账号参考表和 Top20 展示表是静态 HTML；它们不会因修改 JSON 自动全部更新。
6. 笔记素材按需渲染：部分封面内嵌 WebP，视频与正文多图加载小红书公开 CDN 地址。

没有外部 JavaScript、图表库、字体 CDN 或数据请求后端。刷新浏览器只会重新读取这份快照，不会自动从灰豚取最新数据。

### 本次入库与本地原件的区别

本地最终原件名为 `儿童教育_近30天赛道分析报告.html`，交付副本重命名为 `index.html`；原件未修改。

交付时还做了以下处理：

- 格式化 HTML/CSS/JavaScript/内嵌 JSON，便于维护；图片 base64 字符串仍很长，不建议全文件替换或反复输出。
- 清理小红书链接中的 105 处访问令牌参数；部分原笔记链接可能需要登录或从作者主页寻找。
- 将 16 条仅有签名视频地址的笔记改为公开、无查询参数的完整 MP4；逐条读取全片媒体包确认 H.264 + AAC。未做全片人工内容审核或逐帧解码，CDN 的未来可用性不能保证。
- 将达人数据中的本机绝对目录改为相对路径。没有上传本地 MP4、图片素材目录、完整采集响应或历史会话。

不要把带访问令牌、Cookie、API key 或签名下载参数的原始响应直接提交。更新媒体时应从获准的公开来源核实完整音视频地址，而不是猜测删除签名后仍可用。

## 3. 数据从哪里来、原始数据放在哪里

### 3.1 路径的含义

原始采集资料保存在原维护者的本地 `shemeizhanghao/` 工作目录；下表路径均相对该目录，**不是增长仓库内的现成文件**。

本次只交付 `index.html` 和说明，不上传完整采集资料。报告已内嵌实际运行所需数据，同事可以直接查看、导出及维护这份快照。若需要从原始响应重新计算、审计采集过程或重新取数，应向原维护者申请对应资料，脱敏后再共享；不要假设同事机器也存在同名目录。

| 内容 | 原始路径／证据文件 | 平台入口、采集日期及窗口 |
|---|---|---|
| 儿童教育 1.0 总盘与七一级类目 | `儿童教育_总盘_图表证据.json`、`儿童教育_细分类目_精确数据.json`、`儿童教育_报告数据.json`、七类独立页面 JSON | 行业流量大盘→文教服务→儿童教育；11-12 采集；10-13—11-11 |
| 四组子类与独立页证据 | `家庭教育_精确原始数据.json`、`语言培训_原始数据.json`、`常识兴趣_原始数据.json`、`留学_原始数据.json`；另有免费公开课、智能教育学习卡、知识会员的独立 JSON | 有子类的读取列表/图表，无子类的保留平台“没有子类”事实；家庭教育优先精确版本 |
| 儿童教育 2.0 全层级 | `儿童教育_品类搜索新_全量列表.json`、`儿童教育_完整品类取数_20261112/`、`儿童教育_全层级指标汇总_20261112.json`及同名 CSV、`儿童教育_各指标独立降序排名_20261112.csv` | 品类搜索（新）及详情；11-12；63 类目、54 末级目录；观察轴含11-12当日，完整日截至11-11 |
| 教育学习达人与低粉档 | `教育学习_达人大盘取数_20261112/`，其中`低粉计算数据.json`是内嵌达人数据的整理源；原始42档及`细标签补取_20261112/`提供证据 | 行业达人大盘→教育学习；11-12；6 父类、80 细标签、560 标签粉丝档；10-13—11-11 |
| 儿童教育方向笔记 | `儿童教育_候选优质笔记_20261113.json`；历史本地素材在`儿童教育_候选素材/` | 品类搜索（新）→笔记分析→笔记列表，并有同类关键词补充；11-13；10方向100条记录、99唯一笔记 |
| 教育学习11方向笔记 | `教育学习_11方向优质内容_20261113.json` | 灰豚笔记搜索，父类＋主题关键词；11-13；110条记录、107唯一笔记；10-13—11-11 |
| K12近7天低粉热门榜 | `低粉爆文_K12_原始榜单_20261114.json`、`低粉爆文_K12_筛选记录_20261114.json`、`低粉爆文_K12_笔记详情_20261114.json` | 实时→热门笔记榜，K12、粉丝≤1万、类型不限、近7天；11-14；100条初筛，保留78条、剔除22条；不是30天样本 |
| K12媒体回溯 | `低粉爆文_K12_原笔记视频流_20261114.json`、`低粉爆文_K12_原笔记多图_20261114.json`、`低粉爆文_K12_素材清单_20261114.json`；历史素材目录`低粉爆文_K12_素材_20261114/` | 原笔记公开页面的媒体数据与素材核验；当前HTML不依赖这些本地目录；原始文件可能含访问参数，不宜原样入库 |
| 指标定义和制作约束 | `统计口径_最终定义.json`、`报告制作要求.txt` | 正常页面悬浮核验定义；早期悬浮证据存在异步残留，优先最终定义 |
| 分区/领域两份Top20 | `教育起号_蓝海x达人_综合Top20.xlsx`的两张原表，已内嵌至`content-rankings-data` | 11-14导入；按原表排名和格式展示，HTML不重新计算其上游蓝海指数；源工作簿不在本次交付内，当前本地采集目录也未找到 |

### 3.2 如何取数、哪些信息没有留存

可核实的前端页面入口：

- 行业流量大盘：`https://xhs.huitun.com/#/compositeIndex/datatraffic_compositeIndex`
- 品类搜索（新）：`https://xhs.huitun.com/#/category/cate_search_v2`
- 品类详情：`https://xhs.huitun.com/#/category/cate_detail_v2`
- 行业达人大盘：`https://xhs.huitun.com/#/compositeIndex/anchor_compositeIndex`
- 笔记搜索：`https://xhs.huitun.com/#/note/note_list`

初始类目采集是在用户已登录的页面中正常切换筛选、等待数据刷新，然后读取当前 React/ECharts 列表及图表绑定数据。页面导出按钮禁用，没有强行触发导出。达人细标签补取资料保留逐档请求参数、时间和结果证据，但现有资料不足以把所有后续采集归为同一种实现。

这些 URL 是前端路由，**不是后端 API 端点**。本交付没有完整采集器、可复用认证流程或可靠的 API 地址/方法记录；不要把报告中的检索链接当作接口调用说明。重新取数应使用自己的获准账号和正式权限，保存新的窗口、筛选、来源及时间，不绕过配额或导出限制。

原笔记公开页面还可能包含 `__INITIAL_STATE__`，其中 `note.noteDetailMap` 的 `note.video.media.stream` 提供媒体地址；结构与有效期可能变化，不是长期稳定的正式采集API。

## 4. 修改报告时从哪里入手

在编辑器中搜索数据块 ID 或函数名定位，**不要依赖旧行号**。本次格式化后与本地原件行号不同。

### 4.1 七份内嵌数据

| 数据块 ID | 主要结构／字段 | 修改后要联动核对 |
|---|---|---|
| `report-data` | `overall`、`categories`及`children`、`metricContract`、`checks`、`definitions`、`evidence`；计数字段`noteCount/read/stat/hot` | 1.0排行、原始证据、账号方向推荐、父子合计与硬编码校验 |
| `leaf-report-data` | `meta/rows/hierarchy`；行字段`id/name/path/leaf/notes/reads/interactions/hot/daily/flags` | 2.0排名、末级筛选、完整日与当日边界、54行导出；不要与1.0混用分母 |
| `education-creator-data` | `summary/bands/subtags/audit/limitations`；细标签`totalAnchor/lowAnchor/note/hot/lowNote/lowHot/lowStat/bandEvidence` | 达人竞争表、80标签筛选、11候选复算、数量断言 |
| `candidate-notes-data` | `categories[].notes[]`；`coverData`、`videoSourceUrls`（回退`videoSourceUrl`）、`link` | 儿童教育方向卡片展开素材；原始候选文件不能整块替换在线处理后的媒体字段 |
| `education-notes-data` | `categories[].notes[]`；`coverData/videoUrl/searchUrl/originalLinkStatus` | 教育学习11候选展开内容；`searchUrl`为灰豚检索，不是原笔记地址 |
| `lowfan-notes-data` | `meta/rules/rows/decisions`；媒体`coverUrl/videoUrl/videoUrls/images`，来源`noteLink` | 78笔记筛选、分页、多图翻页；100条筛选记录中剔除的22条仍要保留 |
| `content-rankings-data` | 根级`source/sourceSha256/importedAt/method/sheets/methodNotes`；各表`headers/rows/displayRows` | Top20展示表是静态HTML，修改本数据后还需同步表格，否则页面与CSV可能不一致 |

三类笔记常用字段：`id/title/author/fans/tier/type/postedAt/likes/collections/comments/shares/interactions/estimatedRead/description`。不要随意统一不同数据块的字段名：1.0笔记数是`noteCount`，2.0是`notes`，达人是`note/lowNote`。

### 4.2 文案、布局、交互和媒体

- **标题／结论／备注／参考账号**：在静态HTML里搜索对应中文文案；例如搜索“作文备考”及“受众更偏学生本身”。账号主页和笔记地址是两种链接，不要混淆。
- **布局与响应式**：修改`<style>`及其中的`@media`；数据表的容器ID和绑定属性尽量不变。
- **图表与类目排行**：`table()`、`barChart()`、`distributionChart()`、`ranking()`、`subcategoryRanking()`。
- **2.0**：`leafFacts()`、`leafCSV()`。
- **方向素材**：`candidateMediaHtml()`、`candidateTextHtml()`、`renderCandidateNotes()`。
- **达人筛选**：`makeEducationTable()`、`filteredTags()`、`drawTags()`、`educationCSV()`。
- **Top20导出**：`contentRankingCSV()`、`allContentRankingCSV()`；它们不重算上游评分。
- **低粉素材**：对应闭包内的`mediaHtml()`、`card()`、`render()`、`filter()`、`stepImage()`。`card/render`在不同闭包中重名，须连同所属区块定位。
- **导航**：`showReportView()`、`routeReport()`；隐藏旧面板时暂停视频。
- **统一媒体**：`window.reportMedia`的`url/image/sources/attributes`；支持公开HTTPS MP4、备用源、失败回封面、播放互斥及页面隐藏暂停。

视频使用`controls preload="none" playsinline`，不自动播放。CDN可能删除、过期、403或受网络/浏览器限制；部分视频记录本来就没有可播放地址，不能把“类型=视频”解释成一定能播放。地址失效时先核查来源与音视频轨道，不能仅凭扩展名判断完整性。

当前CSP禁止联网取数据（`connect-src 'none'`），图片/媒体仅允许指定小红书CDN；JavaScript还有HTTPS、域名和MP4白名单。改媒体域名需同时核查CSP和`reportMedia.url()`，不能简单关闭安全策略。不要新增登录信息或私有下载签名。

### 4.3 六个视图和导出范围

| 区域 | 浏览器hash入口 | 顶部CSV导出 |
|---|---|---|
| 账号候选 | `#account-candidates` | 48行1.0指标，不是账号参考表 |
| 竞争指标1.0 | `#metrics-overview` | 7父类＋41子类，共48行 |
| 竞争指标2.0 | `#metrics-v2-overview` | 54末级目录 |
| 达人竞争 | `#creator-competition` | 80细标签；区域内另有完整达人JSON及11候选CSV按钮 |
| 分区/领域Top20 | `#content-dimension` | 两榜CSV；也可分别下载 |
| 低粉热门笔记 | `#lowfan-notes` | 78条保留笔记；区域内另有100条筛选记录 |

顶部`download-json`和`download-csv`按当前区域绑定导出。方向卡片内的“下载本方向笔记 CSV”用于复核该方向列表。

### 4.4 同事没有源JSON时如何查看／导出

可以直接使用页面下载按钮。若要提取某个完整内嵌数据块，打开报告后在开发者工具Console执行以下代码；只是读取本地DOM，不调用采集接口：

```javascript
const islandIds = [
  "report-data",
  "leaf-report-data",
  "education-creator-data",
  "candidate-notes-data",
  "education-notes-data",
  "lowfan-notes-data",
  "content-rankings-data"
];
const embeddedReports = Object.fromEntries(
  islandIds.map(id => [id, JSON.parse(document.getElementById(id).textContent)])
);
```

在Chrome/Edge Console中复制单份数据：

```javascript
copy(JSON.stringify(embeddedReports["report-data"], null, 2));
```

这些是**报告快照的整理数据，不是全部原始响应**。笔记数据带内嵌图片，体积较大。更新后将合法JSON替换进相应数据块；字符串中出现`</script>`会提前结束HTML数据块，嵌入前应将`<`编码为`\u003c`。保留原字段、编码和可追溯来源，不用全文件搜索替换修改数值。

## 5. 旧Python脚本能否一键重建

**不能从零完整重建当前最终报告，不建议同事直接运行覆盖交付文件。**

原维护者本地脚本`儿童教育_全层级报告生成.py`是历史局部刷新工具，未随本次交付上传：

- `build()`读取63类目输入及详情目录，生成`儿童教育_全层级指标汇总_20261112.json`、同名CSV、`儿童教育_各指标独立降序排名_20261112.csv`，并读取现有HTML后替换数据块；也依赖已有模板。
- `build_human_candidates()`使用脚本内硬编码账号替换静态参考表，不重新采集账号。
- `build_lowfan()`依赖本地素材清单和媒体文件，写入本地素材路径及旧版渲染代码，**可能把在线视频版回退成本地素材版**。
- 默认入口执行以上三部分；即便使用`--human-only`或`--lowfan-only`也只覆盖相应局部，不等于构建完整报告。
- 脚本不输出增长仓库的`index.html`，不重建1.0全部转换、达人整区、两榜原表和最终在线媒体清理流程。

当前可靠维护方式是以本次`index.html`为基线，小范围更新对应数据块、文案及必要的校验。若以后需要周期性自动重建，应另立任务补齐采集权限、原始数据归档、转换器、模板及回归检查，不把历史脚本当成已有完整流水线。

## 6. 更新数据时必须保留的统计口径

- 爆文：**点赞大于1000**；互动量：**点赞＋收藏＋评论，不含分享**。
- 阅读量是灰豚按互动、达人等级和行业等条件估算，不是真实曝光。页面显示“预估阅读”时仍须按估算解释。
- 篇均阅读=`read/noteCount`、篇均互动=`stat/noteCount`、爆文率=`hot/noteCount`；分母为0时不可计算，不补成0。
- 1.0、2.0、达人标签是不同分类体系，不混算分母；2.0观察日轴含11-12当日，共31个日历日期，完整日截止11-11。
- 总盘44139篇与一级合计44336篇不同；父子差异、缺失日、知识会员350%投流占比等异常须保留，不强行统一或断言必然是重复标签。
- 低粉板块来自近7天**热门笔记榜**，保留78条中仅1条满足上述严格爆文定义；栏目名不能作为所有样本都是爆文的依据。
- 低粉不等于新号，精选榜单不等于全量随机样本；不能据此推算冷启动成功率或真实中位数。
- Top20是源工作簿导入结果，不是页面实时计算的官方评分；更新排行时须说明上游方法。
- 日期字段区分统计窗口、笔记发布时间、采集时间、导入时间、生成时间和媒体核验时间；ISO时间中的`Z`表示UTC。

## 7. 修改后的核对清单

1. 七份JSON都能解析；记录新数据来源、窗口和采集时间，缺失值不虚构。
2. 更新统计期时同时核查标题、页头、各区说明和meta字段；必要时更新数量断言，不为通过检查而掩盖口径差异。
3. 六区导航、排序、筛选、展开、分页、图文翻页及CSV/JSON导出正常；静态表与导出数据一致。
4. 抽查修改过的视频是否有完整音视频；切换区块、隐藏页面及播放另一视频时旧视频会暂停。
5. 断网时仍能读文字与数据；在线媒体失败有封面/提示，不保证断网播放。
6. 检查新增链接是否含访问令牌、签名、个人本机路径；检查第三方内容及未成年人隐私边界。
7. 通过功能分支发起PR，说明变化、来源及核验范围；不要直接覆盖他人的主分支工作。

代码入库不等于部署。这次未配置静态托管、未自动合并PR，也未授权公开分发第三方素材。
