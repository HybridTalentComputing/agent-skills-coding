---
name: deepwiki-skill
description: Generate comprehensive project analysis documentation for code repositories. Use when Claude needs to analyze a codebase and create detailed documentation covering: (1) Project architecture and structure, (2) Component relationships and dependencies, (3) Key functionality and features, (4) Code patterns and design decisions, (5) Setup and usage instructions. Uses DeepResearch multi-turn methodology for thorough analysis. Works with any local or remote repository.
---

# DeepWiki Project Analysis

Generate comprehensive, professional documentation for any code repository using systematic analysis methodology inspired by DeepWiki-Open.

## When to Use

- User asks to "analyze this repository/project/codebase"
- User requests "generate documentation for this project"
- User wants to "understand how this codebase works"
- User needs "project overview and architecture"
- User asks "explain the structure of this project"

**Output: Multiple Document Collection**

This skill generates a COMPREHENSIVE DOCUMENT COLLECTION, not a single report. Each aspect gets its own dedicated document for better organization and maintainability.

## Core Analysis Methodology

### DeepResearch Multi-Turn Approach

For comprehensive analysis, use a structured multi-turn research process:

**Iteration 1: Research Plan**
- Start with "## Research Plan"
- Outline the approach to investigating the topic
- Identify key aspects to research
- Provide initial findings
- End with "## Next Steps"

**Iterations 2-4: Progressive Deepening**
- Start with "## Research Update {N}"
- Review conversation history to avoid repetition
- Focus on specific aspects needing deeper investigation
- Build upon previous findings
- Provide new insights not covered before

**Iteration 5: Final Conclusion**
- Start with "## Final Conclusion"
- Synthesize ALL findings from previous iterations
- Provide comprehensive, definitive answer
- Include specific code references and implementation details

### Context Retrieval Strategy

**When analyzing code:**
1. **Start with file path grouping** - Group context by file paths for better organization
2. **Prioritize implementation files** - Focus on non-test files first
3. **Use targeted queries** - Formulate RAG queries to focus on specific aspects
4. **Manage token limits** - If context exceeds ~8000 tokens, be selective

**Context formatting:**
```
## File Path: path/to/file.py

<code content>

---

## File Path: path/to/another.py

<code content>
```

### Token Management

**Guidelines:**
- **Safe threshold:** ~7500 tokens for input
- **Warning:** If input exceeds 8000 tokens, reduce context
- **Fallback:** If too large, answer without retrieval augmentation
- **Prioritize:** Core implementation files over tests and docs

### Applying DeepResearch by Project Size

**For Small Projects (<10k LOC):**
- **Iterations:** 2-3 iterations sufficient
- **Iteration 1:** Research Plan - understand overall structure
- **Iteration 2:** Final Conclusion - generate all documentation
- **Focus:** Quick overview, essential documentation only

**For Medium Projects (10k-50k LOC):**
- **Iterations:** 3-4 iterations recommended
- **Iteration 1:** Research Plan - identify key components
- **Iteration 2:** Deep dive into core modules
- **Iteration 3:** Explore component relationships
- **Iteration 4:** Final Conclusion - comprehensive documentation
- **Focus:** Balanced detail, all core documents

**For Large Projects (50k-100k LOC):**
- **Iterations:** 4-5 iterations recommended
- **Iteration 1:** Research Plan - architecture overview
- **Iteration 2:** Deep dive into architecture and design patterns
- **Iteration 3:** Explore specific subsystems (e.g., API, UI, data layer)
- **Iteration 4:** Investigate advanced features (testing, deployment, configuration)
- **Iteration 5:** Final Conclusion - full documentation collection
- **Focus:** Detailed analysis with specialized documents

**For Very Large Projects (>100k LOC):**
- **Iterations:** 5+ iterations with focused deep-dives
- **Iteration 1:** Research Plan - high-level architecture
- **Iteration 2:** Architecture and component relationships
- **Iteration 3:** Core functionality deep-dive (Task, Controller, API Handler)
- **Iteration 4:** Specialized systems (MCP, Tools, Context Management)
- **Iteration 5:** Advanced topics (Testing, Deployment, Configuration, Troubleshooting)
- **Iteration 6:** Final Conclusion - complete 10-document collection
- **Focus:** Maximum detail, extensive cross-references, multiple diagrams
- **Note:** May require multiple conversation sessions due to context limits

### When to Use Explore Agent

**Use Task tool with subagent_type=Explore when:**
- Need to understand overall codebase structure
- Searching for patterns across many files
- Investigating how components interact
- Need comprehensive analysis of large code sections

