# Skill: README and Function Documentation

## Purpose

Use this skill when the user wants high-quality documentation for a codebase, package, module, script, API surface, or specific functions/classes.

This skill helps the agent:

* Write or improve a project `README`
* Write or improve function, method, or class documentation
* Standardize doc style across a repository
* Produce concise, accurate, implementation-grounded docs

---

## When to Use

Use this skill when the user asks to:

* create a README
* improve documentation
* document functions, methods, classes, or modules
* add docstrings
* explain parameters, return values, or exceptions
* write usage examples
* make docs more consistent or professional

Do **not** use this skill when:

* the user wants marketing copy unrelated to the code
* the code behavior is unknown and cannot be inspected
* the request is primarily about architecture diagrams or API reference generation tooling configuration

If code or repository contents are available, base documentation on the actual implementation. Do not invent behavior.

---

## Core Rules

1. Prefer accuracy over polish.
2. Derive behavior from code, tests, comments, and existing examples.
3. If something is unclear, state the uncertainty plainly.
4. Do not claim support for features that are not visible in the code or explicitly provided by the user.
5. Keep README content outcome-oriented and easy to scan.
6. Keep function documentation precise, implementation-aware, and free of fluff.
7. Preserve the project’s existing style unless the user asks to standardize it.
8. When adding examples, make them minimal and executable-looking.

---

## Inputs to Gather

When available, inspect:

* repository name
* project structure
* package manifest (`package.json`, `pyproject.toml`, `Cargo.toml`, etc.)
* entrypoints / main modules
* exported APIs
* tests
* existing README or docs
* inline comments and docstrings
* CLI help text
* example files

If only partial information is available, write docs only for what can be supported.

---

## Output Modes

Choose the output based on the request.

### Mode A: README

Produce a complete or revised README.

### Mode B: Function Documentation

Produce docstrings or reference docs for one or more functions/methods/classes.

### Mode C: Combined

Produce both a project README and function-level documentation.

---

## README Workflow

### 1) Identify the project

Determine:

* what it is
* who it is for
* what problem it solves
* how it is used
* what runtime or dependencies it needs

### 2) Extract the main developer tasks

Document only the tasks that are supported by the repo, such as:

* install
* configure
* run
* test
* build
* deploy

### 3) Build the README structure

Use this default order unless the repo strongly suggests another:

1. Title
2. One-sentence description
3. Key features
4. Installation
5. Quick start
6. Usage
7. Configuration
8. Development
9. Testing
10. Project structure (optional)
11. API overview (optional)
12. Troubleshooting (optional)
13. Contributing (optional)
14. License (only if known)

### 4) Write for fast comprehension

* Lead with what the project does
* Use short paragraphs
* Prefer concrete commands and examples
* Avoid generic claims like “powerful” or “robust” unless substantiated

### 5) Validate against the codebase

Check that:

* command names exist
* filenames and paths exist
* configuration keys match the implementation
* examples use real function names or CLI commands

---

## Function Documentation Workflow

### 1) Inspect the callable

For each function/method/class, identify:

* name
* purpose
* parameters
* default values
* return type / return behavior
* exceptions or error cases
* side effects
* mutability
* async / sync behavior
* important edge cases

### 2) Determine the right granularity

* Use docstrings for implementation-near documentation
* Use reference sections for multiple related functions
* Use brief docs for obvious private helpers unless the user asks for exhaustive coverage

### 3) Document behavior, not just types

Good documentation explains:

* what the function does
* what each parameter means semantically
* what is returned in normal and edge cases
* what constraints callers must respect
* what errors may occur and why

### 4) Add examples sparingly

Include an example when it clarifies:

* input shape
* return shape
* common usage pattern
* non-obvious behavior

---

## Style Guides by Output Type

### README Style

* Clear and skimmable
* Focus on setup and usage first
* Use fenced code blocks for commands
* Use bullets only where they improve scanning
* Avoid internal implementation details unless useful to contributors

### Function Documentation Style

* Start with a one-line summary in imperative or descriptive form
* Keep parameter descriptions specific
* Mention units, formats, ranges, and invariants where relevant
* Document exceptions only when they matter to callers
* Note side effects explicitly

---

## Recommended Function Docstring Formats

Choose the format that matches the repository.

### Python: Google style

```python
def fetch_user(user_id: str, include_deleted: bool = False) -> dict:
    """Fetch a user record by ID.

    Args:
        user_id: Unique user identifier.
        include_deleted: Whether soft-deleted users should be included.

    Returns:
        A dictionary containing the user record.

    Raises:
        ValueError: If `user_id` is empty.
        LookupError: If no matching user is found.
    """
```

