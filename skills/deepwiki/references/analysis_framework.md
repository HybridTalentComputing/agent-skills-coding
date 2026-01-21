# Project Analysis Framework

Systematic methodology for analyzing code repositories and generating comprehensive documentation.

## Analysis Methodology

### Level 1: Quick Scan (5-15 minutes)

**Purpose:** Rapid project understanding

**Steps:**

1. **Read README** (2 min)
   - Project description
   - Key features
   - Installation instructions
   - Quick start guide

2. **Scan File Tree** (3 min)
   - Top-level directories
   - Configuration files
   - Build/deployment files
   - Documentation locations

3. **Identify Stack** (2 min)
   - Languages used (file extensions)
   - Frameworks (config files)
   - Dependencies (package files)

4. **Note Entry Points** (3 min)
   - Main files
   - Server startup files
   - CLI entry points
   - Module initialization

**Output:** 1-2 paragraph summary

### Level 2: Structural Analysis (30-60 minutes)

**Purpose:** Understand architecture and organization

**Steps:**

1. **Map Directory Structure**
   ```
   For each directory:
   - Purpose and responsibility
   - Key files and modules
   - Dependencies on other directories
   - External integrations
   ```

2. **Identify Architecture Pattern**
   ```
   Look for:
   - MVC: models/, views/, controllers/
   - Layered: layers/, tiers/
   - Microservices: services/, docker-compose.yml
   - Modular: packages/, modules/
   - Monorepo: apps/, packages/
   ```

3. **Trace Data Flow**
   ```
   Follow path:
   - Input/Entry points
   - Processing layers
   - Data transformations
   - Storage/Output
   - External API calls
   ```

4. **Document Components**
   ```
   For each major component:
   - Name and location
   - Primary responsibility
   - Public interfaces
   - Dependencies (internal/external)
   ```

**Output:** Architecture overview with diagram

### Level 3: Detailed Analysis (2-4 hours)

**Purpose:** Deep understanding of implementation

**Steps:**

1. **Analyze Core Modules**
   ```
   For each core module:
   - Class/function organization
   - Key algorithms
   - Design patterns used
   - Error handling
   - Performance considerations
   ```

2. **Study Data Models**
   ```
   - Entity definitions
   - Relationships
   - Validation rules
   - Data transformations
   - Storage schemas
   ```

3. **Review Interfaces**
   ```
   - API endpoints
   - Function signatures
   - Event handlers
   - Middleware
   - Hooks/Callbacks
   ```

4. **Examine Configuration**
   ```
   - Environment variables
   - Config files
   - Feature flags
   - Default settings
   - Override mechanisms
   ```

**Output:** Detailed component documentation

### Level 4: Comprehensive Analysis (4-8 hours)

**Purpose:** Production-ready documentation

**Steps:**

1. **Complete all previous levels**

2. **Generate Diagrams**
   ```
   - System architecture
   - Component relationships
   - Data flow sequences
   - Entity relationships
   - Deployment architecture
   ```

3. **Create Usage Guides**
   ```
   - Installation steps
   - Configuration guide
   - Common operations
   - Troubleshooting
   - Examples
   ```

4. **Document Development**
   ```
   - Project setup
   - Testing approach
   - Build process
   - Deployment
   - Contribution guidelines
   ```

**Output:** Complete project documentation

## Analysis Techniques

### 1. Trace-Based Analysis

**Follow execution paths:**

```
Entry Point → Processing → Output
```

**Example:**
```
Web Request:
URL → Router → Middleware → Controller → Service → Repository → DB
```

### 2. Dependency Analysis

**Map relationships:**

```
Module A depends on Module B
Module B depends on Module C
Module C depends on Module A (circular!)
```

**Tools:**
- Look for import statements
- Check require/include
- Expose dependency injection

### 3. Pattern Recognition

**Identify common patterns:**

```
Singleton: single instance, private constructor
Factory: create methods, object construction
Observer: event emitters, subscribers
Repository: data access abstraction
Strategy: interchangeable algorithms
Decorator: wrapper functions, middleware
```

### 4. Data Flow Analysis

**Track data transformations:**

```
Input → Validation → Transform → Process → Store → Output
```

**Key questions:**
- What are the data structures?
- How is data validated?
- What transformations occur?
- Where is data stored?
- How is it retrieved?

## Code Reading Strategies

### Bottom-Up Reading

**When to use:**
- Understanding utility functions
- Analyzing algorithms
- Studying data structures

**Process:**
```
Small functions → Classes → Modules → Subsystem → System
```

### Top-Down Reading

**When to use:**
- Understanding architecture
- Mapping component relationships
- Following user flows

**Process:**
```
Main entry → High-level logic → Component details → Implementation
```

### Trace-Driven Reading

**When to use:**
- Understanding specific features
- Debugging flows
- Documenting use cases

**Process:**
```
Identify feature → Find entry point → Trace execution → Document
```

## Project Type-Specific Analysis

### Web Applications

**Focus areas:**

1. **Frontend**
   - Framework (React, Vue, Angular)
   - Routing structure
   - State management
   - Component hierarchy
   - API integration

2. **Backend**
   - Server framework (Express, FastAPI, Django)
   - Route definitions
   - Middleware chain
   - Authentication/authorization
   - Error handling

3. **Database**
   - Schema design
   - ORM models
   - Migrations
   - Queries
   - Indexes

**Key files:**
```
- package.json, requirements.txt
- routes/, controllers/, views/
- models/, schemas/, entities/
- middleware.py, interceptors/
- config/, settings/
```

