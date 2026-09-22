# Claude Opus 5.5 system prompt — split components

This repo is a **reorganized extract** of the public Claude Opus 5.5 system-prompt leak posted by [Pliny the Liberator](https://github.com/elder-plinius/CL4R1T4S/blob/main/ANTHROPIC/CLAUDE-OPUS-5.5.md) on 22 Sep 2026.

The original file is ~1.9 MB / ~21.5k lines because it is a **full session dump** (system prefix + user turns + tool results + on-demand `SKILL.md` files). This repo keeps only the **actual system prefix**: everything before the first `--- [user turn] ---`.

That prefix is **262,652 characters / 976 lines**, about **65k–70k tokens** with tools, or about **24k tokens** of instruction text if you strip the JSON schemas.

This is **not** an official Anthropic document. It is a study split of a public leak. Do not treat it as current product policy.

## Layout

```
00-system-prefix.md                 full system slot (tools + instructions)
01-tool-calling-instructions.md     how to emit {antml:function_calls}
02-functions-block.md               raw <functions> blob from the prefix
03-deferred-tools-note.md           note that some tools load later
04-claude-behavior.md               persona, products, refusals, tone, cutoff
05-agentic-behavior.md              how the desktop/agent harness should work
06-between-agentic-and-memory.md    untagged bridge text
07-user-memory.md                   memory filesystem + privacy rules
08-parallel-tool-call-note.md       last line of the system prefix

functions/                          one pretty-printed JSON schema per tool
claude_behavior/                    subsections of <claude_behavior>
agentic_behavior/                   subsections of <agentic_behavior>
user_memory/                        privacy_requirements + memory_application
```

## Size cheat sheet

Estimates use ~3.93 characters/token (tiktoken-style proxy on this mixed JSON+prose). Anthropic's published English rule of thumb is ~2.5 characters/token, which overstates JSON-heavy slices.

| File | Chars | Est. tokens |
|---|---:|---:|
| `00-system-prefix.md` (whole system slot) | 263k | ~65–70k |
| Tool schemas (`02-functions-block.md`) | 167k | ~42k |
| Instruction text only (`04`+`05`+`06`+`07`+`08`) | 95k | ~24k |
| `<claude_behavior>` only | 31k | ~8k |
| `<agentic_behavior>` | 36k | ~9k |
| `<user_memory>` | 23k | ~6k |

## What this surface is

The prefix identifies itself as:

> You are Claude Code, Anthropic's official CLI for Claude, running within the Claude Agent SDK.

It also carries consumer-product copy (`<product_information>`), artifact/browser/device-bridge rules, and a memory filesystem. So this is a **Claude Code / Agent SDK / desktop-agent** harness, not the slim published claude.ai prompt and not a raw API `system` string.

63 tools are listed at session start. The prefix says additional tools can be injected later via `<function>` blocks.

## Source

- Leak: https://github.com/elder-plinius/CL4R1T4S/blob/main/ANTHROPIC/CLAUDE-OPUS-5.5.md
- Model: `claude-opus-5-5`, announced 22 Sep 2026
- Knowledge cutoff stated in the prompt: end of June 2026

## Method

1. Take lines 1–976 of the leak (before the first user turn).
2. Split on the major XML tags already in the text.
3. Parse each `<function>{...}</function>` line into `functions/*.json`.

Conversation turns, tool results, and on-demand skill files from the rest of the 1.9 MB dump are **not** included. Get those from Pliny's file if you need them.
