# Conventional Commit using Commitlint and Commitzen Documentation

## Purpose
This document provides clear and consistent guidelines for writing commit messages in this repository. Adhering to these rules ensures that commit messages are clear, informative, and standardized, improving collaboration and code quality.

---

## Commit Message Structure

Each commit message must follow the structure below:



```
<type>(<scope>): <description>

[optional body]

[optional footer]

```


---

### 1. `<type>` (Required)

Describes the nature of the change. Use one of the allowed types listed below.

#### Allowed Types:

| Type       | Description                                                  |
|------------|--------------------------------------------------------------|
| `feat`     | A new feature                                                |
| `fix`      | A bug fix                                                    |
| `docs`     | Documentation changes only                                   |
| `style`    | Code style changes (formatting, missing semi-colons, etc.)   |
| `refactor` | Code change that neither fixes a bug nor adds a feature      |
| `perf`     | A code change that improves performance                      |
| `test`     | Adding or updating tests                                     |
| `build`    | Changes that affect the build system or dependencies         |   
| `ci`       | Changes to CI configuration files and scripts                |
| `chore`    | Miscellaneous tasks (e.g., build scripts, maintenance)       |
| `revert`   | Reverts a previous commit                                    |

#### Can't Decide on a Type?

If you're unsure which type to use:

- Default to `feat` if you’re **adding something new or enhancing existing functionality**.
- Default to `fix` if you’re **resolving an issue** or correcting behavior.

When in doubt, ask yourself:
- Does this change add something? → `feat`
- Does this change correct something? → `fix`

Using `feat` and `fix` consistently ensures clarity, even if you're unsure .

---
---
### 2. `<scope>` (Required)

Specifies the area of the codebase affected. Useful for large projects with multiple modules or distinct features.

A **scope** typically refers to a specific feature or module, follow your repository's feature folder. This helps in quickly identifying what part of the code a commit is related to. If you cannot find the scope then follow type labels and find appropriate label where you had changed.

**Examples of common scopes**:
example features
- `auth`
- `apollo`
- `ci`
example components
- `button`
- `dnd` 

#### Scope Naming Conventions:

- If the feature name has **multiple words**, use **kebab-case**:
- If a change affects **multiple scopes**, use **comma-separated** values:

example: 
`feat(auth,inventory):`

🛑 **no spaces in between till `:` i.e. colons**

- ✅ Try to limit to **one scope** per commit for clarity.
- 🚫 Avoid more than **two scopes** unless absolutely necessary.

---
---
### 3. `<description>` (Required)

The **description** is the main summary of your commit and appears right after the scope.

It should be:
- Written in **imperative mood** — as if you are **giving a command** or **telling someone what to do**
- **Short, clear, and to the point**
- Ideally **under 50 characters**
- There should be no space before the `:`, after `:` add a single space and add description
- The first letter **should not be uppercase**
- Important: **No period (`.`)** at the end

Think of it like finishing this sentence:  
**“If applied, this commit will...”**

So instead of writing:
- ❌ "fixed the login bug"  
- ✅ "fix login bug"

#### ✅ Examples (Imperative + Concise):
```
fix(auth): handle null token on login 

feat(ui): add drag-and-drop functionality 

docs(readme): update environment setup instructions

```
---

### 4. `Body` (Optional)

The **body** is an optional section that provides additional context about the commit. It should describe **what** the change does and **why** it was made — **not how**.

Use the body when a short description isn't enough to explain the purpose of the change. This is especially helpful for future contributors (including your future self) to understand the reasoning behind a change.

#### Guidelines:
- **Must have a line as a space 
- Wrap lines at **72 characters** to ensure good readability in various tools.
- Keep the tone **professional and informative**.
- Use the body to explain:
  - The motivation behind the change
  - Related background or context
  - Any design decisions or edge cases
  - Limitations or future considerations

#### ✅ Good Example:

```
feat(inventory): add order scheduling logic

Users can now schedule deliveries for future dates for inventory management. This change adds a new field to the delivery schema and updates the validation logic.

This prepares the system for subscription-based deliveries.
```


#### When to Use:

- The change introduces or affects **complex logic**
- The reason for the change is not obvious
- There is important context or follow-up work to mention

---


### 5. `Footer` (Optional)

The **footer** provides meta-information related to the commit, such as links to pull requests, ticket references (e.g., ClickUp), or special flags like breaking changes.

---

#### 🧱 Format Rules

- Must be separated from the body (or description, if no body) by **one empty line**
- Each footer entry should be on its own line
- Footer entries are used for:
  - Referencing PRs
  - Tracking ticket systems (e.g., ClickUp)
  - Declaring `BREAKING CHANGE`
  - Adding other context that tools or developers may use

---

#### 🔗 Referencing Pull Requests

Use this format to reference a related pull request:


This creates a clickable reference to **Refer #123(PR ID)** on most Git platforms (like GitHub or GitLab).

---

#### 📝 Referencing ClickUp Tasks

Use different keywords depending on the stage of the work related to a ClickUp task:

| Keyword      | When to Use                                              |
|--------------|----------------------------------------------------------|
| `fixes`      | Final commit that **completes and closes** the task      |
| `adds-to`    | Used for commits that **continue working** on a task or post fixes     |


You can add `adds-to` after fixes also, if there  are futher changes after fixes

**Examples:**


This allows ClickUp to automatically track and update ticket progress when used correctly.

---

#### ✅ Example of a complete good commit

```
feat(auth): add token expiration handling

Implements token expiry logic during authentication. This ensures
that users with expired tokens are prompted to re-authenticate,
improving security and reducing session-related errors.

The logic checks token age against server-configured expiry time and
invalidates access accordingly. Future improvements may include
refresh token support.

Refer #452
adds-to CU-123ticket
```
--- Description of above commit:
```
Description: add token expiration handling — imperative and concise

Body: Explains what and why, within 72-character line wraps

Footer: Includes both a PR reference (Refer #452) and a ClickUp reference (adds-to CU-123ticket)
```

---

## How to Write a Commit Message

Depending on the complexity of your change, you can write your commit message in one of two ways:

---

### 1. Single-Line Commit Message

Use the `git commit -m "....."` to add a quick commit message inline:

```
git commit -m "feat(auth): add login form validation"
```

Use the `git commit` to add a more detailed commit message:

```
git commit
feat(auth): add login form validation

Adds custom validation rules to prevent invalid form submissions.
Improves user experience and ensures cleaner backend data.

Refer #101
adds-to CU-456

```

### Generate a commit using Commitizen

To generate a commit, run the following command:

```bash
npm run commit
```
Follow the steps and **✅ Make sure validation rules are followed**