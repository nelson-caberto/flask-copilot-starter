# Development Guide ⚡

> **SPEED-FIRST DEVELOPMENT** | Focus: Immediate Action | Time-Boxed Workflows | Anti-Paralysis Measures

## ⚡ Quick Start (< 5 minutes)

### ⚡ **AI Setup**: Just say `reload_context.md` for instant context loading

### ⚡ **Environment Setup** (Manual if needed)
```bash
# IMMEDIATE SETUP - NO ANALYSIS
git clone <your-repo>
cd flask-copilot-starter
pipenv install --dev
pipenv shell
```

## ⚡ Testing Guidelines (Speed-First)

### 🧪 **CRITICAL**: Check `docs/copilot/TEST_CHEATSHEET.md` before generating ANY tests
**Prevents AI "guessing" - ensures tests use actual codebase structure**

### ⚡ Speed-First Test Execution Patterns
**MANDATORY: Use grep to filter pytest output for efficiency**

#### Immediate Test Health Check (< 30 seconds)
```bash
# Quick pass/fail status - avoid processing full output
pytest --tb=no | grep -E "(PASSED|FAILED|ERROR)" | tail -5

# Emergency health check - binary result
pytest | grep -q "FAILED" && echo "❌ TESTS FAILING" || echo "✅ ALL TESTS PASS"
```

#### Fast Failure Analysis (< 2 minutes)
```bash
# Get only failure details
pytest -x --tb=short | grep -A 10 -B 2 "FAILED\|ERROR"

# Filter specific error types
pytest | grep -E "(AssertionError|TypeError|ValueError)" -A 3

# Database test issues only
pytest | grep -i -C 3 "database\|sql\|migration"
```

#### Coverage Analysis (< 1 minute)
```bash
# Coverage percentage only - no full report
pytest --cov=app | grep -E "TOTAL.*[0-9]+%"

# Missing coverage lines only
pytest --cov=app --cov-report=term-missing | grep -E "Missing"
```

### Test DatabaseTUP - NO ANALYSIS
git clone <repository-url> && cd flask-copilot-starter
pipenv install && pipenv shell
cp .env.example .env
pipenv run flask db init && pipenv run flask db migrate -m "Initial" && pipenv run flask db upgrade
pipenv run flask run  # READY TO CODE
```

## Project Types
This starter supports development of both Flask applications and Flask extensions:
- **Flask Applications**: Complete web applications with routes, templates, and databases  
- **Flask Extensions**: Reusable packages that extend Flask functionality for other applications

## ⚡ Anti-Paralysis Development Workflow

### SPEED-FIRST DECISION HIERARCHY (< 2 minutes per decision)
1. **SIMPLEST SOLUTION** (80% default choice) - Use existing patterns
2. **STANDARD PATTERN** (15% of cases) - Follow Flask conventions  
3. **CUSTOM APPROACH** (5% only) - When 1-2 insufficient

### NO-ANALYSIS ZONES ⚡
**Auto-Proceed Rules** - These operations require ZERO analysis:
- CRUD operations → Use existing model patterns
- Route creation → Follow blueprint structure
- Database changes → Execute Flask-Migrate workflow
- Form validation → Use WTForms patterns
- Authentication → Use Flask-Login patterns

### EMERGENCY DECISION PROTOCOL
**If stuck > 2 minutes on ANY decision:**
1. ⏰ STOP analysis immediately
2. 🎯 Choose simplest approach that could work
3. 🚀 Implement and iterate
4. 📖 Refer to `docs/copilot/DECISION_FRAMEWORK.md`

## Prerequisites
- Python 3.8 or higher
- Pipenv for dependency management
- Git for version control

## Initial Setup

### 1. Clone and Navigate
```bash
git clone <repository-url>
cd flask-copilot-starter
```

### 2. Environment Setup
```bash
# Install dependencies
pipenv install

# Install development dependencies
pipenv install --dev

# Activate virtual environment
pipenv shell
```

### 3. Environment Configuration
```bash
# Copy environment template
cp .env.example .env

# Edit .env with your configuration
# At minimum, set a unique SECRET_KEY
```

### 4. Database Setup
```bash
# Initialize database
pipenv run flask db init

# Create migration
pipenv run flask db migrate -m "Initial migration"

