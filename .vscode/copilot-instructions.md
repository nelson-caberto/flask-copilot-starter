# Flask Development Copilot Instructions

## Project Context
You are working on a Flask web application. Generate code that follows Flask best practices, modern Python conventions, and secure development patterns.

**IMPORTANT: Always ask for explicit permission before creating, modifying, or deleting any files. Never perform any file operations without user consent.**

## Development Workflow Process

### Required Workflow for All Code Changes

**MANDATORY: Follow this exact workflow for every development request:**

1. **Git Status Check**: Before making any changes, verify there are no pending git commits
   - Check `git status` to ensure working directory is clean
   - If there are uncommitted changes, stop and ask user to commit or stash them first
   - Never proceed with new work when there are pending changes

2. **Analysis and Suggestions**: Analyze the request and provide options
   - Break down the request into specific tasks and components
   - Suggest multiple implementation approaches when applicable
   - Explain trade-offs, security implications, and architectural considerations
   - Provide estimated scope of changes (files affected, complexity level)
   - Ask clarifying questions if requirements are unclear

3. **User Approval**: Wait for explicit approval before implementation
   - Present the proposed plan clearly with all affected files listed
   - Get confirmation on the chosen approach
   - Confirm any architectural decisions or new dependencies
   - Only proceed after receiving clear "yes" or "approved" from user

4. **Implementation**: Perform the approved changes
   - Create or modify files as planned
   - Follow all coding standards and security requirements outlined in these instructions
   - Include comprehensive error handling and logging
   - Add detailed docstrings and comments

5. **Comprehensive Testing**: Create or update tests for all changes
   - Write unit tests for new functions and classes
   - Create integration tests for new routes or workflows
   - Include edge cases and error scenarios in tests
   - Test ALL occurrences of modified functionality throughout the project
   - Ensure test coverage remains above 90%
   - Run tests to verify they pass before proceeding

6. **Documentation Updates**: Update all relevant documentation
   - Update API documentation for new or modified endpoints
   - Modify README.md if setup or usage instructions change
   - Update DEVELOPMENT.md for new development procedures
   - Add entries to CHANGELOG.md describing all changes
   - Update any affected configuration documentation

7. **Git Commit**: Create a proper git commit
   - Stage all modified files including tests and documentation
   - Write descriptive commit message following conventional commits format
   - Include summary of changes, files affected, and any breaking changes
   - Commit all changes as a single logical unit

### Workflow Enforcement

- **NEVER skip any step** in this workflow
- **ALWAYS check git status** before starting new work
- **ALWAYS wait for approval** before implementation
- **ALWAYS include comprehensive tests** for every change
- **ALWAYS update documentation** to reflect changes
- **ALWAYS commit changes** with descriptive messages

### Git Commit Message Format

Use conventional commits format:
```
type(scope): description

- Detailed explanation of changes
- Files modified: list of files
- Tests added: description of test coverage
- Documentation updated: list of docs modified
```

Types: `feat`, `fix`, `docs`, `test`, `refactor`, `style`, `chore`

## Architecture Requirements

### Application Structure
- Use Flask Application Factory Pattern with `create_app()` function
- Organize routes using Blueprints for modularity
- Use class-based configuration for different environments
- Separate concerns: models, routes, forms, templates, static files

### Project Structure
Follow this structure:
- `app/` - Main application package
- `app/__init__.py` - Application factory
- `app/config.py` - Configuration classes
- `app/models/` - Database models
- `app/routes/` - Blueprint modules
- `app/templates/` - Jinja2 templates
- `app/static/` - CSS, JS, images
- `tests/` - Test modules with unit/integration/functional separation
- `docs/` - Documentation directory
- `docs/README.md` - Main project documentation
- `docs/API.md` - API documentation
- `docs/CHANGELOG.md` - Change history and version notes
- `docs/DEPLOYMENT.md` - Deployment instructions
- `docs/DEVELOPMENT.md` - Development setup and guidelines
- `Pipfile` - Dependencies and Python version
- `Pipfile.lock` - Locked dependency versions (commit this)
- `.env` - Environment variables (never commit)
- `run.py` - Application entry point

## Coding Standards

### Python Style
- Follow PEP 8 guidelines strictly
- Use type hints for function parameters and return values
- Use f-strings for string formatting
- Use descriptive variable names
- Add Google-style docstrings to functions and classes
- Use snake_case for variables/functions, PascalCase for classes

