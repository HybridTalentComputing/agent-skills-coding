# Code Patterns Recognition

Guide to identifying common architectural and design patterns in codebases.

## Architectural Patterns

### MVC (Model-View-Controller)

**Indicators:**
```
Directory structure:
├── models/         # Data structures, business logic
├── views/          # Templates, UI components
├── controllers/    # Request handlers, coordinators

or:
├── M/              # Models
├── V/              # Views
├── C/              # Controllers
```

**Characteristics:**
- Models contain data and business rules
- Views handle presentation
- Controllers coordinate between models and views
- Common in web frameworks (Django, Rails, Express)

**File naming:**
- `UserModel`, `UserView`, `UserController`
- `user.service.ts`, `user.controller.ts`
- `views/user.py`, `controllers/user.py`

### Layered Architecture

**Indicators:**
```
├── presentation/   # UI, API endpoints
├── business/       # Business logic
├── persistence/    # Data access
├── infrastructure/ # External services

or:
├── controllers/    # Presentation layer
├── services/       # Business logic
├── repositories/   # Data access
├── entities/       # Domain models
```

**Characteristics:**
- Clear separation of concerns
- Each layer has specific responsibility
- Upper layers depend on lower layers
- Common in enterprise applications

### Microservices

**Indicators:**
```
├── services/
│   ├── auth-service/
│   ├── user-service/
│   ├── payment-service/
│   └── notification-service/
├── api-gateway/
├── docker-compose.yml
├── /proto or /grpc  # Service definitions
```

**Characteristics:**
- Each service in own directory
- Service-specific package.json/requirements.txt
- API gateway or service mesh
- Message queue integration
- Service discovery mechanism

### Event-Driven

**Indicators:**
```
├── events/          # Event definitions
├── handlers/        # Event processors
├── publishers/      # Event emitters
├── subscribers/     # Event consumers
├── queue/           # Message queue setup
```

**Characteristics:**
- Event emitters and listeners
- Message queue (RabbitMQ, Kafka, Redis)
- Async processing
- Event sourcing patterns

**Code patterns:**
```python
# Event emitter
emit("user.created", user_data)

# Event listener
on("user.created", handle_new_user)
```

```javascript
// Event emitter
eventBus.emit('user.created', userData);

// Event listener
eventBus.on('user.created', handleNewUser);
```

## Design Patterns

### Repository Pattern

**Indicators:**
```
├── repositories/    # Data access layer
│   ├── user.repository.ts
│   ├── product.repository.ts
│   └── order.repository.ts
```

**Characteristics:**
- Abstract data access
- CRUD operations (create, read, update, delete)
- Query methods
- Database interaction hidden

**Code example:**
```python
class UserRepository:
    def find_by_id(self, id): pass
    def find_all(self): pass
    def save(self, user): pass
    def delete(self, id): pass
    def find_by_email(self, email): pass
```

### Factory Pattern

**Indicators:**
```
├── factories/       # Object creation
│   ├── user.factory.ts
│   └── product.factory.ts
```

**Characteristics:**
- Create objects without specifying exact class
- Centralized creation logic
- Common naming: `create*()`, `make*()`, `*Factory`

**Code example:**
```python
class UserFactory:
    @staticmethod
    def create(data):
        return User(**data)

# or
def create_user(data):
    return User(**data)
```

### Singleton Pattern

**Indicators:**
```
- Private constructors
- Static getInstance() methods
- Global instances
- Module-level singletons
```

**Characteristics:**
- Only one instance exists
- Global access point
- Used for: configs, connections, caches

**Code example:**
```python
class Database:
    _instance = None

    def __new__(cls):
        if cls._instance is None:
            cls._instance = super().__new__(cls)
        return cls._instance
```

### Observer Pattern

**Indicators:**
```
├── observers/       # Event subscribers
├── subjects/        # Event publishers
├── events/          # Event definitions
```

**Characteristics:**
- One-to-many relationship
- Publishers and subscribers
- Event emission and handling
- Common in UI frameworks, real-time systems

**Code example:**
```python
class Subject:
    def __init__(self):
        self._observers = []

    def attach(self, observer):
        self._observers.append(observer)

    def notify(self, data):
        for observer in self._observers:
            observer.update(data)
```

### Strategy Pattern

**Indicators:**
```
├── strategies/      # Interchangeable algorithms
│   ├── payment.strategy.ts
│   └── sorting.strategy.ts
```

