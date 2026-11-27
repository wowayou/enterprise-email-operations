# 出海企业邮箱：从开通到可靠运营

核验日期：2026-11-27｜适用对象：中国大陆出海个人经营者、小团队及企业｜示例域名：example.com（仅示意）

**推荐做法：先保留能达标的现有邮箱；新建时按实际办公网络、团队协作和客户端需求选服务。交付目标是“真实邮件能往返、询盘有留底、人员能交接、账号能恢复”，并为每个结果保留证据。**

本次交付为调研、操作手册与执行模板，未注册客户账号、购买订阅、修改真实 DNS 或发送测试邮件。以下涉及真实账号和收发的验收均为“未执行”。菜单名称可能随产品更新，实施时以文中官方原始链接及客户真实租户为准。

**怎么读：**业务负责人先读第 1–5、10–12 节；开发者与 Agent 重点读第 6–9 节；验收用配套《开工与验收清单》。只需要网站邮箱展示时，直接看第 7 节，不必为一个邮件按钮开通发信 API。

## 1. 企业邮箱的价值，以及什么才算合格

企业邮箱指使用自己掌握的域名作为地址，例如 `sales@example.com`。对小企业最有用的价值，是对外身份统一、业务资料和地址可持续管理，以及员工变化后客户仍能找到正确的人。还未注册公司的个人经营者，也可以按服务商允许的真实身份开通自有域名邮件；域名邮箱本身并不证明某人已注册公司。

| 价值 | 实际例子 | 必须一起交付的能力 |
|---|---|---|
| 对外身份一致 | 网站、报价单、合同沟通使用相同品牌域名 | 域名归客户持有；公开地址真实有人处理 |
| 业务地址持续使用 | 员工离职，`sales@` 继续接待 | 授权交接、历史记录、接任人和撤权流程 |
| 多人协作 | 销售 A 已回复，销售 B 能查到 | 正确的共享/委派权限、已发送副本、分工 |
| 降低冒用和账号失控风险 | 限制未经授权的发信源，保护管理员 | SPF、DKIM、DMARC、MFA和恢复机制 |
| 能定位漏信原因 | 知道是表单没存、通知失败，还是进入垃圾箱 | 询盘底账、日志、退信与异常处理人 |