### Flask Patterns
- Always use Application Factory Pattern
- Register blueprints in the factory function
- Use proper error handlers for 404, 500, etc.
- Implement CSRF protection on all forms
- Use environment variables for configuration
- Include proper logging configuration

### AI-Friendly Code Standards
- Write self-documenting code with clear, descriptive names
- Use explicit imports rather than wildcard imports
- Break complex functions into smaller, single-purpose functions
- Add type hints to all function parameters and return values
- Include comprehensive docstrings with examples where helpful
- Use consistent naming conventions throughout the codebase
- Avoid deeply nested code structures (max 3-4 levels)
- Add inline comments for non-obvious business logic
- Structure code in logical, predictable patterns
- Use constants for magic numbers and strings

## Documentation Requirements

### Code Documentation Standards
- Add comprehensive docstrings to ALL functions, classes, and modules
- Use Google-style docstrings with Args, Returns, Raises sections
- Include usage examples in docstrings for complex functions
- Document all function parameters and return types
- Add inline comments for complex business logic
- Document any assumptions or constraints in the code
- Include TODO comments for future improvements with issue numbers

### API Documentation
- Document all API endpoints with request/response examples
- Include authentication requirements for each endpoint
- Document error responses and status codes
- Use OpenAPI/Swagger specifications where applicable
- Include rate limiting and usage guidelines
- Document data validation rules and constraints

### Database Documentation
- Document all database models and their relationships
- Include migration notes and database schema changes
- Document database indexes and performance considerations
- Add comments explaining complex queries
- Document backup and recovery procedures

### Configuration Documentation
- Document all environment variables and their purposes
- Include default values and acceptable ranges
- Document configuration changes and their impacts
- Provide examples of different environment configurations

## Security Requirements

### Always Implement
- CSRF protection using Flask-WTF
- Input validation and sanitization
- SQL injection prevention with SQLAlchemy ORM
- XSS prevention (Jinja2 autoescaping)
- Secure session configuration
- Environment variables for secrets

### Session Security
- Set SESSION_COOKIE_SECURE = True in production
- Set SESSION_COOKIE_HTTPONLY = True
- Set SESSION_COOKIE_SAMESITE = 'Lax'

## Database Guidelines

### SQLAlchemy Models
- Use descriptive model names and relationships
- Include created_at/updated_at timestamps
- Use proper foreign key constraints
- Include __repr__ methods for debugging
- Use Flask-Migrate for schema changes

### Database Operations
- Always use database transactions appropriately
- Include proper error handling for database operations
- Use db.session.rollback() in error handlers

## Testing Requirements

### Test Organization
- Structure tests in unit/, integration/, functional/ directories
- Use conftest.py for shared fixtures
- Name tests descriptively: test_[unit]_[scenario]_[expected_result]
- Group related tests in classes

### Pytest Best Practices
- Use appropriate fixture scopes (session, module, function)
- Create factory fixtures for test data
- Use parameterized tests for multiple scenarios
- Mock external dependencies properly
- Use test markers for categorization (slow, integration, etc.)
- Maintain test coverage above 90%

### Flask Testing Patterns
- Create separate test application with testing configuration
- Use clean database sessions for each test
- Test both success and error scenarios
- Include authentication fixtures for API tests
- Test template rendering and context variables

### Database Testing Safety
- **NEVER use production database for testing**
- Use separate test database (SQLite in-memory or dedicated test DB)
- Configure test database URL in testing configuration
- Use database transactions that rollback after each test
- Create fresh database schema for each test session
- Drop all test data after test completion

### Test Database Configuration
- Use in-memory SQLite for fast, isolated tests: `sqlite:///:memory:`
- Alternative: separate test database with naming convention (e.g., `myapp_test.db`)
- Set `SQLALCHEMY_DATABASE_URI` to test database in testing config
- Never use environment variables that point to production database
- Use database name suffixes like `_test` to clearly identify test databases

### Production Database Protection
- Use database backup strategies before any testing that might touch production
- Implement database connection verification in test setup
- Use separate database user with limited permissions for testing
- Add assertion checks to verify test database connection
- Use database URL validation to prevent accidental production access
- Implement database migration rollback procedures for development testing

## Error Handling

### Custom Error Pages
- Create custom error handlers for common HTTP errors
- Include database rollback in 500 error handlers
- Use proper HTTP status codes
- Log errors appropriately

### Logging
- Configure rotating file handlers for production
- Use appropriate log levels (DEBUG, INFO, WARNING, ERROR)
- Include structured logging with timestamps and context

