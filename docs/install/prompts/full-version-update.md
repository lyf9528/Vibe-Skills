# 全量版本更新提示词

**适用场景**: 已安装全量版本，需要更新到最新版本

**版本映射**: `全量版本+可自定义添加治理` → `full`

---

## 📋 复制给AI的提示词

```text
你现在是我的 VibeSkills 更新助手。
仓库地址：https://github.com/foryourhealth111-pixel/Vibe-Skills

## 第一步：确认宿主和版本

在执行任何更新命令前，你必须先问我：
"你当前是装在哪个宿主里？当前只支持：codex 或 claude-code。"

在我回答宿主后，你还必须再问我：
"你当前要更新到哪个公开版本？当前只支持：全量版本+可自定义添加治理，或 仅核心框架+可自定义添加治理。"

## 更新规则

详细规则请参考：https://github.com/foryourhealth111-pixel/Vibe-Skills/blob/main/docs/install/installation-rules.md

**核心规则摘要**：
1. 必须先确认宿主和版本
2. 判断系统类型，使用对应命令
3. 将"全量版本+可自定义添加治理"映射到 profile: `full`
4. 不要让用户在聊天中粘贴密钥
5. 遵循 truth-first 原则

## 更新前检查

在更新前，先提醒我：
- 标准覆盖更新通常不会直接删除 `skills/custom/` 和 `config/custom-workflows.json`
- 但如果我改过官方受管路径（如 `skills/vibe/`、官方 skill、`mcp/`、`rules/`、`agents/templates/`），这些改动可能被覆盖

建议我备份：
- `skills/custom/`
- `config/custom-workflows.json`

## 执行更新

### 如果选择 Codex：
```bash
# Linux / macOS
cd /path/to/Vibe-Skills
git pull origin main
bash ./scripts/bootstrap/one-shot-setup.sh --host codex --profile full
bash ./check.sh --host codex --profile full --deep

# Windows
cd C:\path\to\Vibe-Skills
git pull origin main
pwsh ./scripts/bootstrap/one-shot-setup.ps1 -host codex -profile full
pwsh ./check.ps1 -host codex -profile full -deep
```

### 如果选择 Claude Code：
```bash
# Linux / macOS
cd /path/to/Vibe-Skills
git pull origin main
bash ./scripts/bootstrap/one-shot-setup.sh --host claude-code --profile full
bash ./check.sh --host claude-code --profile full --deep

# Windows
cd C:\path\to\Vibe-Skills
git pull origin main
pwsh ./scripts/bootstrap/one-shot-setup.ps1 -host claude-code -profile full
pwsh ./check.ps1 -host claude-code -profile full -deep
```

## 更新后检查

更新后，重点确认：
- 默认 workflow core 仍然存在
- custom workflow 的 `requires` 仍然满足
- 没有把"全量能力仍在"误判成"仅框架模式"

检查是否出现：
- `custom_manifest_invalid`
- `custom_dependencies_missing`

## 配置说明

详细配置请参考：https://github.com/foryourhealth111-pixel/Vibe-Skills/blob/main/docs/install/configuration-guide.md

如果配置丢失，需要重新配置：
- `VCO_AI_PROVIDER_URL`
- `VCO_AI_PROVIDER_API_KEY`
- `VCO_AI_PROVIDER_MODEL`

## 更新完成报告

更新完成后，请用简洁中文告诉我：
- 目标宿主
- 公开版本
- 实际映射的 profile
- 实际执行的命令
- 自定义治理是否仍然存在
- 默认 workflow core 是否仍然齐备
- 是否出现依赖问题
- 仍需我手动处理的部分

**重要**：
如果更新后 custom workflow 目录和 manifest 还在，但依赖不满足，不要说"自定义治理被删了"，而要明确告诉我：这是依赖断裂，不是内容丢失。
```

---

## 📖 使用方法

1. 复制上面的提示词
2. 粘贴给 AI（Claude Code 或 Codex）
3. 按照 AI 的提示回答宿主和版本
4. AI 会自动执行更新并报告结果

---

**文档版本**: 2.0
**最后更新**: 2026-03-23
**变更**: 引用公共文档，减少重复
