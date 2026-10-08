# 最小配置

上下文已经足以确定用途、地域和输出时直接开始 W1。无配置不等于不能分析。默认中立案例研习、标准论证深度、Markdown、正文精确引注、三个分别确认的产物；用户直接完成等指令优先。

只询问会影响本案的用途、适用法域、关键时间或期望输出。能力可通过已有工具只读探测，不能要求用户登记工具产品后才开工。正文不记录能力槽名称。

## 适用地域（jurisdiction）

劳动法的最低工资、社平工资与三倍封顶线、失业金、医疗期与病假口径、一裁终局金额线及多数裁审口径均为**省级参数**，地域直接改变金额结论与口径选择。冷启动须确定受诉地／常用执业地，判定顺序：

1. 已有上下文可确定（案情写明地点、用户此前说明执业地、`.user-config.md` 已登记）→ 直接采用，不重复问；
2. 无法从上下文确定 → **询问一次**："常用适用地域（受诉地）是哪个省市？"；与用户后续确认的受诉地不一致时以案件受诉地为准；
3. 用户未回答且案情未写明 → 教学题以全国性规范为主可继续分析，但地方参数类计算（N/2N 封顶、失业金、病假下限、一裁终局线）一律符号化表达并列"待人工核对清单"，**不得以任何默认地域硬编码数值**。

地域确认结果供 `.user-config.md` 的 jurisdiction 字段使用；受诉地参数未沉淀的，按 `references/local-data-sources.md` 对应类别行锁定入口运行时检索，取值写入**案件工作目录**的地方参数缓存（非技能包内 `references/local-standards.md`），按地域、版本、时间和来源索引。

## 法律检索能力槽

冷启动先用已有工具（如 `qw_mcp_list`）只读探测运行环境是否存在可用的专业法条检索 MCP／连接器（元典、北大法宝等），跑一条最小真实用例确认可用性，据此把校验后端绑定为一级来源。探测到即登记能力槽契约；探测不到不是失败，按 `references/research-protocol.md` §6 降级链落到二级（官方网页）或三级（内置知识），并在台账与正文如实标注级别，绝不因未配置而拒绝开工或通篇免责。

能力槽契约（写入长期配置时用，字段适配劳动法的时际核验需求）：`provider_name`（后端名称）、`tools`（检索／取原文工具名）、`contract`（`article_locator`＝条号定位字段、`version_field`＝行为时版本/修正时点字段、`effectiveness_field`＝效力状态字段、`effective_value`＝现行有效取值、`title_format`／`number_format`＝规范名称与文号引用格式）。契约缺失某字段时，该项退回§6就地标注，不伪填。

## 锚定表抽检

冷启动及每次会话启动时，按 [SKILL.md §9 法条锚定表](../SKILL.md) 抽检 5–8 条：A/B/C 组各抽 1–2 条（如"过错解除条款""经济补偿计算条款""加班费三倍率条款""仲裁时效条款"），E 组（劳动争议司法解释二，法释〔2025〕12 号）**全量**。抽检经法律检索能力槽执行，未配置时按检索协议 §6 降级链二级核验。

抽检结果不打扰用户：命中即静默通过；命中失败在**案件工作目录 `verification-log.md`** 登记受影响条文，并在 W2a 候选清单中提示——报告引用前须补核验，未补核验的按降级链级别就地标注。技能包内的锚定表不在运行时修改。

## 长期配置（.user-config.md）

只有用户同意长期复用才写 `.user-config.md`：jurisdiction、mode、citation、format、confirmation、depth，以及上述法律检索能力槽契约与锚定表抽检结果。案情、人员、工资、时效和地方数值不写入长期偏好。Word 转换不能取得时保持 Markdown，不伪称已生成。

```markdown
# gutachten-labor-case 用户配置

jurisdiction: <省／市，如 河南·郑州；未确定留空>
mode: academic | litigation | compliance
citation: 正文精确引注 | 脚注引注
format: markdown | docx
confirmation: 分段确认 | 全自动
depth: 标准 | 压缩

legal_db:
  provider_name: <后端名称>
  tools: <检索／取原文工具名>
  contract:
    article_locator: <条号定位字段>
    version_field: <行为时版本/修正时点字段>
    effectiveness_field: <效力状态字段>
    effective_value: <现行有效取值>
    title_format: <规范名称引用格式>
    number_format: <文号引用格式>

anchor_check:
  date: <YYYY-MM-DD>
  fail: [<命中失败的语义名称列表，无则空>]
```