## Dependencies

### Core Stack
- Flask - Web framework
- Flask-WTF - Forms and CSRF protection
- python-dotenv - Environment variables (auto-loaded by Pipenv)
- Flask-SQLAlchemy - Database ORM
- Flask-Migrate - Database migrations
- gunicorn - Production WSGI server

### Development Tools
- pytest - Testing framework
- coverage - Test coverage
- black - Code formatting
- flake8 - Linting

### Pipenv Dependency Management
- Use `pipenv install <package>` for production dependencies
- Use `pipenv install <package> --dev` for development dependencies
- Pipenv automatically creates and manages virtual environments
- Use `pipenv shell` to activate the virtual environment
- Use `pipenv run <command>` to run commands in the virtual environment

## Code Generation Guidelines

When generating Flask code:

1. Include proper error handling and HTTP status codes
2. Use environment variables for configuration
3. Add form validation for user inputs
4. Include logging statements for debugging
5. Follow RESTful routing conventions
6. Use template inheritance with base templates
7. Add CSRF tokens to all forms
8. Use flash messages for user feedback
9. Implement proper redirects after form submissions
10. Include comprehensive docstrings

## Template Requirements

### HTML Templates
- Use template inheritance with base template
- Include proper meta tags and viewport
- Use url_for() for static files and routes
- Include flash message handling
- Use CSRF tokens in forms
- Follow semantic HTML structure

## Development Workflow

### Environment Setup
- Always use virtual environments
- Keep requirements.txt updated
- Use .env for local development
- Never commit sensitive data
- Use .gitignore for Python projects

### Quality Assurance
- Write tests for all routes and business logic
- Run linting and formatting tools
- Test migrations before applying to production
- Document API endpoints and complex logic

## API Development (if applicable)

### RESTful Design
- Use proper HTTP methods (GET, POST, PUT, DELETE)
- Return appropriate HTTP status codes
- Use JSON for API responses
- Include proper error responses
- Implement authentication for protected endpoints

Remember: Generate complete, working code that follows these patterns and requirements!

## Testing Requirements (Enhanced)

### Test Organization Structure
- Organize tests in `tests/unit/`, `tests/integration/`, `tests/functional/` directories
- Use `conftest.py` for shared fixtures and configuration
- Group related tests in classes with descriptive names

### Test Naming Convention
- Use pattern: `test_[unit_being_tested]_[scenario]_[expected_result]`
- Include comprehensive docstrings explaining what each test verifies
- Examples: `test_user_registration_with_valid_data_creates_user`

### Pytest Fixture Best Practices
- Use appropriate fixture scopes: session (expensive setup), module (shared within file), function (default)
- Create factory fixtures for parameterized test data
- Include fixtures for: test app, test client, database session, sample users, auth headers

### Testing Patterns to Follow
- **Unit Tests**: Test individual models, forms, and utility functions in isolation
- **Integration Tests**: Test complete user flows and route interactions
- **API Tests**: Test JSON endpoints with authentication and error scenarios
- **Form Tests**: Validate form data and error handling

### Database Testing Best Practices
- Use separate test database configuration class with isolated database URL
- Implement database fixture that creates fresh schema for each test session
- Use transaction-based testing with automatic rollback after each test
- Create database backup fixtures for tests that require production-like data
- Implement database connection validation to ensure test database is being used
- Use database seeding functions for consistent test data setup
- Never run tests against production database under any circumstances

### Test Data Management
- Create factory functions for generating test data
- Use database transactions that automatically rollback
- Implement data cleanup procedures for integration tests
- Use database snapshots for complex test scenarios
- Create isolated test environments for each test worker
- Implement test database reset mechanisms between test runs

### Advanced Testing Techniques
- Use parameterized tests for testing multiple input scenarios
- Mock external dependencies using unittest.mock
- Use test markers for categorization (slow, integration, etc.)
- Skip tests conditionally based on environment
- Maintain test coverage above 90%

### Testing Configuration
- Configure pytest with proper test discovery patterns
- Set up coverage reporting with HTML and terminal output
- Use strict markers and configuration
- Include performance assertions for response times
- Configure separate test database URL in pytest configuration
- Use database fixtures that ensure complete isolation from production
- Implement automatic test database cleanup and reset procedures

## Code Generation Guidelines

**IMPORTANT: Always ask for explicit permission before creating, modifying, or deleting any files. This includes creating new files, editing existing files, or removing files. Never perform any file operations without user consent.**

