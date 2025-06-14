``````````instructions
`````````instructions
````````instructions
# Flask Development Copilot Instructions

## Project Context
You are working on a Flask project that can be either:
1. **Flask Web Application** - A complete web application using Flask
2. **Flask Extension** - A reusable Flask extension for the Flask ecosystem

Generate code that follows Flask best practices, modern Python conventions, secure development patterns, and appropriate patterns for the project type.

**IMPORTANT: Always ask for explicit permission before creating, modifying, or deleting any files. Never perform any file operations without user consent.**

### Project Type Detection
**Always ask the user to clarify the project type if unclear:**
- "Are we building a Flask web application or a Flask extension?"
- "Should this follow Flask application patterns or Flask extension patterns?"
- "Is this intended to be distributed as a reusable Flask extension?"

## AI Collaboration Safety System

### Loop Detection and Circuit Breakers

**MANDATORY: Monitor collaboration patterns to prevent infinite loops and excessive iteration:**

#### Iteration Tracking
- **Track attempt count** for each specific problem or task
- **Maximum 3 attempts** for the same approach before triggering circuit breaker
- **Count total interactions** per session (reset daily)
- **Session limit**: 50 interactions before requiring break

#### Circuit Breaker Triggers
**Activate when any of these conditions occur:**

1. **Repetitive Failure Pattern**: Same error/approach fails 3+ times
2. **Excessive Iteration**: More than 5 back-and-forth cycles on single issue
3. **No Progress Indicator**: No measurable progress after 30 minutes
4. **Complexity Escalation**: Problem keeps getting more complex instead of simpler
5. **Tool Loop**: Using same tool repeatedly without success (5+ times)

#### Automatic Responses When Circuit Breaker Activates
**MANDATORY actions when circuit breaker triggers:**

```
🚨 CIRCUIT BREAKER ACTIVATED 🚨

Problem: [Brief description of stuck pattern]
Attempts made: [Number of attempts]
Time spent: [Approximate duration]

