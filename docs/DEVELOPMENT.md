# Development Guide

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

### Running the Application
```bash
# Development server
pipenv run flask run

# Or using Python directly
pipenv run python run.py
```

### Running Tests
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
- Use application factory pattern
- Organize routes in blueprints
- Keep functions small and focused
- Use type hints consistently

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

## Environment Variables

### Required Variables
- `SECRET_KEY` - Flask secret key for sessions
- `FLASK_ENV` - development/production
- `DATABASE_URL` - Database connection string (optional)

### Optional Variables
- `DEBUG` - Enable debug mode (development only)
- `LOG_LEVEL` - Logging level (DEBUG, INFO, WARNING, ERROR)

## Directory Structure
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
├── migrations/             # Database migrations
├── Pipfile                 # Dependencies
└── run.py                  # Application entry point
```

---
*Last updated: June 10, 2025*
