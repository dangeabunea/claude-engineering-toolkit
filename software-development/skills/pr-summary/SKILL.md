---
name: pr-summary
description: Use when human needs a PR summary, branch summary, or readable description of changes for a code reviewer
tools: Grep, Glob, Read
---

Analyze current changes in a Git branch and summarize them. Keep summary short and concise.


## What
- Write the goal the changes in the PR are trying to achieve
- Mention key files or methods that are involved in the PR, but do not go deep in details. Only focus on things the reviewer might need to know
- Mention key decisions or implementation details if they are required to understand code better

## Output

Select a strategy based on the rules below, then **Read the file listed under `implementation:` and follow its formatting instructions exactly.**

**Strategy selection priority:** explicit `output=` arg > natural language in request > default.

### Strategies:

#### Bullet List

- default: true
- arg: `output=bullet-list`
- implementation: `resources/output-bullet-list.md`
- rules: Default, `output=bullet-list`, or when human specifies bullet list

#### Sentences

- default: false
- arg: `output=sentences`
- implementation: `resources/output-sentences.md`
- rules: `output=sentences`, or human specifies sentences, prose, or paragraphs

#### Detailed with Diagram

- default: false
- arg: `output=detailed`
- implementation: `resources/output-detailed-with-diagram.md`
- rules: `output=detailed`, or human specifies detailed summary, diagram, or visual. Useful for complex changes that span multiple classes or modules.

