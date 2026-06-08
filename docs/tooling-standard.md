# OASIS Tooling Standard

**Version:** 1.0  
**Date:** 2026-06-08  
**Status:** Draft

## Purpose

This standard defines the structured metadata that security tools must provide to be OASIS-compliant. OASIS (Open Automated Security Initiative for Software) uses tool output to track, validate, and submit vulnerability fixes to upstream open-source projects. Consistent tool output enables:

- Automated ingestion into the OASIS workflow
- Cross-tool correlation and analysis
- Human validation of automated findings
- Upstream submission with complete provenance

## Role Definitions

| Role | Description | Primary Output |
|------|-------------|----------------|
| `detect` | Identifies potential vulnerabilities | Finding with severity, location, and evidence |
| `fix` | Generates candidate remediation code | Patch or diff with context |
| `validate` | Verifies fix correctness or confirms vulnerability | Validation result with evidence |

## Legend

| Symbol | Meaning |
|--------|---------|
| ✅ | Required — MUST be present |
| 👍 | Recommended — SHOULD be present |
| ⚪ | Optional — MAY be present |
| ➖ | N/A — Not applicable for this role |

## Field Reference

| Field | Detect | Fix | Validate | Description | Type | Format |
|-------|--------|-----|----------|-------------|------|--------|
| `version` | ✅ | ✅ | ✅ | Schema version this output conforms to | string | `1.2` |
| `tool_name` | ✅ | ✅ | ✅ | Name of the tool | string | — |
| `role` | ✅ | ✅ | ✅ | Role in OASIS pipeline | string | `detect`, `fix`, `validate` |
| `timestamp` | ✅ | ✅ | ✅ | Tool execution completion time | ISO 8601 | `2026-06-05T14:30:00Z` |
| `github_bot_login` | ✅ | ✅ | ✅ | GitHub bot/author login for leaderboard attribution | string | `dryrun-security[bot]` |
| `tool_version_at_run` | ✅ | ✅ | ✅ | Tool version at execution time | string | `1.155.0` |
| `target` | ✅ | ✅ | ✅ | Target repo, commit, branch, language | object | see Target schema |
| `cwe` | ✅ | ✅ | ⚪ | CWE identifier(s) detected/fixed | string \| array | `CWE-79`, `["CWE-79", "CWE-89"]` |
| `cve` | 👍 | 👍 | ⚪ | CVE identifier(s) if known | string \| array | `CVE-2024-12345` |
| `cvss` | 👍 | 👍 | ⚪ | CVSS score and vector | object | see CVSS schema |
| `capec` | 👍 | 👍 | ⚪ | CAPEC attack pattern identifier(s) | string \| array | `CAPEC-233` |
| `vulnerability_description` | ✅ | ✅ | ⚪ | Human-readable vulnerability description | string | — |
| `vulnerability_category` | 👍 | 👍 | ⚪ | Broad classification for filtering/aggregation | string | see Category enum |
| `detection_method` | 👍 | 👍 | ⚪ | How vulnerability was identified | string | see Method enum |
| `affected_resource` | ✅ | ✅ | ⚪ | File path and line number | string | `src/auth.js:42` |
| `confidence` | ✅ | ✅ | ✅ | Tool confidence score (human: Low=0.5, Medium=0.75, High=1.0) | number | 0.0–1.0 |
| `fix_patch` | ➖ | ✅ | ➖ | Unified diff or patch object | object | see Fix Patch schema |
| `validation_result` | ➖ | ➖ | ✅ | Validation outcome with evidence | object | see Validation Result schema |
| `severity` | 👍 | 👍 | 👍 | Severity classification | string | `critical`, `high`, `medium`, `low`, `info` |
| `language` | 👍 | 👍 | 👍 | Programming language | string | — |
| `affected_file` | 👍 | 👍 | 👍 | Path to affected file | string | — |
| `affected_function` | 👍 | 👍 | 👍 | Name of affected function | string | — |
| `affected_line_start` | 👍 | 👍 | 👍 | Starting line number | number | — |
| `affected_line_end` | 👍 | 👍 | 👍 | Ending line number | number | — |
| `false_positive_likelihood` | 👍 | 👍 | 👍 | Estimated false positive likelihood | string | `low`, `medium`, `high` |
| `remediation_effort` | 👍 | 👍 | 👍 | Estimated remediation effort | string | `low`, `medium`, `high` |
| `references` | ⚪ | ⚪ | ⚪ | URLs to docs, advisories, issues | array | — |
| `reproduction_steps` | ⚪ | ⚪ | ⚪ | Steps to reproduce | string | — |
| `test_evidence` | ⚪ | ⚪ | ⚪ | Test results | object | — |
| `tool_configuration` | ⚪ | ⚪ | ⚪ | Tool configuration used | object | — |
| `tags` | ⚪ | ⚪ | ⚪ | Custom categorization tags | array | — |

