---
name: atlasnova-product
description: >
  AtlasNova 产品知识库 — 帮助团队成员快速了解产品全貌、历史 context、功能模块、设计决策、技术方向和 OKR。
  当用户问到 AtlasNova 的产品功能、设计背景、模块说明、路线图、团队角色、客户类型、集成方案、OKR、CRM 方向等任何产品相关问题时，必须使用本 skill。
  也适用于：帮助 AI 改进产品功能时提供 context、新团队成员上手、技术评审前了解产品边界、写 PRD 前了解现有能力范围。
  Use this skill whenever anyone on the AtlasNova team needs to understand the product's current state, history, or direction — even if they don't explicitly ask for "product context."
---

# AtlasNova 产品知识库

AtlasNova 是一个面向**餐厅连锁/加盟品牌**的 AI 营销平台（SaaS），帮助品牌 HQ 和加盟商管理社交媒体、广告投放、内容创作和运营数据。

---

## 1. 产品定位与目标用户

### 核心价值主张
"一个平台，替代 10 个工具" — 让餐厅品牌的营销和运营负责人不需要懂技术，也能用 AI 驱动社媒内容、广告、和数据洞察。

### 目标用户（三层结构）
| 角色 | 英文名 | 权限 | 使用场景 |
|------|--------|------|---------|
| 品牌 HQ / 加盟主 | Brand Owner | 全局控制 | 设置品牌 guardrail、查看所有门店数据、管理内容模板 |
| 加盟商 / 门店 | Franchisee / Store | 门店级别 | 创建本店 campaign、查看本店销售数据 |
| 营销代理机构 | Agency Owner (CRM) | 多客户管理 | 管理多个餐厅品牌客户的营销交付（CRM 模块） |