**Use direct Grep/Glob/Read when:**
- Looking for specific file patterns (e.g., all test files)
- Searching for specific keywords (e.g., "interface Task")
- Reading known specific files
- Quick verification tasks

## Analysis Framework

### Project Size Assessment

**Before generating documentation, assess the project size:**

```
Small Project (< 10k LOC):
- Generate: README.md, ARCHITECTURE.md, DEVELOPMENT.md
- Optional: API.md (if applicable)
- Focus: Essential documentation only

Medium Project (10k-50k LOC):
- Generate: All 5 core documents
- Optional: COMPONENTS.md, DATA-MODELS.md
- Focus: Balanced detail level

Large Project (50k-100k LOC):
- Generate: All 5 core documents + at least 2 specialized documents
- Recommended: COMPONENTS.md, DATA-MODELS.md, CONFIGURATION.md
- Focus: Comprehensive coverage

Very Large Project (>100k LOC):
- Generate: All 10 documents (5 core + 5 specialized)
- Required: COMPONENTS.md, DATA-MODELS.md, CONFIGURATION.md, TESTING.md
- Recommended: DEPLOYMENT.md, TROUBLESHOOTING.md
- Focus: Maximum detail with multiple specialized documents
```

**Project Size Indicators:**
- Lines of code (LOC) - Use `find` and `wc -l` to count
- Number of files - More files = more complex
- Directory depth - Deeper hierarchy = more complex
- Number of dependencies - More dependencies = more complex

### How to Count LOC

**For TypeScript/JavaScript projects:**
```bash
# Count all TS/JS files (excluding tests)
find src -name "*.ts" -o -name "*.tsx" -o -name "*.js" -o -name "*.jsx" | xargs wc -l | tail -1

# Or use a more comprehensive count
find src -name "*.ts" -o -name "*.tsx" | xargs wc -l
```

**For Python projects:**
```bash
# Count all Python files in src/
find src -name "*.py" | xargs wc -l | tail -1
```

**For general projects (all source files):**
```bash
# Count all code files (excluding tests, node_modules, build, etc.)
find . -type f \( -name "*.ts" -o -name "*.tsx" -o -name "*.js" -o -name "*.py" -o -name "*.go" -o -name "*.rs" \) ! -path "*/node_modules/*" ! -path "*/dist/*" ! -path "*/build/*" ! -path "*/test/*" ! -path "*/tests/*" ! -path "*/.next/*" | xargs wc -l | tail -1
```

### Quick Project Size Assessment

**Step 1: Count files and estimate LOC**
```bash
# Count source files
find src -type f -name "*.ts" -o -name "*.tsx" -o -name "*.py" -o -name "*.js" | wc -l

# List directory structure
tree -L 2 -d
```

**Step 2: Check package.json/requirements.txt for dependencies**
```bash
# Count npm dependencies
cat package.json | jq '.dependencies | length'

# Count Python dependencies
cat requirements.txt | wc -l
```

**Step 3: Make decision based on findings**
- < 50 files, < 10k LOC → Small project
- 50-200 files, 10k-50k LOC → Medium project
- 200-500 files, 50k-100k LOC → Large project
- 500+ files, >100k LOC → Very large project

### Phase 1: Project Discovery (5-15 minutes)

**1. Understand Project Scope**
```
- Identify project type (web app, library, API, tool, etc.)
- Determine primary programming languages
- Estimate project size and complexity
- Identify key frameworks and technologies
```

**2. Locate Entry Points**
```
Priority files to examine:
- README.md, CONTRIBUTING.md
- package.json, requirements.txt, pom.xml, go.mod
- main.py, index.js, app.py, main.go
- Dockerfile, docker-compose.yml
```

**3. Initial Structure Assessment**
```
- List top-level directories
- Identify configuration files
- Note build/deployment files
- Check for documentation folder
```

### Phase 2: Architecture Analysis (15-30 minutes)

**1. Directory Structure Analysis**
```
For each directory:
- Understand its purpose
- Identify key files
- Note dependencies on other directories
- Document architecture pattern (MVC, layered, microservices, etc.)
```

**2. Component Identification**
```
- List major components/modules
- Map component relationships
- Identify data flow between components
- Note external service integrations
```

**3. Design Pattern Recognition**
```
Common patterns to identify:
- MVC/MVVM
- Repository pattern
- Factory/Builder pattern
- Observer/Pub-Sub
- Dependency Injection
- Middleware pipeline
- Service layer
```

