# Development Guide

## Project Types
This starter supports development of both Flask applications and Flask extensions:
- **Flask Applications**: Complete web applications with routes, templates, and databases
- **Flask Extensions**: Reusable packages that extend Flask functionality for other applications

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

## Development Workflow

### For Flask Applications

#### Running the Application
```bash
# Development server
pipenv run flask run

# Or using Python directly
pipenv run python run.py
```

### For Flask Extensions

#### Testing Extensions
```bash
# Test extension in isolation
pipenv run pytest tests/test_extension.py

# Test with sample Flask app
pipenv run python tests/test_app.py

# Test compatibility with different Flask versions
tox
```

#### Extension Development
- Create extension class with `init_app()` method
- Follow Flask extension naming conventions
- Implement proper teardown and configuration
- Include comprehensive documentation and examples

### Common Testing
```bash
# Run all tests
pipenv run pytest

# Run with coverage
pipenv run pytest --cov=app

# Run specific test file
pipenv run pytest tests/unit/test_models.py
```

### Code Quality
```bash
# Format code
pipenv run black .

# Lint code
pipenv run flake8

# Type checking (if using mypy)
pipenv run mypy app/
```

## Database Management

### Migrations
```bash
# Create new migration
pipenv run flask db migrate -m "Description of changes"

# Apply migrations
pipenv run flask db upgrade

# Rollback migration
pipenv run flask db downgrade
```

### Database Reset (Development Only)
```bash
# WARNING: This will delete all data
rm app.db
pipenv run flask db upgrade
```

## Decision Framework Integration
Use the decision framework to avoid analysis paralysis:

#### Quick Decisions (< 2 minutes)
- Code style and formatting → Follow existing patterns
- Standard operations (CRUD, routing) → Use established patterns
- Testing approach → Follow current test structure

#### Standard Decisions (< 10 minutes)  
- New features → Break into smallest components, start simple
- Database changes → Use Alembic migrations, follow model patterns
- API design → Follow existing API structure and conventions

#### Decision Hierarchy
1. **Simplest working solution** (preferred default)
2. **Established pattern** from existing codebase  
3. **Industry standard** approach
4. **Custom solution** (only if 1-3 insufficient)

#### Emergency Decision Protocol
If stuck in analysis:
1. Stop analysis immediately
2. Choose simplest approach that could work
3. Implement and iterate
4. Refer to `docs/copilot/DECISION_FRAMEWORK.md` for detailed guidance

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

## AI Collaboration Workflow

### Time-Boxed Development Process
Following the enhanced 8-step workflow with analysis paralysis prevention:

#### Pre-Development (Steps 1-3)
```bash
# 1. Git Status Check (MANDATORY)
git status

# 2. Analysis Phase (MAX 10 minutes)
# - Request analysis from Copilot
# - Limit to 2-3 approaches maximum
# - Focus on simplest viable solution first

# 3. Approval Phase (MAX 5 minutes)
# - Get explicit approval for chosen approach
# - Auto-proceed rule for low-risk changes after 5 minutes
```

#### Development (Steps 4-6)
```bash
# 4. Implementation
# - Follow approved plan
# - Include comprehensive error handling
# - Add detailed docstrings

# 5. Testing
pipenv run pytest --cov=app

# 6. Cleanup and Verification
# - Remove temporary files
# - Reset test database
# - Validate clean state
```

#### Documentation (Steps 7-8)
```bash
# 7. Documentation Updates
# - Update API docs, README, DEVELOPMENT, CHANGELOG
# - Save to Copilot knowledge base:
#   - docs/copilot/INTERACTIONS.md
#   - docs/copilot/PROMPTS.md
#   - docs/copilot/LESSONS.md
#   - docs/copilot/DECISION_FRAMEWORK.md

# 8. Git Commit
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

*Last updated: June 11, 2025*
*This guide evolves with the project. Update it regularly to reflect new patterns and workflows.*
*Last updated: June 10, 2025*
