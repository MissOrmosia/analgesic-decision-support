# 变更日志（CHANGELOG）

本项目的问题日志共记录 103 项，详见 [docs/问题日志.md](docs/问题日志.md)。本文件按版本归纳核心变更。

> 版本号说明：v1.0–v3.0 为早期迭代（问题 1–68），未逐版留档；v4.0 起逐版记录。

## beta1.0（当前版本）

- 问题 103：小儿 + 任意肾功能不全（含轻度）在肾功能分层确认后**直接强制会诊**，不再进入场景推荐，消除"先建议、后强制"的语义重复；`checkChildBoundary` 肾损分支转为防御性兜底
- 问题 101：页面打开时增加红色"使用限制声明"弹窗（仅限临床专业人士使用，每次加载弹一次）

## v4.4 · 第二轮 B 段（17 项）

- 问题 73：儿童肾功能计算改用 Schwartz 公式（0.413 × 身高 / Scr）
- 问题 99：肾功能分层弹窗删除"正常"快捷按钮（已确认异常不应再出现正常）
- 问题 74/86：中度及以上肾功能不全**避免使用 NSAIDs**，直接改写推荐阶梯（不再"先给全量再补警告"）；涉及术后禁食/口服、癌痛口服三条路径
- 问题 92：晚期癌痛 + 任意肾功能不全 → 强制疼痛科 + 肾内科会诊
- 问题 93：带状疱疹 + 中度肾损 → 输出减量方案后弹建议会诊（非强制）
- 问题 75：杜冷丁从术后阶梯移除，改为"芬太尼类（需麻醉/疼痛科评估）"
- 问题 78：成人痉挛痛先做 NSAIDs 筛查，无禁忌时推荐解痉药 + 酮咯酸联用
- 问题 79/82/87/88/89/90：新增 `checkChildBoundary()` 统一小儿边界判定（<2 岁 / 溃疡 / IBD / 肾功能不全 → 强制会诊）；小儿白名单定死（右旋布洛芬、对乙酰氨基酚、曲马多>12 岁、间苯三酚>2 岁）；小儿痉挛路径补 NSAIDs 筛查
- 问题 72：多瑞吉（芬太尼透皮贴）推荐前增加阿片耐受筛查；未耐受者禁用并强制疼痛科会诊
- 问题 100：拒绝会诊理由提交后增加绿色回执弹窗
- 清理：删除 handleCancerPo 不可达肾损补丁（被问题 92 拦截）

## v4.3 · 第二轮 A 段（问题 69/96/98）

- 问题 69：小儿 + 癌痛/神经痛在选完年龄后直接强制会诊，跳过精确年龄输入与肾功能筛查；删除两处不可达死代码
- 问题 96：拒绝会诊弹窗的"取消"改为"返回重新选择"，封堵不留痕绕开会诊的暗道
- 问题 98：术后小儿路径补儿科会诊确认，与痉挛路径行为统一
- 版本号移至标题栏显示

## v4.2 · 历史栈重构（问题 94）

- 方案 A：`captureCurrentScreen` 挂在 `renderOptions` 之后，历史栈只记录"渲染完选项的可交互屏幕"
- 新增 `finishScreen()` 约定：所有终点屏（无选项的推荐屏）统一收尾并入栈
- `goBack` 循环下弹：跳过无选项快照，保证返回落点永远可交互；返回时自动关闭弹窗
- 修复：返回卡死、多弹一层、"已记录患儿年龄"中间态

## v4.1 · 第一轮修复（问题 70/71/76/77/84/91）

- 问题 70：`renderOptions` 重构，选项注册 `data-opt-id` + 处理器注册表，返回键恢复可用
- 问题 76/84：`goBack` 不再调用屏幕函数，改为恢复 state + chatHTML + optionsHTML 快照，消除消息重复与走错分支
- 问题 77：`S.renalAction` 初始化
- 问题 91/71：全代码分支判断 id 化，修复"不能口服"子串命中"能口服"导致的癌痛路径错误

## v4.0（问题 43/45/49/57/60/65/66 等）

- 肾功能筛查全局必经化（正常/异常/未查三态）
- 小儿精确年龄输入 + 2/6/12 岁阈值
- 肾损五级分层 + Scr/eGFR 手动计算
- 高风险场景强制会诊机制、审计日志、返回上一步/返回初始界面

## v1.0–v3.0（问题 1–68）

- 四场景决策流（痉挛 / 术后 / 晚期癌痛 / 带状疱疹后神经痛）
- NSAIDs 胃肠道禁忌三按钮门控、溃疡活动性追问
- 小儿警示与年龄分层、会诊确认机制
- 酮咯酸 5 天限制与老年剂量、吲哚美辛老年警示
- 审计日志、理由校验、癌痛高级方案会诊门控

---

---

# 🇬🇧 English Version

# Changelog