# Apply migration
pipenv run flask db upgrade
```

## ⚡ Speed-First Development Workflow

### For Flask Applications

#### Running the Application ⚡
```bash
# IMMEDIATE START - NO DELAYS
pipenv run flask run
# OR
pipenv run python run.py
```

### For Flask Extensions

#### Testing Extensions ⚡
```bash
# FAST TESTING CYCLE
pipenv run pytest tests/test_extension.py | grep -E "(PASSED|FAILED|ERROR)"     # Unit tests
pipenv run python tests/test_app.py          # Integration test
tox                                           # Multi-version test
```

#### Extension Development ⚡
**NO-ANALYSIS RULES:**
- Extension class with `init_app()` → STANDARD pattern, use immediately
- Flask extension naming → Follow `Flask-ExtensionName` convention
- Configuration → Use Flask config system, no custom patterns
- Documentation → Include usage examples, API reference

### ⚡ Immediate Testing Workflows
```bash
# FAST TEST EXECUTION - NO DELAYS ⚡ GREP REQUIRED
pipenv run pytest | grep -E "(PASSED|FAILED|ERROR)"           # Status only
pipenv run pytest --cov=app | grep -E "TOTAL.*[0-9]+%"        # Coverage %
pipenv run pytest | grep -q "FAILED" && echo "❌ FIX NEEDED" || echo "✅ GOOD"  # Quick check
pipenv run pytest tests/unit/test_models.py | grep -E "(PASSED|FAILED|ERROR)"   # Specific file

# ⚡ SPEED-FIRST: Use grep to filter output for specific information
# Traditional commands (avoid - use grep versions above instead):
# pipenv run pytest                              # All tests (too verbose)
# pipenv run pytest --cov=app                   # With coverage (too verbose)
```

### ⚡ Code Quality (Auto-Format)
```bash
# IMMEDIATE FORMATTING - NO ANALYSIS
pipenv run black .        # Format code
pipenv run flake8         # Lint code  
pipenv run mypy app/      # Type checking (if using mypy)
```

## ⚡ Database Management (NO DELAYS)

### Flask-Migrate Workflow ⚡
```bash
# IMMEDIATE EXECUTION - NO ANALYSIS PHASE
pipenv run flask db migrate -m "Description"   # Create migration
pipenv run flask db upgrade                    # Apply migration  
pipenv run flask db downgrade                  # Rollback migration
```

### Database Reset ⚡ (Development Only)
```bash
# WARNING: Deletes all data - IMMEDIATE execution
rm app.db
pipenv run flask db upgrade
```

## ⚡ Speed-First Decision Framework Integration

### IMMEDIATE Decision Rules (< 2 minutes)
- **Code style/formatting** → Follow existing patterns, NO ANALYSIS
- **Standard operations** (CRUD, routing) → Use established patterns, NO ANALYSIS  
- **Testing approach** → Follow current test structure, NO ANALYSIS

### FAST Decision Rules (< 10 minutes)  
- **New features** → Break into smallest components, start simple
- **Database changes** → Use Flask-Migrate workflow, follow model patterns
- **API design** → Follow existing API structure and conventions

### Decision Hierarchy ⚡
1. **SIMPLEST working solution** (80% default choice)
2. **ESTABLISHED pattern** from existing codebase (15% of cases)
3. **INDUSTRY standard** approach (4% of cases)
4. **CUSTOM solution** (1% only - when 1-3 insufficient)

### EMERGENCY Decision Protocol ⚡
**If stuck > 2 minutes on ANY decision:**
1. ⏰ **STOP** analysis immediately
2. 🎯 **CHOOSE** simplest approach that could work  
3. 🚀 **IMPLEMENT** and iterate
4. 📖 **REFER** to `docs/copilot/DECISION_FRAMEWORK.md`

## Testing Guidelines

### Test Database
- Tests use separate database (`sqlite:///:memory:` by default)
- Never run tests against production database
- Each test runs in isolated transaction

### Writing Tests
- Follow naming convention: `test_[unit]_[scenario]_[expected_result]`
- Use descriptive docstrings
- Group related tests in classes
- Mock external dependencies

## Common Issues

### Pipenv Issues
```bash
# Clear cache
pipenv --clear

# Reinstall dependencies
pipenv install --dev
```

### Database Issues
```bash
# Reset migrations (development only)
rm -rf migrations/
pipenv run flask db init
pipenv run flask db migrate
pipenv run flask db upgrade
```

## Development Best Practices

### Code Organization

#### For Flask Applications
- Use application factory pattern
- Organize routes in blueprints
- Keep functions small and focused
- Use type hints consistently

#### For Flask Extensions
- Create extension class with `init_app()` method
- Support both application factory and direct app binding
- Provide clear configuration options
- Include comprehensive documentation and examples
- Follow Flask extension naming conventions (`Flask-ExtensionName`)

### Documentation
- Update docstrings when changing functions
- Update API documentation for new endpoints
- Add changelog entries for significant changes
- Keep documentation synchronized with code

### Git Workflow
```bash
# Create feature branch
git checkout -b feature/new-feature

# Make changes and commit
git add .
git commit -m "Add new feature with tests and documentation"

# Update documentation
# Update CHANGELOG.md
# Push and create pull request
```

## ⚡ AI Collaboration Workflow (SPEED-OPTIMIZED)

