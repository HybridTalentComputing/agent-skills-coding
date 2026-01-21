# Data Models - {{PROJECT_NAME}}

**Last Updated:** {{DATE}}

## Table of Contents

- [Overview](#overview)
- [Entity Relationships](#entity-relationships)
- [Core Data Models](#core-data-models)
- [API Models](#api-models)
- [Configuration Models](#configuration-models)
- [Data Flow](#data-flow)
- [Validation](#validation)
- [Storage](#storage)

## Overview

This document describes all data structures, schemas, and their relationships in {{PROJECT_NAME}}.

### Data Model Categories

{{DATA_MODEL_CATEGORIES}}

---

## Entity Relationships

### High-Level ER Diagram

```mermaid
erDiagram
    {{ENTITY_RELATIONSHIPS}}
```

### Key Relationships

{{KEY_RELATIONSHIPS}}

---

## Core Data Models

### {{ENTITY_1}}

**File Location:** `{{FILE_PATH}}`

**TypeScript Interface:**
```typescript
{{INTERFACE_DEFINITION}}
```

**Purpose:** {{PURPOSE}}

**Fields:**

| Field | Type | Description | Validation |
|-------|------|-------------|------------|
| {{FIELD_1}} | {{TYPE}} | {{DESCRIPTION}} | {{VALIDATION}} |
| {{FIELD_2}} | {{TYPE}} | {{DESCRIPTION}} | {{VALIDATION}} |

**Example:**
```typescript
{{EXAMPLE}}
```

---

## API Models

### Request Models

#### {{REQUEST_MODEL_1}}

**Purpose:** {{PURPOSE}}

**Interface:**
```typescript
{{INTERFACE}}
```

**Usage:**
```typescript
{{USAGE_EXAMPLE}}
```

#### {{REQUEST_MODEL_2}}

{{REPEAT_PATTERN}}

### Response Models

#### {{RESPONSE_MODEL_1}}

**Purpose:** {{PURPOSE}}

**Interface:**
```typescript
{{INTERFACE}}
```

---

## Configuration Models

### {{CONFIG_ENTITY_1}}

**File:** `{{CONFIG_FILE}}`

**Schema:**
```typescript
{{SCHEMA}}
```

**Configuration Options:**

| Option | Type | Default | Description |
|--------|------|---------|-------------|
| {{OPTION_1}} | {{TYPE}} | {{DEFAULT}} | {{DESCRIPTION}} |
| {{OPTION_2}} | {{TYPE}} | {{DEFAULT}} | {{DESCRIPTION}} |

---

## Data Flow

### {{DATA_FLOW_1}}

```mermaid
flowchart TD
    {{DATA_FLOW_DIAGRAM}}
```

**Description:** {{DESCRIPTION}}

---

## Validation

### Validation Rules

{{VALIDATION_RULES}}

### Error Handling

{{ERROR_HANDLING}}

---

## Storage

### Database Schema

{{DATABASE_SCHEMA}}

### File Storage

{{FILE_STORAGE}}

### Caching Strategy

{{CACHING_STRATEGY}}

---

## Migrations

### Schema Evolution

{{SCHEMA_EVOLUTION}}

---

*See [ARCHITECTURE.md](ARCHITECTURE.md) for system architecture*
*See [API.md](API.md) for API data contracts*