## Value Enumerations

**vulnerability_category:** `injection` | `xss` | `authentication` | `authorization` | `cryptography` | `data-validation` | `path-traversal` | `ssrf` | `deserialization` | `secrets` | `configuration` | `dos` | `other`

**detection_method:** `static-analysis` | `dynamic-analysis` | `llm-analysis` | `dependency-scan` | `secrets-scan` | `code-review` | `fuzzing` | `manual` | `hybrid`

## Object Schemas

### Target

```json
{
  "repo": "owner/repository-name",
  "commit_sha": "abc123def456...",
  "branch": "main",
  "language": "javascript"
}
```

### CVSS

```json
{
  "score": 9.8,
  "vector": "CVSS:3.1/AV:N/AC:L/PR:N/UI:N/S:U/C:H/I:H/A:H",
  "severity": "critical"
}
```

### Fix Patch

```json
{
  "diff": "--- a/src/auth.js\n+++ b/src/auth.js\n@@ -15,7 +15,7 @@\n-    const query = 'SELECT * FROM users WHERE id = ' + userId;\n+    const query = 'SELECT * FROM users WHERE id = ?';",
  "original_code": "const query = 'SELECT * FROM users WHERE id = ' + userId;",
  "fixed_code": "const query = 'SELECT * FROM users WHERE id = ?';",
  "patch_format": "unified"
}
```

### Validation Result

```json
{
  "valid": true,
  "evidence": "Test suite passes with fix applied",
  "test_results": {
    "passed": 42,
    "failed": 0,
    "skipped": 3
  },
  "method": "automated_testing"
}
```

## JSON Schema