**域名后缀好看不等于合格；付费也不等于保证进收件箱。**认证、内容、发送行为、服务商信誉与收件方处理都会影响结果。服务商显示“已发送”或“Delivered”，也不能直接证明客户看到了邮件。[D05](#source-d05)[O01](#source-o01)

本方案把“合格”分为两层：

- **可上线：**归属清楚、独立账号与恢复可用、地址与认证正确、约定样本真实往返成功、网站入口可用、失败能被发现。
- **可持续运营：**有人处理询盘和垃圾/隔离邮件，有报告复核、迁移/离职/恢复和续费安排；自动通知能补漏，未实现的自动能力明确采用人工替代。

## 2. 服务商怎么选：先看场景，不按品牌排座次

下表是方案建议，不是对所有国家和收件系统的性能保证。报价不在本任务范围；购买时核对官方计划页、席位、续费与合同，避免用旧截图里的促销价做决策。

| 场景 | 优先评估 | 为什么适合这个场景 | 下单前必须核对 |
|---|---|---|---|
| 已有网易、腾讯、Zoho等，日常收发正常 | 先验收并补配置 | 迁移会增加数据、权限和收信切换工作 | 自有域DKIM、MFA/恢复、日志、客户端、外部实测和接待流程 |
| 大陆少量人员，主要需要域名邮件与手机/Outlook | Zoho Mail 中国区合适的付费方案 | 可把邮箱与大型办公套件分开采购 | 数据中心、实际付费功能、客户端和共享地址能力 [P01](#source-p01) |
| 重视国内采购支持、已使用阿里云 | 阿里邮箱中国站 | 账号、购买和技术支持路线明确 | 最低采购席位、客户端访问策略、需要的协作功能 [P02](#source-p02) |
| 深度使用 Outlook，多人共同处理业务地址 | Exchange Online / Microsoft 365 | 适合评估共享邮箱、权限与交接流程 | 先选世纪互联版或全球版，再查许可与功能 [P03](#source-p03)[P04](#source-p04) |
| 已有国际 M365 团队与租户 | 优先沿用并测试大陆体验 | 可保持原身份和协作体系 | 微软提示全球租户的跨境延迟/丢包风险，须测办公和手机网络 [P05](#source-p05) |
| 海外团队为主，已使用 Google 协作 | Google Workspace，满足条件后选择 | 与现有工作方式衔接 | 真实计费地区、付款与续费、管理员和员工实际网络 [P06](#source-p06) |

**给没有历史系统的小团队的默认选择顺序：**先试 Zoho 中国区付费 Mail 方案；如果共享 Outlook 工作流是刚需，重点比较合适云环境的 Exchange Online；如果国内采购与支持更重要，把阿里邮箱一起验证。已有 Google/M365 体系时，迁移收益需要明显大于迁移成本。

### 必须分清的四组差异

1. **Microsoft 全球版与世纪互联版不同。**两者的租户、部分功能、管理和应用接入存在差异，不能把全球版 OAuth、DNS、插件教程直接套到中国版。只要邮箱可比较独立 Exchange Online；需要套件再选含邮箱的 M365 计划。只有办公应用的计划未必包含邮件服务。[P03](#source-p03)[P04](#source-p04)
2. **Zoho 中国区与国际区不同。**服务器和组织归属按数据中心确定，换登录网址不是迁移。当前中国区文档中的免费方案只支持 Web；需要 IMAP/Outlook 等时，核对所购付费计划。全球 Shared Mailbox 文档不证明中国区所有套餐都有。[P01](#source-p01)[P07](#source-p07)
3. **Google 的地区可用、能付款与网络可用是三件事。**官方地区页不能证明所有大陆主体都能顺利开户、每张卡都能续费，或每个网络都稳定；也不能拿 Google Cloud 的规则替代 Workspace。[P06](#source-p06)
4. **别名不等于共享邮箱。**别名只是附加地址；多人共同处理必须另外解决权限、回复身份和处理记录。M365 共享箱在通常 50 GB 等条件内可免单独许可，但访问它的员工仍需适当的个人邮箱许可，高级功能另算。[P04](#source-p04)

**关于参考 PDF：**它可帮助理解“注册、域名解析、添加用户”的起步过程。文件中的网易免费“50 个账号”未取得本轮当前官方权益证明；应到客户实际账号后台或官方支持确认。不能把付费版能力外推给免费版，也不因本轮官方页面无法读取就判断网易不可用。现有腾讯、网易邮箱通过下文标准即可保留。

## 3. 一个可以照着做的账号与地址方案

示例：两位业务人员 Alice 与 Bob 处理海外客户，域名为 `example.com`。地址仅用于说明结构，实施前替换为客户拥有、验证并同意公开的域名。

| 地址/身份 | 推荐用途与形态 | 由谁操作 | 检查重点 |
|---|---|---|---|
| `alice@example.com`、`bob@example.com` | 每人一个实际工作账号 | 个人账号＋MFA | 不共用密码；离职能单独撤权 |
| `sales@example.com` | 对外询盘地址；多人用共享邮箱/队列 | 主负责人＋替补 | 都能看到已回复内容；有分工 |
| `support@example.com` | 有独立售后流程才建立 | 售后负责人 | 单人且相同流程可先用别名 |
| `notify@notify.example.com` | 网站内部通知发件身份 | 服务端发送服务 | 验证子域；不当作员工可登录收件箱 |
| `dmarc-reports@example.com` | 聚合报告入口或获准分析服务 | 邮箱维护者 | 有人读取分析；容量与访问受控 |
| 专用管理员身份 | 租户管理和紧急恢复 | 客户控制 | 不作为日常销售邮箱；有备份恢复方式 |

一个人起步时，不必为每个角色买一个独立登录账号。可以一个人员邮箱加业务别名，但要验证“发往 sales@ 能收到、以合适的身份回复、以后可迁成共享处理”。不同厂商的别名发件能力及许可不同，不能只看收件成功。[P04](#source-p04)[P07](#source-p07)[P08](#source-p08)

网站自动邮件与人工邮箱分开管理，主要是让权限、发送源和排障更清楚。子域不能保证信誉绝对隔离。初期不自建 SMTP 服务器，也不为了加邮箱按钮安装 MCP；这些不会自动解决销售漏回复的问题。

## 4. 客户开工前准备什么，谁负责什么

| 准备项 | 客户提供或确认 | 实施人员交付 |
|---|---|---|
| 域名与 DNS | 域名归属、注册商、实际 DNS 管理入口 | 权威 DNS 核对、原记录备份、变更表 |
| 主体和地区 | 真实个人/企业资料、员工所在地、目标市场 | 对应产品/云环境，不代编海外身份 |
| 已有邮箱 | 地址、别名、共享箱、旧数据和现有客户端 | 盘点清单；有旧系统就做迁移与回退方案 |
| 人员与接待 | 主负责人、替补、营业时间与回复承诺 | 权限表和处理流程 |
| 所有发信系统 | 网站、CRM、账单、扫描仪、营销平台等 | From/信封域/DKIM/回信地址清单 |
| 费用与续费 | 所需席位、套餐、账单与续费联系人 | 当前功能核验和续费提醒，不代填历史价格 |
| 安全与恢复 | 可长期使用的恢复渠道和保管方式 | MFA、权限、恢复步骤的脱敏确认 |
| 实测配合 | 允许发送的测试邮箱、参与人、附件与时段 | 验收矩阵、样本编号、原始邮件头/日志证据 |

客户自己完成身份验证、手机验证码及付款；可委派实施人员做必要配置。密码、备用恢复码、私钥、API key 通过受控密钥渠道管理，不贴进聊天或公开仓库。交付文件记录“谁控制、放在哪里、怎样恢复”，不记录密钥本身。

**先约定的建议目标：**工作时间 1 个工作日内首次人工响应；每日两次核查未处理询盘和失败任务；通知积压超过约定时限有告警。这些是项目建议，需按人员与时区确认，不是厂商 SLA。没有替补的单人业务，应给客户显示真实营业时间和自动回复边界。

## 5. 从账号注册到正式使用：客户操作路线

下面先走公共步骤，再按选中的一条厂商路线操作。已有邮箱时先做审计，未确认迁移前不要改 MX。

### 5.1 所有厂商共用的八步

1. **选定产品与环境。**写下品牌、国际/中国区、计划、席位和实际登录网址；先测试办公室、家庭/备用网络、手机的访问与恢复入口。
2. **客户创建组织管理员。**用自己掌握的资料注册，保存账单与续费信息，开启 MFA；同时准备备用管理员或安全的应急恢复方式。至少保留一个客户控制、且不依赖本企业邮箱域名正常收信的恢复途径，例如平台支持的外部恢复邮箱、电话或独立应急机制；实际演示恢复入口可访问。
3. **验证自有域名。**在邮箱后台添加域名，复制本租户产生的 TXT/CNAME 验证值，到真正托管 DNS 的平台添加；返回邮箱后台验证。验证归属不等于已切换收信。
4. **先创建人员和业务地址。**分配必要许可，配置别名/共享权限及发件身份；已有旧邮件时先做第 9 节的迁移准备。
5. **按第 6 节准备认证，依厂商流程完成激活与获准的收信切换。**先准备 SPF/DMARC 和当时可生成的 DKIM；需要激活后等待的项目保留待完成状态，完成签名与实测后才通过相关验收。具体 MX、SPF来源与DKIM值来自当前租户；不照抄其他客户截图。
6. **每人设置客户端。**优先服务商正式支持的网页、手机和现代认证客户端；需要 IMAP/SMTP 的设备单独核验协议、端口和凭据。
7. **共同做第 10 节验收。**至少覆盖约定的外部系统与业务地址，确认双方收发、回复身份、附件、垃圾/隔离位置和接待记录。
8. **交接后再结束项目。**客户独立演示查信、回复、查异常、恢复和撤权；登记未完成项及下次复核日期。[P07](#source-p07)[P09](#source-p09)[P10](#source-p10)

### 5.2 路线 A：Zoho Mail 中国区，小团队示例

- 从 [Zoho 中国区企业邮箱](https://www.zoho.com.cn/mail/) 进入企业域名邮箱注册。不要把注册个人 Zoho 邮箱误当企业域名配置。
- 按 [中国区计划说明](https://www.zoho.com.cn/mail/help/adminconsole/subscription.html) 选定付费功能，确认客户端能力；试用期开放的高级功能不代表试用后仍能使用。
- 组织管理员添加域名，完成验证；创建成员与业务地址。开发者按照 [Email Hosting Setup（企业邮箱部署流程）](https://www.zoho.com/mail/help/adminconsole/email-hosting-setup.html) 理解顺序，但记录值必须取中国区实际后台。
- 配置域名后，去账户的 **Server Configuration Details（服务器配置详情）**读取该账号适用的客户端参数；开启 MFA 后按官方要求配置应用专用密码或支持的认证方式。
- 多人处理 sales@ 时，确认本区域本计划的 Shared Mailbox 或其他协作能力，并实际演示 A 回复、B 可见；若只做别名转发，清楚写明谁接单。[P01](#source-p01)[P07](#source-p07)

### 5.3 路线 B：Microsoft 365 / Exchange Online

- 从 [微软中国产品选择页](https://www.microsoft.com/zh-cn/microsoft-365/business-china-offers) 确认国际版还是世纪互联版，以及是否需要整套办公软件。世纪互联版的组织设置入口与全球版不同。[P03](#source-p03)
- 管理员进入所购环境的管理中心，按 **Settings → Domains（设置 → 域名）**的对应向导添加域名并验证。先建用户、分配许可、准备历史数据，再切换 MX。[P09](#source-p09)
- 按 **Teams & groups → Shared mailboxes（团队与组 → 共享邮箱）**或当前等效入口创建 sales@，添加成员；核对读取权限与 **Send As（以该身份发送）**。Full Access 不自动等于 Send As。[P04](#source-p04)
- 让共享箱保持禁止直接登录，员工用各自账号访问。配置共享“已发送”副本，再验另一位员工能看到回复，避免重复处理。[P04](#source-p04)
- 新网站发信优先评估适配云环境的 Graph/API 或独立事务邮件服务。不要为旧插件默认关闭整个租户安全保护。Graph 的 `202 Accepted` 只说明请求已受理。[P11](#source-p11)

**2026 年 SMTP 提醒：**微软最新时间表把现有租户默认关闭 SMTP AUTH 基本认证安排在 2026 年 12 月底，管理员当时仍可按政策启用；12 月后新租户默认不可用基本认证，最终移除日期计划在 2027 年下半年宣布。另外，安全默认值开启时 SMTP AUTH 本身被禁用，所以“只把密码换成 OAuth”不一定解决问题。实施当天重新核验公告与租户策略。[P11](#source-p11)

### 5.4 路线 C：阿里邮箱中国站

- 客户从 [官方购买流程](https://help.aliyun.com/zh/document_detail/36702.html) 进入，确认实际版本、席位、续费与域名。所需域名可在别处注册，不必仅为邮箱迁注册商。
- 根据 [首次开通指南](https://help.aliyun.com/zh/document_detail/36698.html) 设置邮箱管理员、恢复方式、员工和业务地址；阿里云主账号、RAM 与邮箱管理员不是同一套凭据。
- 根据控制台配置 DNS，开启两阶段认证。客户端所需协议按人员最小范围启用，使用相应专用密码。
- 当前新购邮箱默认限制第三方客户端。官方标准配置为 IMAP SSL 993、SMTP SSL 465，并说明 SMTP 587 未开放。遇到客户端失败，先查策略与正确端口，不要套其他厂商的 587 参数或关闭 MFA。[P02](#source-p02)[P12](#source-p12)

### 5.5 路线 D：Google Workspace，已有可用环境时

- 先确认真实计费地区、可用付款/续费方式及网络，再按 [组织设置指南](https://knowledge.workspace.google.com/admin/getting-started/set-up-google-workspace-for-your-organization) 建立组织；管理员开启两步验证。
- 验证域名、建立用户、选择委派邮箱或 Google Groups Collaborative Inbox。群组需要允许预期外部客户来信，别名不能当独立可委派账号。[P08](#source-p08)
- 依当前向导配置 MX 与认证，不把旧“五条 MX”截图视为唯一方法。客户端使用当前支持的 OAuth 或符合账号策略的专用方式；2025 年起普通用户名＋账户密码的旧低安全应用流程不能继续照搬。[P10](#source-p10)
- 完成真实网络、外部往返和共享处理测试后使用；如果上述条件不满足，改用已验证的候选服务。[P06](#source-p06)

## 6. 开发者操作：DNS、认证和变更控制

### 6.1 先盘点，再写记录

**先保存当前 DNS 全量记录和邮件路由，再给每条改动写明“旧值、新值、目的、来源、回退”。**注册商未必是权威 DNS 服务商；只在实际生效的平台修改。保留网站 A/AAAA/CNAME 与无关的 TXT 验证记录。

| 类型 | 通俗作用 | 从哪里拿准确值 | 完成证据 |
|---|---|---|---|
| 所有权 TXT/CNAME | 证明域名由客户控制 | 当前邮箱组织的验证向导 | DNS可查＋租户验证通过 |
| MX | 决定发往此域的邮件先交给谁 | 当前环境收信配置 | 全部收件地址已建；真实外部来信到达 |
| SPF TXT | 授权某个信封域的发信来源 | 已盘点的各服务要求，合并审核 | 同名仅一条策略；含嵌套的查询预算合规 |
| DKIM TXT/CNAME | 为发信签名提供验证依据 | 当前租户生成的选择器和完整值 | DNS可查＋平台启用签名＋真实邮件验签 |
| DMARC TXT | 将可见发件域与认证结果关联，并声明策略/报告 | 客户发信清单与本节方案 | 实际对齐、适当策略、报告可分析 |

MX 数字越小优先级越高。两家服务商的 MX 并挂不会自动按员工分流，也不会每封信各投一份。短期共存应按厂商正式路由设计和实测；不要把一个低优先级旧 MX 当作已经完成的灾备方案。[D01](#source-d01)

### 6.2 SPF：只有一条有效策略，但可有其他 TXT

在同一个 DNS 名称下只发布一条可选中的 `v=spf1` TXT。新增发信商时，先确认它真正使用哪个 **MAIL FROM/Return-Path（信封发件/退信域）**，再合并需要的授权；若服务使用独立子域，则在相应名称维护策略。不要因为网站托管在某云就授权整个云网络。

SPF 求值中会触发 DNS 查询的机制与修饰符有 10 次预算，包含递归 include/redirect；不是只数表面 include，也不是域名只能有十条 DNS 记录。超限要精简、清理停用来源或采用合理子域设计，不能再加一条 SPF。不要使用 `+all`，也不要无人维护地把服务商动态授权压成静态 IP。[D02](#source-d02)

### 6.3 DKIM：发布公钥之后还要启用并实测

Google 通常提供 TXT，Microsoft 通常提供两条 CNAME，但具体选择器和目标值必须从当前租户复制。支持时优先采用 RSA 2048 位。长 DKIM TXT 按 DNS 平台支持的方式保存；需要分段时，应是同一条 TXT 记录内的多个字符串片段，不能拆成同名的多条 TXT 记录，也不能截断公钥。保存后检查完整解析值。[D03](#source-d03)

Google 新组织启用 Gmail 后，官方提示可能需等待 24–72 小时才能生成 DKIM 密钥；不要用教程公钥代填，也不要把等待状态标为已通过。配置后返回邮箱后台完成启用动作，例如 Google 的 **Start authentication（开始认证）**。从员工网页邮箱、网站、CRM 各发一条授权测试消息，检查实际签名的 `d=` 域和收件端验签结果。只发现 DNS 有公钥不能判定已签名。[D03](#source-d03)

### 6.4 DMARC：按真实邮件流选策略

新的部署可先用下面的观察记录；必须先准备真正可接收报告的地址，再将示例域替换为客户域：

```text
记录类型：TXT
主机名：_dmarc
值：v=DMARC1; p=none; rua=mailto:dmarc-reports@example.com
```

一封邮件的 DMARC 通过，需要**对齐的 SPF 或对齐的 DKIM 至少一个通过**；不是看到任何 `spf=pass` 就算数。直接发信的工程目标仍应把两种认证都正确配置，避免只靠一个脆弱环节。[D05](#source-d05)

**2026 更新：**RFC 9989 已替代旧 DMARC 标准；`pct`、`ri`、`rf` 已被列为 historic。新方案不把 `pct=10/25/50` 当作可靠的分批执行保护；旧收件系统可能忽略新的 `t` 参数，不能用 `p=reject; t=y` 冒充普遍安全的观察模式。[D04](#source-d04)

日常员工往来域不把 `p=reject` 设为统一毕业条件。先查转发、群组/邮件列表及第三方发信；受控的网站通知子域可单独评估更严格策略。需要让可能参加邮件列表的日常邮箱域采用 reject 时，新标准给出更长的 none/quarantine 观察建议；这不等于所有新邮箱必须等两个月才能上线。[D04](#source-d04)

**项目执行原则：**新域先观察；已有成熟策略先保留并审计；收紧前有完整发信源清单、实际对齐、报告分析与回退。不要未经评估同时开启 strict 对齐、失败报告 ruf 或把报告发到不明第三方。复杂子域/委派关系交由执行者按当前标准验证，不能只检查根域一条记录。

### 6.5 只读检查命令：检查“存在”，不能替代真实收发

以下示例中的域名与 selector 都必须替换为真实值。没有 dig 时可用系统 nslookup；不要把命令输出的某个 pass 当作完整认证结论。

```bash
dig NS example.com +short
dig MX example.com +short
dig TXT example.com +short
dig TXT _dmarc.example.com +short
dig TXT selector._domainkey.example.com +short
dig CNAME selector._domainkey.example.com +short
```

再从收件方真实邮箱取得原始邮件头，查看其可信认证结果：SPF 检查域、DKIM 的 d=/s=、DMARC 可见 From 对齐。任意一条 `Authentication-Results` 都可被伪造，需结合收件服务商认可的结果与日志，而非只搜索字符串 pass。[O02](#source-o02)

转发可能破坏 SPF；SRS 改写信封域不必然与原 From 对齐；ARC 也不保证所有接收方采信。实际有转发/列表的业务另做测试，不能只测直达。[D06](#source-d06)

## 7. 网站展示邮箱和邮件按钮：Astro 优先

**页面上同时提供完整可复制地址和邮件按钮。**`mailto:` 请求打开访客设置的邮件处理程序，用户仍需主动发送；没有设置客户端时应能复制地址或改用网站表单。统计只能记“邮箱入口点击”，不能记“收到询盘”。[W01](#source-w01)

页脚展示完整地址，桌面侧边栏可保留简短 Email 按钮；手机侧边控件应避开正文、Cookie 提示和屏幕安全区，页面内仍保留地址。可延用任务 1 的 `ContactLinks` / `ContactRail` 布局。

### 7.1 可复用 Astro 组件

保存为 `src/components/EmailContact.astro`，把邮箱替换成客户确认的地址。这个组件只负责展示与复制；本轮未在客户 Astro 项目里构建或运行。

```astro
---
const email = "sales@example.com"; // 必须替换为已确认的公开邮箱
const subject = "Product enquiry";
const href = `mailto:${email}?subject=${encodeURIComponent(subject)}`;
---
<email-contact data-address={email}>
  <a href={href}>{email}</a>
  <button type="button" hidden>Copy email</button>
  <span aria-live="polite"></span>
</email-contact>

<script>
  if (!customElements.get("email-contact")) {
    class EmailContact extends HTMLElement {
      connectedCallback() {
        const button = this.querySelector("button");
        const status = this.querySelector("[aria-live]");
        const address = this.dataset.address;
        if (!button || !status || !address) return;
        button.hidden = false;
        button.onclick = async () => {
          try {
            await navigator.clipboard.writeText(address);
            status.textContent = "Email address copied.";
          } catch {
            status.textContent = "Please select and copy the address above.";
          }
        };
      }
    }
    customElements.define("email-contact", EmailContact);
  }
</script>
```

在页脚或联系区域导入并放置 `<EmailContact />`，样式沿用网站的按钮/链接与键盘焦点规范。组件名称与已有项目冲突时改名。复制依赖安全上下文及浏览器许可，失败时保留手动复制；无 JavaScript 时按钮隐藏、地址仍可见。[W01](#source-w01)

### 7.2 WordPress / 普通 HTML

WordPress 在页脚模板的链接/段落区块写完整邮箱，链接目标填 `mailto:实际邮箱`；侧边联系方式组件同样填已确认地址。普通 HTML 可用：

```html
<a href="mailto:sales@example.com?subject=Product%20enquiry">
  sales@example.com
</a>
```

替换示例域，测试电脑、手机、无邮件客户端与键盘操作。不把邮箱地址做成只能看不能复制的图片，也不要在前端放员工密码、SMTP 凭据或 API key。

## 8. 网站表单通知：给开发者和 Agent 的实施路线

### 8.1 先选可实现的可靠性等级

| 等级 | 能交付什么 | 适用前提 | 不可夸大的地方 |
|---|---|---|---|
| 基础可靠 | 询盘后台留底＋邮件提醒＋明确人工补漏 | 每日有人检查条目、失败和未回复 | 未实现自动恢复就不能写“自动重试已通过” |
| 自动补漏 | 持久待发任务＋重试/幂等＋事件状态＋独立告警 | 有服务端、持久存储和维护者 | 服务商受理/送达事件仍不等于已读 |
| 多人协作 | 共享收件箱/工单＋分配＋交接 | 已有实际重复回复或漏分配问题 | 开源核心不等于所有功能、托管和模块免费 |

默认先让询盘可靠留底；业务量和人工响应要求明确后再增加自动化。不要承诺一个免费发送插件天然具备完整可靠性。

### 8.2 建议的数据流与状态

**访客提交 → 服务端校验 → 持久保存询盘与通知任务 → 返回编号 → 后台发信 → 跟踪异常 → 业务回复。**

这是本方案的工程设计：有数据库时，在同一事务里保存 inquiry 和 outbox（待发任务）；使用托管服务时，验证其等价保障。不能只放在内存数组、临时 Promise 或易失的请求生命周期里。

| 状态 | 可以告诉业务人员什么 |
|---|---|
| `inquiry_saved` | 已保存，可在后台处理；尚未证明提醒已送达 |
| `provider_accepted` | 发送服务已受理；保存对应 message ID |
| `delivered` | 收件服务器已接受；仍需查垃圾/隔离及业务人员可见性 |
| `failed / bounced / suppressed` | 有明确异常或不应继续发；交给责任人 |
| `owner_replied` | 已由指定人员回复并留痕；不等于买方已读或成交 |

上述服务商事件语义见 [Resend Event Types（事件类型）](https://resend.com/docs/webhooks/event-types)。状态设计和后台补漏仍需要开发实现。[W04](#source-w04)

### 8.3 From、To、Reply-To 按这个填

访客邮箱假设为 `buyer@example.net`：

| 字段 | 内部销售通知 | 可选访客回执 |
|---|---|---|
| From（发件人） | `Website <notify@notify.example.com>`，本方验证域 | 同左 |
| To（收件人） | 服务端固定 `sales@example.com` | 已校验的访客邮箱，另做反滥用 |
| Reply-To（点回复去哪里） | 访客邮箱 | `sales@example.com` |
| Subject（主题） | 服务端生成，含询盘编号 | 简短确认，含编号 |
| Body（正文） | 纯文本或正确转义的HTML，必要字段 | 固定简短文本，不回显任意HTML/外链 |

不要把客户填写的 Gmail/公司邮箱放到 From 假装由客户域发出。格式校验也不证明提交人拥有该邮箱；若业务需要证明所有权，另做验证。默认只发内部通知；公开表单自动回执要防止被用来向任意人轰炸邮件。[W03](#source-w03)

### 8.4 具体案例：Astro＋持久存储＋Resend

1. **检查项目实际版本和运行时。**读取 package.json、锁文件、现有 adapter 与托管配置；按官方版本文档决定新增 POST endpoint 或 Actions，不盲改整站架构。
2. **客户注册事务邮件账号。**使用真实资料、MFA和自己控制的账单/恢复。Resend 当前没有独立“申请解除沙盒”的生产审批步骤，但仍需域名验证、额度和条款符合要求；本轮未确认对全部大陆主体保证准入。[W05](#source-w05)
3. **验证通知子域。**添加 `notify.example.com`，逐条复制 Records 页的记录。只用于通知时保留根域人工收信 MX；不要误启用根域 Resend 收信。2026 年 8 月后新增域可能生成 CNAME，而不是旧 MX＋TXT，不能固定照抄旧参数。[W06](#source-w06)
4. **创建限制用途的凭据。**仅用于本网站通知并尽可能限制域名/权限，存在主机密钥配置里；密钥不使用 `PUBLIC_` 前缀，不放到浏览器。运行时读取方法取决于 adapter，不能跨平台一律套 process.env。[W02](#source-w02)
5. **实现接收与持久任务。**服务端校验、限流、保存询盘与 outbox；只有持久保存成功才提示“已收到提交，编号……”。保存失败保留输入并给重试和邮箱备用入口。
6. **发信与跟踪。**worker/可靠调度器读取待发任务，保存服务商ID；处理退信/失败与 webhook，业务人员可查后台。API 返回成功不替代第 10 节真实收件测试。[W03](#source-w03)[W04](#source-w04)

**部署选择：**Astro 有服务器/函数时，配置匹配的官方 adapter，新增动态接口；静态站可保持大部分页面静态，只让必要接口按需运行。纯静态托管若不改环境，就用独立后端或具备留底、导出和异常处理的托管表单。HTML 表单直接调用 Astro Actions 的页面有按需渲染要求，按当前官方指南配置；仅上传 .ts 文件到静态空间不会得到后端。[W02](#source-w02)

下面只展示 REST 请求结构，**不是完整后端，也不能放到浏览器执行**：

```http
POST https://api.resend.com/emails
Authorization: Bearer <由服务端密钥管理注入>
Content-Type: application/json
Idempotency-Key: enquiry-notification/<询盘编号>

{
  "from": "Website <notify@notify.example.com>",
  "to": ["sales@example.com"],
  "reply_to": "buyer@example.net",
  "subject": "New enquiry <询盘编号>",
  "text": "Enquiry <询盘编号> - <已校验的需求内容>"
}
```

API 字段 `reply_to` 与部分 SDK 的 `replyTo` 不要混用，代码按实际安装版类型与官方接口验证。[W03](#source-w03)

### 8.5 自动补漏需要实现和测试的项目

- **幂等：**同一次提交重试用同一标识；数据库唯一约束保证不重复建单；同键异文拒绝。通知载荷冻结，任务唯一，多个 worker 原子认领。
- **有上限的重试：**429 根据 Retry-After 等当前规则退避；临时错误有限重试；凭据、域名和格式错误暂停并告警。不要在等待 delivered 时反复新建邮件。
- **响应丢失：**用原幂等键和相同载荷重试。Resend 当前幂等窗口为 24 小时；超出窗口仍无法确认时先查记录/人工核对，不盲目切供应商重发。[W07](#source-w07)
- **验签与去重：**webhook 对原始 body 按官方方法验签，持久保存并按事件 ID 去重；写库成功再返回成功；处理重复和乱序事件，不能用晚到的 sent 覆盖已知 delivered。[W08](#source-w08)
- **防滥用：**服务端字段/体积限制、CR/LF头注入防护、HTML转义、共享限流；首版不开放附件上传。使用验证码时要服务端验证；验证码不能替代数据库幂等。[W09](#source-w09)
- **故障可见：**监控待发最老时间、失败数量和后台异常；至少一条告警路线不依赖出故障的同一邮件链路。失败任务有人工查单、恢复和补发说明。

这些是实施要求，不能从服务商快速开始样例自动推断已具备；本轮没有在真实应用里完成上述故障演练。

### 8.6 WordPress 具体路线

| 步骤 | 操作 | 完成证据 |
|---|---|---|
| 1. 留存提交 | 用有 Entries 的表单；已有 Contact Form 7 时可加 Flamingo | 提交后后台有编号、字段与时间；CF7自身不保存消息 [W10](#source-w10) |
| 2. 配通知 | 固定To、自家验证域From、访客Reply-To | 实际通知头部与回复目标正确 |
| 3. 配一条发送路径 | 选一款维护中的发送插件，如 WP Mail SMTP 的 Resend API mailer，或适合租户的 FluentSMTP OAuth | 当前版本、权限、许可和密钥位置有记录 [W11](#source-w11) |
| 4. 配日志与补漏 | 核对插件实际版本的日志、重发、告警能力 | 不把Pro功能写成免费；后台条目与通知记录可对账 |
| 5. 验证调度 | 需要及时自动恢复时接合适的系统调度 | WP-Cron依访问触发的延迟被处理 [W12](#source-w12) |
| 6. 故障与业务实测 | 断通知服务、恢复、查条目，再让销售回复测试买方 | 记录没丢、重复可控、双方收到 |

只保留一款主要插件接管发信，避免重复 hook/通知。`wp_mail()` 返回 true 只表示调用处理未报错，不能写成“客户已收到”。插件有日志或手工重发，不等于具备持久自动重试和不重复投递，必须实测；无自动恢复时登记人工巡检负责人。[W13](#source-w13)

### 8.7 成熟开源项目什么时候用

- **Chatwoot：**适合多人分配和多渠道会话；社区部分 MIT，enterprise 目录另有许可。采用当前邮箱渠道和认证说明，不照搬旧 Gmail “低安全应用”教程。
- **FreeScout：**适合邮件工单式共享接待；核心 AGPL-3.0，商业模块能力与许可单独确认。

两者都需要版本、安全更新、备份、恢复和运维负责人。已有企业邮箱共享功能够用时先沿用；这些项目也不意味着需要自己运营 SMTP 服务器。[W14](#source-w14)

## 9. 已有邮箱迁移：避免业务突然断信

新开空域名可以跳过本节。已有日常邮件时，由客户确认切换窗口，按以下顺序执行：

1. 导出原 DNS、账号/别名/共享权限、转发和所有发信源。写清旧邮箱数据、日历/联系人、附件与历史文件夹迁移范围。
2. 在新平台先建全部收件对象和授权，选择当前支持的迁移工具，预迁移并抽样检查附件和文件夹；不要先删旧账号。
3. 准备新的认证与客户端，核对旧发信系统过渡期仍被合法授权。降低 TTL 需要等待旧缓存，不能承诺立即全球生效。
4. 如果已有 MTA-STS enforce，先核对其允许的MX和缓存策略能够接纳新入口。不要只换 MX 后才处理传输政策。
5. 在获准窗口切换 MX/路由，持续查看新旧系统、退信与未处理邮件，补增量迁移，再做外部往返和共享处理验收。
6. 验收数据与业务连续性后，按保存方案结束旧服务，清理确已停用的发送授权。换回 MX 不会把新邮箱已经接收的信自动搬回去。[D01](#source-d01)[O03](#source-o03)

迁移工具也会变：例如 Google 官方说明从 2026 年 10 月起其旧 Exchange Online 迁移路线有调整，应按来源系统选择当前支持的 advanced data import 等工具，而不是按历史截图操作。[O03](#source-o03)

## 10. 提前写好的验收标准

每项填写“通过 / 失败 / 阻塞 / 未执行 / 不适用”。不适用必须说明理由。资料已核验和真实账号已验收分开；本轮下面各项初始都是 **未执行**。

| ID | 必须证明的结果 | 怎么测、留下什么证据 |
|---|---|---|
| A01 | 客户掌握系统 | 负责人可访问域名、DNS、邮箱组织和账单；恢复资料有受控保管 |
| A02 | 独立身份与恢复 | 员工新登录受MFA保护；测试恢复路径；不同时锁死全部管理员 |
| A03 | 业务地址可接待 | 发给sales@能收到，正确身份回复；多人能看已发送，未授权者不能读 |
| A04 | DNS和认证成立 | 当前MX、同名单一SPF及查询预算、启用DKIM、DMARC及报告路线有记录 |
| A05 | 每条直接发信来源合格 | 员工、网站、实际CRM分别取得收件方可信认证头部与对齐结果 |
| A06 | 真实双向联系 | 外部发入→业务回复→外部确认；附件/签名可读，来源和回复归属正确 |
| A07 | 约定样本的传输与入箱分别合格 | 预先选定Gmail、Outlook、Yahoo/目标企业域及QQ或163等适用样本；记录首次落点与时间。垃圾/隔离不能标为自然进入约定收件箱通过 |
| A08 | 网站邮箱入口可用 | 页脚与侧边按钮正确；手机、键盘、无邮件客户端时有可复制地址 |
| A09 | 表单完整闭环 | 真页面提交→后台记录→通知→销售回复→外部收到，同一询盘编号 |
| A10 | 邮件提醒失败不会丢单 | 模拟通知故障，记录仍在；恢复/人工补漏有效，告警能到责任人 |
| A11 | 保存失败不报成功 | 模拟存储失败，提示可理解、输入可保留、有重试与邮箱备用 |
| A12 | 防重复与防滥用 | 双击/超时同键不重复建单；恶意字段、限流、错误验证码按预期处理 |
| A13 | 自动事件处理可用 | 如启用webhook，验签、重放/乱序处理、写库失败恢复有证据 |
| A14 | 异常可定位 | 退信、拒收、隔离、通知失败有查找方式和负责人 |
| A15 | 迁移可交付 | 数据、权限、增量与旧入口残留已核对；无迁移写不适用 |
| A16 | 离职与恢复可操作 | 用测试身份验证撤权与业务继续接收；按约定做数据恢复抽样 |
| A17 | 运营有人承担 | 巡检、回复、报告复核、续费和支持渠道均有负责人与频次 |

所有公开表单都要验证输入校验、防注入、限流等基础安全，以及防重复策略；不能因选择基础等级就免验。A10在基础等级可按明确的人工补漏流程验收；选择自动补漏时另测自动重试、告警与恢复。A13只要启用webhook就必须验签、去重和失败恢复，未使用才可写不适用。没有网站表单则相关项写不适用，不应为了验收临时添加无需求功能。

### 真实收发样本怎么测

1. 先确认允许使用的测试收件人和内容，主题带统一编号，例如 `MAIL-ACCEPT-20261127-01`。
2. 从实际业务账号发正常中/英文短邮件与约定附件；测试者在加白名单、联系人或“不是垃圾”前记录首次文件夹。
3. 外部测试者回复原线程，业务人员确认正确邮箱/共享入口收到，再回复确认。
4. 保存时间、双方地址、Message-ID/供应商ID、文件夹、可信认证摘要和异常；脱敏后放入证据目录。
5. 进垃圾、隔离或丢失都保留原结果，排查后单列复测。人工挪到收件箱不算自然首投通过。

| 系统 | 外部收发 | 首次文件夹/延迟 | 认证与回复证据 | 本轮状态 |
|---|---|---|---|---|
| Gmail | 未执行 | 未核验 | 未取得 | 未执行 |
| Outlook.com | 未执行 | 未核验 | 未取得 | 未执行 |
| Yahoo或目标市场第三方 | 未执行 | 未核验 | 未取得 | 未执行 |
| QQ/163等选定中国邮箱 | 未执行 | 未核验 | 未取得 | 未执行 |
| 实际目标客户企业域（若获准） | 未执行 | 未核验 | 未取得 | 未执行 |

一次样本通过不能保证以后永远进收件箱。打开像素也不作为“已读”的验收证据，缓存/隐私机制会影响其准确性；以真实回复、文件夹和日志为准。[O01](#source-o01)[O04](#source-o04)

## 11. 上线后业务人员每天怎么用

| 频率 | 要做的事 | 责任与完成标志 |
|---|---|---|
| 每个工作日 | 查sales@、垃圾/隔离、网站未处理条目、失败通知 | 主负责人处理或分配；替补可接手 |
| 每次回复前 | 核对客户地址、询盘编号、发件身份和附件 | 不把内部备注或其他客户附件发出去 |
| 每周（建议） | 对照后台条目与已回复记录，查积压和异常发信 | 有负责人清理和复盘，不只看邮箱未读数 |
| 每月（建议） | 复核发送源、DMARC聚合报告、权限/外部转发、容量和凭据到期 | 维护者留下结论，旧服务授权及时撤销 |
| 人员变动时 | 阻断访问、撤会话/令牌和委派，保留数据并安排接任 | 不能只改密码或先删邮箱再交接 |
| 续费前 | 核对域名和邮箱到期、账单方式、恢复渠道 | 客户指定负责人完成续费与复核 |
| 约定周期 | 抽样恢复/导出数据、测试备用接待与告警 | 能证明可恢复，而非只有“已备份”按钮 |

MFA优先选择服务商支持的安全密钥/通行密钥等抗钓鱼方式，备用恢复独立保管。发生账号异常，先控制访问并检查自动转发、规则、代理和应用授权，再按官方恢复流程处理。报价/收款账户更改通过已知的独立联系人渠道核实，不能只因邮件显示熟悉姓名就执行。[O05](#source-o05)

### 可直接给销售的首次响应模板

```text
Subject: Re: Enquiry [询盘编号] — [产品或项目]

Hello [Name],
Thank you for contacting [真实品牌/公司名称].
I am [Name], and I will help with your enquiry.

To prepare a suitable quotation, could you confirm:
1. Required specification and quantity
2. Destination country and delivery requirements
3. Any relevant drawings or standards

I will update you by [真实可兑现的日期、时区].

Best regards,
[Name] | [Role]
[Brand / Company]
[Website] | [Business email] | [Optional business phone]
```

只索取当前询盘所需信息，不自动加入营销名单。签名使用真实主体名称，不把尚未注册的品牌描述为已注册公司；回复期限由业务人员真实安排。

## 12. 常见故障：按症状查，避免乱改 DNS

| 症状 | 先查哪里 | 下一步 |
|---|---|---|
| 网页邮箱能收发，Outlook却登录失败 | 套餐协议权限、区域服务器、MFA/专用密码、OAuth、客户端访问策略 | 对照该租户官方说明；不先关闭全局安全 |
| 网站显示成功，但没有询盘 | 数据是否真正落库、编号是否存在 | 存储失败改为失败提示；邮件不能代替底账 |
| 后台有询盘，销售没通知 | outbox、供应商ID、失败/抑制、垃圾/隔离和地址 | 在后台先处理客户，随后修通知与补发 |
| 一般邮箱正常，某类客户进垃圾 | 真实头部、对齐、内容、附件、发送来源与收件方日志 | 不承诺换服务商立刻解决；保留样本复测 |
| 同名DNS有两条v=spf1，或可信结果显示spf=permerror | 同名重复策略、嵌套查询预算 | 合并合法来源，保留无关TXT |
| DKIM DNS显示正确但邮件没有签名 | 平台启用、实际selector、发信路径与d= | 返回服务商启用；每条路径分别测试 |
| 手机点Email没有反应 | 默认邮件处理程序与浏览器行为 | 显示可复制地址和表单备用 |
| 同事看不到已经回复 | 共享Sent Items、委派权限、实际From | 配共享副本和分配流程 |
| 换MX后旧邮箱仍有信 | 原TTL缓存、旧入口、明确路由和增量迁移 | 同时巡检旧新系统；按计划核对，不急停旧服务 |
| 报告或日志写Delivered却没有看到 | 具体事件、最终收件方、垃圾/隔离/规则 | 让受控收件人验证实际位置，不能直接判已读 |

### 给 Agent 的执行任务模板

```text
请使用 enterprise-email-operations。
目标：为 [真实域名] 配置/审计 [当前邮箱服务及云环境]，网站为 [框架与托管]。
现有情况：[用户/别名/共享箱、旧邮件、网站/CRM发信源、客户网络]。
已授权范围：[只读审计/测试环境实现/已批准DNS变更/指定外部测试收件人]。
请先读取项目说明与现状，完成信息清单、逐条DNS变更表和回退方案；
具体记录只取真实租户，不编造selector、公钥、域名验证值或准入条件。
业务邮箱与网站通知分开，表单保留持久记录，按已选等级实现补漏。
按验收表逐项报告通过/失败/阻塞/未执行/不适用，并附实际证据。
已有授权内直接推进；缺少资料或权限时只阻塞受影响步骤，继续准备可审查交付。
不要把研究、代码示例、API成功码或DNS存在写成真实投递已通过。
交付中文业务手册、技术配置差异、英文原始官方链接与待办责任人。
```

## 13. 可选能力：何时值得增加

**群发营销：**另外设计订阅、退订、退信和投诉管理。个人 Gmail、Yahoo和Outlook.com的批量要求与范围不同，不能合并成一个“统一5000封”门槛；Yahoo官方未公开固定数量门槛。普通一对一询盘回复不必被强加营销退订按钮。[D05](#source-d05)[O06](#source-o06)

**MTA-STS / TLS-RPT：**用于传输策略和报告，不替代SPF/DKIM/DMARC；需要维护HTTPS政策、证书、允许MX及缓存。已有策略必须纳入迁移。普通小团队先完成核心闭环，再按风险和维护能力增加。[O03](#source-o03)

**BIMI：**是品牌标识显示专项，需满足对应收件服务的认证/证书/信誉等条件；DNS存在不保证显示，更不保证进收件箱。不要为了Logo把日常邮箱域未经评估就改reject。[O07](#source-o07)

**归档/备份/CRM：**根据合同、业务保存需求和恢复目标采购及测试。服务商能同步多端不等于可恢复误删或离职造成的数据缺口；先定义需保留什么、谁可访问、多久能恢复，再选能力。

## 14. 官方原始资料与中文阅读指引

以下保留官方/项目维护者原始链接。英文标题后给出中文用途说明；中国运营版只提供中文官方资料时，保留其正确产品文档，不用国际版替代。核验日期为 2026-11-27，实施当天重新确认套餐、账号环境和操作界面。

<!-- OFFICIAL-SOURCE-INDEX -->

<a id="source-p01"></a>

### P01 · Zoho：中国区计划与客户端

- **Manage subscriptions / 中国区订阅**：[https://www.zoho.com.cn/mail/help/adminconsole/subscription.html](https://www.zoho.com.cn/mail/help/adminconsole/subscription.html)
- **IMAP Access / 中国区客户端**：[https://www.zoho.com.cn/mail/help/imap-access.html](https://www.zoho.com.cn/mail/help/imap-access.html)

<a id="source-p02"></a>

### P02 · 阿里邮箱：中国站购买与开通

- **购买阿里邮箱**：[https://help.aliyun.com/zh/document_detail/36702.html](https://help.aliyun.com/zh/document_detail/36702.html)
- **首次开通和管理员设置**：[https://help.aliyun.com/zh/document_detail/36698.html](https://help.aliyun.com/zh/document_detail/36698.html)

<a id="source-p03"></a>

### P03 · Microsoft：区分全球版、世纪互联版和计划

- **中国企业产品选择页**：[https://www.microsoft.com/zh-cn/microsoft-365/business-china-offers](https://www.microsoft.com/zh-cn/microsoft-365/business-china-offers)
- **Microsoft 365 operated by 21Vianet / 中国版说明**：[https://learn.microsoft.com/office365/servicedescriptions/office-365-platform-service-description/microsoft-365-operated-by-21vianet](https://learn.microsoft.com/office365/servicedescriptions/office-365-platform-service-description/microsoft-365-operated-by-21vianet)
- **Exchange Online operated by 21Vianet / 功能矩阵**：[https://learn.microsoft.com/en-us/office365/servicedescriptions/office-365-platform-service-description/exchange-online-operated-by-21vianet](https://learn.microsoft.com/en-us/office365/servicedescriptions/office-365-platform-service-description/exchange-online-operated-by-21vianet)

<a id="source-p04"></a>

### P04 · Microsoft：共享邮箱、许可、权限和发送副本

- **About shared mailboxes / 条件和许可**：[https://learn.microsoft.com/en-us/microsoft-365/admin/email/about-shared-mailboxes](https://learn.microsoft.com/en-us/microsoft-365/admin/email/about-shared-mailboxes)
- **Create a shared mailbox / 创建及授权**：[https://learn.microsoft.com/en-us/microsoft-365/admin/email/create-a-shared-mailbox?view=o365-worldwide](https://learn.microsoft.com/en-us/microsoft-365/admin/email/create-a-shared-mailbox?view=o365-worldwide)
- **Configure a shared mailbox / 已发送副本等设置**：[https://learn.microsoft.com/en-us/microsoft-365/admin/email/configure-a-shared-mailbox?view=o365-worldwide](https://learn.microsoft.com/en-us/microsoft-365/admin/email/configure-a-shared-mailbox?view=o365-worldwide)

<a id="source-p05"></a>

### P05 · Microsoft：大陆访问全球租户的网络边界

- **Microsoft 365 performance optimization for China users / 中国网络说明**：[https://learn.microsoft.com/en-us/microsoft-365/enterprise/microsoft-365-networking-china?view=o365-worldwide](https://learn.microsoft.com/en-us/microsoft-365/enterprise/microsoft-365-networking-china?view=o365-worldwide)

<a id="source-p06"></a>

### P06 · Google：地区与计费，须分别核验

- **Countries or regions where Google Workspace is available / 地区可用性**：[https://knowledge.workspace.google.com/admin/support/troubleshooting/countries-or-regions-where-google-workspace-is-available](https://knowledge.workspace.google.com/admin/support/troubleshooting/countries-or-regions-where-google-workspace-is-available)
- **Payment options in my country / 按计费国家付款**：[https://knowledge.workspace.google.com/admin/billing/payment-options-in-my-country](https://knowledge.workspace.google.com/admin/billing/payment-options-in-my-country)

<a id="source-p07"></a>

### P07 · Zoho：区域、域名部署与安全

- **GDPR / Data center locations / 数据中心**：[https://www.zoho.com/mail/gdpr.html](https://www.zoho.com/mail/gdpr.html)
- **Email Hosting Setup / 部署顺序**：[https://www.zoho.com/mail/help/adminconsole/email-hosting-setup.html](https://www.zoho.com/mail/help/adminconsole/email-hosting-setup.html)
- **Configure Email Delivery / 按数据中心取MX**：[https://www.zoho.com/mail/help/adminconsole/configure-email-delivery.html](https://www.zoho.com/mail/help/adminconsole/configure-email-delivery.html)
- **Two-factor authentication / 中国区双重认证**：[https://www.zoho.com.cn/mail/help/adminconsole/two-factor-authentication.html](https://www.zoho.com.cn/mail/help/adminconsole/two-factor-authentication.html)
- **Shared Mailbox settings / 全球版协作设置**：[https://www.zoho.com/mail/help/adminconsole/collaborative-inbox-settings.html](https://www.zoho.com/mail/help/adminconsole/collaborative-inbox-settings.html)

<a id="source-p08"></a>

### P08 · Google：许可、委派与协作收件箱

- **Delegate a user’s email address / 邮箱委派**：[https://knowledge.workspace.google.com/admin/users/delegate-a-users-email-address](https://knowledge.workspace.google.com/admin/users/delegate-a-users-email-address)
- **How licensing works / 用户许可**：[https://knowledge.workspace.google.com/admin/billing/how-licensing-works](https://knowledge.workspace.google.com/admin/billing/how-licensing-works)
- **Collaborative Inbox / 群组协作收件箱**：[https://support.google.com/a/users/answer/9259857?hl=en](https://support.google.com/a/users/answer/9259857?hl=en)

<a id="source-p09"></a>

### P09 · Microsoft：添加域名和创建组织

- **Add a domain / 先验证并建用户再切换**：[https://learn.microsoft.com/en-us/microsoft-365/admin/setup/add-domain?view=o365-worldwide](https://learn.microsoft.com/en-us/microsoft-365/admin/setup/add-domain?view=o365-worldwide)
- **Set up your organization for 21Vianet / 中国版设置**：[https://support.microsoft.com/en-us/office/o365-gallatin-adm/set-up-your-organization-for-office-365-operated-by-21vianet](https://support.microsoft.com/en-us/office/o365-gallatin-adm/set-up-your-organization-for-office-365-operated-by-21vianet)

<a id="source-p10"></a>

### P10 · Google：注册、当前MX与现代认证

- **Set up Google Workspace / 组织设置**：[https://knowledge.workspace.google.com/admin/getting-started/set-up-google-workspace-for-your-organization](https://knowledge.workspace.google.com/admin/getting-started/set-up-google-workspace-for-your-organization)
- **Set up MX records / 当前向导及旧MX说明**：[https://knowledge.workspace.google.com/admin/domains/set-up-mx-records-for-google-workspace](https://knowledge.workspace.google.com/admin/domains/set-up-mx-records-for-google-workspace)
- **Control access to less secure apps / 旧密码接入变化**：[https://knowledge.workspace.google.com/admin/apps/control-access-to-less-secure-apps](https://knowledge.workspace.google.com/admin/apps/control-access-to-less-secure-apps)
- **Send email from a printer, scanner, or app / 应用认证**：[https://knowledge.workspace.google.com/admin/gmail/send-email-from-a-printer-scanner-or-app](https://knowledge.workspace.google.com/admin/gmail/send-email-from-a-printer-scanner-or-app)

<a id="source-p11"></a>

### P11 · Microsoft：SMTP现行时间表、租户策略与Graph

- **Updated SMTP AUTH Basic Authentication Deprecation Timeline / 2026更新**：[https://techcommunity.microsoft.com/blog/exchange/updated-exchange-online-smtp-auth-basic-authentication-deprecation-timeline/4489835](https://techcommunity.microsoft.com/blog/exchange/updated-exchange-online-smtp-auth-basic-authentication-deprecation-timeline/4489835)
- **Enable or disable SMTP AUTH / 安全默认值限制**：[https://learn.microsoft.com/en-us/exchange/clients-and-mobile-in-exchange-online/authenticated-client-smtp-submission](https://learn.microsoft.com/en-us/exchange/clients-and-mobile-in-exchange-online/authenticated-client-smtp-submission)
- **user: sendMail / Graph权限、云环境和202状态**：[https://learn.microsoft.com/en-us/graph/api/user-sendmail?view=graph-rest-1.0](https://learn.microsoft.com/en-us/graph/api/user-sendmail?view=graph-rest-1.0)

<a id="source-p12"></a>

### P12 · 阿里邮箱：客户端准入、专用密码和端口

- **第三方客户端访问策略**：[https://help.aliyun.com/zh/document_detail/606337.html](https://help.aliyun.com/zh/document_detail/606337.html)
- **客户端专用密码策略**：[https://help.aliyun.com/zh/document_detail/444380.html](https://help.aliyun.com/zh/document_detail/444380.html)
- **IMAP/POP/SMTP服务器与端口**：[https://help.aliyun.com/zh/document_detail/36576.html](https://help.aliyun.com/zh/document_detail/36576.html)
- **两阶段认证**：[https://help.aliyun.com/zh/document_detail/2387281.html](https://help.aliyun.com/zh/document_detail/2387281.html)

<a id="source-d01"></a>

### D01 · MX优先级、DNS变更与分流

- **RFC 5321 / SMTP与MX规则**：[https://datatracker.ietf.org/doc/html/rfc5321.html](https://datatracker.ietf.org/doc/html/rfc5321.html)
- **Create DNS records at any DNS hosting provider / 微软DNS**：[https://learn.microsoft.com/en-us/microsoft-365/admin/get-help-with-domains/create-dns-records-at-any-dns-hosting-provider?view=o365-worldwide](https://learn.microsoft.com/en-us/microsoft-365/admin/get-help-with-domains/create-dns-records-at-any-dns-hosting-provider?view=o365-worldwide)
- **Split delivery / 按明确路由分流**：[https://knowledge.workspace.google.com/admin/gmail/advanced/send-email-to-2-email-systems-with-split-delivery](https://knowledge.workspace.google.com/admin/gmail/advanced/send-email-to-2-email-systems-with-split-delivery)

<a id="source-d02"></a>

### D02 · SPF：同名策略、递归查询与排障

- **RFC 7208 / SPF标准，尤其§3、§4.6.4**：[https://www.rfc-editor.org/rfc/rfc7208.html](https://www.rfc-editor.org/rfc/rfc7208.html)
- **Troubleshoot SPF issues / 合并与排查**：[https://knowledge.workspace.google.com/admin/security/troubleshoot-spf-issues](https://knowledge.workspace.google.com/admin/security/troubleshoot-spf-issues)

<a id="source-d03"></a>

### D03 · DKIM：生成、启用与轮换

- **Set up DKIM / Google设置**：[https://knowledge.workspace.google.com/admin/security/set-up-dkim](https://knowledge.workspace.google.com/admin/security/set-up-dkim)
- **Troubleshoot DKIM issues / Google开始认证**：[https://knowledge.workspace.google.com/admin/security/troubleshoot-dkim-issues](https://knowledge.workspace.google.com/admin/security/troubleshoot-dkim-issues)
- **RFC 6376 / DKIM TXT字符串与选择器规则**：[https://www.rfc-editor.org/rfc/rfc6376.html#section-3.6.2.2](https://www.rfc-editor.org/rfc/rfc6376.html#section-3.6.2.2)
- **Configure DKIM / Microsoft选择器与轮换**：[https://learn.microsoft.com/en-us/defender-office-365/email-authentication-dkim-configure](https://learn.microsoft.com/en-us/defender-office-365/email-authentication-dkim-configure)

<a id="source-d04"></a>

### D04 · DMARC：2026标准更新与报告

- **RFC 9989 / DMARC，重点§7.4及附录C**：[https://www.rfc-editor.org/rfc/rfc9989.html](https://www.rfc-editor.org/rfc/rfc9989.html)
- **IANA DMARC parameters / active与historic标签**：[https://www.iana.org/assignments/dmarc-parameters](https://www.iana.org/assignments/dmarc-parameters)
- **RFC 9990 / Aggregate Reporting 聚合报告**：[https://www.rfc-editor.org/rfc/rfc9990.html](https://www.rfc-editor.org/rfc/rfc9990.html)

<a id="source-d05"></a>

### D05 · Gmail：认证与发件要求

- **Email sender guidelines / 全量与批量发件要求**：[https://support.google.com/mail/answer/81126](https://support.google.com/mail/answer/81126)
- **Email sender guidelines FAQ / 对齐、范围与退订条件**：[https://support.google.com/mail/answer/14229414?hl=en](https://support.google.com/mail/answer/14229414?hl=en)

<a id="source-d06"></a>

### D06 · 转发、SRS和ARC的边界

- **Best practices for forwarding email / 转发注意事项**：[https://support.google.com/mail/answer/175365](https://support.google.com/mail/answer/175365)
- **Sender Rewriting Scheme / SRS修改什么**：[https://learn.microsoft.com/en-us/exchange/reference/sender-rewriting-scheme](https://learn.microsoft.com/en-us/exchange/reference/sender-rewriting-scheme)
- **RFC 8617 / ARC认证链**：[https://www.rfc-editor.org/info/rfc8617/](https://www.rfc-editor.org/info/rfc8617/)

<a id="source-w01"></a>

### W01 · 邮箱链接与复制的浏览器行为

- **The Anchor element / mailto链接**：[https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Elements/a](https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Elements/a)
- **Clipboard.writeText / 安全上下文与失败处理**：[https://developer.mozilla.org/en-US/docs/Web/API/Clipboard/writeText](https://developer.mozilla.org/en-US/docs/Web/API/Clipboard/writeText)

<a id="source-w02"></a>

### W02 · Astro：真实服务端、表单与密钥

- **On-demand rendering / 服务器适配与按需运行**：[https://docs.astro.build/en/guides/on-demand-rendering/](https://docs.astro.build/en/guides/on-demand-rendering/)
- **Actions / 服务端表单调用**：[https://docs.astro.build/en/guides/actions/](https://docs.astro.build/en/guides/actions/)
- **Build forms with API routes / 接口表单**：[https://docs.astro.build/en/recipes/build-forms-api/](https://docs.astro.build/en/recipes/build-forms-api/)
- **Using environment variables / PUBLIC与服务端环境**：[https://docs.astro.build/en/guides/environment-variables/](https://docs.astro.build/en/guides/environment-variables/)
- **Send emails with Astro / Resend官方起步案例**：[https://resend.com/docs/send-with-astro](https://resend.com/docs/send-with-astro)

<a id="source-w03"></a>

### W03 · 表单发信请求与身份

- **Send Email / Resend API字段**：[https://resend.com/docs/api-reference/emails/send-email](https://resend.com/docs/api-reference/emails/send-email)
- **Troubleshooting WordPress contact forms / From与Reply-To**：[https://help.dreamhost.com/hc/en-us/articles/214831378-Troubleshooting-WordPress-contact-forms](https://help.dreamhost.com/hc/en-us/articles/214831378-Troubleshooting-WordPress-contact-forms)

<a id="source-w04"></a>

### W04 · Resend：事件与实际投递

- **Event Types / sent、delivered、bounce等**：[https://resend.com/docs/webhooks/event-types](https://resend.com/docs/webhooks/event-types)
- **Why users are not getting emails / delivered不等于入箱**：[https://resend.com/guides/email/users-never-got-login-code](https://resend.com/guides/email/users-never-got-login-code)

<a id="source-w05"></a>

### W05 · Resend：开户条件与域名

- **Does Resend require production approval? / 没有独立生产审批**：[https://resend.com/docs/knowledge-base/does-resend-require-production-approval](https://resend.com/docs/knowledge-base/does-resend-require-production-approval)
- **Terms of Service / 账号和使用条款**：[https://resend.com/legal/terms-of-service](https://resend.com/legal/terms-of-service)
- **Introduction: Domains / 验证子域**：[https://resend.com/docs/dashboard/domains/introduction](https://resend.com/docs/dashboard/domains/introduction)

<a id="source-w06"></a>

### W06 · Resend：现有收信MX与新DNS形态

- **How to avoid conflicts with MX records / 2026新域可能用CNAME**：[https://resend.com/docs/knowledge-base/how-do-i-avoid-conflicting-with-my-mx-records](https://resend.com/docs/knowledge-base/how-do-i-avoid-conflicting-with-my-mx-records)

<a id="source-w07"></a>

### W07 · Resend：幂等键与窗口

- **Idempotency Keys / 24小时窗口及API、SMTP头**：[https://resend.com/docs/dashboard/emails/idempotency-keys](https://resend.com/docs/dashboard/emails/idempotency-keys)

<a id="source-w08"></a>

### W08 · Resend：webhook验签

- **Verify webhooks requests / 原始body与签名**：[https://resend.com/docs/webhooks/verify-webhooks-requests](https://resend.com/docs/webhooks/verify-webhooks-requests)

<a id="source-w09"></a>

### W09 · 验证码须在服务端验证

- **Validate the token / Cloudflare Turnstile服务端验证**：[https://developers.cloudflare.com/turnstile/get-started/server-side-validation/](https://developers.cloudflare.com/turnstile/get-started/server-side-validation/)

<a id="source-w10"></a>

### W10 · WordPress：保存询盘底账

- **Managing Entries in Fluent Forms / 后台条目**：[https://fluentforms.com/docs/managing-entries-in-fluent-forms/](https://fluentforms.com/docs/managing-entries-in-fluent-forms/)
- **Save submitted messages with Flamingo / CF7留存**：[https://contactform7.com/save-submitted-messages-with-flamingo/](https://contactform7.com/save-submitted-messages-with-flamingo/)

<a id="source-w11"></a>

### W11 · WordPress：成熟发信插件及能力边界

- **Set up the Resend Mailer / WP Mail SMTP维护者指南**：[https://wpmailsmtp.com/docs/how-to-set-up-the-resend-mailer-in-wp-mail-smtp/](https://wpmailsmtp.com/docs/how-to-set-up-the-resend-mailer-in-wp-mail-smtp/)
- **WP Mail SMTP / 版本与免费Pro能力**：[https://wordpress.org/plugins/wp-mail-smtp/](https://wordpress.org/plugins/wp-mail-smtp/)
- **FluentSMTP / 维护与功能**：[https://wordpress.org/plugins/fluent-smtp/](https://wordpress.org/plugins/fluent-smtp/)
- **FluentSMTP Outlook/Office setup / OAuth配置，核对云环境**：[https://fluentsmtp.com/docs/configure-fluentsmtp-with-microsoft-outlook-office/](https://fluentsmtp.com/docs/configure-fluentsmtp-with-microsoft-outlook-office/)

<a id="source-w12"></a>

### W12 · WordPress：定时任务不应只靠访问

- **Cron / WP-Cron运行方式**：[https://developer.wordpress.org/plugins/cron/](https://developer.wordpress.org/plugins/cron/)
- **System Task Scheduler / 接系统调度**：[https://developer.wordpress.org/plugins/cron/hooking-wp-cron-into-the-system-task-scheduler/](https://developer.wordpress.org/plugins/cron/hooking-wp-cron-into-the-system-task-scheduler/)

<a id="source-w13"></a>

### W13 · WordPress：发信函数成功不等于收到

- **wp_mail / 返回值的真实含义**：[https://developer.wordpress.org/reference/functions/wp_mail/](https://developer.wordpress.org/reference/functions/wp_mail/)

<a id="source-w14"></a>

### W14 · 开源共享收件箱的许可与接入

- **Chatwoot LICENSE / 社区与enterprise区分**：[https://github.com/chatwoot/chatwoot/blob/develop/LICENSE](https://github.com/chatwoot/chatwoot/blob/develop/LICENSE)
- **Chatwoot inboxes / 当前渠道接入**：[https://app.chatwoot.com/hc/user-guide/articles/1677492191-adding-inboxes](https://app.chatwoot.com/hc/user-guide/articles/1677492191-adding-inboxes)
- **FreeScout LICENSE / 核心许可**：[https://github.com/freescout-help-desk/freescout/blob/dist/LICENSE](https://github.com/freescout-help-desk/freescout/blob/dist/LICENSE)
- **FreeScout repository / 功能与维护**：[https://github.com/freescout-help-desk/freescout](https://github.com/freescout-help-desk/freescout)

<a id="source-o01"></a>

### O01 · 日志的Delivered不等于业务收到

- **Message Trace FAQ / Microsoft事件与排障**：[https://learn.microsoft.com/en-us/exchange/monitoring/trace-an-email-message/message-trace-faq](https://learn.microsoft.com/en-us/exchange/monitoring/trace-an-email-message/message-trace-faq)
- **Email Log Search status definitions / Google日志语义**：[https://knowledge.workspace.google.com/admin/gmail/advanced/email-log-search-delivery-status-definitions](https://knowledge.workspace.google.com/admin/gmail/advanced/email-log-search-delivery-status-definitions)

<a id="source-o02"></a>

### O02 · 邮件头证据要在可信边界内解读

- **RFC 8601 / Authentication-Results与伪造风险**：[https://www.rfc-editor.org/rfc/rfc8601.html](https://www.rfc-editor.org/rfc/rfc8601.html)

<a id="source-o03"></a>

### O03 · 迁移、传输策略和当前工具

- **RFC 8461 / MTA-STS的MX政策和缓存**：[https://www.rfc-editor.org/info/rfc8461/](https://www.rfc-editor.org/info/rfc8461/)
- **About MTA-STS and TLS reporting / 作用与操作**：[https://knowledge.workspace.google.com/admin/gmail/advanced/about-mta-sts-and-tls-reporting](https://knowledge.workspace.google.com/admin/gmail/advanced/about-mta-sts-and-tls-reporting)
- **Google Workspace Migrate / Exchange Online当前迁移路线**：[https://support.google.com/workspacemigrate/answer/9229021?hl=en](https://support.google.com/workspacemigrate/answer/9229021?hl=en)

<a id="source-o04"></a>

### O04 · 打开像素不可靠地证明已读

- **Mail Privacy Protection / Apple远程内容预载**：[https://www.apple.com/legal/privacy/data/en/mail-privacy-protection/](https://www.apple.com/legal/privacy/data/en/mail-privacy-protection/)

<a id="source-o05"></a>

### O05 · 管理员、恢复与离职

- **Security checklist for small businesses / Google安全清单**：[https://knowledge.workspace.google.com/admin/security/security-checklist-for-small-businesses-1-100-users](https://knowledge.workspace.google.com/admin/security/security-checklist-for-small-businesses-1-100-users)
- **Security defaults / Microsoft租户保护**：[https://learn.microsoft.com/en-us/entra/fundamentals/security-defaults](https://learn.microsoft.com/en-us/entra/fundamentals/security-defaults)
- **Remove a former employee / 先阻断、保留再删除**：[https://learn.microsoft.com/en-us/microsoft-365/admin/add-users/remove-former-employee?view=o365-worldwide](https://learn.microsoft.com/en-us/microsoft-365/admin/add-users/remove-former-employee?view=o365-worldwide)

<a id="source-o06"></a>

### O06 · Yahoo与Outlook.com各自的发件规则

- **Yahoo Sender FAQs / 无固定公开bulk门槛**：[https://senders.yahooinc.com/faqs/](https://senders.yahooinc.com/faqs/)
- **Yahoo Best Practices / 认证和退订**：[https://senders.yahooinc.com/best-practices/](https://senders.yahooinc.com/best-practices/)
- **Outlook high-volume sender requirements / 消费者服务高量发件**：[https://techcommunity.microsoft.com/blog/microsoftthreatprotectionblog/strengthening-email-ecosystem-outlook%E2%80%99s-new-requirements-for-high%E2%80%90volume-senders/4399730](https://techcommunity.microsoft.com/blog/microsoftthreatprotectionblog/strengthening-email-ecosystem-outlook%E2%80%99s-new-requirements-for-high%E2%80%90volume-senders/4399730)

<a id="source-o07"></a>

### O07 · BIMI仅作专项

- **Set up BIMI / Google显示要求**：[https://knowledge.workspace.google.com/admin/security/set-up-bimi](https://knowledge.workspace.google.com/admin/security/set-up-bimi)
