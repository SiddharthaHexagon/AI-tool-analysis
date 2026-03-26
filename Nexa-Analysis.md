## **Nexa is a Canonical, Repo-Aware Orchestrator** — Not Just a Coding Assistant

### **Nexa =  AI-Powered Development Orchestrator**

**Think of Nexa as:**
- 🧠 **Smart Project Manager** - Understands entire codebase
- 🔧 **Automation Engine** - Handles repetitive tasks
- 📚 **Knowledge Base** - Stores project-specific patterns
- 🚀 **Productivity Multiplier** - 3-5x faster development
  
# NEXA — Setup & Usage Guide
https://dev.azure.com/hexagonPPMInnerSource/Visualization/_artifacts/feed/PPM/Npm/@ppm%2Fnexa/overview/4.0.0

# NEXA- What happens in Setup phase?
- Step 1: Scan repository
- Step 2: Detect layers (Backend, Frontend, Native, etc.)
- Step 3: Map 100% workspace coverage
- Step 4: Generate repository-structure.md
- Step 5: Launch parallel subagents (one per workspace area)
- Step 6: Verify 100% coverage + create architecture docs
- Step 7: Update copilot-instructions.md
ONLY THEN: Show main menu

# Nexa.agent.md (Agent Mode Definition)
**Location**: \.github\agents\Nexa.agent.md

**Purpose**: The orchestrator/brain of Nexa Mode itself

**What it contains:**

- Complete mode configuration and execution logic
- Main menu structure (8 workflow options)
- Architecture generation protocols
- Mandatory guidelines and enforcement rules
- Intent recognition mappings
- Workflow routing logic
- Quality gates and validation rules
- Persistent state management
- Version control requirements (4.0.0)
- References to all guidelines and supporting documents
- Analogy: Operating system or central controller

**Invocation**: Activated when you switch to Nexa mode in GitHub Copilot

**Scope**: Controls the ENTIRE Nexa mode behavior

# How They Work Together
1. User activates Nexa mode
2. Nexa.agent.md loads
3. Validates architecture, repository structure
4. Shows main menu (Bug Fixing, Code Review, etc.)
5. User selects workflow (e.g., "1" for Bug Fixing)
6. Nexa.agent.md loads: "nexa guidelines/Speed Up Bug Fixing.md"
7. During execution, Nexa may reference skill files:
- If creating a service → Uses #create-webgis-service patterns
- If debugging backend → Uses #investigate-backend-bug guidance
- If generating tests → Uses #generate-backend-unit-tests templates
8. Skills provide focused, reusable knowledge for specific tasks

# Nexa Capabilities
- 1️⃣ Bug Fixing: 7-phase systematic workflow with ADO integration
- 2️⃣ Code Review: Technology-adaptive review with architecture context
- 3️⃣ Test Management: Dynamic framework detection + execution validation
- 4️⃣ Scrum Management: Work items + Sprint wiki automation
- 5️⃣ Architecture Management: Selective regeneration + gap analysis
- 6️⃣ Custom Instructions Management: Template creation + standards management
- 7️⃣ Workflow Diagram Generation: Static/interactive diagram generation
- 8️⃣ Skill Files Management: Guided authoring + auto-referencing


### 🎯 **Nexa: Core Differentiators:**

**1. Architecture-First Approach**
-  MANDATORY comprehensive architecture generation before any operations, Nexa has complete context; others make assumptions

**2. Zero Hallucination Protocol**
-  Every claim MUST be verified with actual code evidence (no "this probably uses X")
-  Nexa documentation is 100% fact-based, not inferred

**3. Parallel Subagent Analysis**
-  Launches 8-15 specialized subagents for workspaces >2000 files
-  Nexa achieves 100% workspace coverage

**4. Information Preservation Rules**
-  ALL code elements transferred exactly (if subagent finds 50 classes, doc lists all 50)
-  Nexa preserves complete detail

**5. Versioned Architecture Files**
- All docs tagged with version 4.0.0, auto-regenerates outdated files
- Nexa guarantees current documentation

**6. Predefined Canonical Content**
- Uses strict templates per layer (Backend must have: Service Architecture, API Patterns, Caching, etc.)