### API Services

**Focus areas:**

1. **Endpoint Structure**
   - URL patterns
   - HTTP methods
   - Request/response models
   - Status codes
   - Error responses

2. **Business Logic**
   - Service layer
   - Validation
   - Processing logic
   - External integrations

3. **API Design**
   - REST principles
   - Versioning
   - Authentication
   - Rate limiting
   - Documentation

**Key files:**
```
- routes/, api/, endpoints/
- controllers/, handlers/
- services/, business/
- models/, schemas/, dtos/
- middleware/, guards/
- swagger.json, openapi.yaml
```

### Libraries/Packages

**Focus areas:**

1. **Public API**
   - Exported functions/classes
   - API surface
   - Parameter types
   - Return types
   - Error handling

2. **Core Functionality**
   - Main algorithms
   - Data structures
   - Utilities
   - Helpers

3. **Usage Patterns**
   - Examples in README
   - Test files
   - Documentation
   - Demo files

**Key files:**
```
- index.js, main.py, __init__.py
- lib/, src/
- examples/, samples/
- tests/, test/
- README.md, API.md
```

### Data Projects

**Focus areas:**

1. **Pipeline**
   - Data sources
   - Extraction
   - Transformation
   - Loading
   - Scheduling

2. **Processing**
   - ETL/ELT logic
   - Validation
   - Aggregation
   - Analysis
   - Machine learning

3. **Storage**
   - Databases
   - Data warehouses
   - File systems
   - Caching
   - Backups

**Key files:**
```
- pipeline/, etl/, jobs/
- notebooks/, scripts/
- models/, schemas/
- config/, parameters/
- requirements.txt, environment.yml
```

## Documentation Structure

### Executive Summary (1-2 paragraphs)

```
What:
- Project name and purpose
- Type of application
- Main features

How:
- Technology stack (brief)
- Architecture pattern (brief)

Why:
- Problem it solves
- Target users/use cases
```

### Architecture Overview

```
High-level diagram
- Components and their roles
- Data flow
- External integrations

Directory structure
- Top-level directories explained
- Key files identified
- Organization pattern
```

### Component Details

```
For each major component:
- Purpose and responsibility
- Key classes/functions
- Interfaces
- Dependencies
- Usage examples
```

### Setup and Usage

```
Installation:
- Prerequisites
- Dependencies
- Build steps
- Configuration

Running:
- Development mode
- Production mode
- Environment variables
- Common issues
```

### Development Guide

```
Project setup:
- Clone and install
- Development server
- Testing
- Building

Contributing:
- Code structure
- Adding features
- Testing guidelines
- Commit conventions
```

## Quality Metrics

### Completeness Checklist

**Must have:**
- [x] Project purpose explained
- [x] Architecture documented
- [x] Main components listed
- [x] Setup instructions provided
- [x] Key APIs/interfaces documented

**Should have:**
- [x] Diagrams included
- [x] Code examples provided
- [x] Dependencies listed
- [x] Design decisions explained
- [x] Testing approach documented

**Nice to have:**
- [x] Performance considerations
- [x] Security notes
- [x] Deployment guide
- [x] Troubleshooting section
- [x] Changelog/version history

### Accuracy Verification

**Cross-check:**
- Code matches documentation
- Examples actually work
- Dependencies are current
- Links are valid
- Diagrams reflect reality

**Validation:**
- Try the setup instructions
- Run code examples
- Test API endpoints
- Verify imports
- Check configurations

## Common Analysis Mistakes

### 1. Getting Lost in Details

**Problem:** Spending time on boilerplate code

**Solution:** Focus on unique, business-logic code

### 2. Ignoring Configuration

**Problem:** Missing how the project is configured

**Solution:** Always examine config files and environment variables

### 3. Missing the Big Picture

**Problem:** Documenting trees instead of forest

**Solution:** Start with architecture, drill down as needed

### 4. Assuming Without Verifying

**Problem:** Documenting what you think, not what is

**Solution:** Trace code execution, verify assumptions

### 5. Overlooking Documentation

**Problem:** Not reading existing docs

**Solution:** Always start with README, docs/, comments

## Time Management

### Time Allocation Guide

```
Small project (<100 files):
- Quick scan: 5-10 min
- Structure: 15-20 min
- Details: 30-40 min
- Total: 1-1.5 hours

Medium project (100-500 files):
- Quick scan: 10-15 min
- Structure: 30-45 min
- Details: 1-2 hours
- Total: 2-3 hours

Large project (500-2000 files):
- Quick scan: 15-20 min
- Structure: 1-2 hours
- Details: 3-5 hours
- Total: 4-7 hours

Very large (2000+ files):
- Focus on core modules
- Use sampling techniques
- Iterative approach
- Multiple sessions
```

### Prioritization Matrix

```
High Impact, Low Effort:
- README and configs
- Main entry points
- Package.json/requirements.txt

High Impact, High Effort:
- Core algorithms
- Architecture patterns
- Data models

Low Impact, Low Effort:
- Utility functions
- Helper classes
- Standard patterns

Low Impact, High Effort:
- Test files
- Build scripts
- CI/CD configs (skip initially)
```

## Progressive Deepening

**Start shallow:**
1. What is this project?
2. What are the main parts?
3. How do they connect?

**Go deeper:**
1. How does each part work?
2. What are the key functions?
3. What data flows through?

**Full detail:**
1. Implementation specifics
2. Design decisions
3. Edge cases
4. Performance characteristics

This framework ensures systematic, comprehensive analysis while managing time effectively.