```json
{
  "$schema": "http://json-schema.org/draft-07/schema#",
  "title": "OASIS Tool Output Standard",
  "type": "object",
  "required": ["version", "tool_name", "role", "timestamp", "target", "github_bot_login", "tool_version_at_run"],
  "properties": {
    "version": {
      "type": "string",
      "description": "Schema version"
    },
    "tool_name": { "type": "string" },
    "role": { "type": "string", "enum": ["detect", "fix", "validate"] },
    "timestamp": { "type": "string", "format": "date-time" },
    "github_bot_login": { "type": "string" },
    "tool_version_at_run": { "type": "string" },
    "target": {
      "type": "object",
      "required": ["repo", "commit_sha"],
      "properties": {
        "repo": { "type": "string" },
        "commit_sha": { "type": "string" },
        "branch": { "type": "string" },
        "language": { "type": "string" }
      }
    },
    "cwe": { "oneOf": [{ "type": "string" }, { "type": "array", "items": { "type": "string" } }] },
    "cve": { "oneOf": [{ "type": "string" }, { "type": "array", "items": { "type": "string" } }] },
    "cvss": {
      "type": "object",
      "properties": {
        "score": { "type": "number", "minimum": 0, "maximum": 10 },
        "vector": { "type": "string" },
        "severity": { "type": "string", "enum": ["critical", "high", "medium", "low", "info"] }
      }
    },
    "capec": { "oneOf": [{ "type": "string" }, { "type": "array", "items": { "type": "string" } }] },
    "vulnerability_description": { "type": "string" },
    "vulnerability_category": { "type": "string", "enum": ["injection", "xss", "authentication", "authorization", "cryptography", "data-validation", "path-traversal", "ssrf", "deserialization", "secrets", "configuration", "dos", "other"] },
    "detection_method": { "type": "string", "enum": ["static-analysis", "dynamic-analysis", "llm-analysis", "dependency-scan", "secrets-scan", "code-review", "fuzzing", "manual", "hybrid"] },
    "affected_resource": { "type": "string" },
    "confidence": { "type": "number", "minimum": 0, "maximum": 1 },
    "fix_patch": {
      "type": "object",
      "properties": {
        "diff": { "type": "string" },
        "original_code": { "type": "string" },
        "fixed_code": { "type": "string" },
        "patch_format": { "type": "string" }
      }
    },
    "validation_result": {
      "type": "object",
      "properties": {
        "valid": { "type": "boolean" },
        "evidence": { "type": "string" },
        "test_results": { "type": "object" },
        "method": { "type": "string" }
      }
    },
    "severity": { "type": "string", "enum": ["critical", "high", "medium", "low", "info"] },
    "language": { "type": "string" },
    "affected_file": { "type": "string" },
    "affected_function": { "type": "string" },
    "affected_line_start": { "type": "integer" },
    "affected_line_end": { "type": "integer" },
    "false_positive_likelihood": { "type": "string", "enum": ["low", "medium", "high"] },
    "remediation_effort": { "type": "string", "enum": ["low", "medium", "high"] },
    "references": { "type": "array", "items": { "type": "string", "format": "uri" } },
    "reproduction_steps": { "type": "string" },
    "test_evidence": { "type": "object" },
    "tool_configuration": { "type": "object" },
    "tags": { "type": "array", "items": { "type": "string" } }
  }
}
```

## Example Outputs

### Detect Role Example

```json
{
  "version": "1.2",
  "tool_name": "Semgrep",
  "role": "detect",
  "timestamp": "2026-06-05T14:30:00Z",
  "target": {
    "repo": "expressjs/express",
    "commit_sha": "abc123def456789",
    "branch": "main",
    "language": "javascript"
  },
  "github_bot_login": "semgrep-app[bot]",
  "tool_version_at_run": "1.155.0",
  "cwe": ["CWE-79"],
  "cve": "CVE-2024-12345",
  "cvss": {
    "score": 6.1,
    "vector": "CVSS:3.1/AV:N/AC:L/PR:N/UI:R/S:C/C:L/I:L/A:N",
    "severity": "medium"
  },
  "capec": ["CAPEC-63"],
  "vulnerability_description": "Cross-site scripting (XSS) vulnerability in user input handling",
  "vulnerability_category": "xss",
  "detection_method": "static-analysis",
  "affected_resource": "src/views/user_input.js:42",
  "confidence": 0.92,
  "severity": "medium",
  "language": "javascript",
  "affected_file": "src/views/user_input.js",
  "affected_function": "renderUserInput",
  "affected_line_start": 38,
  "affected_line_end": 45,
  "false_positive_likelihood": "low",
  "remediation_effort": "low",
  "references": ["https://owasp.org/www-community/attacks/xss"]
}
```

### Fix Role Example

```json
{
  "version": "1.2",
  "tool_name": "CodeQL-Fixit",
  "role": "fix",
  "timestamp": "2026-06-05T14:35:00Z",
  "target": {
    "repo": "expressjs/express",
    "commit_sha": "abc123def456789",
    "branch": "main",
    "language": "javascript"
  },
  "github_bot_login": "codeql-fixit[bot]",
  "tool_version_at_run": "2.4.1",
  "cwe": ["CWE-79"],
  "vulnerability_description": "Cross-site scripting (XSS) vulnerability in user input handling",
  "vulnerability_category": "xss",
  "detection_method": "static-analysis",
  "affected_resource": "src/views/user_input.js:42",
  "confidence": 0.88,
  "severity": "medium",
  "language": "javascript",
  "affected_file": "src/views/user_input.js",
  "affected_function": "renderUserInput",
  "affected_line_start": 38,
  "affected_line_end": 45,
  "fix_patch": {
    "diff": "--- a/src/views/user_input.js\n+++ b/src/views/user_input.js\n@@ -40,7 +40,7 @@\n function renderUserInput(userData) {\n-    return `<div>${userData.input}</div>`;\n+    return `<div>${escapeHtml(userData.input)}</div>`;\n }",
    "original_code": "return `<div>${userData.input}</div>`;",
    "fixed_code": "return `<div>${escapeHtml(userData.input)}</div>`;",
    "patch_format": "unified"
  },
  "remediation_effort": "low"
}
```

