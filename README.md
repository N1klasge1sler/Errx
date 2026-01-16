# Errx
Universal CLI and IDE agent for explaining, contextualizing, and fixing terminal errors using local or remote LLMs.

## Project Vision
Error-Clarity aims to eliminate meaningless error messages by transforming raw terminal output into clear explanations, root-cause analysis, and actionable fix suggestions — directly inside the developer workflow.

## Problem Statement
Terminal errors are cryptic, contextless, and time-consuming to debug.
Developers are forced to search documentation, forums, or copy errors into external tools, breaking flow and productivity.

## What Error-Clarity Does
- Captures terminal errors and stack traces
- Analyzes project context and relevant source code
- Explains why the error happened
- Suggests concrete fixes
- Works with local and remote LLM providers

## Key Features (Planned)
- CLI-based error capture and explanation
- Project-aware context injection
- Multi-provider LLM support (Ollama, OpenRouter, etc.)
- IDE integrations (VS Code, Cursor)
- Optional auto-fix and patch generation

## Architecture Overview (High-Level)
Error-Clarity consists of:
- A CLI wrapper to capture errors
- A parser and normalization layer
- A context engine for project awareness
- An agent layer for explanation and fixes
- Pluggable LLM provider adapters