The project's issue log records 103 items in total (IDs 1–103); see [docs/问题日志.md](docs/问题日志.md). This file summarizes the core changes by version.

> Version numbering: v1.0–v3.0 were early iterations (Issues 1–68) without per-version archives; per-version records begin with v4.0.

## beta1.0 (current)

- Issue 103: Child + any degree of renal impairment (including mild) now triggers a **mandatory consult immediately upon renal stratification**, without entering scenario recommendations — eliminating the contradictory "suggest first, block later" semantics; the renal branch of `checkChildBoundary` is retained only as a defensive fallback
- Issue 101: A red "Usage Restriction Notice" modal on page load (clinical professionals only; shown once per load)

## v4.4 · Second Round, Segment B (17 items)

- Issue 73: Pediatric renal function calculation switched to the Schwartz formula (0.413 × height / Scr)
- Issue 99: The "normal" shortcut button removed from the renal stratification modal (a confirmed abnormality should not offer "normal" again)
- Issues 74/86: Moderate-to-severe renal impairment — **avoid NSAIDs**, with the recommendation ladder rewritten at the source (no more "full dose first, warning later"); covers postoperative NPO/PO and cancer-pain oral paths
- Issue 92: Advanced cancer pain + any renal impairment → mandatory Pain Medicine + Nephrology consult
- Issue 93: Postherpetic neuralgia + moderate renal impairment → reduced-dose regimen printed first, then a recommended (non-mandatory) consult modal
- Issue 75: Pethidine (meperidine) removed from the postoperative ladder, replaced by "fentanyl-class agents (requires anesthesia/pain-specialist assessment)"
- Issue 78: Adult spasmodic pain now runs NSAID screening first; if no contraindication, recommends antispasmodic + ketorolac combination therapy
- Issues 79/82/87/88/89/90: New unified `checkChildBoundary()` pediatric boundary check (<2 y / ulcer / IBD / renal impairment → mandatory consult); pediatric whitelist hard-coded (dexibuprofen, acetaminophen, tramadol >12 y, phloroglucinol >2 y); NSAID screening added to the pediatric spasm path
- Issue 72: Durogesic (fentanyl transdermal patch) gated behind opioid-tolerance screening; opioid-naïve patients are barred and referred for a mandatory pain-specialist consult
- Issue 100: A green confirmation receipt modal after consult-refusal reason submission
- Cleanup: removed the unreachable renal patch in `handleCancerPo` (already intercepted by Issue 92)

## v4.3 · Second Round, Segment A (Issues 69/96/98)

- Issue 69: Pediatric + cancer pain/neuralgia triggers a mandatory consult immediately after age selection, skipping precise age input and renal screening; two unreachable dead-code blocks removed
- Issue 96: The consult-refusal modal's "Cancel" replaced with "Go back and choose again," sealing the unaudited backdoor around the consult
- Issue 98: Pediatric consult-confirmation added to the postoperative path, unifying behavior with the spasm path
- Version number moved to the title bar

## v4.2 · History-Stack Refactor (Issue 94)

- Plan A: `captureCurrentScreen` hooks in after `renderOptions`; the history stack records only "interactive screens with rendered options"
- New `finishScreen()` convention: all terminal screens (recommendation screens without options) finish uniformly and are pushed onto the stack
- `goBack` loops down past option-less snapshots, guaranteeing the Back landing point is always interactive; modals auto-close on Back
- Fixed: frozen Back, overshoot by one level, the "pediatric age recorded" intermediate state

## v4.1 · First Repair Round (Issues 70/71/76/77/84/91)

- Issue 70: `renderOptions` refactored — options register `data-opt-id` + a handler registry; the Back button works again
- Issues 76/84: `goBack` no longer calls screen functions; it restores state + chatHTML + optionsHTML snapshots, eliminating duplicated messages and wrong-branch navigation
- Issue 77: `S.renalAction` initialized
- Issues 91/71: all branch logic converted to id-based checks, fixing the cancer-pain path error caused by "不能口服" substring-matching "能口服"

## v4.0 (Issues 43/45/49/57/60/65/66, etc.)

- Globally mandatory renal screening (three states: normal / abnormal / unchecked)
- Precise pediatric age input + 2/6/12-year thresholds
- Five-tier renal impairment stratification + manual Scr/eGFR calculation
- High-risk mandatory-consult mechanism, audit log, Back / Back-to-Home navigation

## v1.0–v3.0 (Issues 1–68)

- Four-scenario decision flow (spasm / postoperative / advanced cancer pain / postherpetic neuralgia)
- Three-button NSAID gastrointestinal gate, ulcer-activity follow-up
- Pediatric warnings and age stratification, consult-confirmation mechanism
- Ketorolac 5-day limit and geriatric dosing, indomethacin geriatric warning
- Audit log, reason validation, cancer-pain advanced-procedure consult gate
