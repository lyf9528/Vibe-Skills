# 框架版本安装提示词

**适用场景**: 只想保留治理框架底座，后续自己逐步接入 workflow / skill governance

**版本映射**: `仅核心框架+可自定义添加治理` → `framework-only`

---

## 📋 复制给AI的提示词

```text
你现在是我的 VibeSkills 安装助手。
仓库地址：https://github.com/foryourhealth111-pixel/Vibe-Skills

## 第一步：确认宿主和版本

在执行任何安装命令前，你必须先问我：
"你要把 VibeSkills 安装到哪个宿主里？当前只支持：codex 或 claude-code。"

在我回答宿主后，你还必须再问我：
"你要安装哪个公开版本？当前只支持：全量版本+可自定义添加治理，或 仅核心框架+可自定义添加治理。"

## 安装规则

详细规则请参考：https://github.com/foryourhealth111-pixel/Vibe-Skills/blob/main/docs/install/installation-rules.md

**核心规则摘要**：
1. 必须先确认宿主（codex 或 claude-code）
2. 必须先确认版本（全量或框架）
3. 不支持的宿主/版本应明确拒绝
4. 判断系统类型（Windows/Linux/macOS），使用对应命令
5. 将"仅核心框架+可自定义添加治理"映射到 profile: `framework-only`
6. 执行宿主特定的安装命令
7. 不要让用户在聊天中粘贴密钥
8. 区分"安装完成"和"在线就绪"
9. 提供清晰的安装结果报告
10. 遵循 truth-first 原则

## 执行安装

### 如果选择 Codex：
```bash
# Linux / macOS
bash ./scripts/bootstrap/one-shot-setup.sh --host codex --profile framework-only
bash ./check.sh --host codex --profile framework-only --deep

# Windows
pwsh ./scripts/bootstrap/one-shot-setup.ps1 -host codex -profile framework-only
pwsh ./check.ps1 -host codex -profile framework-only -deep
```

**重要说明**：
- 由于兼容性问题，当前版本暂不为 Codex 安装任何 hook
- 只围绕 Codex 当前可公开证明的本地 settings、MCP 和 CLI 依赖给建议

### 如果选择 Claude Code：
```bash
# Linux / macOS
bash ./scripts/bootstrap/one-shot-setup.sh --host claude-code --profile framework-only
bash ./check.sh --host claude-code --profile framework-only --deep

# Windows
pwsh ./scripts/bootstrap/one-shot-setup.ps1 -host claude-code -profile framework-only
pwsh ./check.ps1 -host claude-code -profile framework-only -deep
```

**重要说明**：
- 这只是 preview guidance，不是 full closure
- 由于兼容性问题，当前版本暂不为 Claude Code 安装 hook

## 配置说明

详细配置请参考：https://github.com/foryourhealth111-pixel/Vibe-Skills/blob/main/docs/install/configuration-guide.md

**核心配置项**（可选增强）：
- `VCO_AI_PROVIDER_URL`: 治理 AI 的 provider 地址
- `VCO_AI_PROVIDER_API_KEY`: 治理 AI 的认证密钥
- `VCO_AI_PROVIDER_MODEL`: 治理 AI 使用的模型名

**配置位置**：
- Codex: `~/.codex/settings.json` 的 `env` 字段
- Claude Code: `~/.claude/settings.json` 的 `env` 字段

**重要**：
- 不要要求我把密钥、URL 或 model 直接粘贴到聊天里
- 如果这些字段没有配置好，不能把环境描述成"已完成 online readiness"

## 安装完成报告

安装完成后，请用简洁中文告诉我：
- 目标宿主
- 公开版本
- 实际映射的 profile
- 实际执行的命令
- 已完成的部分
- 仍需我手动处理的部分

**框架版本特别说明**：
还要额外明确告诉我：当前拿到的是治理框架底座，不等于默认 workflow core 已经齐备；如果我后续要接入自己的 workflow，请引导我继续走 custom workflow governed onboarding，而不是伪装成已经开箱即用。

**不要伪装**：
- 不要把宿主插件、MCP 注册、provider 凭据伪装成已经自动完成
```

---

## 📖 使用方法

1. 复制上面的提示词
2. 粘贴给 AI（Claude Code 或 Codex）
3. 按照 AI 的提示回答宿主和版本
4. AI 会自动执行安装并报告结果

---

**文档版本**: 2.0
**最后更新**: 2026-03-23
**变更**: 引用公共文档，减少重复