### Phase 3: Deep Code Analysis (30-60 minutes)

**1. Core Functionality Analysis**
```
For each major component:
- Understand primary purpose
- Identify key classes/functions
- Trace execution flow
- Note important algorithms
- Document edge cases handled
```

**2. Data Model Analysis**
```
- Identify data structures
- Map entity relationships
- Note data validation rules
- Understand data flow and transformations
```

**3. Dependencies Analysis**
```
External dependencies:
- List major libraries/packages
- Understand their purposes
- Note version constraints

Internal dependencies:
- Map module imports
- Identify circular dependencies
- Note coupling levels
```

### Phase 4: Documentation Generation (30-120 minutes)

**Generate a DOCUMENT COLLECTION based on project size:**

#### For All Projects (Core Documents - Always Generate)

1. **README.md** - Project overview and quick start
2. **ARCHITECTURE.md** - System architecture and design
3. **DEVELOPMENT.md** - Development setup and guidelines

#### Conditional Documents (Generate based on project type)

4. **API.md** - API reference (if project has API endpoints or programming interface)
5. **DEPLOYMENT.md** - Deployment and operations (if project has deployment process)

#### For Medium+ Projects (Recommended for 10k+ LOC)

6. **COMPONENTS.md** - Component catalog and details
7. **DATA-MODELS.md** - Data schemas and relationships

#### For Large+ Projects (Recommended for 50k+ LOC)

8. **CONFIGURATION.md** - Configuration options (if project has extensive configuration)
9. **TESTING.md** - Testing strategy and guidelines

#### For Very Large Projects (Required for 100k+ LOC)

10. **TROUBLESHOOTING.md** - Common issues and solutions

**Document Generation Decision Matrix:**

```
Project Size → Documents Generated
─────────────────────────────────────
Small (< 10k) → README.md, ARCHITECTURE.md, DEVELOPMENT.md (+ API.md if applicable)
Medium (10k-50k) → Core 5 docs: README, ARCHITECTURE, API (if exists), DEVELOPMENT, DEPLOYMENT
              → Add: COMPONENTS.md, DATA-MODELS.md
Large (50k-100k) → Core 5 docs + COMPONENTS.md, DATA-MODELS.md
              → Add: CONFIGURATION.md, TESTING.md
Very Large (>100k) → All 10 documents (5 core + 5 specialized)
```

**Documentation Best Practices for Large Projects:**

1. **Use Progressive Disclosure** - Start with overview, then dive deeper
2. **Cross-Reference Extensively** - Link related documents
3. **Include Code Examples** - Show actual usage patterns
4. **Add Mermaid Diagrams** - Visualize architecture and relationships
5. **Provide Multiple Levels** - Overview → Detailed → Reference

Each document is a separate markdown file, cross-referenced where appropriate.

## Prompt Engineering Patterns

### First Iteration Prompt Template

```
You are an expert code analyst examining the {repo_type} repository: {repo_url}.
You are conducting a multi-turn Deep Research process to thoroughly investigate the specific topic in the user's query.
Your goal is to provide detailed, focused information EXCLUSIVELY about this topic.

<guidelines>
- This is the first iteration of a multi-turn research process
- Start your response with "## Research Plan"
- Outline your approach to investigating this specific topic
- Identify the key aspects you'll need to research
- Provide initial findings based on the information available
- End with "## Next Steps" indicating what you'll investigate next
- Do NOT provide a final conclusion yet
- Focus EXCLUSIVELY on the specific topic being researched
```

### Intermediate Iteration Prompt Template

```
You are in iteration {N} of a Deep Research process focused EXCLUSIVELY on the user's query.
Your goal is to build upon previous research iterations and go deeper into this specific topic.

<guidelines>
- CAREFULLY review the conversation history to understand what has been researched
- Your response MUST build on previous research - do not repeat information
- Identify gaps or areas that need further exploration
- Focus on one specific aspect that needs deeper investigation
- Start your response with "## Research Update {N}"
- Provide new insights that weren't covered in previous iterations
```

### Final Iteration Prompt Template

```
You are in the final iteration of a Deep Research process.
Your goal is to synthesize all previous findings and provide a comprehensive conclusion.

<guidelines>
- CAREFULLY review the entire conversation history
- Synthesize ALL findings from previous iterations
- Start with "## Final Conclusion"
- Your conclusion MUST directly address the original question
- Include specific code references and implementation details
- Provide a complete and definitive answer to the original question
```