STOPPING current approach. Initiating problem decomposition protocol.
```

### Problem Decomposition Protocol

**When circuit breaker activates, ALWAYS follow this protocol:**

#### Step 1: Problem Analysis Reset
- **Stop current approach immediately**
- **Summarize what has been attempted**
- **Identify specific blocking points**
- **List assumptions that may be incorrect**

#### Step 2: Decomposition Strategy
```
DECOMPOSITION ANALYSIS:
1. Core Problem: [Single sentence problem statement]
2. Sub-problems identified: [List 3-5 smaller problems]
3. Dependencies: [What depends on what]
4. Minimum Viable Solution: [Simplest possible working version]
5. Alternative Approaches: [2-3 completely different methods]
```

#### Step 3: Collaborative Decision Point
**Present options to user:**
- **Option A**: Continue with simplified approach
- **Option B**: Switch to alternative method
- **Option C**: Take a break and return later
- **Option D**: Seek additional information or clarification

### Progress Validation Checkpoints

**MANDATORY: Validate progress at regular intervals:**

#### Every 3 Interactions
- **Summarize progress made**
- **Confirm we're moving toward solution**
- **Check if approach is still valid**
- **Ask user for feedback on direction**

#### Every 15 Minutes
- **Time check**: "We've been working on this for [X] minutes"
- **Progress assessment**: "Here's what we've accomplished..."
- **Path validation**: "Should we continue this approach or pivot?"

#### Before Major Changes
- **Impact assessment**: Files/systems that will be affected
- **Rollback plan**: How to undo if approach fails
- **Success criteria**: How we'll know it worked
- **Alternative plan**: What to try if this doesn't work

### Escalation Protocols

**When problems persist despite safety measures:**

#### Level 1: Approach Reset (After 3 failed attempts)
- Switch to completely different implementation approach
- Research alternative solutions or patterns
- Consult documentation or external resources
- Break problem into smaller, independent pieces

#### Level 2: Scope Reduction (After 6 failed attempts)
- Implement minimal viable solution first
- Remove non-essential features temporarily
- Focus on single core functionality
- Plan incremental improvements later

#### Level 3: Expert Consultation (After 9 failed attempts)
- Recommend consulting documentation, Stack Overflow, or community resources
- Suggest pair programming with human developer
- Propose research phase before continuing implementation
- Consider if problem requires domain-specific expertise

#### Level 4: Session Pause (After 12 failed attempts)
- **Mandatory break**: Stop all implementation work
- **Document current state**: What was attempted, what failed
- **Create resumption plan**: Steps for when work resumes
- **Recommend timeline**: Suggest minimum break duration

### Self-Monitoring Guidelines

**CONTINUOUS: Monitor these indicators during collaboration:**

#### Red Flags (Stop Immediately)
- Repeating same suggestion after it failed
- Increasing complexity instead of simplifying
- Making assumptions without verification
- Ignoring user feedback or constraints
- Generating code without understanding requirements

#### Yellow Flags (Slow Down and Reassess)
- Multiple tool calls with same parameters
- Long responses without clear progress
- Technical jargon without user confirmation
- Skipping workflow steps due to "efficiency"
- Solutions that seem too complex for the problem

#### Green Flags (Healthy Collaboration)
- Clear progress toward defined goals
- User engagement and feedback
- Incremental improvements and validation
- Appropriate tool usage and workflow adherence
- Solutions that match problem complexity

### Prevention Strategies

**PROACTIVE: Implement these to prevent loops before they start:**

#### Clear Communication
- **Always confirm understanding** before implementation
- **Ask clarifying questions** when requirements are vague
- **Provide multiple options** instead of single solutions
- **Explain trade-offs** of different approaches

#### Structured Problem Solving
- **Break complex requests** into smaller tasks
- **Validate each step** before proceeding to next
- **Test incrementally** rather than implementing everything at once
- **Document decisions** and reasoning for future reference

#### User Engagement
- **Regular check-ins** during long implementations
- **Progress updates** every few interactions
- **Explicit approval requests** before major changes
- **Feedback solicitation** on approach and progress

## Development Workflow Process

### Required Workflow for All Code Changes

**MANDATORY: Follow this exact workflow for every development request:**

1. **Git Status Check**: Before making any changes, verify there are no pending git commits
   - Check `git status` to ensure working directory is clean
   - If there are uncommitted changes, stop and ask user to commit or stash them first
   - Never proceed with new work when there are pending changes

2. **Analysis and Suggestions**: Analyze the request and provide focused options (MAX 10 minutes)
   - Break down the request into specific tasks and components
   - **Limit to 2-3 approaches maximum** - more options create decision paralysis
   - **Start with simplest viable approach** - complexity can be added later if needed
   - Explain trade-offs, security implications, and architectural considerations
   - Provide estimated scope of changes (files affected, complexity level)
   - Ask clarifying questions if requirements are unclear
   - **Decision criteria**: If analysis exceeds 10 minutes or 3 back-and-forth exchanges, present best option and proceed with approval request

3. **User Approval**: Wait for explicit approval before implementation (MAX 5 minutes)
   - Present the proposed plan clearly with all affected files listed
   - **Default to simplest approach if no preference specified**
   - Get confirmation on the chosen approach
   - Confirm any architectural decisions or new dependencies
   - **Auto-proceed rule**: If user doesn't respond within 5 minutes and approach is low-risk, proceed with simplest option
   - Only proceed after receiving clear "yes" or "approved" from user

4. **Implementation**: Perform the approved changes
   - Create or modify files as planned
   - Follow all coding standards and security requirements outlined in these instructions
   - Include comprehensive error handling and logging
   - Add detailed docstrings and comments
   - **Database Model Changes**: If modifying SQLAlchemy models, IMMEDIATELY run Flask-Migrate workflow:
     - Generate migration: `pipenv run flask db migrate -m "Description"`
     - Review migration file in `migrations/versions/`
     - Apply migration: `pipenv run flask db upgrade`
     - Test that migration works correctly

5. **Comprehensive Testing**: Create or update tests for all changes
   - Write unit tests for new functions and classes
   - Create integration tests for new routes or workflows
   - Include edge cases and error scenarios in tests
   - Test ALL occurrences of modified functionality throughout the project
   - Ensure test coverage remains above 90%
   - Run tests to verify they pass before proceeding
   - **Use grep to filter pytest output** for efficiency: `pytest | grep -E "(PASSED|FAILED|ERROR)"`

6. **Cleanup and Verification**: Clean up workspace and verify completion
   - Remove temporary files and development artifacts
   - Clear test database and reset test state
   - Verify all tests still pass after cleanup
   - Close database connections and release resources
   - Reset development environment to clean state
   - Clear any cached data or temporary configurations
   - Validate that application still runs correctly in clean state

7. **Documentation Updates**: Update all relevant documentation
   - Update API documentation for new or modified endpoints
   - Modify README.md if setup or usage instructions change
   - Update DEVELOPMENT.md for new development procedures
   - Add entries to CHANGELOG.md describing all changes
   - Update any affected configuration documentation
   - **Save Copilot interactions to knowledge base**:
     - Add successful interaction patterns to `docs/copilot/INTERACTIONS.md`
     - Record effective prompts and templates in `docs/copilot/PROMPTS.md`
     - Document insights and lessons learned in `docs/copilot/LESSONS.md`
     - Update decision patterns and frameworks in `docs/copilot/DECISION_FRAMEWORK.md`
     - Include session details in CHANGELOG.md Copilot sessions section

8. **Git Commit**: Create a proper git commit
   - Stage all modified files including tests and documentation
   - Write descriptive commit message following conventional commits format
   - Include summary of changes, files affected, and any breaking changes
   - Commit all changes as a single logical unit
   - Provide summary of completed work and next steps

### Workflow Enforcement

- **NEVER skip any step** in this workflow
- **ALWAYS check git status** before starting new work
- **ALWAYS wait for approval** before implementation
- **ALWAYS include comprehensive tests** for every change
- **ALWAYS update documentation** to reflect changes
- **ALWAYS commit changes** with descriptive messages

### Analysis Paralysis Prevention

**MANDATORY: Apply these rules to prevent decision delays:**

#### Time-Boxing Rules (STRICTLY ENFORCED)
- **Analysis Phase**: Maximum 10 minutes per request - SET TIMER
- **Option Generation**: Maximum 2-3 approaches per decision point (NO MORE)
- **Approval Wait**: Maximum 5 minutes before auto-proceeding with simplest approach
- **Research**: Maximum 15 minutes before presenting findings and proceeding
- **Flask-Migrate**: IMMEDIATE generation when models change (NO DELAYS)

#### Decision Hierarchy (When Multiple Options Exist)
1. **Simplest working solution** (preferred default - choose this 80% of the time)
2. **Established pattern** from existing codebase (follow existing code)
3. **Industry standard** approach (Flask best practices)
4. **Custom solution** (only if 1-3 are insufficient - requires justification)

#### Quick Decision Triggers (USE THESE TO AVOID PARALYSIS)
- **Low-risk changes**: Auto-proceed after 3 minutes if no user response
- **Standard patterns**: Use established codebase patterns WITHOUT analysis
- **Maintenance tasks**: Default to existing code style and patterns IMMEDIATELY  
- **Testing**: Follow existing test patterns and structures WITHOUT discussion
- **Test Output**: Use grep to filter pytest output for specific information instead of processing full output
- **Flask-Migrate**: Generate migration IMMEDIATELY when models change
- **Documentation updates**: Follow existing format and structure patterns

#### Complexity Escalation Rules
- Start with minimal viable implementation
- Add complexity only when simple solution proves insufficient
- Document why complexity was necessary
- Always provide rollback plan for complex changes

#### Circuit Breaker Activation
Automatically activate circuit breaker when:
- Same problem attempted 3+ times without success
- Analysis phase exceeds 15 minutes
- User requests become increasingly complex without clear requirements
- Implementation attempts result in repeated failures

## Architecture Requirements

### Flask Application Structure
**For Flask Web Applications:**
- Use Flask Application Factory Pattern with `create_app()` function
- Organize routes using Blueprints for modularity
- Use class-based configuration for different environments
- Separate concerns: models, routes, forms, templates, static files

### Flask Extension Structure
**For Flask Extensions:**
- Create extension class that follows Flask extension patterns
- Use `init_app()` method for application initialization
- Support deferred initialization and multiple application instances
- Follow Flask extension naming conventions (Flask-ExtensionName)
- Implement proper state management and context handling

### Project Structure

#### Flask Application Structure
```
flask-app/
├── app/                    # Main application package
│   ├── __init__.py        # Application factory
│   ├── config.py          # Configuration classes
│   ├── models/            # Database models
│   ├── routes/            # Blueprint modules
│   ├── templates/         # Jinja2 templates
│   └── static/            # CSS, JS, images
├── tests/                 # Test modules
├── docs/                  # Documentation
├── migrations/            # Database migrations (if using Flask-Migrate)
├── Pipfile               # Dependencies
├── Pipfile.lock          # Locked versions
├── run.py                # Application entry point
└── .env                  # Environment variables (never commit)
```

#### Flask Extension Structure
```
flask-extension/
├── flask_extension_name/   # Main extension package
│   ├── __init__.py        # Extension class and public API
│   ├── core.py           # Core extension logic
│   ├── utils.py          # Utility functions
│   ├── exceptions.py     # Custom exceptions
│   └── templates/        # Extension templates (if needed)
├── tests/                # Test modules
├── docs/                 # Documentation
├── examples/             # Usage examples
├── setup.py              # Package setup (for distribution)
├── setup.cfg             # Setup configuration
├── pyproject.toml        # Modern Python packaging
├── MANIFEST.in           # Package manifest
├── requirements.txt      # Runtime dependencies
├── requirements-dev.txt  # Development dependencies
└── tox.ini              # Testing configuration
```

### Flask Extension Development Patterns

#### Extension Class Pattern
```python
from flask import Flask, current_app

