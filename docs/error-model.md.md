# Error Model – Errx

## Purpose
This document defines the **standardized internal representation of errors** in Error-Clarity.
The goal is to convert **all types of terminal errors** (Python, JavaScript, Rust, etc.) into a **consistent format** so that the AI agent can analyze and provide explanations, root-cause analysis, and fix suggestions reliably.

---

## 1. Core Fields

| Field | Type | Description | Example |
|-------|------|-------------|---------|
| `language` | string | Programming language where the error originated | `"Python"`, `"JavaScript"` |
| `error_type` | string | Specific type of the error | `"TypeError"`, `"SyntaxError"`, `"E0382"` |
| `message` | string | Raw error message | `"undefined is not a function"` |
| `file` | string | File where the error occurred | `"app.js"` |
| `line` | integer | Line number in the file | `42` |
| `stacktrace` | string[] | Array of stack frames, top-down | `["at foo() in app.js:42", "at main() in index.js:10"]` |
| `command` | string | Terminal command that produced the error | `"npm test"` |
| `exit_code` | integer | Process exit code | `1` |
| `timestamp` | string | ISO 8601 timestamp when error occurred | `"2026-01-16T14:32:00Z"` |

---

## 2. Optional Fields

| Field | Type | Description | Example |
|-------|------|-------------|---------|
| `dependencies` | string[] | Relevant dependencies at time of error | `["express@4.18.2", "axios@1.6.0"]` |
| `config_files` | string[] | Related configuration files | `["tsconfig.json", ".env"]` |
| `project_root` | string | Absolute path of project root | `"/home/user/projects/my-app"` |
| `notes` | string | Optional notes from CLI capture | `"Error happened during unit test run"` |

---

## 3. Guidelines for Usage

1. **Normalize all errors** from raw terminal or IDE output into this structure before passing to the AI agent.
2. **Always include mandatory fields** (`language`, `error_type`, `message`, `file`, `line`, `stacktrace`, `command`, `exit_code`, `timestamp`).
3. Optional fields should be **added when context is available**; they improve the AI agent’s accuracy.
4. Keep the structure **immutable** once captured, only enrich with additional context (dependencies, config_files) before AI analysis.
5. This structure should be **consistent across all programming languages** and terminal environments.

---

## 4. Example Error Object (JSON)

```json
{
  "language": "JavaScript",
  "error_type": "TypeError",
  "message": "undefined is not a function",
  "file": "app.js",
  "line": 42,
  "stacktrace": [
    "at foo() in app.js:42",
    "at main() in index.js:10"
  ],
  "command": "npm test",
  "exit_code": 1,
  "timestamp": "2026-01-16T14:32:00Z",
  "dependencies": ["express@4.18.2", "axios@1.6.0"],
  "config_files": ["tsconfig.json", ".env"],
  "project_root": "/home/user/projects/my-app",
  "notes": "Error happened during unit test run"
}
