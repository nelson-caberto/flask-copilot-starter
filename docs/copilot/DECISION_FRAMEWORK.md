# Quick Decision Framework for Copilot Collaboration

## ⚡ **AI Setup**: Say `reload_context.md` for instant project context

## ⚡ **SPEED RULES**: Default to action over analysis

**PRIMARY RULE**: Choose the simplest solution and ship it. Perfect is the enemy of good.

## Decision Speed Guidelines

### ⚡ Immediate Decisions (< 2 minutes) - NO ANALYSIS NEEDED
**Just do these patterns without thinking:**

#### Code Style & Formatting
- **Copy existing file patterns** - don't reinvent style
- **Match current naming** - follow what's already there  
- **Use same indentation** - maintain consistency

#### Standard Flask Operations
- **CRUD operations** → Copy existing model patterns EXACTLY
- **API endpoints** → Follow current routing structure EXACTLY
- **Database queries** → Use established ORM patterns EXACTLY
- **Error handling** → Copy existing error patterns EXACTLY
- **Flask-Migrate** → Generate migration IMMEDIATELY (no delays)

#### Testing
- **Unit tests** → Copy existing test file structure
- **Integration tests** → Use current testing patterns
- **Fixtures** → Match existing fixture patterns
- **Test generation** → 🧪 **CRITICAL**: Check `docs/copilot/TEST_CHEATSHEET.md` to verify actual code structure before generating ANY tests

### 🚀 Quick Decisions (< 5 minutes) - MINIMAL ANALYSIS
**Simple choice required - pick the obvious option:**

#### Library Choices (Decision Tree)
```
Need a library?
├── Already in requirements? → USE IT (stop here)
├── Standard Flask library? → USE IT (Flask-Login, Flask-WTF, etc.)
└── Not standard? → Research for 5 minutes MAX, then choose most popular
```

#### Architecture Patterns (Decision Tree)
```
Need architecture pattern?
├── Pattern exists in codebase? → EXTEND IT (stop here)
├── Standard Flask pattern exists? → USE IT (Blueprints, Application Factory)
└── Custom needed? → Use simplest approach that works
```

### ⏱️ Standard Decisions (< 10 minutes) - MODERATE ANALYSIS
**Only for significant changes - still time-boxed:**

#### New Features (Decision Tree)
```
Building new feature?
├── Break into smallest components (2 min)
├── Identify reusable patterns (3 min)  
├── Choose established Flask approach (3 min)
├── Security check (2 min)
└── PROCEED - don't overthink
```
## ⚡ Decision Trees (FAST LOOKUPS)

### Authentication Implementation (< 3 minutes)
```
Need Authentication?
├── Simple login? → Flask-Login (DONE - no analysis)
├── API tokens? → Flask-JWT-Extended (DONE - no analysis)  
├── OAuth? → Authlib (DONE - no analysis)
└── Complex? → Use Flask-Login + research later (DONE)
```

### Database Operations (< 2 minutes)
```
Database Operation?
├── Basic CRUD? → Copy existing model patterns (IMMEDIATE)
├── Complex query? → SQLAlchemy ORM (IMMEDIATE)
├── Performance issue? → Profile first, optimize later (IMMEDIATE)
└── Migration needed? → flask db migrate (IMMEDIATE)
```

### Testing Strategy (< 2 minutes)
```
What to Test?
├── New function? → Unit test (IMMEDIATE)
├── New route? → Integration test (IMMEDIATE)
├── New feature? → Both unit + integration (IMMEDIATE)
└── Bug fix? → Reproduce + fix test (IMMEDIATE)

🧪 CRITICAL: Before generating ANY test, check docs/copilot/TEST_CHEATSHEET.md
- Verify actual model fields and types
- Check actual route paths and methods  
- Confirm actual form fields and validators
- Use real import paths from codebase
```

## 🚫 Anti-Patterns to Eliminate

### Analysis Paralysis KILLERS
❌ **NEVER do this**:
- Generating 4+ implementation options (MAX 3)
- Spending >10 minutes on ANY architectural decision
- "What's the best approach?" questions without context
- Researching multiple libraries for standard Flask tasks
- Custom solutions when established patterns exist

✅ **DO this instead**:
- Present 2 options with clear recommendation
- Set 5-minute timer for any decision
- Start with simplest working solution
- Use Flask ecosystem defaults
- Copy existing patterns in codebase

### Decision Loop ELIMINATORS
❌ **Kill these patterns**:
- Asking "What approach should we use?" repeatedly
- Reopening architectural decisions that are already made
- Switching implementation mid-development without clear reason
- Seeking perfect solution before shipping working code

✅ **Use these patterns**:
- Make decision with current info and move forward
- Document why you chose approach (for future reference)
- Ship working solution, iterate based on real feedback
- Refactor when requirements become concrete, not theoretical

## 🆘 Emergency Decision Protocol (When Stuck)

### Step 1: STOP (30 seconds)
- Stop current analysis immediately
- State problem in ONE sentence
- Identify simplest solution that could work

### Step 2: DEFAULT (2 minutes)
- Choose most standard Flask approach
- Use existing pattern from codebase if available
- Document: "Using [X] because it's standard and works"
- PROCEED immediately

### Step 3: Ship & Iterate
- Implement the default solution
- Get it working and shipped
- Gather real feedback
- Refactor based on actual needs (not theoretical problems)

## 📊 Success Metrics (Track These)

### 🟢 Good Decision Velocity
- ✅ Analysis phase: 3-7 minutes average
- ✅ Working solution within 20 minutes for simple tasks
- ✅ Complex features broken into 30-minute chunks
- ✅ Database changes include migration immediately

### 🟡 Warning Signs (Fix These)
- ⚠️ Analysis exceeding 10 minutes on any task
- ⚠️ More than 3 implementation options presented
- ⚠️ Repeated architecture discussions for same component
- ⚠️ No working code within 25 minutes of starting

### 🔴 Red Flags (EMERGENCY PROTOCOL)
- 🚨 Analysis paralysis lasting >15 minutes
- 🚨 Going in circles on implementation approach
- 🚨 Custom solutions when standard patterns exist
- 🚨 Perfect-seeking behavior preventing shipping

## 🎯 Remember: VELOCITY > PERFECTION

**Core Principle**: Ship working solutions in 30 minutes or less. Perfect solutions never ship.

---
*Last updated: June 11, 2025*
*Use this framework to maintain velocity while ensuring quality. When in doubt, choose the simple path.*