## Code Reading Strategy

**Top-Down Approach:**
```
1. Start with README and documentation
2. Examine configuration files
3. Look at main entry points
4. Study directory structure
5. Dive into specific modules
6. Trace execution flows
```

**What to Focus On:**
```
Priority order:
- Public APIs and interfaces
- Core business logic
- Data models and schemas
- Configuration and setup
- Utilities and helpers
- Tests (for usage examples)
```

## Pattern Recognition

**Web Application Indicators:**
```
- package.json with React/Vue/Angular
- static/ or public/ directory
- routes/, controllers/, views/
- middleware/, templates/
```

**API Service Indicators:**
```
- api/, routes/ directories
- FastAPI, Express, Flask imports
- OpenAPI/Swagger specs
- HTTP method decorators
```

**Library/Package Indicators:**
```
- lib/, src/ directories
- setup.py, pyproject.toml
- minimal main/entry point
- extensive __init__.py files
```

**Microservice Indicators:**
```
- docker-compose.yml
- service-specific directories
- API gateway or proxy
- message queue integration
```

## Document Generation Structure

### Document Collection Organization

**Create a docs/ directory with separate markdown files:**

```
docs/
├── README.md                 # Project overview (entry point)
├── ARCHITECTURE.md           # System architecture
├── API.md                    # API documentation
├── COMPONENTS.md             # Component catalog
├── DATA-MODELS.md            # Data schemas
├── DEVELOPMENT.md            # Development guide
├── DEPLOYMENT.md             # Deployment guide
├── CONFIGURATION.md          # Configuration
├── TESTING.md                # Testing guide
└── TROUBLESHOOTING.md        # Common issues
```

### Cross-References

**Link between documents:**
```markdown
See [ARCHITECTURE.md](ARCHITECTURE.md) for system design.
See [API.md](API.md) for endpoint documentation.
See [DEVELOPMENT.md](DEVELOPMENT.md) for setup instructions.
```

### Document Templates

Use templates from `assets/document_templates/` for each document type.

**Core Documents (5 templates):**
- `README.md` - Project overview template
- `ARCHITECTURE.md` - Architecture template
- `API.md` - API documentation template
- `DEVELOPMENT.md` - Development guide template
- `DEPLOYMENT.md` - Deployment guide template

**Specialized Documents (5 templates):**
- `COMPONENTS.md` - Component catalog template
- `DATA-MODELS.md` - Data models and schemas template
- `CONFIGURATION.md` - Configuration guide template
- `TESTING.md` - Testing guide template
- `TROUBLESHOOTING.md` - Troubleshooting guide template

### Template Usage Guidelines

**For Small Projects (<10k LOC):**
- Use core templates: README, ARCHITECTURE, DEVELOPMENT
- Add API template if project has API endpoints
- Keep documentation concise and focused

**For Medium Projects (10k-50k LOC):**
- Use all 5 core templates
- Add COMPONENTS and DATA-MODELS for better organization
- Include moderate level of detail

**For Large Projects (50k-100k LOC):**
- Use all 5 core templates + COMPONENTS + DATA-MODELS
- Add CONFIGURATION and TESTING for comprehensive coverage
- Include detailed explanations with multiple code examples

**For Very Large Projects (>100k LOC):**
- Use all 10 templates (5 core + 5 specialized)
- Maximum detail with extensive cross-references
- Include multiple levels: overview → detailed → reference
- Add Mermaid diagrams for visualization

### Diagram Guidelines

**Create Mermaid diagrams for:**
- System architecture (graph TD)
- Component relationships (graph LR)
- Data flow (sequenceDiagram)
- Entity relationships (erDiagram)
- State machines (stateDiagram-v2)

**Diagram Best Practices:**
- Keep diagrams simple (max 10-15 nodes)
- Use consistent styling
- Label edges clearly
- Group related components
- Use subgraphs for layers

## Handling Different Project Types

### Web Applications
```
Focus on:
- Frontend framework and routing
- Backend API structure
- Database schema
- Authentication/authorization
- State management
```

### API Services
```
Focus on:
- Endpoint definitions
- Request/response models
- Middleware and validation
- Authentication
- Rate limiting
```

### Libraries/Packages
```
Focus on:
- Public API surface
- Core functionality
- Usage examples
- Configuration options
- Extension points
```

### Data Projects
```
Focus on:
- Data pipeline stages
- Processing logic
- Storage schemas
- ETL/ELT flows
- Quality checks
```

## Common Pitfalls to Avoid