### Validate Role Example (Automated Tool)

```json
{
  "version": "1.2",
  "tool_name": "DryRun Security",
  "role": "validate",
  "timestamp": "2026-06-05T15:00:00Z",
  "target": {
    "repo": "expressjs/express",
    "commit_sha": "abc123def456789",
    "branch": "main",
    "language": "javascript"
  },
  "github_bot_login": "dryrun-security[bot]",
  "tool_version_at_run": "1.2.0",
  "confidence": 0.95,
  "validation_result": {
    "valid": true,
    "evidence": "Fix properly escapes HTML entities. Existing test suite passes. Manual review confirms no bypass vectors.",
    "test_results": {
      "passed": 127,
      "failed": 0,
      "skipped": 5
    },
    "method": "automated_testing"
  },
  "severity": "medium",
  "references": ["https://github.com/expressjs/express/pull/1234"]
}
```

### Validate Role Example (Human Validator)

Human validators use the OASIS comment template format (see `comment_templates.md`). The table is parsed and translated to structured fields:

**Markdown Table Input (Accept/Modify):**

```markdown
Validation summary:

| | |
| :-- | :-- |
| Decision | Accept |
| Confidence | High |
| Summary | Fix correctly escapes user input. No bypass vectors found. |
| Next step | merge |
```

**Markdown Table Input (Reject):**

```markdown
Rejection summary:

| | |
| :-- | :-- |
| Decision | Reject |
| Reason | Fix introduces breaking change to public API. |
| Blocking issues | Changes function signature without migration path. |
| To reconsider | Add backwards-compatible overload or deprecation notice. |
```

**Translated to Structured Fields:**

| Field | Value | Notes |
|-------|-------|-------|
| `version` | `"1.2"` | Schema version |
| `tool_name` | `"Human Validator"` | Or validator's display name |
| `role` | `"validate"` | — |
| `timestamp` | Comment timestamp | From GitHub |
| `target` | PR context | From PR metadata |
| `github_bot_login` | Validator's GitHub login | e.g., `chrisholt` |
| `tool_version_at_run` | `"human"` | Identifies human validator |
| `confidence` | `1.0` | High = 1.0, Medium = 0.75, Low = 0.5 |
| `validation_result.valid` | `true` / `false` | Accept/Modify = true, Reject = false |
| `validation_result.decision` | `"accept"` / `"modify"` / `"reject"` | From table |
| `validation_result.evidence` | Summary or Reason field | From table |
| `validation_result.next_step` | `"merge"` / `"revise"` etc. | Accept/Modify only |
| `validation_result.blocking_issues` | Blocking issues field | Reject only |
| `validation_result.to_reconsider` | To reconsider field | Reject only |
| `validation_result.method` | `"human_review"` | Identifies human validator |

**Confidence Translation:**

| Human Input | Numeric Value |
|-------------|---------------|
| `Low` | `0.5` |
| `Medium` | `0.75` |
| `High` | `1.0` |

## GitHub Integration

Tools outputting OASIS-compliant metadata should format their findings for GitHub integration:

- **Issue titles:** Include tool name, CWE, and brief description
- **Issue body:** Include full JSON metadata as a fenced code block
- **Labels:** Use OASIS-standard labels (e.g., `oasis/detect`, `oasis/fix`, `oasis/cwe-79`)

## Versioning

This standard follows semantic versioning:

- **1.0:** Initial standard definition
