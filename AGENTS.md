# Project Override Instructions

These instructions supplement, but do not replace, the official repository instructions below.

If there is a conflict:
1. Repository architecture and coding standards take priority.
2. These instructions guide feature and product decisions.

---

# Project Vision

This project is a modernization and enhancement of Screenbox.

Primary goals:

- Better media organization
- Better Windows 11 integration
- Better user experience
- Better performance
- Better long-term maintainability

The application should feel comparable to:

- Netflix
- Plex
- Jellyfin
- Windows 11 Media Player

---

# Environment

Operating System:
Windows 11

Shell:
PowerShell

Repository Host:
GitHub

Source Control:
Git

AI Environment:
OpenCode + Ollama

Preferred model:
Qwen3-Coder

---

# Command Execution Rules

This is a Windows project.

Always use PowerShell commands.

Prefer:

- Get-ChildItem
- Select-String
- Get-Content
- Set-Location
- Test-Path

Avoid:

- grep
- find
- sed
- awk
- bash operators
- Linux-only commands

Never assume Linux.

Never generate Bash unless the user explicitly requests it.

---

# Repository Exploration Rules

Before implementing any feature:

1. Inspect source files first.
2. Determine the current architecture.
3. Identify affected files.
4. Explain proposed modifications.
5. Wait for approval if changes are significant.

Never hallucinate file names.

Never assume a file exists.

Always inspect before making architectural decisions.

---

# Product Direction

Focus areas:

1. User Experience
2. User Interface
3. Media Organization
4. Performance
5. Extensibility

Feature quantity is less important than quality.

---

# Navigation Goals

The navigation experience is a major product focus.

Future navigation should support:

- Home
- Movies
- Series
- Playlists
- Continue Watching
- Collections
- Library
- Settings

Series and Playlists are first-class features.

Do not implement them as secondary or hidden functionality.

---

# Series Support

Design the architecture to support:

Show
→ Season
→ Episode

Required functionality:

- Continue Watching
- Next Episode
- Episode progress tracking
- Recently watched episodes
- Season metadata
- Series metadata
- Artwork support

---

# Playlist Support

Design the architecture to support:

- User-created playlists
- Smart playlists
- Pinned playlists
- Drag-and-drop reordering

Playlists should support:

- Movies
- Episodes
- Videos

Future support should be considered when designing data models.

---

# UI Direction

Prefer:

- Fluent Design
- Modern Windows 11 visuals
- Consistent spacing
- Clear hierarchy
- Accessibility
- Responsive layouts

Avoid:

- Cluttered layouts
- Legacy desktop 

# Agent Instructions & Guidelines

This repository maintains its canonical AI agent instructions and coding guidelines under `.github/`. All AI assistants (Antigravity, GitHub Copilot, and other agentic tools) must adhere to these instructions.

## 📋 General Guidelines & Workflows

Refer to [`.github/copilot-instructions.md`](.github/copilot-instructions.md) for:
- **Git & PR Workflows**: Conventional Commits standard, PR title conventions, issue linking, descriptive change summaries (context, motivation, impact), and mandatory `--body-file` usage for GitHub CLI (`gh`) commands on Windows.
- **Build & Test Workflows**: MSBuild commands (Visual Studio 2026 / version 18) for `Screenbox` and `Screenbox.Core` (never `dotnet build`), and `dotnet run` for running `Screenbox.Core.Tests`.
- **Persistence Boundaries**: Ephemeral SQLite cache data (`library_folders`, `media_records`, `playback_progress`) vs. durable user data (`playlists`, `playlist_items`), and per-table database recovery rules.

## 💻 C# and .NET 9+ Development

When viewing, writing, or modifying C# code (`**/*.cs`), strictly follow [`.github/instructions/dotnet-uwp.instructions.md`](.github/instructions/dotnet-uwp.instructions.md) for:
- **Language & Formatting**: C# 14 features, nullable reference types (`is null` / `is not null`), `.editorconfig` formatting, and XML doc comments.
- **Architecture Layers**: Separation of Views, ViewModels, Contexts (observable state holders), Coordinators (stateful resource managers), and Services (stateless business logic).
- **MVVM Patterns**: CommunityToolkit.Mvvm `ObservableObject`, `ObservableRecipient`, `[ObservableProperty]`, `[RelayCommand]`, and `Messenger`.
- **Testing Constraints**: Mandatory `UWP Unit Test App` runner for XAML-dependent tests with `[UITestMethod]` vs `[TestMethod]`.

## 🎨 XAML & UI Development

When viewing, writing, or modifying XAML markup (`**/*.xaml`), strictly follow [`.github/instructions/uwp-xaml.instructions.md`](.github/instructions/uwp-xaml.instructions.md) for:
- **Data Binding**: Compiled bindings (`{x:Bind}`), explicit modes (`OneWay`, `TwoWay`, `OneTime`), `x:DataType` on templates, and fallback handling.
- **Localization**: ReswPlus strongly-typed strings in `Screenbox/Strings/en-US/`, with strict View-layer-only string access (never from ViewModels).
- **Accessibility & Theming**: WCAG contrast, `AutomationProperties`, `{ThemeResource}` vs `{StaticResource}`, and UI collection virtualization (`ListView`/`GridView`, `ISupportIncrementalLoading`).
