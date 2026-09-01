# Durable Research Memory

[English](README.md)

一套轻量的 `AGENTS.md` 框架，让长期科研项目在切换 Agent 会话后仍能从可靠状态继续工作。

聊天记录是临时的，项目状态不应该是。这套框架把稳定规则、当前执行状态、研究方向和可选的组会沟通材料分开保存，让新会话依据已验证证据恢复工作，而不是重新口述大量上下文。

## 四层结构

| 层级 | 文件或系统 | 用途 |
| --- | --- | --- |
| 稳定规则 | `AGENTS.md` | 工程约束、记忆协议和更新纪律 |
| 当前状态 | `work_progress.md` 与 `work_progress/*.md` | 工作交接、阻塞、证据和明确的下一步 |
| 研究方向 | `RESEARCH_PROGRESS.md` | 假设、持久结论、决策和路线图 |
| 对外沟通 | 可选的飞书组会文档 | 面向读者的精炼研究叙事 |

核心区别是：`work_progress.md` 回答“现在正在发生什么”，`RESEARCH_PROGRESS.md` 回答“项目当前相信什么，以及为什么”。

## 快速开始

1. 将 [`AGENTS.md`](AGENTS.md) 复制到科研项目的仓库根目录。
2. 可选：将 [`templates/work_progress.md`](templates/work_progress.md) 复制为根目录的 `work_progress.md`。
3. 对长期科研项目，可选：将 [`templates/RESEARCH_PROGRESS.md`](templates/RESEARCH_PROGRESS.md) 复制为根目录的 `RESEARCH_PROGRESS.md`。
4. 用仓库中已验证的事实替换占位内容；未知信息明确写为未知，不要猜测。
5. 从仓库根目录启动 coding agent，并让它继续项目。

Codex 会在开展项目工作前读取 `AGENTS.md`，并支持从项目根目录到当前目录的分层指令。参见 [OpenAI 官方文档](https://developers.openai.com/codex/guides/agents-md)。

## 可选的飞书集成

框架本身不依赖飞书。如果希望 Agent 直接读取或更新飞书组会文档，需要先安装并认证官方 [Lark CLI](https://github.com/larksuite/cli)：

```sh
npx @larksuite/cli@latest install
lark-cli config init --new
lark-cli auth login --recommend
lark-cli auth status
```

部分配置步骤需要在浏览器中授权。不要把凭据写入仓库；只授予必需权限，并在项目专用文档中记录准确的目标文档链接。

## 设计规则

- 只保留一个精炼的根交接文件，主题文件必须确有必要才创建。
- 状态结论必须先有证据。
- 只在有意义的状态转换时更新，而不是每条命令后都更新。
- 稳定知识迁移到正式文档；过期进度直接替换，不堆积矛盾记录。
- 研究结论与单次实验日志、实现过程分离。
- 外部组会文档只是展示层，不是真相来源。
- 只有重复成功且稳定的流程才升级为项目 Skill；一次性流程不升级。

## 兼容性

该文件面向 Codex 设计，也适用于识别 [`AGENTS.md`](https://agents.md/) 约定的其他 coding agent。不同工具的发现与优先级规则可能不同，正式依赖前请先验证。

## 许可证

[MIT](LICENSE)
