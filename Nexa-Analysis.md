## **Nexa is a Canonical, Repo-Aware Orchestrator** — Not Just a Coding Assistant

### **Nexa =  AI-Powered Development Orchestrator**

**Think of Nexa as:**
- 🧠 **Smart Project Manager** - Understands your entire codebase
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

This approach transforms Copilot from a code completion tool into a project-aware development assistant.

**Bottom Line**: NEXA MODE says, "Let me FIRST understand your ENTIRE canonical architecture with 100% coverage, THEN orchestrate systematic, evidence-based, multi-workflow operations with zero hallucination, persistent state, and architectural integrity enforcement"
