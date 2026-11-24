# TDesign 微信小程序 Agent Skill

面向支持 [Agent Skills 规范](https://agentskills.io/specification) 的 AI Agent，提供 TDesign 微信小程序组件库的本地参考。适合查阅组件注册路径、WXML 示例、属性、事件、插槽、样式变量，以及 Skyline 和 WebView 的兼容说明。

[Skill 入口](skills/tdesign-miniprogram/SKILL.md) 按类索引 75 篇参考文档，覆盖快速开始、主题、深色模式、更新日志和组件用法。

## 安装

### 从 GitHub 安装

仓库公开后，在要使用该 Skill 的项目目录运行以下命令。

```bash
npx skills add halifox/tdesign-miniprogram-skill --skill tdesign-miniprogram
```

按提示选择要安装到的 Agent。默认安装到当前项目，追加 `-g` 可安装到用户级。安装器需要 Node.js 22.20 或更高版本。详见 [skills CLI](https://github.com/vercel-labs/skills#install-a-skill)。

### 从本地目录安装

如果已下载或克隆本仓库，在要使用该 Skill 的项目目录运行以下命令，将路径替换为本仓库的实际路径。

```bash
npx skills add /path/to/tdesign-miniprogram-skill --skill tdesign-miniprogram
```

也可以把整个 `skills/tdesign-miniprogram/` 目录复制到所用 Agent 的 Skill 目录中。复制时保留 `SKILL.md`、`references/` 和 `LICENSE` 的相对位置。

## 使用示例

> 使用 tdesign-miniprogram Skill，给我一个微信小程序表单校验示例，包含组件注册、WXML 和提交校验逻辑。

## 文档来源和许可证

这是社区维护的文档整理项目。参考内容采集于 2026 年 11 月 24 日，每篇文档附有对应来源。上游资料来自 [TDesign 微信小程序官网](https://tdesign.tencent.com/miniprogram)、[TDesign 小程序仓库](https://github.com/Tencent/tdesign-miniprogram) 和 [TDesign 公共文档仓库](https://github.com/Tencent/tdesign-common)。

本项目采用 [MIT 许可证](LICENSE)，并保留了 TDesign 的原始版权声明。安装目录随附一份 [许可证](skills/tdesign-miniprogram/LICENSE)。
