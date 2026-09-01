# ZhiShiExpertKnowledge

[ZhiShi](https://github.com/LielingAi/ZhiShi)（安全研究 agent harness）官方共享的专家知识仓库。不定期分享经审定（reviewer）的专家知识，导入后进入 `expert.db`，在 harness 研究过程中按需检索注入。

## 目录内容

| 文件 | 主题 | 条目数 |
| --- | --- | --- |
| `expert-import-go-0day.yaml` | Go 0day 挖掘：cmd/go 工具链供应链、net/http 协议边界（HTTP/2 CONTINUATION 洪泛、请求走私）、crypto/tls 时序侧信道、x/crypto/ssh 握手面 | 11 |
| `expert-import-dotnet-0day.yaml` | .NET 0day 挖掘：Kestrel/ASP.NET Core 认证边界与请求走私、System.Formats.Nrbf 反序列化、NuGet/MSBuild 供应链、Runtime/WPF 审计 | 10 |

条目 `kind` 覆盖 `idea`（思路判断）/ `technique`（具体技术）/ `sop`（步骤流程），`domain` 统一 `whitebox`（代码级 0day 挖掘场景，域选错会被检索过滤）。每条均含 `criteria`（成立/失效判定标准）与 `reviewer`（审定人），符合专家知识入库规范；所引 CVE 已对 OSV 核实、源码路径已对 GitHub 核实。

## 导入用法

需要 ZhiShi ≥ 1.2.10（`zhishi expert import` 通道）：

```bash
zhishi expert import expert-import-go-0day.yaml --reviewer j0hnexp
zhishi expert import expert-import-dotnet-0day.yaml --reviewer j0hnexp
```

`reviewer` 取值顺序：条目字段 → `--reviewer` 参数兜底 → 都没有则该条拒绝导入。

导入后：

```bash
zhishi expert list                 # 专家库清单
zhishi expert search "请求走私"     # 全文检索（title/applicability/content/tags）
zhishi expert rm <id>              # 删除重复/废弃条目
```

注意：导入不去重，同一文件只导一次；重复了用 `zhishi expert rm` 清理。字段规范与导入规则详见主仓库 [docs/expert-import-guide.md](https://github.com/LielingAi/ZhiShi/blob/master/docs/expert-import-guide.md)。

## 免责声明

本仓库知识仅面向**合法授权**的安全研究（漏洞挖掘、复现、渗透测试）。禁止对未授权目标使用；使用者须遵守当地法律法规。

## 相关链接

- 主项目：[LielingAi/ZhiShi](https://github.com/LielingAi/ZhiShi)
- 导入指南：[docs/expert-import-guide.md](https://github.com/LielingAi/ZhiShi/blob/master/docs/expert-import-guide.md)
