# 龍魂 Kimi 技能集 / LongHun Kimi Skills

面向 [Kimi Code CLI](https://www.moonshot.cn/) 的技能集合，提供中文原生数字生态、三色审计、DNA追溯、通心译等能力。

## 包含技能

| 技能 | 目录 | 说明 |
|------|------|------|
| `longhun-memory-bootstrap` | `skills/longhun-memory-bootstrap/` | 多平台记忆归集启动器 |
| `longhun-priority-sort` | `skills/longhun-priority-sort/` | 龍魂三色审计优先级排序器 |
| `dragon-soul-agent` | `skills/dragon-soul-agent/` | 中文编程治理、通心译、DNA追溯智能体 |

## 安装

将本仓库克隆到任意位置，然后把需要的技能目录复制到 Kimi 的用户技能目录：

```bash
# 克隆仓库
git clone https://github.com/[OWNER]/longhun-kimi-skills.git

# 复制到 Kimi 用户技能目录
mkdir -p ~/.kimi-code/skills
cp -r longhun-kimi-skills/skills/* ~/.kimi-code/skills/
```

> 若希望仅在某个项目内使用，可复制到项目下的 `.kimi-code/skills/` 目录。

## 使用

复制完成后，在 Kimi 中提及对应关键词即可触发：

- **记忆启动**："启动记忆"、"读取记忆"、"bootstrap"
- **优先级排序**："帮我排序"、"按三色审计排优先级"
- **龍魂治理**："CNSH"、"中文编程"、"三色审计"、"DNA追溯"、"通心译"

## 配置

- `longhun-memory-bootstrap` 依赖本地脚本 `~/.longhun/scripts/longhun_memory_bootstrap.py`，请按自己的日志路径修改脚本。
- 六层来源链中的 `[YOUR_UID]` 请替换为你自己的标识符。

## 协议

默认采用 [CC BY-NC-SA 4.0](LICENSE)（署名-非商业性使用-相同方式共享）。

核心原则：
- 来源链不可切断
- DNA 标签不可移除
- 三色审计继承
- 非商业优先，商业使用需单独授权

## 贡献

欢迎提交 Issue 和 PR。首次贡献需通过 🔴 阻断级审计。
