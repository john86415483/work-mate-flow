# 为 OpenCode 安装 work-mate-flow

## 前置条件

- 已安装 [OpenCode.ai](https://opencode.ai)

## 安装

### 1. 确认安装范围

询问用户希望安装到全局还是当前项目：

- **全局安装**（默认）：添加到 `~/.config/opencode/opencode.json`
- **项目安装**：添加到当前项目的 `opencode.json`

### 2. 配置插件

在对应 `opencode.json` 的 `plugin` 数组中添加：

```json
{
  "plugin": ["work-mate-flow@git+https://github.com/john86415483/work-mate-flow.git"]
}
```

### 3. 重启 OpenCode

插件通过 OpenCode 的插件管理器自动安装，并注册所有 skill。

### 4. 验证安装

询问"你有什么技能？"确认 skill 已加载。

## 使用

使用 OpenCode 原生的 `skill` 工具：

```
skill tool to list skills
skill tool to load <skill-name>
```

## 更新

OpenCode 通过 git 包规范安装 work-mate-flow。某些 OpenCode 和 Bun 版本会锁定已解析的 git 依赖，重启可能不会自动获取最新提交。如更新未生效，清除 OpenCode 的包缓存或重新安装插件。

固定特定版本：

```json
{
  "plugin": ["work-mate-flow@git+https://github.com/john86415483/work-mate-flow.git#v1.0.0"]
}
```

## 故障排查

### 插件未加载

1. 检查日志：`opencode run --print-logs "hello" 2>&1 | grep -i work-mate-flow`
2. 验证 `opencode.json` 中的 plugin 配置
3. 确保使用最新版本的 OpenCode

### Skill 未找到

1. 使用 `skill` 工具列出已发现的 skill
2. 检查插件是否正常加载（见上方）

### 工具映射

当 skill 引用 Claude Code 工具时，使用 OpenCode 对应工具：
- `TodoWrite` → `todowrite`
- `Task` + 子代理 → `@mention` 语法
- `Skill` 工具 → OpenCode 原生 `skill` 工具
- 文件操作 → 原生工具