**Characteristics:**
- Multiple algorithms for same task
- Interchangeable at runtime
- Common in: sorting, payment, validation

**Code example:**
```python
class PaymentStrategy:
    def pay(self, amount): pass

class CreditCardStrategy(PaymentStrategy):
    def pay(self, amount):
        # Process credit card
        pass

class PayPalStrategy(PaymentStrategy):
    def pay(self, amount):
        # Process PayPal
        pass
```

### Dependency Injection

**Indicators:**
```
- Constructor injection
- Setter injection
- Service containers
- IoC containers
```

**Characteristics:**
- Dependencies passed in, not created internally
- Easier testing
- Loose coupling
- Common in: Angular, Spring, .NET

**Code example:**
```python
class UserService:
    def __init__(self, user_repo, email_service):
        self.user_repo = user_repo
        self.email_service = email_service
```

## Web Application Patterns

### REST API

**Indicators:**
```
├── routes/          # Route definitions
├── controllers/     # Request handlers
├── middleware/      # Request processing pipeline
├── validators/      # Input validation
```

**Characteristics:**
- HTTP methods (GET, POST, PUT, DELETE)
- Resource-based URLs
- Stateless
- JSON request/response

**Code example:**
```python
@app.get("/users/{id}")
def get_user(id: int):
    return user_service.find(id)

@app.post("/users")
def create_user(user: UserCreate):
    return user_service.create(user)
```

### GraphQL API

**Indicators:**
```
├── schema/          # GraphQL schema
├── resolvers/       # Field resolvers
├── queries/         # Query definitions
├── mutations/       # Mutation definitions
```

**Characteristics:**
- Single endpoint
- Schema-first design
- Query language
- Strongly typed

### MVC Web Framework

**Indicators:**
```
Django:
├── models.py
├── views.py
├── urls.py
├── forms.py
└── templates/

Rails:
├── app/
│   ├── models/
│   ├── views/
│   └── controllers/
```

**Characteristics:**
- Convention over configuration
- Scaffolding tools
- Active Record pattern
- Template engines

## Data Access Patterns

### ORM (Object-Relational Mapping)

**Indicators:**
```
├── models/          # Database models
├── migrations/      # Schema migrations
├── seeders/         # Seed data
```

**Characteristics:**
- Classes map to tables
- Objects map to rows
- Methods for CRUD
- Relationship definitions

**Code example:**
```python
class User(Base):
    __tablename__ = 'users'
    id = Column(Integer, primary_key=True)
    email = Column(String(255), unique=True)
    posts = relationship("Post", back_populates="author")
```

### Query Builder

**Indicators:**
```
- Fluent interface
- Method chaining
- Where, orderBy, limit methods
```

**Code example:**
```python
query = (db.query(User)
    .filter(User.active == True)
    .order_by(User.created_at)
    .limit(10))
```

### Repository (Data Access Layer)

**Indicators:**
```
├── repositories/
│   ├── base.repository.ts
│   ├── user.repository.ts
│   └── product.repository.ts
```

**Characteristics:**
- Abstraction over data source
- Custom query methods
- Unit of work pattern
- Testable data access

## Concurrency Patterns

### Promise/Future

**Indicators:**
```
- async/await keywords
- Promise objects
- then/catch chains
- Future objects
```

**Code example:**
```python
async def fetch_user(id):
    return await database.find_user(id)
```

```javascript
async function fetchUser(id) {
    return await database.findUser(id);
}
```

### Reactive Programming

**Indicators:**
```
- Observables
- Streams
- Subscriptions
- Operators (map, filter, reduce)
```

**Code example:**
```javascript
userStream$
    .pipe(
        filter(user => user.active),
        map(user => user.name)
    )
    .subscribe(name => console.log(name));
```

### Thread/Process Pool

**Indicators:**
```
├── workers/         # Worker threads
├── tasks/           # Task definitions
├── queues/          # Task queues
```

**Characteristics:**
- Parallel execution
- Thread-safe operations
- Work queues
- Result aggregation

## Security Patterns

### Authentication/Authorization

**Indicators:**
```
├── auth/            # Authentication logic
├── middleware/      # Auth middleware
├── guards/          # Auth guards
├── policies/        # Access policies
```

**Characteristics:**
- JWT tokens
- Session management
- Role-based access
- Permission checks

