# 为 OpenCode 安装 work-mate-flow

## 前置条件

- 已安装 [OpenCode.ai](https://opencode.ai)

## 安装

将 work-mate-flow 添加到你的 `opencode.json`（全局或项目级别）的 `plugin` 数组中：

```json
{
  "plugin": ["work-mate-flow@git+https://github.com/john/work-mate-flow.git"]
}
```

重启 OpenCode。

验证安装：询问"你有什么技能？"

## 使用

使用 OpenCode 原生的 `skill` 工具：

```
skill tool to list skills
skill tool to load <skill-name>
```

## 更新

```json
{
  "plugin": ["work-mate-flow@git+https://github.com/john/work-mate-flow.git#v1.0.0"]
}
```