### Don't:
- List every file exhaustively
- Include generated/minified files
- Get lost in implementation details
- Ignore configuration files
- Skip the README
- Assume without verifying

### Do:
- Focus on understanding over listing
- Identify patterns and conventions
- Trace key execution paths
- Document non-obvious decisions
- Cross-reference with documentation
- Verify assumptions with code

## Quality Checklist

**Before finalizing documentation, ensure:**
- [ ] Architecture is clearly explained
- [ ] Key components are documented
- [ ] Data flow is traceable
- [ ] Setup instructions are complete
- [ ] Diagrams are accurate
- [ ] Code examples are correct
- [ ] Dependencies are listed
- [ ] Design decisions are explained

## Reference Resources

- **Analysis Framework**: [references/analysis_framework.md](references/analysis_framework.md) - Detailed analysis methodology
- **Code Patterns**: [references/code_patterns.md](references/code_patterns.md) - Common patterns recognition
- **Documentation Standards**: [references/documentation_standards.md](references/documentation_standards.md) - Writing guidelines
- **Document Templates**: [assets/document_templates/](assets/document_templates/) - Document-specific templates

## Tips for Effective Analysis

**Speed vs Depth:**
- Quick overview: 30-60 minutes
- Detailed analysis: 2-4 hours
- Comprehensive: 4-8 hours

**When to Deep Dive:**
- Complex business logic
- Unusual architecture
- Critical algorithms
- Security-sensitive code

**When to Stay High-Level:**
- Standard patterns
- Boilerplate code
- Well-documented libraries
- Configuration files

**When to Use DeepResearch:**
- User requests comprehensive analysis
- Topic requires multiple aspects to be covered
- Question is complex or multi-faceted
- User asks for "deep dive" or "thorough analysis"

## Working with Large Projects

For large projects (>1000 files or >100k LOC):

### Strategy 1: Modular Deep-Dive

1. **First Pass - Architecture Overview**
   - Use Explore agent to understand overall structure
   - Identify major subsystems and components
   - Map out component relationships
   - Generate ARCHITECTURE.md first

2. **Second Pass - Core Functionality**
   - Focus on main entry points (e.g., main.py, index.ts, app.py)
   - Trace request flow from entry point to completion
   - Identify core business logic
   - Generate COMPONENTS.md for core components

3. **Third Pass - Specialized Systems**
   - Investigate specific subsystems based on project type:
     - API projects: endpoints, middleware, authentication
     - Web apps: routing, state management, data flow
     - Libraries: public API, extension points, examples
   - Generate specialized documents (API.md, DATA-MODELS.md, etc.)

4. **Fourth Pass - Supporting Systems**
   - Configuration management
   - Testing infrastructure
   - Deployment setup
   - Troubleshooting guides

### Strategy 2: Layer-by-Layer Analysis

**Top-Down Approach:**
```
1. UI Layer → Components, Pages, Views
2. API Layer → Routes, Controllers, Handlers
3. Service Layer → Business Logic, Services
4. Data Layer → Models, Repositories, Schemas
5. Infrastructure → Config, Logging, Utilities
```

### Strategy 3: Feature-Based Analysis

For projects organized by features:
```
1. Identify main features (e.g., auth, dashboard, settings)
2. Analyze each feature's implementation
3. Document feature interactions
4. Map shared components and utilities
```

### Managing Context Limits

**For very large projects that exceed single context window:**

1. **Split analysis into multiple conversations:**
   - Session 1: Architecture + Core Components
   - Session 2: API + Data Models
   - Session 3: Testing + Deployment
   - Session 4: Final synthesis and cross-references

2. **Use Explore agent strategically:**
   - Let Explore agent handle deep codebase exploration
   - Focus your analysis on synthesizing Explore agent findings
   - Use Explore agent's summaries to build documentation

3. **Iterative document generation:**
   - Generate high-level documents first (README, ARCHITECTURE)
   - Use those as foundation for detailed documents
   - Cross-reference extensively to avoid duplication

### Quality Signals for Large Projects

**Signs you're doing well:**
- ✅ Each document has a clear, unique purpose
- ✅ Cross-references connect related documents
- ✅ Code examples are accurate and tested
- ✅ Architecture diagrams match actual implementation
- ✅ No contradictions between documents

**Warning signs:**
- ❌ Repeating same information across documents
- ❌ Vague descriptions without specific examples
- ❌ Missing critical components or systems
- ❌ Outdated information (doesn't match current code)
- ❌ Documents too generic (could apply to any project)