class FlaskExtensionName:
    def __init__(self, app=None):
        self.app = app
        if app is not None:
            self.init_app(app)
    
    def init_app(self, app: Flask):
        """Initialize extension with Flask application."""
        app.config.setdefault('EXTENSION_CONFIG_KEY', 'default_value')
        
        # Store extension instance on app
        app.extensions['extension_name'] = self
        
        # Register blueprints, error handlers, etc.
        if hasattr(app, 'teardown_appcontext'):
            app.teardown_appcontext(self.teardown)
```

#### Extension State Management
- Store configuration in `app.config` with prefixed keys
- Use `app.extensions` dict to store extension instances
- Handle application context properly with `current_app`
- Support multiple application instances
- Implement proper cleanup in teardown handlers

#### Extension API Design
- Provide clear public API in `__init__.py`
- Use descriptive class and function names
- Follow Flask's naming conventions
- Provide configuration options with sensible defaults
- Include comprehensive docstrings for all public methods

#### Extension Testing Patterns
- Test extension in isolation from specific applications
- Test with multiple Flask application configurations
- Mock external dependencies appropriately
- Test extension lifecycle (init, teardown, etc.)
- Include integration tests with real Flask applications

## Coding Standards

### Python Style
- Follow PEP 8 guidelines strictly
- Use type hints for function parameters and return values
- Use f-strings for string formatting
- Use descriptive variable names
- Add Google-style docstrings to functions and classes
- Use snake_case for variables/functions, PascalCase for classes

### Flask Application Patterns
**For Flask Applications:**
- Always use Application Factory Pattern with `create_app()`
- Register blueprints in the factory function
- Use proper error handlers for 404, 500, etc.
- Implement CSRF protection on all forms
- Use environment variables for configuration
- Include proper logging configuration

### Flask Extension Patterns
**For Flask Extensions:**
- Follow Flask extension initialization pattern with `init_app()`
- Support both direct initialization and deferred initialization
- Use `app.extensions` dict to store extension instances
- Prefix all configuration keys with extension name
- Handle application context correctly with `current_app`
- Implement proper cleanup in teardown handlers
- Follow Flask extension naming conventions (Flask-ExtensionName)
- Provide clear separation between public and private APIs

### Universal Flask Patterns
**For Both Applications and Extensions:**
- Use proper error handling and HTTP status codes
- Implement comprehensive logging
- Follow security best practices
- Use type hints and docstrings
- Implement proper testing patterns

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

### Documentation Files Update Protocol

**MANDATORY: When making any changes, update ALL relevant documentation files:**

#### Flask Application Documentation Files (Always Review)
1. **`docs/README.md`** - Main project documentation
   - Update getting started instructions if setup changes
   - Modify feature descriptions for new capabilities
   - Update troubleshooting section for new issues
   - Refresh project structure if architecture changes
   - Update extension recommendations if tools change

2. **`docs/API.md`** - API documentation  
   - Add new endpoints with complete examples
   - Update existing endpoint documentation for changes
   - Include authentication requirements for new endpoints
   - Document new error responses and status codes
   - Update rate limiting information if applicable
   - Add request/response examples for all changes

3. **`docs/CHANGELOG.md`** - Change tracking
   - Add entry to [Unreleased] section for every change
   - Include Copilot session details for AI-assisted changes
   - Document breaking changes with migration notes
   - Update version notes when releasing
   - Track dependency updates and their impacts

4. **`docs/DEVELOPMENT.md`** - Development setup and workflow
   - Update setup instructions for new dependencies
   - Modify environment variable documentation
   - Update testing procedures for new test types
   - Add troubleshooting for new common issues
   - Update directory structure if files are added/moved

5. **`docs/DEPLOYMENT.md`** - Production deployment
   - Update deployment steps for infrastructure changes
   - Modify configuration examples for new settings

#### Flask Extension Documentation Files (Always Review)
1. **`README.md`** - Main extension documentation (root level)
   - Update installation instructions for new requirements
   - Modify quick start examples for API changes
   - Update configuration options documentation
   - Add new usage examples for new features
   - Update compatibility information

2. **`CHANGELOG.md`** - Version history and changes
   - Document all API changes and new features
   - Include breaking changes with migration instructions
   - Note Flask version compatibility changes
   - Track dependency requirement updates

3. **`docs/`** directory - Detailed documentation
   - Update API reference for new methods/classes
   - Add examples for new functionality
   - Update configuration reference
   - Modify integration guides for changes

4. **`setup.py`** or **`pyproject.toml`** - Package metadata
   - Update version numbers for releases
   - Modify dependency requirements if needed
   - Update classifiers for new Python/Flask versions
   - Update description and keywords if scope changes

5. **`examples/`** directory - Usage examples
   - Add examples for new features
   - Update existing examples for API changes
   - Test all examples with current Flask versions
   - Include configuration examples for new options
   - Update backup procedures for new data types
   - Add performance optimization notes for new features
   - Update security considerations for new endpoints

6. **`docs/COPILOT.md`** - AI collaboration guide
   - Update workflow integration for new procedures
   - Add maintenance instructions for new practices
   - Update best practices based on learnings
   - Modify troubleshooting for new AI collaboration issues

#### Copilot Knowledge Base Files (Update After AI Sessions)
7. **`docs/copilot/INTERACTIONS.md`** - Collaboration patterns
   - Add successful interaction examples after each session
   - Document new conversation templates that work well
   - Update success metrics and quality assessments
   - Add workflow examples for new development procedures

8. **`docs/copilot/PROMPTS.md`** - Effective prompts
   - Add new prompt templates discovered during development
   - Update existing prompts based on effectiveness
   - Add documentation-specific prompts for new file types
   - Include maintenance prompts for new tools or procedures

9. **`docs/copilot/LESSONS.md`** - AI insights and learnings
   - Document new insights gained from AI collaboration
   - Add best practices discovered during development
   - Update troubleshooting patterns for new issues
   - Include performance tips for new AI interaction patterns

10. **`docs/copilot/DECISION_FRAMEWORK.md`** - Decision-making guidelines
    - Update decision trees and frameworks based on experience
    - Add new time-boxing rules and quick decision patterns
    - Document successful anti-paralysis strategies
    - Include project-specific decision hierarchies and patterns

#### Documentation Update Checklist
**For EVERY development task, check these items:**

- [ ] **README.md**: Does this change affect getting started, features, or troubleshooting?
- [ ] **API.md**: Are there new/modified endpoints, authentication, or error responses?
- [ ] **CHANGELOG.md**: Has an entry been added with proper categorization and Copilot session details?
- [ ] **DEVELOPMENT.md**: Do setup, testing, or workflow procedures need updates?
- [ ] **DEPLOYMENT.md**: Are there infrastructure, configuration, or security changes?
- [ ] **COPILOT.md**: Do AI collaboration workflows or best practices need updates?
- [ ] **Copilot Knowledge Base**: Should successful patterns/prompts/lessons be captured?
- [ ] **DECISION_FRAMEWORK.md**: Do decision patterns or anti-paralysis strategies need updates?

#### Documentation Quality Standards
- **Consistency**: Use same formatting and style across all docs
- **Completeness**: Include examples, error cases, and edge scenarios
- **Currency**: Ensure all information reflects current state
- **Cross-references**: Link between related sections in different files
- **Searchability**: Use clear headings and keywords for easy navigation

#### Documentation Testing
- **Links**: Verify all internal and external links work
- **Examples**: Test all code examples and commands
- **Accuracy**: Ensure all information matches actual implementation
- **Formatting**: Check Markdown rendering and syntax highlighting

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

### Flask-Migrate Workflow Requirements

**MANDATORY: When ANY database model is touched, IMMEDIATELY execute this workflow:**

#### Model Creation Workflow (NO DELAYS)
```bash
# 1. Create model → 2. Generate migration → 3. Apply → 4. Test → 5. Commit
pipenv run flask db migrate -m "Add [ModelName] model"
pipenv run flask db upgrade
# Test app runs → Commit changes
```

#### Model Modification Workflow (NO DELAYS)  
```bash
# 1. Modify model → 2. Generate migration → 3. Apply → 4. Test → 5. Commit
pipenv run flask db migrate -m "Update [ModelName] - [brief description]"
pipenv run flask db upgrade
# Test app runs → Commit changes
```

#### Model Deletion Workflow (BACKUP FIRST)
```bash
# 1. BACKUP DB → 2. Remove from model → 3. Generate migration → 4. Apply → 5. Test → 6. Commit
pipenv run flask db migrate -m "Remove [field/model] from [ModelName]"
pipenv run flask db upgrade
# Test on backup data first → Commit changes
```

#### Anti-Paralysis Rules for Migrations
- **NO analysis phase** - just generate the migration immediately
- **NO option generation** - Flask-Migrate is the standard approach  
- **NO approval wait** - migrations are mandatory for model changes
- **AUTO-PROCEED** if user doesn't respond within 2 minutes

#### Migration Safety Rules
- **NEVER modify existing migration files** - always create new ones
- **ALWAYS review generated migrations** before applying
- **TEST migrations on copy of production data** for destructive changes
- **BACKUP database** before applying migrations in production
- **Keep migrations small and focused** - one logical change per migration

#### Error Recovery
If migration fails:
```bash
# Rollback to previous migration
pipenv run flask db downgrade