When generating Flask code:

1. **Always include error handling** and proper HTTP status codes
2. **Use environment variables** for configuration values
3. **Include form validation** for user inputs
4. **Add logging statements** for debugging
5. **Follow RESTful routing conventions** when appropriate
6. **Include template inheritance** with base templates
7. **Add CSRF tokens** to all forms
8. **Use flash messages** for user feedback
9. **Implement proper redirects** after form submissions
10. **Include comprehensive docstrings** and helpful comments
11. **Update documentation** when adding new features or endpoints
12. **Add changelog entries** for significant changes

## Documentation Generation Requirements

### When Creating New Code
- Add complete docstrings to all new functions and classes
- Update API documentation for new endpoints
- Add examples to complex functions
- Document any new configuration options
- Include security considerations in documentation

### When Modifying Existing Code
- Update existing docstrings to reflect changes
- Modify API documentation for endpoint changes
- Update configuration documentation for new options
- Add changelog entry describing the modification
- Update deployment documentation if infrastructure changes

### Documentation Format Standards
- Use Markdown format for all documentation files
- Include code examples with proper syntax highlighting
- Use consistent heading structure and formatting
- Include table of contents for longer documents
- Use proper cross-references between documentation files

## AI-Friendly Code Generation

### Readability Requirements
- Use descriptive variable and function names that explain their purpose
- Write functions that do one thing well (single responsibility principle)
- Keep functions under 20-30 lines when possible
- Use clear, logical code organization and structure
- Add whitespace and formatting for visual clarity
- Use meaningful constants instead of magic numbers

### Maintainability Focus
- Include comprehensive type hints for all functions
- Write modular code that can be easily modified or extended
- Use dependency injection patterns where appropriate
- Separate configuration from implementation
- Create reusable utility functions for common operations
- Follow consistent patterns throughout the codebase

### Troubleshooting Support
- Add detailed logging at appropriate levels (DEBUG, INFO, WARNING, ERROR)
- Include error context in exception handling
- Use descriptive error messages that explain what went wrong
- Add assertions for critical assumptions
- Include debug information in development mode
- Create clear separation between different concerns

### Future Expansion Design
- Design functions and classes to be easily extensible
- Use abstract base classes or protocols for common interfaces
- Structure code to support new features without major refactoring
- Include configuration options for future customization
- Document extension points and customization guidelines
- Use flexible data structures that can accommodate new fields

## Template Requirements

### HTML Template Structure
- Use template inheritance with a base template
- Include proper meta tags and viewport for responsive design
- Use `url_for()` for all static file and route references
- Include flash message handling in base template
- Add CSRF tokens to all forms
- Follow semantic HTML structure with proper accessibility

## Development Workflow

### Environment Setup
- Use Pipenv for dependency management (`pipenv install`)
- Pipenv automatically creates and manages virtual environments
- Use `pipenv shell` to activate environment or `pipenv run` for commands
- Environment variables in `.env` are automatically loaded by Pipenv
- Never commit sensitive data or `.env` files
- Commit both `Pipfile` and `Pipfile.lock` to version control
- Use comprehensive `.gitignore` for Python projects

### Quality Assurance
- Write tests for all routes and business logic
- Run code formatting and linting tools (black, flake8)
- Test database migrations before applying to production
- Document API endpoints and complex business logic
- Maintain high test coverage (90%+)
- Update documentation when making any code changes
- Review and update CHANGELOG.md for all significant changes

### Documentation Maintenance
- Update relevant documentation files when modifying code
- Keep API documentation synchronized with code changes
- Update deployment documentation for infrastructure changes
- Maintain up-to-date dependency documentation
- Review documentation for accuracy during code reviews
- Use semantic versioning and document breaking changes

### Change History Management
- Maintain detailed CHANGELOG.md with version history
- Document breaking changes, new features, and bug fixes
- Include migration notes for database schema changes
- Track dependency updates and their impacts
- Document configuration changes and environment updates
- Include rollback procedures for major changes

### Common Pipenv Commands
- `pipenv install` - Install dependencies from Pipfile
- `pipenv install <package>` - Add production dependency
- `pipenv install <package> --dev` - Add development dependency
- `pipenv shell` - Activate virtual environment
- `pipenv run <command>` - Run command in virtual environment
- `pipenv run flask run` - Run Flask development server
- `pipenv run pytest` - Run tests

Remember: Generate complete, working code that follows these patterns and requirements!