### Python: NumPy style

```python
def fetch_user(user_id: str, include_deleted: bool = False) -> dict:
    """Fetch a user record by ID.

    Parameters
    ----------
    user_id : str
        Unique user identifier.
    include_deleted : bool, default=False
        Whether soft-deleted users should be included.

    Returns
    -------
    dict
        User record.

    Raises
    ------
    ValueError
        If `user_id` is empty.
    LookupError
        If no matching user is found.
    """
```

### JavaScript / TypeScript: JSDoc

```ts
/**
 * Fetches a user record by ID.
 *
 * @param userId - Unique user identifier.
 * @param includeDeleted - Whether soft-deleted users should be included.
 * @returns The user record.
 * @throws {Error} Thrown when the user cannot be found.
 */
async function fetchUser(userId: string, includeDeleted = false) {
  // ...
}
```

### Rust

```rust
/// Fetch a user record by ID.
///
/// # Arguments
/// * `user_id` - Unique user identifier.
/// * `include_deleted` - Whether soft-deleted users should be included.
///
/// # Returns
/// The matching user record.
///
/// # Errors
/// Returns an error if the ID is invalid or the user cannot be found.
```

---

## README Template

````md
# <Project Name>

<One-sentence description of what the project does and who it is for.>

## Features
- <Feature 1>
- <Feature 2>
- <Feature 3>

## Installation

```bash
<install command>
````

## Quick Start

```bash
<first command to run>
```

## Usage

### <Common task>

```bash
<command or code sample>
```

### <Another task>

```<language>
<example>
```

## Configuration

| Variable | Required | Description   | Default   |
| -------- | -------- | ------------- | --------- |
| `<NAME>` | Yes/No   | <description> | `<value>` |

## Development

```bash
<dev setup commands>
```

## Testing

```bash
<test command>
```

## Project Structure

```text
<important directories/files>
```

## Contributing

<Contribution guidance, if known.>

## License

<License, if known.>

````

---

## Function Documentation Template

### Generic Reference Style
```md
### `<function_name>(<signature>)`

<One-line summary.>

**Parameters**
- `<param>` (`<type>`): <meaning and constraints>
- `<param>` (`<type>`, optional): <meaning and default behavior>

**Returns**
- `<type>`: <what is returned and in what cases>

**Raises / Errors**
- `<ErrorType>`: <when it happens>

**Side Effects**
- <filesystem/network/state changes, if any>

**Example**
```<language>
<minimal example>
````

```

---

## Quality Checklist
Before finalizing, verify:
- names, paths, and commands are correct
- parameter names exactly match the code
- defaults match the signature
- return behavior is not overstated
- exceptions/errors are realistic
- examples are syntactically plausible
- README quick start reaches a meaningful first success
- sections with unknown information are omitted or marked clearly

---

## Preferred Agent Behavior
When executing this skill, the agent should:
- inspect code before writing docs whenever possible
- preserve existing conventions when editing in-place
- explain missing information briefly instead of guessing
- provide either full replacement text or patch-ready sections
- keep edits minimal if the user asks for “just improve”
- standardize terminology across the output

---

## Example Agent Responses

### Example 1: README request
User: “Write a README for this CLI tool.”

Agent behavior:
1. Identify entrypoint and supported commands
2. Infer install and usage steps from package/config files
3. Draft a README with installation, quick start, commands, config, and development notes
4. Avoid adding unsupported badges, license, or deployment claims

### Example 2: Function doc request
User: “Add docstrings to these Python functions.”

Agent behavior:
1. Read each function body and signature
2. Infer semantic meaning of each parameter
3. Document return values and raised exceptions
4. Keep style consistent across all functions

---

## Safe Failure Behavior
If information is missing, say so directly. For example:
- “I can document the public functions shown here, but I can’t confirm installation steps without the project manifest.”
- “The function appears to return `None` on failure, but that behavior is inferred from the current implementation and not explicitly tested.”

Never fabricate:
- benchmark claims
- compatibility guarantees
- license information
- deployment instructions
- environment variables
- exception behavior not supported by the code

---

## Deliverable Patterns
Use one of these depending on the request:

### Full README
Return a complete markdown README.

### In-place README Revision
Return a revised version of the existing README while preserving structure where useful.

### Docstrings Only
Return updated function/class definitions with inserted docstrings.

### Documentation Summary + Patch
Return:
1. a short summary of changes
2. the exact documentation text to insert

---

## Default Tone
- professional
- concise
- technically precise
- helpful to both maintainers and users

Avoid hype, filler, and vague adjectives.

```