# Fix the issue in model or migration
# Generate new migration if needed
pipenv run flask db migrate -m "Fix [issue description]"

# Apply corrected migration
pipenv run flask db upgrade
```

#### Migration Workflow Integration
**This workflow MUST be integrated into the main development workflow:**
- Step 4 (Implementation): Include migration generation when models change
- Step 5 (Testing): Test that migrations work correctly
- Step 7 (Documentation): Document schema changes in CHANGELOG.md
- Step 8 (Git Commit): Include both model and migration files

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
- **Use grep to filter pytest output** for specific information instead of processing full output

### Testing Tools
1. **Unit & Integration Tests**: pytest
2. **Browser & E2E Tests**: pytest-playwright
3. **Test Organization**: conftest.py fixtures

### Test Types & Tools Matrix ⚡
| Test Type | Tool | Priority | Time Limit | Example |
|-----------|------|----------|------------|---------|
| Unit | pytest | HIGH | < 2 min/test | `test_user_model.py` |
| API | pytest | HIGH | < 3 min/test | `test_auth_api.py` |
| Browser/E2E | playwright | MEDIUM | < 5 min/test | `test_login_flow.py` |
| Visual | playwright | LOW | < 2 min/test | `test_responsive.py` |

### Speed-First Testing Guidelines ⚡
1. **Start Simple, Ship Fast**
   - Write minimal passing test first
   - Add complexity only after basics work
   - Ship with core test coverage

2. **Prioritize Test Types**
   ```bash
   # 1. Unit Tests (REQUIRED) - < 2 min each
   pytest tests/unit/

   # 2. API Tests (REQUIRED) - < 3 min each
   pytest tests/api/

   # 3. Critical E2E (Only key flows) - < 5 min each
   pytest tests/e2e/test_critical.py

   # 4. Visual/Responsive (If needed) - < 2 min each
   pytest tests/e2e/test_visual.py
   ```

3. **Emergency Test Protocol** (When time critical)
   ```bash
   # 1. Run only changed files
   pytest tests/unit/test_changed.py

   # 2. Run only critical paths
   pytest tests/e2e/test_critical.py

   # 3. Skip slow tests
   pytest -m "not slow"
   ```

4. **Quick Test Status** (< 30 seconds)
   ```bash
   # Fast overview
   pytest --tb=no | grep -E "(PASSED|FAILED|ERROR)" | tail -5

   # Critical test status
   pytest tests/e2e/test_critical.py -v | grep -E "(PASSED|FAILED)"

   # Coverage check
   pytest --cov=app | grep -E "TOTAL.*[0-9]+%"
   ```

### Browser Testing with Playwright ⚡
#### Core Principles
- **Use for critical user flows**: Login, signup, core business processes
- **Test responsive design**: Mobile, tablet, desktop viewports
- **Verify JavaScript interactions**: Dynamic UIs, client-side validation 
- **Cross-browser compatibility**: Chrome, Firefox, Safari

#### Speed-First Test Generation ⚡
1. **Start with flow only** (< 5 minutes):
   - Happy path user journey
   - Most frequent user action
   - Skip edge cases initially

2. **Add core validations** (< 10 minutes):
   - Basic form validation
   - Error messages
   - Success states

3. **Optimize later** (if needed):
   - Device testing
   - Visual regression
   - Network conditions

### MANDATORY: Browser Test Setup ⚡
```bash
# 1. Install pytest-playwright (REQUIRED)
pip install pytest-playwright

