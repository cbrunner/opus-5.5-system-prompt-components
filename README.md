# Claude Opus 5.5 system prompt — split components

Public repo: https://github.com/cbrunner/opus-5.5-system-prompt-components

## Credit

**All of the underlying text comes from Pliny the Liberator.**

- Pliny extracted and published the full Opus 5.5 session dump on 22 September 2026
- Source file: [elder-plinius/CL4R1T4S — `ANTHROPIC/CLAUDE-OPUS-5.5.md`](https://github.com/elder-plinius/CL4R1T4S/blob/main/ANTHROPIC/CLAUDE-OPUS-5.5.md)
- Repo: [elder-plinius/CL4R1T4S](https://github.com/elder-plinius/CL4R1T4S)
- X: [@elder_plinius](https://x.com/elder_plinius)

This repo only splits and labels that public extract so it is easier to read. It is not an official Anthropic document, and it is not a new leak.

If you use or cite this split, credit **Pliny the Liberator** for the extraction.

For the same kind of artifact obtained the other way round, recorded off the wire rather than dumped from a session, see [OrcaPromptVault](https://github.com/Continuum-AI-Corp/OrcaPromptVault): the request as the client sent it, with the tool JSON separated out and the command that reproduces the capture. Useful as a cross-check on where a session dump ends and the system prefix begins.

## What we split

Pliny's file is ~1.9 MB / ~21.5k lines because it is a full **session dump** (system prefix + user turns + tool results + on-demand skill files). The actual system prompt is only the prefix before the first `--- [user turn] ---`:

**262,652 characters / 976 lines ≈ 65k–70k tokens** with tools, or **~24k tokens** of instruction text without the JSON schemas.

## Layout

| Path | What it is |
|---|---|
| `00-system-prefix.md` | Full system slot (tools + instructions) |
| `01-tool-calling-instructions.md` | How to emit `{antml:function_calls}` |
| `02-functions-block.md` | Raw `<functions>` blob |
| `03-deferred-tools-note.md` | Tools that load later |
| `04-claude-behavior.md` | Persona, products, refusals, tone, cutoff |
| `05-agentic-behavior.md` | Desktop / agent harness rules |
| `06-between-agentic-and-memory.md` | Skills, container, device link, model id |
| `07-user-memory.md` | Memory filesystem + privacy |
| `08-parallel-tool-call-note.md` | Parallel vs dependent tool calls |
| `functions/` | One pretty-printed JSON schema per tool |
| `claude_behavior/` | Subsections of `<claude_behavior>` |
| `agentic_behavior/` | Subsections of `<agentic_behavior>` |
| `user_memory/` | Privacy + memory-application slices |

## Token cheat sheet

| Slice | Chars | Est. tokens |
|---|---:|---:|
| Whole system prefix (lines 1–976 of Pliny's file) | 263k | ~65–70k |
| Tool schemas | 167k | ~42k |
| Instruction text only | 95k | ~24k |
| `<claude_behavior>` | 31k | ~8k |
| `<agentic_behavior>` | 36k | ~9k |
| `<user_memory>` | 23k | ~6k |

Estimates use ~3.93 characters/token on this mixed JSON+prose. Anthropic's published English rule of thumb is ~2.5 characters/token, which overstates the schema-heavy slices.

## Surface

> You are Claude Code, Anthropic's official CLI for Claude, running within the Claude Agent SDK.

Configured model id: `claude-opus-5-5`. Knowledge cutoff stated in the prompt: end of June 2026.
