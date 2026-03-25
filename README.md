# Universal Test Audit Agent

A GitLab-based autonomous agent that audits a repository’s test suite, identifies quality risks, and generates a structured Test Health Report along with fixed test files for the highest-priority issues.

## Overview

The Universal Test Audit Agent is designed to analyze any software project’s tests in a repo-aware way. It does not assume a specific codebase structure until it inspects the repository. The agent reads the project layout, discovers tests and source files, reviews pipeline history, and evaluates the suite across five dimensions:

- Flaky tests
- Brittle tests
- Missing edge cases
- Integration coverage gaps
- Test documentation quality

After the audit, it creates a GitLab issue containing the report and writes corrected test files for the top issues.

## Goals

- Improve test reliability
- Reduce false positives and intermittent failures
- Replace brittle implementation-coupled tests with behavior-focused tests
- Increase edge-case and integration coverage
- Improve test readability and maintainability

## What the Agent Does

1. Discovers the project structure.
2. Finds and reads all test files.
3. Reads the corresponding source files.
4. Reviews recent pipeline history and commit activity.
5. Produces a detailed test health analysis.
6. Creates a GitLab issue for the report.
7. Writes fixed versions of the three highest-priority test files.

## Audit Dimensions

### 1. Flaky Tests
Looks for tests that may fail intermittently because they rely on:

- current time
- random values
- real network calls
- SMTP calls
- file system state
- execution order
- sleep-based waiting

### 2. Brittle Tests
Looks for tests that are too tightly coupled to implementation details, such as:

- private attributes
- internal helper methods
- exact formatting internals
- unstable data structures

### 3. Missing Edge Cases
Checks whether public functions are covered for:

- null or empty inputs
- boundary values
- invalid types
- out-of-range values
- expected exceptions

### 4. Integration Coverage Gaps
Checks whether interactions between components are tested, such as:

- module-to-module calls
- database interactions
- API calls
- email or notification flows

### 5. Test Documentation Quality
Flags tests that are hard to understand because of:

- cryptic names
- weak intent
- missing comments or docstrings
- unclear assertions

## Workflow

### Step 1: Discover the Project Structure
Use the repository tree to identify:

- source directories
- test directories
- dependency files
- project layout

### Step 2: Read All Test Files
Locate and read every test file in the repository.

### Step 3: Read Source Files
Read the source files that the tests exercise.

### Step 4: Inspect Pipeline History
Review recent job logs and commit history for failed or unstable tests.

### Step 5: Perform the Test Audit
Evaluate the suite across all five audit dimensions and assign severity.

### Step 6: Generate the Report
Create a GitLab issue titled:

`Test Health Report — [date]`

The report should include:

- overall score
- summary
- findings by dimension
- priority recommendations

### Step 7: Generate Fixes
For the three highest-severity issues, create fixed test files using the repository’s file creation tool.

## Output Requirements

The agent must:

- base findings on actual repository evidence
- include file names and line numbers
- avoid inventing problems
- keep explanations understandable to junior developers
- preserve passing tests
- avoid editing original test files

## Tools Used

The agent may use:

- `list_repository_tree`
- `find_files`
- `read_file`
- `read_files`
- `grep`
- `get_job_logs`
- `list_commits`
- `create_issue`
- `create_file_with_contents`
- `get_project`

## Expected Deliverables

### 1. Test Health Report
A GitLab issue containing the audit results.

### 2. Fixed Test Files
New files created for the top three issues, named in the format:

`tests/fixed_[original_filename].py`

Each fixed file should include a short comment at the top explaining:

- what was wrong
- what the fix changes
- why the new version is safer or more maintainable

## Notes

- The agent should adapt to the repository it finds.
- It should not assume Python unless the repository evidence supports it.
- It should not create issues instead of files.
- It should not overwrite existing code.
- It should not report a problem unless it can point to concrete evidence.

## Example Use Case

This agent is useful when you want to:

- assess test reliability before a demo
- improve a legacy test suite
- identify hidden quality risks
- generate safer test replacements
- make quality assurance more systematic

## Maintenance

When updating the prompt or workflow:

- keep the steps repository-aware
- keep the output structure stable
- avoid hardcoding project-specific assumptions
- ensure file creation remains part of the workflow

---

## Author

Built by **Saanvi Dhote and Ritisha Bobde** for the GitLab AI Hackathon.

---

## License

This project is licensed under the MIT License. See [LICENSE](LICENSE) for details.