# 2. Install browsers (run ONE of these)
playwright install chromium  # Fastest for CI/CD
playwright install firefox   # For Firefox-specific testing
playwright install webkit   # For Safari testing

# 3. Create test structure (REQUIRED)
mkdir -p tests/e2e/pages  # For page objects
touch tests/e2e/conftest.py  # For fixtures
touch tests/e2e/test_critical_flows.py  # For tests
```

### Speed-First Playwright Patterns ⚡

#### 1. Quick Test Development (< 2 minutes per test)
```python
# tests/e2e/test_critical_flows.py
from playwright.sync_api import expect

def test_login_quick(page):
    """Minimal login test - implement first"""
    page.goto("/login")
    page.fill("[data-testid=email]", "test@example.com")
    page.fill("[data-testid=password]", "password123")
    page.click("[data-testid=login-button]")
    expect(page).to_have_url("/dashboard")

def test_registration_quick(page):
    """Minimal registration test - implement first"""
    page.goto("/register")
    page.fill("[data-testid=email]", "new@example.com")
    page.fill("[data-testid=password]", "newpass123")
    page.click("[data-testid=register-button]")
    expect(page).to_have_url("/dashboard")
```

#### 2. Page Object Pattern (Add after basics work)
```python
# tests/e2e/pages/login_page.py
class LoginPage:
    def __init__(self, page):
        self.page = page
        self.email_input = page.locator("[data-testid=email]")
        self.password_input = page.locator("[data-testid=password]")
        self.login_button = page.locator("[data-testid=login-button]")
    
    def login(self, email, password):
        self.page.goto("/login")
        self.email_input.fill(email)
        self.password_input.fill(password)
        self.login_button.click()
