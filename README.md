# 🧠 Universal Test Audit Agent

An AI-powered GitLab agent that audits test suites, identifies quality issues, and generates actionable fixes — directly inside your repository.

---

## 🚀 Overview

The **Universal Test Audit Agent** transforms any GitLab project into a self-auditing system for test quality.

It automatically:
- Analyzes your repository
- Evaluates test quality across key dimensions
- Generates a structured **Test Health Report**
- Produces **ready-to-run fixed test files**

---

## 🧪 Demo Project

This agent has been tested on a real project:

👉 https://gitlab.com/Saanvi1710/task-manager

### About the Project
A Python Flask-based **Task Management API** with:
- User authentication  
- Task creation & priority handling  
- Due dates & time-based logic  
- Email notifications  

This project is ideal because it naturally includes:
- Multiple modules (auth, tasks, notifications, database)
- External dependencies (SMTP, DB)
- Time-dependent logic

---

## 🔍 What the Agent Evaluates

The agent audits test suites across **five dimensions**:

### 1. Flaky Tests
Detects instability caused by:
- Real-time dependencies
- Network/SMTP calls
- Randomness
- Sleep-based timing

### 2. Brittle Tests
Finds tests tightly coupled to implementation:
- Private attributes
- Internal methods
- Exact formatting checks

### 3. Missing Edge Cases
Identifies gaps in:
- Null/empty inputs  
- Boundary values  
- Invalid inputs  
- Exception handling  

### 4. Integration Coverage Gaps
Checks whether interactions are tested:
- Service-to-service
- Database calls
- External APIs

### 5. Documentation Quality
Flags:
- Poor test naming  
- Missing intent  
- Weak assertions  

---

## ⚙️ How It Works

1. **Project Discovery**
   - Detects language, framework, structure

2. **Test & Source Analysis**
   - Reads all test and related source files

3. **Pipeline Inspection**
   - Reviews logs and commit history

4. **Audit Execution**
   - Evaluates across five dimensions

5. **Report Generation**
   - Creates a GitLab issue with findings

6. **Fix Generation**
   - Produces corrected test files

---

## 🛠️ Tools & Technologies

- Claude AI  
- GitLab MCP Tools  
- Python  
- pytest  
- freezegun  
- pytest-mock  
- GitLab CI/CD  
- GitLab Issues API  

---

## ▶️ How to Use

1. Open the GitLab project  
   👉 https://gitlab.com/Saanvi1710/task-manager  

2. Launch the Test Audit Agent  

3. Provide the project ID  

4. Approve required actions:
   - Repository access  
   - Issue creation  
   - File generation  

5. View outputs:
   - 📋 **Test Health Report** → Issues tab  
   - 🔧 **Fixed Test Files** → `fixes/<timestamp>/` or linked issues  

6. Run tests:
```bash
pytest