### 两个产品入口
1. **app.atlasnova.ai** — 独立 SaaS 平台，功能最完整
2. **pos.chowbus.com/ai-marketing-concierge/** — 嵌入 Chowbus POS，仅提供 3 个模块（Ads Optimization、AI Social Media、AI Creatives Assets）

---

## 2. 产品模块全图

### 🎯 Marketing（CMO 功能）

#### 2.1 Social Media（核心模块）
- **Dashboard**：Total Followers、Reach、Total Interactions、Profile Visits（多平台汇总：Instagram + Facebook）
- **Suggested Campaigns**：AI 根据品牌数据自动生成的 campaign 建议（加载时实时 generating）
- **Active Campaigns**：正在运行的 campaign 列表
- **Schedule Calendar**：月视图，支持按 Platform / Content Type / Status / All Accounts 筛选
- **Create Campaign 流程**：用户选择平台、时间、内容类型
- **Boost Ads**：直接 boost 已发布的帖子
- **Analytics Tab**：社媒数据深度分析
- **Market Insights Tab**：竞品/市场洞察

> **设计决策**：Franchisee 可以继承 Brand Owner 创建的 campaign 模板，减少重复工作。（Done）
> **待做**：More Feedback / log UI；Analytics Aggregation Report for all campaigns

#### 2.2 AI Content Studio（图像 + 视频）
**图像生成 5 种模式：**
| 模式 | 说明 |
|------|------|
| Open Image Editor | 全画布编辑器 |
| Create with Reference | 上传参考图，AI 生成新视觉 |
| Create Poster Variations | Remix 现有海报（新产品、新文案） |
| Smart Poster Text | 将任意图片变为带自定义文字的设计海报 |
| Create Template Poster | 组合背景、产品、设计元素生成定制海报 |

**视频生成（开发中，Video_Generation_Plan）：**
- User Input：大量分类的图片和 audio
- 模式切换：直接 mode / 后期 mode
- 功能：溶解 Remix、PPT 转视频、Video gen（AI-driven）、Template 视频（不同风格/样式）、Reference video remake
- Audio：BGM、Voice Over、Background
- CTA Cut

**质量标准（Unit Test）：**
- 原始数据集：从 Yelp 抓取的 50+ 图片（真实多样性）
- 当前 Prompt 版本：Kinds × Style（e.g., Poster × Outdoor）
- Ground Truth = SOTA = Golden：视觉质量评分 1~100（Wanlun 人工评分 25，GPT 评分 60 为目标）
- 测试站：https://super-disco-jz965yz.pages.github.io/

#### 2.3 Media Library
- 分类：Products / Brand / Store / Menu / Poster / People / Moments / Other
- 功能：Upload（图片 ≤128MB，视频 ≤300MB）、Search by name/tag/product
- AI 生成的素材会标注 "AI" 标签
- Shared with me 视图

#### 2.4 Paid Ads（Google Ads + Instagram Boosting）
- **Google Ads**：Search、Display、Performance Max campaign 管理
- **Instagram Post Boosting**：已开发，等待 Meta app 审核
- **Chowbus 版本额外支持**：Yelp、Nextdoor 广告
- 功能定位：AI 建议 campaign，用户一键启动

---

### 📊 Operations（COO 功能）

#### 2.5 Store Dashboard
**Sales Tab：**
- Key Metrics：Net Sales、Average Order Value（对比上一周期）
- Analytics：
  - Sales Analysis（Daily Trend / Hourly Average）
  - Top Products（By Sales / By Quantity，Top 10 / Bottom 10）
  - Product Loyalty / Repurchase Rate
  - Popular Combinations

**Reviews Tab（Customer Reviews）：**
- 自动匹配 Google + Yelp 门店 listing（搜索 "Searching listings..."）
- 支持按时间段筛选（Last 7 days / Last 14 days）

> **技术细节**：Review API verification，从 Google scrape 图片。当前限制：每个地点平均缺少 1-5 条 Yelp reviews（scraper 限制）。进行中：review notifications。

#### 2.6 Brand Dashboard（企业级）
- 需要 Brand Owner 权限
- 功能：跨门店数据汇总（测试账号无权限访问）

#### 2.7 未来 COO 功能（V3 规划中）
- **Labor Manager**：
  - 对接 Square 劳工数据（进行中）
  - 对接 Toast 劳工数据（等待 Anton verify）
  - 日劳工图表（Oliver intern 开发中）
- **Data Robustness**：Tongsui
- **Review Manager（完整版）**：Review AI Agent → 减少人工干预

---

### 🔧 Data & Media

#### 2.8 Integrations
数据接入方案（已支持或规划中）：

| 平台 | 状态 | 接入方式 |
|------|------|---------|
| **Chowbus** | ✅ 已集成 | 原生合作，嵌入 POS |
| **Toast** | 🔄 进行中 | Custom API Key 或 Standard API Access（店主生成） |
| **Square** | 🔄 进行中 | 验证 Square labor data |
| **Shift4 / SkyTab** | 📋 规划中 | OAuth ISV 合作；需申请 Shift4 Marketplace 入驻 |
| **Clover** | ⏳ 等待 | 等待 Clover 团队 verify（developer-relations@devrel.clover.com） |
| **Eats365** | 🆕 新增 | 通过 RBAC 系统集成，支持 Store Management（Usaib，May 21） |
| **Google** | ✅ | Google Ads API，Review scraping |
| **Yelp** | ✅ | Review scraping（有限制） |
| **Meta (Instagram/Facebook)** | ⏳ | App 审核中（Post Boosting） |

**Shift4 数据架构：**
- 数据来源：Payments/payouts（Shift4 public API）；Orders/Customers/Loyalty（Lighthouse/Transaction Manager exports）
- 自动化：One-time Custom Export → stable Export ID → 每日定时拉取

#### 2.9 Brand Kit
- 品牌视觉资产管理

#### 2.10 Organization > Brands
- 多品牌管理（Brand Owner 视角）

---

## 3. 账号系统 & 权限（RBAC）— 详细版

> 来源：Account System Org（Jing Hu + Wanlun Ding，May 26）；Deliverables & Testing（May 29）；RBAC and Multi Account Testing（Usaib Khan）

### 六级角色体系（来自 Usaib RBAC doc，May 21）

| 角色 | 说明 | 示例 |
|------|------|------|
| **Owner** | 组织 Owner，最高权限 | Jeffery（品牌创始人） |
| **Admin** | 组织 Admin，按功能权限分配（marketing / designer） | Marketing team、HQ designer |
| **Manager** | 中间层（有限权限，介于 Admin 和 Member 之间） | 区域经理 |
| **Member** | 加盟商/门店，只操作自己的数据 | New York Franchise（多门店 group account） |
| **Agency (Chowbus)** | Chowbus 代理角色，通过 Chowbus 入口访问 | Chowbus agency user |
| **Workspace** | = Owner 权限，跨 org 的聚合视图 | 一个用户同时管理多个品牌 |

**Agency vs Workspace 的区别：**
- **Workspace tool**：一个用户同时查看多个 org 品牌；acts like a shell/group pointing to multiple existing org accounts；最高 access role（owner）
- **Agency tool**：模拟 Chowbus agency access；一次只能 navigate 到一个 org；Agency account 是 org 里的一个特定角色 member

**关键规则：Owner 和 Admin 互相共享数据，但 feature 权限有所不同。**

### 完整权限矩阵（RBAC，Usaib Khan）

| 功能 | Owner | Admin | Manager | Member | Agency (Chowbus) |
|------|-------|-------|---------|--------|-----------------|
| Social accounts（org） | connect + assign | connect + assign | connect | connect | connect |
| Campaign share | Can share | Can share | Create local copy | Create local copy | — |
| Campaign approval | Can approve | Can approve | Can request | Can request | |
| Brand kit（org） | Can edit | Can edit | Can view | Can view | Can edit |
| AI Content Studio（user） | Can use | Can use | Can use | Can use | Can use |
| GBP account（org） | connect + assign | connect + assign | connect | view/use | connect |
| Review（org） | Aggregated data | Aggregated data | Aggregated data | Store data only | Store data only |
| Competitors（user） | **Per-user list（不跟 org 走）** | Per-user | Per-user | Per-user | |
| Media library（user） | All can share assets | | | | |

**已知设计张力**：
- Competitors list 是 per-user（不是 org 共享）→ 见 Open Tasks #36
- Member 生成的 campaign 只有 member 自己看到（与 media lib 不一致）

### Integrations 权限规则
- **Top-down**：Owner + Admin 共享账号链接；Manager 和 Member 看不到
- **Bottom-up**：Admin & Owner 可以看到 Member 的 connected account；Manager 看不到
- **Primary 账号**：跟 Org 走（不跟 user 走）；Admin 修改 primary → Owner 那边自动同步
- **已知 Bug**：Member account connection 有 bug，connect 成功但 UI 上没显示

### Campaign 权限规则
- Primary account 跟 Org 走（primary-user 暂不支持）
- **Admin = Owner**（campaign 权限层面等同）
- Member 生成的 campaign：只有 member 自己能看到（⚠️ 与 media lib 和 integrations 行为不一致）
- **Campaign Sharing**：Admin & Owner 可以 share；Manager 和 Member 只能被 share，不能主动 share

### Media Library 权限规则
- **Owner = Admin**：实时自动共享；看到的是所有 member assets 的聚合
- **Member**：上传的 media → Owner 和 Admin 自动看到；自己看到的 = shared assets + 自己的 local assets
- Member 需要 share assets 给其他 member（不自动共享）

### Asset Approval 流程（⭐ 重要）
**Owner/Admin 端：**
- 可以主动 approve member Media Library 里的 assets
- 可以对 approval request 留 comment + 参考图
  
**Member 端：**
- 可以从 Media Library 发送 approval request
- **AI-generated images 必须经过 approval 才能使用**
- 有未 approve 的 assets → campaign 无法 launch
- 未 approve 的 assets 无法下载

### Campaign Sharing 流程
1. Owner 创建 campaign → 分享给 Member
2. Member 收到后：**复制 → 编辑 → 自己 launch**（不能直接改 Owner 的）

### Content Guardrail（内容安全）
- 禁止词系统（e.g., "trump" forbidden）
- 加盟商违规时触发 alert 系统
- 适用于：图像/视频/文案 prompt 过滤

### Export / 图片输出格式（Wanlun，May 29）
| 格式 | 尺寸 |
|------|------|
| Letter | 2550 × 3300 px（8.5:11 比例） |
| Kiosk | 1080 × 1408 px |
| 24×36 Poster | 3600 × 5400 px |
| Facebook Cover | 1640 × 624 px（21:9） |
| Custom | 用户输入 width & height |

**Crop & Save 功能**：在 Image Editor 里新增，让用户在生成后把图片裁剪为指定输出尺寸（Closest Generation Ratio Logic 自动匹配最接近的模型支持比例）。

---

## 3.5 当前 Open Tasks / 已知问题（2026-05-20，69条，Wanlun Base）

> 测试环境：CoCo Testing（测试餐厅账号）和 Chowbus Agency（Chowbus 嵌入环境）

### P0 Bug（严重，需立即修复）
| # | 问题 | 功能模块 |
|---|------|---------|
| 19 | chowbus insufficient permissions to change time on social media dashboard | Infrastructure |
| 20 | member account connection not showing up even though connection is made | Integrations |
| 21 | Allow UI selection of social account(s) + show throughout campaign flow | Campaign Creation |
| 22 | Store dashboard: support user-specific store lists（hard code 先 hide 一些） | Analytics |
| 23 | Google-link button missing for some merchants on Reviews dashboard | Reviews |
| 24 | GBP and social disconnect button needs confirmation modal | Reviews |
| 25 | Calendar leaks all merchants' posts to a single agency user（偶现） | Campaign Management |
| 26 | chowbus domain: Calendar sometimes leaks all merchants' posts to a single... | Campaign Management |
| 27 | Reviews Ingestion V2 — testing on prod（Outscraper + smart business matching） | Reviews |
| 28 | Instagram media readiness false failure on FB campaign + swallowed error | Campaign Creation |

### P1 Bug（重要）
| # | 问题 | 功能模块 |
|---|------|---------|
| 29 | All Reviews: data range 30d missing data + wrong time window | Competitors |
| 30 | Hide custom cover-image picker for carousels containing video (Meta API 不支持) | Campaign Creation |
| 31 | Internal alert when posting fails | Infrastructure |
| 32 | Show in-app notification for failed posts + failed campaign share report | Campaign Management |
| 33 | Post date adjustment resets caption edits on update page | Campaign Management |
| 34 | Can't add social URL after adding competitor | Competitors |
| 35 | Social follower trend line chart is still fake/hard-coded | Competitors |
| 36 | Make competitors list per-user（replacing org-wide shared list） | Competitors |
| 37 | Caption generation：支持 French、Traditional Chinese、Simplified Chinese；hide Indonesian | Campaign Creation |
| 38 | Raise single-video upload limit from 300MB to 1GB（Meta Graph API 支持） | Campaign Creation |
| 39 | Data isolation bug：member 删除 store 也会从 admin 那里删除 | Competitors |
| 40 | Reel post type: video frame 应该是 9:16 on output/update page | Campaign Creation |
| 41 | [Gen] 1st Video Template | AI Content Studio |
| 42 | [Remix] Video upload | AI Content Studio |

**功能分类 tag**：Reviews、Campaign Creation、Campaign Management、Competitors、Infrastructure、Integrations、Analytics、AI Content Studio

---

## 4. CRM 模块（新方向）

> 来源：CRM MVP PRD、CRM App-MVP PRD（Yanice，Jun 2）；PRD — CRM engineering spec v1（今天）；Insight Brew Buddy CRM PRD v1.0

面向**营销代理机构**的客户管理工作台（Agency workspace），帮助代理机构管理多个餐厅品牌客户。

**原型代码库**：branch `CRM0523` on `CD3-github/insight-brew-buddy`，commit `97d9d2b`（prototype 用 localStorage，production 需要接真实 database + auth）

### 核心概念
- Atlas 替代 spreadsheets + Notion + chat threads
- 两个界面：
  - **CRM**（内部，agency-facing）：Dashboard + Client Pipeline + Work Hub
  - **Client Portal**（品牌客户面向，per-client read-only）：目前只有 Profile

### 用户（v1）
| 用户 | 角色 | 主要页面 |
|------|------|---------|
| Boba Tea（Agency Owner） | 拥有所有客户，运营 sales + 交付 | CRM Dashboard → Work Hub → Client detail → Profile |
| Scoped Client（模拟） | 品牌运营商，read-only | Client Portal → Profile |

### V1 In-Scope 页面（已有 prototype）
| 页面 | 路由 | 文件 | 说明 |
|------|------|------|------|
| CRM Dashboard | /crm/dashboard | CRMDashboard.jsx | 4 个 portfolio metrics + Work Hub kanban |
| CRM Clients（Pipeline） | /crm/clients | CRMClients.jsx | Lifecycle kanban（拖拽改 stage） |
| Client Portal hub | /portal | ClientPortalLanding.tsx | 无 client 时的 empty state |
| Client Profile | /client-profile | ClientProfile.tsx | Read + inline edit + inline Add Client + soft Delete |
| Work Hub（嵌入） | （在 Dashboard 内） | WorkHub.jsx | Task kanban（urgency rules） |

### V1 FAKE / Out of Scope（不做数据接入）
- **Content Studio**（/content-studio）：只有 hardcoded mock data，不建数据模型
- **Account Settings**（/account-settings）：复用主平台 existing UI，不重新设计

### 数据模型（TypeScript）
```
Client: id, name, businessType, cuisine, logoUrl
  contactName, contactEmail, contactPhone, contactChannel（email|whatsapp|wechat|phone|sms|other）
  address, website, googleUrl, yelpUrl
  socialChannels[], igHandle, fbHandle
  urgencyOverride: 'waiting-on-client' | null
  dueDate, ownerId, contextLine, completedAt（auto-archives 7d after）

AgencyProfile: companyName, companyWebsite
  businessType（restaurant|cafe|bubble-tea|dessert|bakery|food-truck|retail-fnb|other）
  logoUrl
```

### 5 个核心 Jobs-to-be-done
1. **J1 — Onboard 新客户**：销售通话后立即录入，不丢失 context → /client/new
2. **J2 — 每日待办一览**：Dashboard 9am 看 Work Hub kanban（Overdue/Due today/Waiting on Client）
3. J3-J5：待后续 PRD 补充

### Success Criteria
- 用户完成 5 个 core jobs 无需离开 Atlas
- 每次 save/create/switch 有 1 秒内的 clear feedback
- Empty states 始终有 next clear action

### 完整导航结构（来自 Insight Brew Buddy PRD v1.0，May 31）
| 模块 | 路由 | 说明 |
|------|------|------|
| Dashboard | / | 业务 metrics + Work Hub |
| Clients（Pipeline） | /clients | Client cards + pipeline views |
| Tasks | /tasks | 跨客户 task list |
| Content Calendar | /calendar | 按客户的内容排期 |
| Workflow Library | /workflows | SOP 模板库 |
| Client Detail | /client/:id | Per-client SOP runner + profile |

**核心设计原则**（Insight Brew Buddy）：
> "Every surface derives from real workflow data — there are no manual health scores. Status badges, attention flags, and task urgency are all computed from dates, progress, and ownership fields the team already fills in."
> （所有界面的健康状态都来自真实工作流数据，不允许手动打分）

### 不做（v1）
real auth、OAuth（IG/FB/Google）、notifications、invoicing、mobile-first、Client Portal 完整功能

---

## 5. 产品版本路线图

### 历史版本（2024，Feature Map by Xing Wen）
| 版本 | 日期 | 目标 |
|------|------|------|
| V0.1 | 2024/07/31 | End-2-End working：logging、payment、uploading、KB、DB、RAG、LLM API、Chatbot、AWS 部署 |
| V0.2 | 2024/08/15-30 | Internal Testing（10+ users）：Expert Committee/Guru Clones、Knowledge Base、SOC2 认证？ |
| V0.3 | 2024/09/15 | Public Testing Beta：自媒体内容创作平台 |
| V0.4 | 2024/10/15 | B2B Testing：国际新闻产品 |
| V0.5 | 2024/11/15 | Globalization |

### 当前方向（OKR 2026 Q1）
| 版本 | 代号 | 核心 |
|------|------|------|
| V2 | 当前 | 功能稳定性：CMO（社媒）+ COO（Review、Labor）+ Data Robustness |
| V3 | 规划中 | **Multi-Agent 自动协作**：Command Center + AI CMO + AI COO + AI CDO + SEO Manager |
| V4/V5 | 未来 | TBD |

### V3 AI Agent 架构（重点方向）
- **Command Center**：统一控制台（有设计图）
- **AI CMO**：社媒、广告、内容自动化
- **AI COO**：Review Manager（全自动）、Labor Manager
- **AI CDO**：数据分析
- **SEO Manager**：
  - 信息层：Google Search Console + Google Analytics 4（Impressions、CTR、Keyword Analysis）
  - 自动化层：Local SEO、Google Ads（Create/Manage）
  - Workflow 层：Local SEO Workflow、Review Response Campaign、Tracking/Local Search Cost

---

## 6. OKR 2026 Q1

### O1：Product Development
**KR1：Endless Competitor Analysis + Brain Storming**
- Direct Competitors：产品分析+Competitor Analysis
- New Version：Competitor Analysis
- Other AI Agent for vertical industries

**KR2：V2 稳定 + V3 Multi-Agent**
- 标准化流程：Ticket（Lark or Github）、Auto Agent（Umetea 监控：Fwd、Expired Token、Warnings、Critical Errors）
- 无 P0 Bug 政策（100% repeat、crashing、stuck、data mis-calculation）
- CMO 功能：Social Media Campaign Manager
  - Front-end implementation by 09/04（Yelp retouch）
  - **Owned channels / Owned media（Private traffic）**：Facebook Group、Instagram Broadcast Channel、Instagram Group Chats、Social Media DM、Chatbot（manychat.com）、SMS/MMS、Email
  - Paid Ads：Google Ads（✅完成），Instagram Post Boosting（✅功能完成，等待 Meta 审核）
  - SEO：规划中

**Feature Qualities 目标**：Efficiency 1000x

### O2：Sales
- 目标：5 个 pilot 客户（Small/Medium Franchise，1-2 个非餐厅）
- 10 qualified meetings，20 warm leads
- **销售渠道**：Gregg（40 contacts）、YK Digital（5000 contacts、$2000）、Targeted email outbound（3600/day）、Direct Outreach（40-50 ideal brands）、Restaurant Rockstars Podcast、Ecosystem Partners（Franchise marketing agencies、Franchise sales/development consultants、PE/franchise investment groups）、FRANdata target list、IG Advertising、IFA Show Vegas

---

## 6b. Brand Kit 模块（正在完善）

> 来源：Brand DNA（Yanice，May 13）

### 当前状态
Brand Kit 目前 layout 比较临时，没有被其他功能模块引用。

### 规划方向
1. **设计整理 Brand Kit layout**，并连接到其他功能（内容生成、campaign 等）
2. **Brand Template** 放在 Brand Kit 下面，收纳用户的：
   - Caption generation 偏好（tone、风格、语言）
   - Review reply 偏好

### Brand Kit 包含字段
- **Brand & Files**：主品牌、合作品牌
- **Color Palette**：品牌颜色
- **Cuisine Tags**：餐厅类型
- **Location**：品牌所在地
- **Brand Tone**：内容风格标签
- **Audience**：目标用户群体
- **Price Range**：$ / $$ / $$$ / $$$$
- **Proof of Age**：酒水相关
- **Customer Groups**：客群分类
- **Language Settings**：多语言偏好
- **Similar Brands**：参考竞品
- **Brand Voice Guide**：品牌声音指南（内容风格）
- **Top Brand-Representative Images**：品牌代表性图片

### 示例（Coco Bubble Tea）
- Mission tagline：*"Embrace Tradition, Unleash Innovation, Savor the World"*
- 颜色：黑、橙、灰
- 菜单数据与定价集成

---

## 6.3 Gen-Image Logo 稳定性优化（AI Content Studio 技术细节）

> 来源：Gen-Image Logo 稳定性优化 — 修改总结（Yanice，Jun 1，项目日期 2026-05-28）

### 背景问题（logo 生成的已知 bug）
| 问题 | 描述 |
|------|------|
| Logo 变形/不可读 | 模型重新"绘制" logo，字形错误 |
| Duplicate logo | 同一画面出现多个相同 logo |
| 派生品牌图形 | 模型根据 logo 颜色生成额外弧线、徽章、丝带等（hallucination） |
| Logo 泄漏到背景 | Logo 品牌色被扩展到包装/场景背景 |
| 已有 branding 冲突 | 产品图本身有 logo，上传后系统仍叠加额外 corner logo |

### 修复方案（已上线）
**Product Studio V2：**
- 新增可选 Logo 上传控件（不替换原有 Product image 入口）
- 6 个生成 prompt（Single/Multi/Human × Color/Lifestyle）全部加入 **LOGO LAYER 规则**：
  - Logo 是最后一个 reference image
  - 无 logo 时不生成/不 invent
  - 有 logo 时只放一个
- Scene Plate 系列 prompt 保持不注入 logo（不让 logo 进入背景阶段）
- Dev mode 新增 Logo QA Tab（read-only），实时检查 prompt 的 logo 规则覆盖情况

**Smart Poster：**
- Step 1 Analysis prompt 加强：只读 logo 做品牌信号，不改写 logo 文字
- Step 2 System prompt 新增完整 **logo contract**：
  - Logo 作为 independent flat overlay / brand mark layer 处理
  - 自动移除 logo 纯色背景，不改变主体
  - **禁止**重写/重绘/变形 logo
  - **禁止** fake / duplicate logo
  - 安全区放置（默认右上角）

---

## 6.5 Competitor Insights 模块（重要产品决策）

> 来源：Competitor Insights PRD（---no use，May 13）

### 核心定位（设计决策）
**Competitor Insights = "决策支持产品"，不是"监控型信息面板"**

用户进入这个页面的核心目的（按优先级）：
1. 复盘近期表现
2. 理解自己与竞品的相对位置
3. 诊断表现变化的原因
4. 找到下一步可调整的方向

用户真正想要的是**信心**（confidence），不是更多数据：
- 没有漏掉关键信号的信心
- 理解自己当前位置的信心
- 知道下一步该怎么做的信心

### 现有问题（用户反馈）
当前按数据来源分类（Social / Reviews / News），不能快速回答用户最重要的问题。

**用户具体需求**：
- Granular metrics：views、likes、comments、shares
- 社媒和 Reviews 的 AI 摘要
- 可调整时间范围（不只是 30 天）
- 每个竞品的通常发帖时间
- 跨竞品的 Dashboard 比较视图
- 高互动评论/信号

### 四模块产品结构（V1）
| 模块 | 说明 |
|------|------|
| **Performance** | 复盘近期表现（Social + Reviews，按 domain 分领域） |
| **Comparison** | 与竞品的比较（跨竞品 Dashboard） |
| **Diagnosis** | 诊断表现变化原因（含外部信号） |
| **Action** | 下一步可调整方向（V1 不做强推荐，原因：数据还不够成熟） |

### V1 数据范围
- **Social**：社媒数据（views、likes、comments、shares 等）
- **Reviews**：Google + Yelp
- **Time range**：可调整
- **Competitor support**：支持自定义竞品列表（per-user，不再是 org-wide 共享）

### 目标用户
- **User Type 1**：Franchise / Single Store Operators（单店/加盟商）
- **User Type 2**：Brand Headquarters（品牌总部）

### 未来连接
Competitor Insights 计划连接到其他 Atlas Nova workflows：dynamic menu adjustments + campaign planning

---

## 7. 团队结构

| 成员 | 角色 |
|------|------|
| **Yanice Yang** | PM / 产品负责人（本 skill 的 owner） |
| **Xing Wen** | Co-founder / 技术 lead（Feature Map、OKR 原版、Video 规划） |
| **Jing Hu** | Engineering lead（Account System、Ticket List、Review Test Cases） |
| **Wanlun Ding** | Design / Product（Deliverables & Testing、图片质量评分） |
| **Usaib Khan** | RBAC / Account System |
| **Jason Li** | Ticket System |
| **Ethan Zhu** | 外部合作（Video Generation） |
| **Oliver** | Intern（Labor Manager 日图表） |
| **Anton** | Toast 数据验证 |

**GitHub Org：** https://github.com/orgs/AtlasNovaAI  
**当前 Ticket Board：** https://github.com/orgs/AtlasNovaAI/projects/10/views/1

---

## 8. 关键文档索引

| 文档 | Owner | 用途 |
|------|-------|------|
| OKR_2026_Q1 Copy | Yanice Yang | 当前季度目标（含完整功能列表） |
| Feature Map | Xing Wen | 产品版本路线图（2024 历史） |
| CRM MVP PRD | Yanice Yang | CRM 模块产品需求文档 |
| CRM App-MVP PRD | Yanice Yang | CRM App 版本 PRD |
| all competitors AI Insights reference | Yanice Yang | 竞品分析汇总 |
| Bug List | Yanice Yang | 当前 Bug 清单 |
| Bug List Competitor Analysis | Yanice Yang | 竞品 Bug 对比分析 |
| Video_Generation_Plan | Xing Wen | 视频生成架构设计（流程图） |
| AtlasNova OKR | Xing Wen | 原始 OKR（2024 版） |
| Brand DNA | Yanice Yang | 品牌视觉/声音指南 |
| Account System Org | Jing Hu | 账号系统架构 |
| Deliverables & Testing | Wanlun Ding | 交付物 & 测试清单 |
| Competitor Insights PRD | ---no use | 竞品洞察产品文档 |

---

## 9. 常见场景 Q&A

**Q：AtlasNova 和 Chowbus 是什么关系？**  
A：Chowbus 是 AtlasNova 的渠道合作伙伴，AtlasNova 的 AI Marketing 功能嵌入在 Chowbus POS 系统里，通过 Chowbus 服务其餐厅客户。Chowbus 版本只有 3 个模块（Ads Optimization、AI Social Media、AI Creatives Assets）。

**Q：Brand Owner 和 Franchisee 有什么区别？**  
A：Brand Owner 是品牌 HQ（加盟主），可以看所有门店数据、设置品牌 guardrail（禁止词、内容规范）；Franchisee 是单个加盟店，只能管理自己门店，但可以继承 Brand Owner 的 campaign 模板。

**Q：V2 和 V3 有什么区别？**  
A：V2 是当前版本，目标是"功能稳定可用，无 P0 bug"，包括 CMO（社媒、广告）和 COO（Reviews、Labor 数据）基础功能。V3 是 Multi-Agent 自动协作架构，有 Command Center 统一调度 AI CMO、AI COO、AI CDO、SEO Manager 等多个 AI agent 自动完成任务。

**Q：CRM 模块是给谁用的，和主产品是什么关系？**  
A：CRM 是面向**营销代理机构**（Agency）的新模块，帮助代理机构在 Atlas 里管理他们服务的多个餐厅品牌客户。主产品是给品牌和加盟商直接用的，CRM 是 B2B2B 模式（Atlas → Agency → 餐厅品牌）。

**Q：我想用 AI 改进 Social Media Campaign 功能，需要知道什么背景？**  
A：核心设计是"AI Suggested Campaigns"（实时生成）+ "Schedule Calendar"（月视图）。加盟商可以继承 Brand Owner 的模板（已完成）。待做的是：campaign 汇总报表（Aggregation Report）、更好的 Feedback/Log UI。平台连接：Instagram + Facebook，Instagram Post Boosting 等待 Meta 审核。

**Q：图片生成的质量是怎么评估的？**  
A：Ground Truth = SOTA = Golden，评分 1~100。Wanlun 人工看 25 张图片后评分，再把 retouched 图片输入 GPT 要求打分（目标 60+）。测试数据集：从 Yelp scrape 的 50+ 真实餐厅图片（多样性：各类食物、地点、光线条件、有无人物）。

---

## 10. 产品哲学与设计原则

1. **Efficiency 1000x** — 所有功能设计目标是让餐厅营销效率提升千倍
2. **Brand Guardrails** — 品牌方可以控制加盟商的内容边界（禁止词、风格规范）
3. **Inherit, Don't Duplicate** — 加盟商继承品牌模板，减少重复工作
4. **No P0 Bugs** — 产品稳定性是 V2 阶段的优先级，100% repeat/crash bug 必须消除
5. **Multi-Agent Collaboration（V3 方向）** — 未来由多个专业 AI agent 协作自动完成营销和运营任务，减少人工干预