```

#### 3. Data-Testid Conventions (REQUIRED)
```html
<!-- ALWAYS add data-testid to elements -->
<input data-testid="email" type="email">
<button data-testid="submit-button">Submit</button>
<div data-testid="error-message">Invalid input</div>
```

### Quick Testing Commands ⚡
```bash
# Run all E2E tests (CI/CD mode)
pytest --browser chromium --headless tests/e2e/

# Development mode (with browser visible)
pytest --browser chromium --headed tests/e2e/test_login.py

# Run tests on multiple browsers
pytest --browser chromium --browser firefox tests/e2e/

# Screenshot on failure
pytest --screenshot only-on-failure tests/e2e/

# Record video for failing tests
pytest --video retain-on-failure tests/e2e/
```

### Emergency Debug Commands ⚡
```bash
# Live debug with browser
pytest --browser chromium --headed --slowmo 1000 tests/e2e/test_login.py

# Find selector issues
pytest --browser chromium --headed --debug tests/e2e/

# Get detailed failure screenshots
pytest --screenshot on --browser chromium tests/e2e/

# Trace failing tests
pytest --trace on tests/e2e/test_login.py
```

### ⚡ QUICK REFERENCE: Testing Setup & Commands

#### 1. Initial Setup (< 2 minutes)
```bash
# Install core testing tools
pip install pytest pytest-playwright pytest-cov

