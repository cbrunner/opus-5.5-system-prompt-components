# Claude Opus 5.5 system prompt — split components

Public repo: https://github.com/cbrunner/opus-5.5-system-prompt-components

Reorganized extract of the public leak posted by [Pliny the Liberator](https://github.com/elder-plinius/CL4R1T4S/blob/main/ANTHROPIC/CLAUDE-OPUS-5.5.md) on 22 Sep 2026. Not an official Anthropic document.

The original leak is ~1.9 MB because it is a full session dump. The actual system prompt is the prefix before the first user turn: **262,652 characters / 976 lines ≈ 65k–70k tokens** with tools, or **~24k tokens** of instruction text without the JSON schemas.

## In this repo now

| Path | What it is |
|---|---|
| `01-tool-calling-instructions.md` | How to emit `{antml:function_calls}` |
| `03-deferred-tools-note.md` | Some tools load later |
| `06-between-agentic-and-memory.md` | Skills / cloud container / device-link / model-id notes |
| `08-parallel-tool-call-note.md` | Parallel vs dependent tool calls |
| `functions/INDEX.md` | All 63 tools listed at session start |
| `claude_behavior/` | Identity, legal/finance, mistakes, knowledge-cutoff slices |
| `NOTICE.md` | Source attribution |

Larger slices (`04-claude-behavior.md` ~8k tokens, `05-agentic-behavior.md` ~9k, `07-user-memory.md` ~6k, plus pretty-printed `functions/*.json`) were isolated locally and can be added in follow-up commits. Until then those sections are lines 85–976 of Pliny's file.

## Token cheat sheet

| Slice | Chars | Est. tokens |
|---|---:|---:|
| Whole system prefix (lines 1–976) | 263k | ~65–70k |
| Tool schemas | 167k | ~42k |
| Instruction text only | 95k | ~24k |
| `<claude_behavior>` | 31k | ~8k |
| `<agentic_behavior>` | 36k | ~9k |
| `<user_memory>` | 23k | ~6k |

## Surface

> You are Claude Code, Anthropic's official CLI for Claude, running within the Claude Agent SDK.

Configured model id: `claude-opus-5-5`. Knowledge cutoff in the prompt: end of June 2026.
