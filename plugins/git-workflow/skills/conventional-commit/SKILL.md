---
name: conventional-commit
description: 'Prompt and workflow for generating conventional commit messages using a structured XML format. Guides users to create standardized, descriptive commit messages in line with the Conventional Commits specification, including instructions, examples, and validation. Always presents the proposed message and staged files for user review before committing.'
---

### Instructions

```xml
	<description>This file contains a prompt template for generating conventional commit messages. It provides instructions, examples, and formatting guidelines to help users write standardized, descriptive commit messages in accordance with the Conventional Commits specification.</description>
```

### Workflow

**Follow these steps:**

1. Run `git status` to review changed files.
2. Run `git diff` or `git diff --cached` to inspect changes.
3. Propose which files to stage. Do not stage anything the user has not agreed to.
4. Construct your commit message using the following XML structure.
5. **Stop and present for review.** Show the user:
   - the exact list of files that will be included in the commit, and
   - the full proposed commit message (subject, body and footer).
6. **Wait for explicit confirmation.** Only after the user approves both the files and the message, stage the approved files with `git add <file>` and run the commit. If the user asks for changes, revise and present again.

**Never commit automatically.** Do not run `git commit` (or `git commit --amend`, `git push`, or `git merge`) without the user's explicit approval of the proposed message and files in the current conversation.

### Commit Message Structure

```xml
<commit-message>
	<type>feat|fix|docs|style|refactor|perf|test|build|ci|chore|revert</type>
	<scope>()</scope>
	<description>A short, imperative summary of the change</description>
	<body>(optional: more detailed explanation)</body>
	<footer>(optional: e.g. BREAKING CHANGE: details, or issue references)</footer>
</commit-message>
```

### Examples

```xml
<examples>
	<example>feat(parser): add ability to parse arrays</example>
	<example>fix(ui): correct button alignment</example>
	<example>docs: update README with usage instructions</example>
	<example>refactor: improve performance of data processing</example>
	<example>chore: update dependencies</example>
	<example>feat!: send email on registration (BREAKING CHANGE: email service required)</example>
</examples>
```

### Validation

```xml
<validation>
	<type>Must be one of the allowed types. See <reference>https://www.conventionalcommits.org/en/v1.0.0/#specification</reference></type>
	<scope>Optional, but recommended for clarity.</scope>
	<description>Required. Use the imperative mood (e.g., "add", not "added").</description>
	<body>Optional. Use for additional context.</body>
	<footer>Use for breaking changes or issue references.</footer>
</validation>
```

### Final Step

```xml
<final-step>
	<precondition>The user has explicitly approved the proposed commit message and the list of files.</precondition>
	<cmd>git commit -m "type(scope): description"</cmd>
	<note>Replace with the approved message. Include body and footer if needed.</note>
</final-step>
```
