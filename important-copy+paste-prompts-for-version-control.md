---
description: >-
  These are essential prompts one must use to commit their code to their VCS
  properly, and in human-developer-understandable format. Must use
---

# (Important) Copy+Paste Prompts for Version Control

### Prompt 1 - Generating Commit Messages

When you're done generating code with AI to implement a feature, fix a bug, or refactor some code, there will be changes to multiple code files, and it is almost impossible to properly order them and note down what exactly happened and write good commit messages, just by looking at it. Also, it is very exhausting.

However, writing good commit messages, grouping relevant files and in the right order, is essential for human reviewers. A good commit message will provide important context and saves time for human reviewers from wasting time trying to understand what every single line is doing, or sitting down in long PR review meetings.

So, every time, a usable change is made, irrespective of how many files were updated, use the following prompt with AI to create good commit messages and use them to commit your code. Here is the prompt:

{% code overflow="wrap" %}
```
Analyze the current changes, use Git CLI to read through the code changes, and give me the order of files (or batches of files) to commit, along with detailed and technical  commit messages for each commit based on what changed. carefully think through about how all the commit(s) builds on top of each other before writing the next one, and produce them.
```
{% endcode %}

### Prompt 2 - Generating PR Messages

Clear PR messages help with human reviews by recording the summary of the changes made, before vs after comparison, and to record the history of updates properly for future reference, guidance, and proof of work & liability.

Use this prompt after **Prompt 1**, to create a proper PR message and use the generated message when creating or updating pull requests. Here is the prompt:

{% code overflow="wrap" %}
```
Create a detailed PR message in markdown that i can copy, for the past {x} commits. Analyze every changes to the fullest using the git cli, read the full commit messages, and then generate a PR message that is very useful to a developer trying to review it would understand everything that was changed/updated/refactored/removed/deleted. Include details about before the PR and what was achieved with his PR as the result of the changes.
```
{% endcode %}

> **Note:** Replace {x} with the number of latest commits you want to be included, to generate the PR message