# Install browsers
playwright install chromium  # Required
playwright install firefox   # Optional
playwright install webkit    # Optional
```

#### 2. Fast Test Commands (< 30 seconds)
```bash
# Run critical tests
pytest tests/critical/

# Quick status check
pytest --tb=no | grep -E "FAILED|ERROR"

# Coverage check
pytest --cov=app --cov-report=term-missing | grep TOTAL
```

#### 3. Browser Test Commands (< 1 minute)
```bash
# Run E2E tests
pytest tests/e2e/

# Debug mode
pytest --headed tests/e2e/

# Multiple browsers
pytest --browser chromium --browser firefox tests/e2e/
```

#### 4. Emergency Commands (< 30 seconds)
```bash
# Critical failures only
pytest -x tests/critical/

# Last 5 failures
pytest --tb=short | grep -A 5 FAILED

# Quick screenshot
pytest --screenshot only-on-failure tests/e2e/
```

### Pipenv Environment Management ⚡

#### Initial Setup (< 2 minutes)
```bash
# 1. Install Pipenv if not installed
pip install pipenv

# 2. Install dependencies
pipenv install  # Production deps
pipenv install --dev  # Development deps

# 3. Activate environment
pipenv shell
```

#### Daily Development Commands
```bash
# Start development server
pipenv run flask run