**7. Multi-Workflow Integration**
-  Integrated menu for Bug Fixing, Code Review, Test Management, Scrum, Architecture Management, Custom Instructions, Workflow Diagrams, Skills

**8. Repository Structure Validation**
-  \.github\repository-structure.md MUST exist
-  MUST read repository-structure.md before ANY task (no assumptions about paths)

**9. Dynamic Technology Detection**
- Detects ONLY frameworks actually present in code (no hardcoded assumptions)

**10. Bug Fixing with Context Continuity**
- Follows strict 7-phase workflow with work item integration, architecture context, test validation


# Nexa.agent.md (Agent Mode Definition)
**Location**: \.github\agents\Nexa.agent.md

**Purpose**: The orchestrator/brain of Nexa Mode itself

**What it contains:**

- Complete mode configuration and execution logic
- Main menu structure (8 workflow options)
- Architecture generation protocols
- Mandatory guidelines and enforcement rules
- Intent recognition mappings
- Workflow routing logic
- Quality gates and validation rules
- Persistent state management
- Version control requirements (4.0.0)
- References to all guidelines and supporting documents
- Analogy: Operating system or central controller

**Invocation**: Activated when you switch to Nexa mode in GitHub Copilot

**Scope**: Controls the ENTIRE Nexa mode behavior

# How They Work Together
1. User activates Nexa mode
2. Nexa.agent.md loads
3. Validates architecture, repository structure
4. Shows main menu (Bug Fixing, Code Review, etc.)
5. User selects workflow (e.g., "1" for Bug Fixing)
6. Nexa.agent.md loads: "nexa guidelines/Speed Up Bug Fixing.md"
7. During execution, Nexa may reference skill files:
- If creating a service → Uses #create-webgis-service patterns
- If debugging backend → Uses #investigate-backend-bug guidance
- If generating tests → Uses #generate-backend-unit-tests templates
8. Skills provide focused, reusable knowledge for specific tasks

# NEXA Skills

**NEXA skills**  demonstrate enterprise-level prompt engineering by:

- Encoding Domain Knowledge: classes, services, plugin architecture
- Enforcing Patterns: Layered architecture, Active Record, event-driven design
- Reducing Cognitive Load: Developers don't need to remember all patterns
- Accelerating Onboarding: New team members reference skills instead of digging through docs
- Maintaining Consistency: All generated code follows established conventions

