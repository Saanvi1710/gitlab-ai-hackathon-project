# Test Health Intelligence Agent

> A GitLab Duo custom agent that autonomously audits a repository's test suite across five dimensions and generates a prioritised health report with concrete fixes — so developers spend less time chasing bugs and more time shipping features.

---

## Overview

Poor test quality is one of the most expensive hidden problems in software development. Flaky tests erode team trust. Brittle tests shatter during refactors. Missing edge cases let critical bugs slip into production. Most AI tools can *generate* tests, but none reason about the *health* of an existing test suite.

**Test Health Intelligence Agent** changes that. Point it at any GitLab repository and it performs a deep, multi-dimensional audit — reading your source code, analysing your test files, examining your pipeline history — then produces a structured Test Health Report as a GitLab Issue and writes fixed versions of the most critical problems it finds.

This agent was built for the [GitLab AI Hackathon](https://gitlab.com/gitlab-ai-hackathon) as a demonstration of what agentic AI can do when given access to the full context of a living software project.

---

## The Five Dimensions

| Dimension | What It Catches |
|---|---|
| 🎲 **Flaky Tests** | `datetime.now()` without mocking, real network calls, timezone-dependent logic |
| 🔩 **Brittle Tests** | Tests coupled to private attributes, internal data formats, implementation details |
| 🕳 **Missing Edge Cases** | Empty inputs, boundary values, invalid types, uncovered exception paths |
| 🔗 **Integration Gaps** | Untested boundaries between modules, external services, and APIs |
| 📝 **Documentation Quality** | Cryptic test names, missing docstrings, no clear assertion intent |

---

## How It Works

When triggered via GitLab Duo Chat, the agent runs a seven-step autonomous workflow:

```
1. List repository tree          → understand project structure
2. Find and read all test files  → analyse what is being tested
3. Read all source files         → understand what should be tested
4. Examine pipeline history      → detect flakiness patterns over time
5. Perform five-dimension audit  → identify every category of problem
6. Create a GitLab Issue         → structured Test Health Report with scores
7. Write fixed test files        → concrete, ready-to-use fixes for top issues
```

No human is in the loop between steps. The agent reasons, decides, and acts autonomously.

---

## Demo

To see the agent in action, trigger it on any public GitLab repository:

```
Perform a full test health audit on this project: hhttps://gitlab.com/Saanvi1710/task-manager
```

The agent will produce:
- A **Test Health Report Issue** with a score out of 100 and findings across all five dimensions
- **`tests/fixed_*.py` files** with corrected versions of the most critical test problems

### Example Test Project

A purpose-built test project demonstrating all five problem types is available at:
**[https://gitlab.com/Saanvi1710/task-manager](https://gitlab.com/Saanvi1710/task-manager)**

This Python Flask task management API contains deliberately seeded test health issues across all five dimensions, making it an ideal demo target.

---

## Tech Stack

| Component | Technology |
|---|---|
| Agent Platform | GitLab Duo Agent Platform |
| Agent Type | Custom Agent |
| Configuration | YAML (`agents/agent.yml`) |
| Language Model | GitLab Duo (built-in LLM) |
| Tools Used | `list_repository_tree`, `find_files`, `read_files`, `grep`, `get_job_logs`, `create_issue`, `create_file_with_contents` |
| Test Project Stack | Python 3.11, Flask 3.0, pytest 7.4 |

---

## Project Structure

```
.
├── agents/
│   └── agent.yml          ← Agent definition: system prompt + tools
├── flows/
│   └── flow.yml.template  ← Flow template (not used in this project)
├── .ai-catalog-mapping.json
├── LICENSE
└── README.md
```

---

## Installation & Usage

### Prerequisites
- A GitLab account with GitLab Duo enabled
- Maintainer or Owner access to a project where you want to enable the agent

### Enable the Agent

1. Go to [AI Catalog → Agents](https://gitlab.com/gitlab-ai-hackathon/participants/Saanvi1710) and find **Test Health Intelligence Agent**
2. Navigate to the project you want to audit → **Automate → Agents**
3. Click **Enable** next to Test Health Intelligence Agent
4. Open **GitLab Duo Chat** in the left sidebar
5. Select **Test Health Intelligence Agent** from the New Chat dropdown
6. Make sure the **Agentic toggle is ON**

### Trigger the Agent

```
Perform a full test health audit on this project: https://gitlab.com/YOUR_USERNAME/YOUR_PROJECT
```

### View Results

- Check the project's **Issues** tab for the generated Test Health Report
- Check the `tests/` directory for `fixed_*.py` files with corrected test code

---

## What Makes This Different

Most AI coding tools are **reactive** — they respond to what you paste into a chat window. This agent is **proactive and contextual**. It has access to your project's entire history — every commit, every pipeline run, every file — and reasons across all of it to find problems that a static code analysis tool would never catch.

The flaky test detector, for example, doesn't just look at code statically. It cross-references pipeline run history with test code to identify tests that show inconsistent behaviour over time. This is something no IDE plugin or code completion tool currently does.

---

## Responsible AI

This agent operates under the following principles:

- **It never invents findings.** Every issue reported is grounded in specific file names and line numbers found in the actual repository.
- **It never modifies original files.** Fixes are always written as new `fixed_*.py` files, leaving the original test suite untouched.
- **It acknowledges good work.** If a test is well-written, the agent says so rather than manufacturing problems.
- **It explains in plain English.** Every finding is described in language accessible to a junior developer, not just technical jargon.

---

## Author

Built by **Saanvi Dhote and Ritisha Bobde** for the GitLab AI Hackathon.

---

## License

This project is licensed under the MIT License. See [LICENSE](LICENSE) for details.