# Run tests
pipenv run pytest

# Database operations
pipenv run flask db migrate -m "Description"
pipenv run flask db upgrade

# Install new dependencies
pipenv install package-name  # Production
pipenv install --dev package-name  # Development only
```

#### Speed-First Pipenv Guidelines ⚡
1. **Quick Environment Check**
   ```bash
   # Verify environment
   pipenv verify
   
   # Check dependencies
   pipenv graph
   
   # Update all packages
   pipenv update
   ```

2. **Emergency Recovery**
   ```bash
   # Reset environment
   pipenv --rm
   pipenv install --dev
   
   # Clean unused packages
   pipenv clean
   
   # Regenerate lockfile
   pipenv lock
   ```

3. **Virtual Environment Rules**
- Always use Pipenv for dependency management
- Keep Pipfile.lock in version control
- Run all commands through pipenv
- Use `pipenv shell` for long sessions
- Use `pipenv run` for single commands

#### Common Issues & Solutions
```bash
# Dependencies not found
pipenv install --skip-lock
pipenv lock --clear

# Environment not working
pipenv --rm
pipenv install --dev

# Wrong Python version
pipenv --python 3.8  # Specify version
```

### Dependency Management Guidelines
1. **Adding Dependencies**
   - Add to Pipfile directly for clarity
   - Use exact versions for critical packages
   - Document why each package is needed

2. **Updating Dependencies**
   - Update one package at a time
   - Test after each update
   - Keep track of breaking changes

3. **Security Updates**
   - Run `pipenv check` regularly
   - Update vulnerable packages immediately
   - Keep track of security advisories

### Always Runnable Code Rule ⚡

#### CRITICAL: Keep Code Runnable at All Times
- **Every commit must run**: No broken intermediate states
- **Test before commit**: Ensure all changes are functional
- **Incremental changes**: Break large changes into runnable steps
- **Revert if broken**: If tests fail, revert to last working state

#### Implementation Strategy
1. **Start from working state**
   - Verify current version runs
   - Run all tests before changes
   - Check git status is clean

2. **Make atomic changes**
   - One functional change at a time
   - Test after each change
   - Commit working increments

3. **Emergency fixes**
   - Fix failing tests immediately
   - Don't stack changes on broken code
   - Roll back if can't fix quickly

#### Example Workflow
```bash
# 1. Verify starting state
pytest
python run.py  # or flask run

# 2. Make small change
# Edit one file/feature

# 3. Verify still runs
pytest
python run.py

# 4. Commit if working
git commit -m "feat: add X (verified running)"

# If broken:
git reset --hard  # Return to last working state
```

### Speed-First Runnable Guidelines ⚡
1. **Ship Fast, Ship Working**
   - Minimal viable implementation
   - Must pass core tests
   - Must start and run

2. **No Broken WIP**
   - Don't commit broken code
   - Don't stack changes on failures
   - Keep main branch always runnable

3. **Quick Recovery**
   - Know how to revert changes
   - Keep last working version tagged
   - Document startup requirements
``````````