Read [](file:///c%3A/GtechCore/.github/agents/nexa%20guidelines/Skill%20Files%20Management.md#1-1), lines 1 to 300

Read [](file:///c%3A/GtechCore/.github/agents/nexa%20guidelines/Skill%20Files%20Management.md#300-300), lines 300 to 600

Read [](file:///c%3A/GtechCore/.github/agents/nexa%20guidelines/Skill%20Files%20Management.md#600-600), lines 600 to 900

Read [](file:///c%3A/GtechCore/.github/agents/nexa%20guidelines/Skill%20Files%20Management.md#900-900), lines 900 to 1200

Read [](file:///c%3A/GtechCore/.github/agents/nexa%20guidelines/Skill%20Files%20Management.md#1200-1200), lines 1200 to 1500

Read [](file:///c%3A/GtechCore/.github/agents/nexa%20guidelines/Skill%20Files%20Management.md#1500-1500), lines 1500 to 1678

# 🧩 Skill Files Management - Complete Guide

## 📋 **Overview**

**Skill Files Management** is NEXA's system for creating, managing, and validating **reusable AI prompt templates** stored as `SKILL.md` files. 
These skills can be invoked in GitHub Copilot Chat using the `#` prefix.

### **Key Benefits**
- ✅ **Team consistency** - Standardize AI-assisted workflows across your team
- ✅ **Reusable patterns** - Define once, use everywhere
- ✅ **Project-specific** - Tailored to your tech stack and conventions
- ✅ **Version controlled** - Skills travel with your repository
- ✅ **Easy to invoke** - Type `#skill-name` in Copilot Chat
- ✅ **Quality assured** - Built-in validation and review tools

---

## 🎯 **What Are Skill Files?**

Skill files are **reusable prompt definitions** stored as `SKILL.md` inside dedicated folders under `.github/skills/`.

### **Structure**
```
.github/skills/{skill-name}/SKILL.md
```

### **Example Skill File**

**Path:** `.github/skills/generate-unit-tests/SKILL.md`

```markdown
---
name: generate-unit-tests
description: Generate comprehensive unit tests for the selected code or file
---

# Generate Unit Tests

Generate comprehensive unit tests for the selected code.

## Requirements
- Use the project's existing test framework
- Follow the patterns in #file:tests/example.test.ts
- Achieve 100% code coverage
- Include edge cases and error scenarios
- Use descriptive test names following "should [expected behavior] when [condition]" pattern

## Output Format
- Create test file following project's test file naming convention
- Include necessary imports and setup/teardown
- Add brief comments explaining complex test scenarios
```

### **How to Use**
1. Open **Copilot Chat** in VS Code
2. Type `#` to see available skills
3. Select `#generate-unit-tests`
4. Copilot follows the skill's instructions

---

## 🗂️ **The 7 Skill Management Options**

### **8a. Skill File Creation** (Interactive Authoring Assistant)

**Purpose:** NEXA guides you through creating a well-structured skill with Q&A, then creates the file for you.

**Workflow:**
1. **Understand Intent** - NEXA asks: "What should this skill do?"
2. **Follow-Up Questions** - NEXA clarifies:
   - What type of code/files does it operate on?
   - What are the specific requirements?
   - What output format is expected?
   - Any constraints or edge cases?
3. **Define Metadata** - NEXA prompts for:
   - Skill name (kebab-case)
   - Brief description
4. **Compose Content** - NEXA presents recommended skill content
5. **Review & Refine** - You can request changes
6. **Create File** - NEXA creates `.github/skills/{skill-name}/SKILL.md`
7. **Auto-Reference** - NEXA automatically adds reference to copilot-instructions.md

**Example Interaction:**
```
NEXA: What should this skill do?
USER: Help refactor legacy VB6 code to follow modern patterns

NEXA: What type of code will this operate on?
USER: VB6 .cls and .bas files in our Packages/ directory

NEXA: Should it reference specific project files for patterns?
USER: Yes, reference VBUtil/GMCommonUtilities.bas for error handling

NEXA: Skill Name (kebab-case):
USER: refactor-vb6-legacy

NEXA: Brief Description:
USER: Refactor legacy VB6 code to follow modern patterns with GMCommonUtilities error handling

[NEXA presents recommended content]
[User confirms]
[NEXA creates file + auto-references in copilot-instructions.md]
```

---

### **8b. Browse Skill Templates**

**Purpose:** View pre-built skill templates for inspiration and quick creation.

**Available Template Categories:**

#### **1. Code Generation Skills**
- **Generate Unit Tests** - Comprehensive test creation
- **Generate API Endpoint** - REST API scaffolding
- **Generate Documentation** - JSDoc/TSDoc comments
- **Generate Database Migration** - Schema change scripts

#### **2. Code Improvement Skills**
- **Refactor Code** - Improve readability & maintainability
- **Add Error Handling** - Comprehensive error management
- **Optimize Performance** - Identify bottlenecks
- **Add Logging** - Consistent logging patterns

#### **3. Review & Analysis Skills**
- **Security Review** - Vulnerability detection
- **Accessibility Check** - A11y compliance
- **Code Smell Detection** - Anti-pattern identification
- **Dependency Analysis** - Dependency health check

#### **4. Documentation Skills**
- **Generate README Section** - Documentation components
- **Generate API Documentation** - Endpoint documentation
- **Generate Changelog Entry** - Release notes
- **Generate ADR** - Architecture Decision Records

#### **5. DevOps & Infrastructure Skills**
- **Generate CI/CD Pipeline** - Automation workflows
- **Generate Docker Configuration** - Containerization
- **Generate Infrastructure as Code** - Terraform/ARM
- **Generate Monitoring Alert Rules** - Observability

**Example: Security Review Template**

```markdown
---
name: security-review
description: Perform a security-focused review of the selected code
---

# Security Review

Perform a security-focused review of the selected code.

## Check For
- SQL injection vulnerabilities
- Cross-site scripting (XSS) opportunities
- Authentication/authorization bypasses
- Sensitive data exposure (API keys, passwords, tokens)
- Input validation gaps
- Insecure deserialization
- Path traversal vulnerabilities
- Insecure cryptographic usage
- CORS misconfigurations
- Rate limiting gaps

## Output Format
For each finding:
1. **Severity:** Critical / High / Medium / Low
2. **Location:** File and line reference
3. **Description:** What the vulnerability is
4. **Impact:** What could happen if exploited
5. **Remediation:** How to fix it with code example
```

---

### **8c. Validate Existing Skill File**

**Purpose:** Quality assurance - check skill files for compliance and best practices.

**9 Validation Checks:**

| # | Check | Pass Criteria |
|---|-------|---------------|
| 1 | File structure | SKILL.md in `.github/skills/{name}/` folder |
| 2 | YAML front-matter | File starts with `---` delimiter |
| 3 | Name field | `name` field exists in YAML |
| 4 | Name matches folder | `name: generate-tests` ↔ folder `generate-tests/` |
| 5 | Description field | `description` field exists in YAML |
| 6 | Description quality | Clear, concise, not vague |
| 7 | Content present | Skill instructions below front-matter |
| 8 | Content quality | Well-structured sections |
| 9 | Kebab-case naming | Folder uses lowercase-with-hyphens |

**Example Validation Report:**

```
✅ Skill File Validation Report: generate-unit-tests

📁 Path: .github/skills/generate-unit-tests/SKILL.md

| # | Check | Status |
|---|-------|--------|
| 1 | File structure | ✅ Pass |
| 2 | YAML front-matter | ✅ Pass |
| 3 | Name field | ✅ Pass |
| 4 | Name matches folder | ✅ Pass |
| 5 | Description field | ✅ Pass |
| 6 | Description quality | ✅ Pass |
| 7 | Content present | ✅ Pass |
| 8 | Content quality | ⚠️ Warning |
| 9 | Kebab-case naming | ✅ Pass |

**Result:** 8/9 checks passed, 1 warning, 0 failures

### 💡 Suggestions for Improvement
⚠️ Content quality: Consider adding:
  - "Examples" section showing sample test output
  - "File References" section pointing to existing test patterns
  - "Constraints" section defining limitations
```

---

### **8d. List Existing Skill Files**

**Purpose:** View all skill files in an organized inventory.

**Example Output:**

```
📚 Skill Files Inventory

| # | Skill Name | Folder | Description | Invoke With |
|---|------------|--------|-------------|-------------|
| 1 | generate-unit-tests | generate-unit-tests/ | Generate comprehensive unit tests | #generate-unit-tests |
| 2 | refactor-vb6-legacy | refactor-vb6-legacy/ | Refactor legacy VB6 code to modern patterns | #refactor-vb6-legacy |
| 3 | security-review | security-review/ | Perform security-focused code review | #security-review |
| 4 | add-error-handling | add-error-handling/ | Add comprehensive error handling | #add-error-handling |
| 5 | generate-documentation | generate-documentation/ | Generate JSDoc/TSDoc comments | #generate-documentation |

**Total Skill Files:** 5

💡 Tip: Use #{skill-name} in Copilot Chat to invoke any skill.
```

---

### **8e. Review & Refine Skill File**

**Purpose:** Improve existing skill quality through guided review.

**Review Dimensions:**
- **Clarity** - Are instructions clear and unambiguous?
- **Completeness** - Does it cover all necessary aspects?
- **Specificity** - Are instructions specific enough for consistent results?
- **Structure** - Is content well-organized?
- **Metadata Compliance** - Is metadata correct?

**Example Review:**

```
🔍 Skill Review: generate-unit-tests

### Review Findings

**Clarity:** ✅ Good
Instructions are clear about what tests to generate.

**Completeness:** ⚠️ Needs Improvement
Missing:
- Edge case handling guidance
- Mock/stub patterns for external dependencies
- Test data setup examples

**Specificity:** ⚠️ Needs Improvement
- "Use project's existing test framework" is vague - specify detection method
- "Achieve 100% coverage" - clarify what coverage metric (line/branch/function)

**Structure:** ✅ Good
Well-organized sections with clear headings.

**Metadata:** ✅ Good
Name matches folder, description is concise.

---

### 📝 Recommended Improvements

1. Add "Framework Detection" section explaining how to identify test framework
2. Include "Mock Patterns" section with examples from project's existing tests
3. Define coverage metric explicitly (e.g., "minimum 80% branch coverage")
4. Add "Edge Cases" subsection listing common scenarios to test
5. Add #file: references to existing test files as examples
```

NEXA can then suggest improved content, and after user confirmation, apply the changes automatically.

---

### **8f. Delete Skill File**

**Purpose:** Remove skill files safely with confirmation.

**Workflow:**
1. List available skills
2. User selects skill to delete
3. Confirmation prompt (type 'yes' to confirm)
4. Delete folder and SKILL.md
5. Remove reference from copilot-instructions.md (if present)
6. Display confirmation

**Example:**

```
⚠️ Are you sure you want to delete the skill "old-pattern" (.github/skills/old-pattern/SKILL.md)?

Type 'yes' to confirm or 'no' to cancel:
> yes

✅ Skill file deleted successfully!

🗑️ Removed: .github/skills/old-pattern/SKILL.md
📄 Reference also removed from copilot-instructions.md
```

---

### **8g. Apply Skills to Copilot Instructions**

**Purpose:** Bulk re-sync all skill references in copilot-instructions.md.

**Note:** This is usually automatic (8a/8b auto-reference when creating), but 8g is available for:
- Manual bulk updates
- Re-syncing after external changes
- Regenerating the skills section

**Workflow:**
1. Check if copilot-instructions.md exists
2. Scan all skill files in `.github/skills/`
3. Display found skills
4. Ask for confirmation
5. Update/append "Available Skill Files" section in copilot-instructions.md
6. Verify update successful

**Result:**

```
✅ Skill file references successfully added to copilot-instructions.md!

📋 References Added (5 skills):
- #generate-unit-tests
- #refactor-vb6-legacy
- #security-review
- #add-error-handling
- #generate-documentation

📄 Location: .github/copilot-instructions.md
```

---

## 📐 **File Structure & Naming**

### **Expected Structure**

```
.github/
├── skills/
│   ├── README.md                       # Overview and usage guide
│   ├── generate-unit-tests/
│   │   └── SKILL.md                    # Test generation skill
│   ├── refactor-vb6-legacy/
│   │   └── SKILL.md                    # VB6 refactoring skill
│   ├── security-review/
│   │   └── SKILL.md                    # Security review skill
│   ├── add-error-handling/
│   │   └── SKILL.md                    # Error handling skill
│   └── generate-documentation/
│       └── SKILL.md                    # Documentation skill
├── copilot-instructions.md             # Updated with skill references
└── ...
```

### **Naming Conventions**

**Folder Names:**
- ✅ `generate-unit-tests/` - kebab-case (lowercase with hyphens)
- ✅ `refactor-code/` - descriptive and focused
- ✅ `add-error-handling/` - starts with verb
- ❌ `MySkill/` - not PascalCase
- ❌ `test_generation/` - no underscores
- ❌ test - too vague

**File Names:**
- ✅ `SKILL.md` - MUST be uppercase
- ❌ `skill.md` - not lowercase
- ❌ `README.md` - wrong filename

**Metadata Name Field:**
```yaml
---
name: generate-unit-tests    # MUST match folder name exactly
description: Generate comprehensive unit tests for the selected code or file
---
```

---

## 🎨 **Skill File Examples**

### **Example 1: VB6 Refactoring (Project-Specific)**

**Path:** `.github/skills/refactor-vb6-legacy/SKILL.md`

```markdown
---
name: refactor-vb6-legacy
description: Refactor legacy VB6 code to follow modern patterns with GMCommonUtilities error handling
---

# Refactor VB6 Legacy Code

Refactor the selected VB6 code (.cls or .bas files) to follow modern patterns used in GTechnology Core.

## Requirements
- Replace direct `Err.Raise` with `GMCommonUtilities.GMRaiseError()` for consistent error handling
- Use `ADO2GDO.CopyADO2GDO()` for recordset conversions (not manual field-by-field)
- Follow metadata query patterns from `MetadataUtils.bas` (GetComponentName, GetFeatureClassName)
- Apply Hungarian notation consistently (o- for objects, s- for strings, i- for integers)
- Ensure universal utilities are included in project references

## Constraints
- Do NOT change COM interface signatures (breaks consumers)
- Do NOT remove existing error handlers (refactor, don't delete)
- Preserve all existing functionality
- Keep changes minimal and focused

## File References
- Error handling: #file:VBUtil/src/GMCommonUtilities.bas
- Recordset conversion: #file:VBUtil/src/ADO2GDO.bas
- Metadata utilities: #file:VBUtil/src/MetadataUtils.bas

## Output Format
- Provide refactored code with inline comments explaining changes
- List all VBUtil modules that need to be added to .vbp project references
```

### **Example 2: C++ Memory Leak Detection**

**Path:** `.github/skills/detect-memory-leaks/SKILL.md`

```markdown
---
name: detect-memory-leaks
description: Analyze C++ code for potential memory leaks and resource management issues
---

# Detect Memory Leaks in C++ Code

Analyze the selected C++ code for memory leaks, resource management issues, and COM object lifetime problems.

## Check For
- Raw pointers without corresponding delete
- COM object creation without smart pointer wrappers (use CComPtr instead of raw pointers)
- Memory allocated in constructor without corresponding deallocation in destructor
- Missing IUnknown::Release() calls
- Resources (file handles, database connections) not released in all code paths
- Exception paths that skip cleanup code
- Circular references in COM objects

## Requirements
- Recommend using CComPtr/CComQIPtr for all COM objects
- Suggest RAII patterns for resource management
- Flag manual AddRef/Release pairs (should use smart pointers)
- Identify error paths missing cleanup

## Severity Levels
- **Critical:** Definite memory leak on common code path
- **High:** Memory leak in error handling path
- **Medium:** Potential leak depending on usage
- **Low:** Non-optimal pattern but no leak

## Output Format
For each finding:
1. **Severity:** Critical / High / Medium / Low
2. **Location:** File:Line
3. **Issue:** Description of the memory management problem
4. **Recommendation:** How to fix (with code example)

## Example Fixes
```cpp
// BAD: Manual Release
IGMGeometry* pGeometry = nullptr;
CoCreateInstance(..., (void**)&pGeometry);
pGeometry->DoSomething();
pGeometry->Release();  // Fragile

// GOOD: Smart pointer
CComPtr<IGMGeometry> spGeometry;
spGeometry.CoCreateInstance(...);
spGeometry->DoSomething();
// Automatically released
```
```

### **Example 3: Azure DevOps Work Item Template**

**Path:** `.github/skills/create-ado-pbi/SKILL.md`

```markdown
---
name: create-ado-pbi
description: Generate well-structured Azure DevOps Product Backlog Item from requirements
---

# Create Azure DevOps PBI

Generate a well-structured Product Backlog Item (PBI) for Azure DevOps from the given requirements.

## Required Fields
- **Title:** Clear, concise summary (max 80 characters)
- **Description:** Detailed explanation with acceptance criteria
- **Acceptance Criteria:** Bulleted list of testable conditions
- **Story Points:** Estimate (1, 2, 3, 5, 8, 13, 21)
- **Priority:** 1 (Critical), 2 (High), 3 (Medium), 4 (Low)
- **Area Path:** Project area classification
- **Iteration Path:** Target sprint

## Description Template
```
## User Story
As a [type of user], I want [goal] so that [reason/benefit].

## Background
[Context and why this work is needed]

## Acceptance Criteria
- [ ] Criterion 1 (testable)
- [ ] Criterion 2 (testable)
- [ ] Criterion 3 (testable)

## Technical Notes
[Implementation considerations, dependencies, risks]

## Testing Strategy
[How this will be validated]
```

## Output Format
Generate the PBI in markdown format ready to paste into Azure DevOps.
Include all required fields with reasonable defaults based on the requirements provided.
```

---

## ✅ **Best Practices**

### **For Creating Skills**

1. **Be Specific, Not Generic**
   - ✅ "Generate unit tests for TypeScript React components using Jest"
   - ❌ "Generate tests"

2. **Include Project Context**
   - Use `#file:` references to existing code examples
   - Reference project-specific conventions
   - Mention framework versions

3. **Define Clear Output**
   - Specify format (code, documentation, report)
   - Include structural requirements
   - Add examples of expected output

4. **One Skill = One Task**
   - ✅ Separate skills: `generate-unit-tests`, `generate-integration-tests`
   - ❌ Combined skill: `generate-all-tests` (too broad)

5. **Use Descriptive Names**
   - ✅ `refactor-vb6-error-handling`
   - ❌ `fix-vb6` (vague)

### **For Skill Organization**

1. **Group Related Skills**
   - `review-security/`, `review-accessibility/`, `review-performance/`
   - `generate-unit-tests/`, `generate-integration-tests/`, `generate-e2e-tests/`

2. **Keep Skills Updated**
   - Review skills when project patterns change
   - Use Option 8e (Review & Refine) periodically
   - Validate with Option 8c after updates

3. **Share Across Team**
   - Skills are in repository - everyone benefits
   - Document team standards as skills
   - Review skills during onboarding

---

## 🔗 **Integration with copilot-instructions.md**

### **Auto-Reference on Creation**

When you create a skill (8a or 8b), NEXA **automatically** adds it to copilot-instructions.md:

```markdown
## 🚨 MANDATORY PRE-TASK VALIDATION

### 1. Repository Structure Reference (MANDATORY)
[existing content...]

### 2. Available Skill Files (MANDATORY REFERENCE)
**Location:** `.github/skills/`

**Available Skills:** (Invoke with `#skill-name` in Copilot Chat)
- **#generate-unit-tests** — Generate comprehensive unit tests for the selected code or file
- **#refactor-vb6-legacy** — Refactor legacy VB6 code to follow modern patterns with GMCommonUtilities error handling
- **#security-review** — Perform a security-focused review of the selected code
- **#add-error-handling** — Add comprehensive error handling to the selected code
- **#detect-memory-leaks** — Analyze C++ code for potential memory leaks and resource management issues

**Usage Instructions:**
- Skills are reusable prompt templates for common tasks
- Reference skills by typing `#skill-name` in Copilot Chat
- Each skill enforces project-specific patterns and conventions
- Use skills to maintain consistency across the team

**When to Check Skills:**
- ✅ Before implementing any new feature
- ✅ During code refactoring
- ✅ When writing tests
- ✅ During bug fixing to maintain patterns
- ✅ When adding documentation
```

This ensures GitHub Copilot is **always aware** of available skills and can suggest them in context.

---

## 🎯 **Summary**

| Option | Purpose | Key Features |
|--------|---------|--------------|
| **8a** | Create skill | Interactive Q&A → Compose → Review → Create → Auto-reference |
| **8b** | Browse templates | 15+ pre-built templates across 5 categories |
| **8c** | Validate | 9-point quality check with detailed reporting |
| **8d** | List skills | Organized inventory of all skills |
| **8e** | Review & refine | Guided improvement with 5 review dimensions |
| **8f** | Delete skill | Safe deletion with confirmation + auto-cleanup |
| **8g** | Apply to copilot | Bulk re-sync (usually automatic via 8a/8b) |

**Key Takeaways:**
- 🎯 **NEXA guides you** - Interactive assistant, not auto-generator
- 📁 **One folder per skill** - Clean, organized structure
- ✅ **Automatic validation** - Built-in quality assurance
- 🔗 **Auto-integration** - Skills automatically referenced in copilot-instructions.md
- 👥 **Team consistency** - Shared standards across your repository

---

Would you like me to:
1. **Create example skill files** for your GtechCore project (VB6, C++, .NET specific)?
2. **Show more template examples** from any category?
3. **Walk through creating a skill** interactively (Option 8a)?
4. **Return to main menu**?

This approach transforms Copilot from a code completion tool into a project-aware development assistant.

**Bottom Line**: NEXA MODE says, "Let me FIRST understand your ENTIRE canonical architecture with 100% coverage, THEN orchestrate systematic, evidence-based, multi-workflow operations with zero hallucination, persistent state, and architectural integrity enforcement"
