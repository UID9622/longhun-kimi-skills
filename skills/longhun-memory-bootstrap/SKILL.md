---
name: longhun-memory-bootstrap
description: |
  龍魂记忆启动器：多平台记忆归集压缩技能。
  当用户启动 Kimi、或说"启动记忆""读取记忆""加载日志""归集日记""压缩记忆""bootstrap"时，
  自动运行配置脚本，把 Kimi / Claude / CNSH / DragonSoul / longhun-system 等平台的记忆与操作日志
  压缩成摘要，并读给 Kimi 作为上下文。
  支持 DNA 追溯码、369/太极/易经/河图洛书/CNSH/龍魂关键词检索。
  同时集成 longhun_senses 感知模块：图片识别、语音识别、语音合成、情感化文本。
---

# 龍魂记忆启动器

## 触发条件（任一匹配即调用）

用户提到以下关键词时：
- "启动"、"开机"、"启动记忆"、"读取记忆"、"加载记忆"
- "归集日志"、"读取日记"、"压缩记忆"、"汇总记忆"
- "bootstrap"、"memory bootstrap"、"load memory"
- 用户刚启动 Kimi 后第一句话

**推荐**：使用 `lh-kimi` 启动器，一打开 Kimi 记忆已经准备好了。

## 配置

在使用前，请将本仓库的脚本复制到本地约定路径，或修改 `SKILL.md` 中的路径为你自己的路径：

```bash
export LONGHUN_HOME="${LONGHUN_HOME:-$HOME/.longhun}"
```

默认脚本位置：`$LONGHUN_HOME/scripts/longhun_memory_bootstrap.py`

## 执行流程

### 第一步：生成记忆摘要

```bash
python3 "$LONGHUN_HOME/scripts/longhun_memory_bootstrap.py"
```

该脚本会自动扫描并压缩：

| 平台/系统 | 来源路径 | 内容 |
|---|---|---|
| Kimi 自身 | `~/.kimi-code/sessions/.../wire.jsonl` | 操作留痕、工具调用、对话 |
| Claude | `~/.claude/history.jsonl` | 历史提示词、项目、会话 |
| CNSH 审计 | `~/.cnsh/logs/audit.log` | 命令级审计 |
| DragonSoul DNA | `~/.dragonsoul/dna_trace.db` | 操作链、DNA 编码 |
| 龍魂收割审计 | `~/dragon_soul/audit/harvester_audit.jsonl` | 代码收割审计 |
| 代码知识库 | `~/_work/dragon_knowledge.db` | 收割的源码记忆 |
| 链哈希 | `~/chain_hash.jsonl` | 链式审计哈希 |
| longhun 备份日志 | `~/longhun-system/logs/*` | 各类审计与同步日志 |

> 注意：上表路径为默认约定，实际路径请在脚本中按自己的目录结构配置。

### 第二步：读取生成的摘要

脚本会输出两个文件：
- `$LONGHUN_HOME/memory/latest_digest.json`（结构化数据）
- `$LONGHUN_HOME/memory/latest_digest.md`（人类可读摘要）

用 `Read` 工具读取 Markdown 摘要，向用户汇报关键信息。

### 第三步：汇报给用户

用中文汇报：
1. 本次归集了多少个平台/源
2. 最近有哪些关键操作/事件
3. DNA 追溯码
4. 369 / 太极 / 易经 / 河图洛书 / CNSH / 龍魂 关键词命中情况

## 公开模式

如果用户要求"公开数据""脱敏发布"，运行：

```bash
python3 "$LONGHUN_HOME/scripts/longhun_memory_bootstrap.py" --public-mode
```

该模式会输出 `$LONGHUN_HOME/memory/public_digest.json`，已脱敏用户名、路径、IP、密钥。

## 龍魂感知模块 (longhun_senses)

当用户提到"识别图片""读图片""图片里有什么""看图""视觉识别"时，调用：

```bash
python3 "$LONGHUN_HOME/scripts/longhun_senses/senses_cli.py" vision <图片路径> [--context "额外上下文"]
```

当用户提到"语音转文字""语音识别""把录音转成文字""transcribe"时，调用：

```bash
python3 "$LONGHUN_HOME/scripts/longhun_senses/senses_cli.py" stt <音频路径> [--language Chinese]
```

当用户提到"文字转语音""读出来""朗读""speak""TTS"时，调用：

```bash
python3 "$LONGHUN_HOME/scripts/longhun_senses/senses_cli.py" tts "要朗读的文字" [--no-play]
```

当用户提到"加情感""情感化""有感情地读""soul""SSML"时，调用：

```bash
python3 "$LONGHUN_HOME/scripts/longhun_senses/senses_cli.py" soul "要情感化的文字" [--style storyteller]
```

可用的 `style`：`storyteller`（讲故事）、`educator`（教育）、`passionate`（激情）、`calm`（平静）。

## 注意事项

- 如果脚本输出报错，先检查 Python3 是否可用，再检查路径是否存在。
- 每次调用会重新生成摘要，覆盖旧文件。
- 用户只使用 Kimi 作为主控编辑器，因此本技能是启动后的首要任务。
- 原始日志严禁直接开源；公开数据必须使用 `--public-mode`。
- longhun_senses 需要的依赖：`anthropic`（视觉/情感）、`elevenlabs`（TTS）、`openai-whisper` + `ffmpeg`（STT）。