### Time-Boxed Development Process ⚡
Enhanced 8-step workflow with **STRICT** analysis paralysis prevention:

#### Pre-Development (Steps 1-3) - MAX 15 MINUTES TOTAL
```bash
# 1. Git Status Check ⚡ (MANDATORY - 30 seconds max)
git status

# 2. Analysis Phase ⚡ (STRICTLY ENFORCED: MAX 10 minutes)
# - Request analysis from Copilot  
# - LIMIT to 2-3 approaches maximum
# - Focus on SIMPLEST viable solution first
# - SET TIMER: Auto-proceed after 10 minutes

# 3. Approval Phase ⚡ (STRICTLY ENFORCED: MAX 5 minutes)
# - Get explicit approval for chosen approach
# - AUTO-PROCEED rule: Low-risk changes proceed after 5 minutes
# - EMERGENCY: Choose simplest option if decision takes > 5 minutes
```

#### Development (Steps 4-6) - IMMEDIATE EXECUTION
```bash
# 4. Implementation ⚡ (NO DELAYS)
# - Follow approved plan with NO additional analysis
# - Include comprehensive error handling
# - Add detailed docstrings

# 5. Testing ⚡ (NO DELAYS) - GREP REQUIRED
pipenv run pytest --cov=app | grep -E "TOTAL.*[0-9]+%"

# 6. Cleanup and Verification ⚡ (NO DELAYS)
# - Remove temporary files
# - Reset test database  
# - Validate clean state
```

#### Documentation (Steps 7-8) - IMMEDIATE EXECUTION
```bash
# 7. Documentation Updates ⚡ (NO ANALYSIS)
# - Update API docs, README, DEVELOPMENT, CHANGELOG
# - Save to Copilot knowledge base:
#   - docs/copilot/INTERACTIONS.md
#   - docs/copilot/PROMPTS.md
#   - docs/copilot/LESSONS.md
#   - docs/copilot/DECISION_FRAMEWORK.md

# 8. Git Commit ⚡ (NO DELAYS)
git add .
git commit -m "feat: description of changes"
```

## Environment Variables

### Required Variables
- `SECRET_KEY` - Flask secret key for sessions
- `FLASK_ENV` - development/production
- `DATABASE_URL` - Database connection string (optional)

### Optional Variables
- `DEBUG` - Enable debug mode (development only)
- `LOG_LEVEL` - Logging level (DEBUG, INFO, WARNING, ERROR)

## Directory Structure

### Flask Application Structure
```
flask-copilot-starter/
├── app/
│   ├── __init__.py         # Application factory
│   ├── config.py           # Configuration classes
│   ├── models/             # Database models
│   ├── routes/             # Blueprint routes
│   ├── templates/          # Jinja2 templates
│   └── static/             # Static files
├── tests/
│   ├── conftest.py         # Test configuration
│   ├── unit/               # Unit tests
│   ├── integration/        # Integration tests
│   └── functional/         # Functional tests
├── docs/                   # Documentation
│   ├── copilot/           # AI collaboration knowledge base
│   │   ├── DECISION_FRAMEWORK.md # Quick decision guidelines
│   │   ├── INTERACTIONS.md       # Successful patterns
│   │   ├── PROMPTS.md           # Effective templates
│   │   └── LESSONS.md           # Best practices
│   ├── README.md          # Project overview
│   ├── DEVELOPMENT.md     # This file
│   ├── CHANGELOG.md       # Change history
│   └── COPILOT.md         # AI collaboration guide
├── migrations/             # Database migrations
├── Pipfile                 # Dependencies
└── run.py                  # Application entry point
```

### Flask Extension Structure
```
flask-extension-name/
├── flask_extension_name/
│   ├── __init__.py         # Extension class and init_app()
│   ├── core.py             # Core extension functionality
│   ├── utils.py            # Utility functions
│   └── templates/          # Optional: Extension templates
├── tests/
│   ├── conftest.py         # Test configuration
│   ├── test_extension.py   # Extension unit tests
│   ├── test_integration.py # Integration tests
│   └── test_app.py         # Sample test application
├── docs/                   # Documentation
│   ├── copilot/           # AI collaboration knowledge base
│   │   ├── DECISION_FRAMEWORK.md # Quick decision guidelines  
│   │   ├── INTERACTIONS.md       # Successful patterns
│   │   ├── PROMPTS.md           # Effective templates
│   │   └── LESSONS.md           # Best practices
│   └── API.md             # Extension API documentation
├── examples/               # Usage examples
├── setup.py                # Package configuration
├── MANIFEST.in             # Package manifest
├── tox.ini                 # Multi-environment testing
└── README.md               # Extension documentation
```

---

*Last updated: June 11, 2025 - Enhanced with speed-first anti-paralysis measures*
*This guide evolves with the project. Update it regularly to reflect new patterns and workflows.*