**Code example:**
```python
@app.route("/admin")
@login_required
@admin_required
def admin_panel():
    return render_template("admin.html")
```

### Middleware Chain

**Indicators:**
```
├── middleware/
│   ├── auth.middleware.ts
│   ├── logging.middleware.ts
│   ├── cors.middleware.ts
│   └── error.middleware.ts
```

**Characteristics:**
- Request/response interception
- Chain of responsibility
- Cross-cutting concerns
- Common in Express, FastAPI, Django

## Testing Patterns

### Unit Testing

**Indicators:**
```
├── __tests__/
├── tests/unit/
├── spec/
```

**Characteristics:**
- Test individual functions/classes
- Mocked dependencies
- Fast execution
- Isolated tests

### Integration Testing

**Indicators:**
```
├── tests/integration/
├── e2e/
├── tests/api/
```

**Characteristics:**
- Test component interactions
- Real dependencies
- Slower execution
- Database connections

### Test Fixtures

**Indicators:**
```
├── fixtures/
├── tests/fixtures/
├── mock-data/
```

**Characteristics:**
- Sample data
- Test configurations
- Factory patterns
- Common setup/teardown

## API Patterns

### Client-Server

**Indicators:**
```
├── client/          # API client
├── server/          # API server
├── shared/          # Shared types/models
```

### GraphQL Resolvers

**Indicators:**
```
├── resolvers/
│   ├── query.resolvers.ts
│   ├── mutation.resolvers.ts
│   └── field.resolvers.ts
```

**Characteristics:**
- Nested resolvers
- Data loading
- Batching
- Caching

## Configuration Patterns

### Environment-Based Config

**Indicators:**
```
├── config/
│   ├── development.json
│   ├── production.json
│   └── test.json
├── .env.development
├── .env.production
```

**Characteristics:**
- Multiple environment configs
- Feature flags
- Environment variables
- Config validation

### Options Pattern

**Indicators:**
```
- Options objects
- Default values
- Options merging
```

**Code example:**
```python
def process_data(data, options=None):
    opts = {
        'validate': True,
        'timeout': 30,
        'retries': 3
    }
    if options:
        opts.update(options)
```

## Pattern Recognition Tips

### 1. Look at Imports

```python
from abc import ABC, abstractmethod  # Abstract patterns
from dataclasses import dataclass    # Data classes
from typing import Protocol          # Protocols
import pubsub                         # Observer pattern
```

### 2. Check Class Names

```
Factory, Builder, Creator  → Factory pattern
Repository, DAO            → Repository pattern
Controller, Handler        → MVC/Controller
Service, UseCase           → Service layer
Middleware, Interceptor    → Middleware pattern
Strategy, Provider         → Strategy pattern
```

### 3. Examine Method Names

```
create*, make*             → Factory pattern
get*, find*                → Accessor/Repository
notify*, emit*, publish*   → Observer pattern
validate*, check*          → Strategy/Validator
process*, handle*          → Handler/Controller
connect*, disconnect*      → Connection/Resource management
```

### 4. Study Directory Structure

```
Direct naming often indicates pattern:
- models/, views/, controllers/   → MVC
- services/, repositories/        → Layered
- factories/, builders/           → Creational patterns
- observers/, listeners/          → Observer
- strategies/                     → Strategy pattern
- middleware/, interceptors/      → Middleware
```

### 5. Look for Patterns in Code

**Singleton:**
```python
_instance = None
def getInstance():  # or __new__
```

**Factory:**
```python
def create_*():    # or make_*
    return Object()
```

**Observer:**
```python
def add_observer():
def notify_observers():
```

## Common Anti-Patterns

### God Object

**Indicators:**
- Single class does everything
- Thousands of lines
- Many responsibilities

### Code Duplication

**Indicators:**
- Similar code in multiple places
- Copy-pasted logic
- Should use abstraction

### Tight Coupling

**Indicators:**
- Hard to test
- Changes cascade
- No clear interfaces

## Pattern Application Guide

**When analyzing, note:**

1. **Which patterns are used?**
   - Identify by structure and naming

2. **Why were they chosen?**
   - Problem being solved
   - Benefits provided

3. **How are they implemented?**
   - Specific implementation details
   - Framework-specific variations

4. **Are they appropriate?**
   - Do they fit the use case?
   - Any anti-patterns present?

Understanding these patterns helps in quickly grasping a codebase's architecture and design decisions.
