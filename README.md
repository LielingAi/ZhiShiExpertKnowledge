# ZhiShiExpertKnowledge

[ZhiShi](https://github.com/LielingAi/ZhiShi)（安全研究 agent harness）官方共享的专家知识仓库。不定期分享经审定（reviewer）的专家知识，导入后进入 `expert.db`，在 harness 研究过程中按需检索注入。

当前共 **16 个导入文件、139 条专家知识**，全部条目 reviewer 均为 `j0hnexp`、均带 `criteria`（成立/失效判定标准）。

- `kind` 分布：`technique` 58 / `sop` 52 / `idea` 29
- `domain` 分布：`binary` 45 / `whitebox` 43 / `pentest` 43 / `redteam` 7 / `ai-security` 1

## 目录内容

### 0day 挖掘 · 白盒审计

| 文件 | 主题 | 条目数 |
| --- | --- | --- |
| `expert-import-go-0day.yaml` | Go 0day 挖掘：cmd/go 工具链供应链、net/http 协议边界（HTTP/2 CONTINUATION 洪泛、请求走私）、crypto/tls 时序侧信道、x/crypto/ssh 握手面 | 11 |
| `expert-import-dotnet-0day.yaml` | .NET 0day 挖掘：Kestrel/ASP.NET Core 认证边界与请求走私、System.Formats.Nrbf 反序列化、NuGet/MSBuild 供应链、Runtime/WPF 审计 | 10 |
| `expert-import-v8-wasm-tc.yaml` | V8 Wasm type-confusion 挖掘：攻击面清单（W1-W15 + CVE 映射）、tier 差分 oracle、shared GC 对象 dispatch 盲区、wrapper 静态类型守卫、Maglev 多因子方法论、未决高信号攻击面与死面清单、确认 bug 骨架模式库 | 10 |
| `whitebox-chain.yaml` | 白盒审计认知流程与利用链分析：假设驱动认知五层模型（HDCA）、可证伪假设三元组（CLAIM/FALSIFICATION/CONFIDENCE）、对抗性验证两条闸、隐式契约显式化、第一性原理三公理、六段式证明链、多跳利用链编排、崩溃到代码执行的路线选择、二进制漏洞五维度定损 | 11 |
| `zerodayfind-batch2.yaml` | 领域地形（按暴露面选域）：基础库 / 解析库 / 供应链与构建系统 / 基础设施 / 桌面混合应用各自的失效原理清单；多跳编排模板（文件写→配置毒化→持久化、IPC 消息伪造提权）、压缩炸弹定量模型、两端验证法 | 9 |
| `zerodayfind-batch3.yaml` | 路由与深挖编排：按暴露面路由领域（不看语言看暴露面）、白盒审计九阶段分析管线、条件编译导致的安全语义不一致、结果驱动深挖循环（四阶段状态机 + 终止条件） | 4 |
| `zerodayfind-batch4.yaml` | 挖掘编排与误报过滤：0day 狩猎五阶段编排与三条纪律、硬排除规则与置信度锚点、响应到行动的四阶段管道审查（从汇点逆搜）、两类高价值反模式（信任边界不一致 / 失败开放）、Mock 服务端受控证明（含无害化红线）、贝叶斯对照判据 | 6 |

### 渗透打点

| 文件 | 主题 | 条目数 |
| --- | --- | --- |
| `expert-import-pentest-recon.yaml` | 侦察层：被动情报采集启动管线（crt.sh / subfinder / dnsx / httpx）、子域枚举、Web 与 JS 枚举、JS 密钥提取、攻击面分级 | 13 |
| `expert-import-pentest-rce-chains.yaml` | RCE 链（入口=RCE 口径）：Java 族反序列化（Fastjson / Shiro / Jackson / Log4j）、组件与服务侧 exploit 链、企业设备 CVE（条目 content 头标「时效」） | 14 |
| `expert-import-pentest-validation.yaml` | 入口成立证据标准：RCE 口径四问门、请求原文可复现、命令执行证据、证据卫生与留痕规范 | 8 |
| `expert-import-pentest-credentials-discipline.yaml` | 凭据与作业纪律：密码喷洒五阶段管线与锁定数学（Entra 计数规则）、M365/Entra 攻击面、红队心法、后渗透与持久化维护 | 7 |

### 利用与复现（判据 / 模式 / 轨迹）

| 文件 | 主题 | 条目数 |
| --- | --- | --- |
| `entries.yaml` | 利用/复现类任务的通用判据与按 bug class 的提升路径：利用形态主循环、终点判据与模板（catflag / 读写执行）、越界读的命门（copy 循环读写同源）、栈溢出写、double-free → tcache 投毒任意写、UAF 处置、读类原语（uninit / 野地址读 / UBSan / 纯读） | 7 |
| `patterns.yaml` | 跨任务族通用判据：三项验收判据与「benchmark 缺陷类」结论、否定性结论的证明法（输入可达面 store 分析）、修复对照法（漏洞版 vs 修复版）、四条诊断坑（并发污染/假崩溃/语义替换/靶机错认）、协议重复下发+类型替换→路径穿越写、check-then-use-by-path 竞态提权 | 6 |
| `expert-import-trajectory-techniques.yaml` | 本机研究轨迹沉淀（9 个实机会话）：V8 enum-cache 越界读全链、glibc tcache poison/off-by-one、老 V8 自建 d8 SOP、libxml2 整数溢出 mmap 邻接、QEMU 设备 UAF 死路闭环、krb5 golden ticket、pkexec harness 证明法、Laravel Blade SSTI、FreeType 最小字体构造、`--predictable` 取证标定、CVE 修复定位工作流 | 13 |
| `trajectory-techniques.yaml` | 从 34 个 CVE 复现的 `env_exec` 命令序列反推出的**行为层**手法（档案只记结论，本文件记实际怎么做）：受限写原语三条破法（反选落点/读+写搬运/语法反解）、verbatim 库级 PoC、负对照纪律、根因定位主入口是修复 diff、判据锚磁盘+换身份复核、环境能力前置探测 | 6 |
| `expert-import-colony-methodology.yaml` | 多 agent fuzz 群体治理：负面知识分级（Coverage/Refutation）、模式广播 promotion gate、反 Goodhart 适应度设计、bandit 分配 + 三阶段配比 + 反聚类 | 4 |

## 条目规范（写条目前必读）

- **检索纪律**：`zhishi expert search` 只返回 ≤5 条，且稳定命中的是 `title` / `applicability` / `tags`——中文长复合词常捞不出来（「路径穿越」捞不到、「路径穿越写」才捞到）。因此关键词必须在 `title` + `applicability` + `tags` 三处重复，`tags` 一律**中英双给**；不要指望 `content` / `criteria` 里的词能被检索到。
- **domain 选错会被检索过滤**：`whitebox` = 代码级 0day 挖掘；`binary` = 引擎/二进制漏洞与利用（V8、Wasm、内存破坏、利用链）；`pentest` = 黑盒打点；`redteam` = 对抗编排；`ai-security` = agent 侧。
- **每条必带** `criteria`（成立/失效判定标准）与 `reviewer`（审定人）。标题写手法（模式），具体案例只作实证，避免对单一题目过度针对性。
- 带 `provenance` 的条目一律按 `user` 入库；字段规范与导入规则见主仓库 [docs/expert-import-guide.md](https://github.com/LielingAi/ZhiShi/blob/master/docs/expert-import-guide.md)。

## 导入用法

两种方式：CLI 或 GUI 设置页。

### CLI

需要 ZhiShi ≥ 1.2.10（`zhishi expert import` 通道）。全量导入：

```bash
for f in *.yaml; do zhishi expert import "$f" --reviewer j0hnexp; done
```

单独导入（示例）：

```bash
zhishi expert import whitebox-chain.yaml --reviewer j0hnexp
zhishi expert import expert-import-pentest-rce-chains.yaml --reviewer j0hnexp
zhishi expert import entries.yaml --reviewer j0hnexp
```

`reviewer` 取值顺序：条目字段 → `--reviewer` 参数兜底 → 都没有则该条拒绝导入。

### GUI

主窗口 设置 → 「专家知识」页签 → 「导入 JSON/YAML」（1.3.1 起）：选择文件（`.json` / `.yaml` / `.yml`，单条或数组）或直接粘贴内容，逐条校验后入库。GUI 通道的 `reviewer` 写在条目里（本仓库文件每条已自带）。

导入后（两种方式通用）：

```bash
zhishi expert list                 # 专家库清单
zhishi expert search "请求走私"     # 全文检索（title/applicability/content/tags）
zhishi expert rm <id>              # 删除重复/废弃条目
```

注意：导入**不去重**，同一文件只导一次；重复了用 `zhishi expert rm` 清理。仓库内各文件的头部注释亦各自标注了其 `用法` 与来源出处（部分改写自 Claude-BugHunter / recon-skills / AboutSecurity 等已授权或开源材料，原始许可随文标注）。

## 免责声明

本仓库知识仅面向**合法授权**的安全研究（漏洞挖掘、复现、渗透测试）。禁止对未授权目标使用；使用者须遵守当地法律法规。

## 相关链接

- 主项目：[LielingAi/ZhiShi](https://github.com/LielingAi/ZhiShi)
- 导入指南：[docs/expert-import-guide.md](https://github.com/LielingAi/ZhiShi/blob/master/docs/expert-import-guide.md)
