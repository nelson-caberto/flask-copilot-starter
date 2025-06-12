# Copilot Prompt Templates

## ⚡ **SPEED-FIRST PROMPTS** - Anti-Analysis Paralysis

## ⚡ **AI Setup**: Say `reload_context.md` for instant project context

## Quick Decision Prompts (Use These First)

### ⚡ Immediate Action Prompt
```
I need to [specific task]. Please provide the simplest solution that works and implement it immediately.

Requirements:
- [Requirement 1]
- [Requirement 2]
- [Requirement 3]

Don't analyze multiple approaches - just use the most standard Flask pattern and proceed.
Follow the established patterns in this codebase.
```

### ⚡ Copy Pattern Prompt  
```
I need to [task] similar to [existing functionality in codebase].

Please:
1. Find the existing pattern for [similar functionality]
2. Copy and adapt it for [new requirement]
3. Implement immediately without analysis

Use exactly the same structure and patterns as the existing code.
```

### ⚡ Testing Efficiency Prompt
```
Run tests and show me only the essential results using grep filters.

IMMEDIATE COMMANDS NEEDED:
# Quick health check (< 30 seconds)
pytest | grep -q "FAILED" && echo "❌ TESTS FAILING - DETAILS BELOW" || echo "✅ ALL TESTS PASS"

# If failures detected, show details:
pytest -x --tb=short | grep -A 10 -B 2 "FAILED\|ERROR"

# Coverage summary only:
pytest --cov=app | grep -E "TOTAL.*[0-9]+%"

Don't show me full pytest output - just the filtered results above.
Use grep to process the output efficiently instead of showing everything.
```

### ⚡ Emergency Decision Prompt
```
We've been analyzing this for [time] and need to make a decision NOW.

Problem: [One sentence problem statement]
Context: [Brief context]

Please choose the simplest standard Flask approach and implement it.
No analysis needed - just pick the most obvious solution and proceed.
```

## Problem Decomposition Prompts (When Stuck)

### Circuit Breaker Activation
```
🚨 ANALYSIS PARALYSIS DETECTED - Activating circuit breaker

Current situation:
- Problem: [Brief description]
- Time spent: [Duration]
- Attempts made: [Number of attempts]

STOPPING current approach. Please:
1. State the core problem in ONE sentence
2. Identify the simplest solution that could work
3. Implement that solution immediately
4. NO analysis phase - just proceed

Use the emergency decision protocol from DECISION_FRAMEWORK.md
```

### Progress Validation
```
Let's pause and validate our progress:

Time spent: [Duration]
Interactions: [Number of back-and-forth exchanges]
Completed: [What we've accomplished]
Remaining: [What still needs to be done]
Blockers: [Current obstacles]

Questions:
- Are we moving in the right direction?
- Should we continue this approach or pivot?
- Is there a simpler way to achieve the goal?
- Do we need additional information or clarification?
```

### Approach Reset
```
I think we need to reset our approach for [problem description].

What we've tried:
- [Approach 1]: [Result]
- [Approach 2]: [Result]
- [Approach 3]: [Result]

Let's try a completely different strategy:
1. Research alternative patterns or solutions
2. Simplify the requirements to core functionality
3. Break into smaller, independent components
4. Consider if we're solving the right problem

What would you recommend as our next approach?
```

### Complexity Reduction
```
This problem seems more complex than initially expected.

Current complexity indicators:
- [Factor 1 making it complex]
- [Factor 2 making it complex]
- [Factor 3 making it complex]

Simplification options:
1. **Minimal Viable Solution**: [Simplest version that works]
2. **Phase 1 Implementation**: [Core features only]
3. **Proof of Concept**: [Basic functionality to validate approach]

Which simplification approach would you prefer?
```

### Environment Setup
```
# Pipenv Environment Setup
I need to set up the development environment for this Flask project using Pipenv.

Please help me:
1. Create a Pipfile with the core Flask dependencies listed in the project documentation
2. Set up the virtual environment using Pipenv
3. Install development dependencies for testing and code quality
4. Create a basic .env template file
5. Verify the setup is working correctly

Follow the project's 8-step workflow and ask for permission before creating any files.

# Development Environment Verification
Please verify my development environment is set up correctly:
- Check that Pipenv is working and virtual environment is active
- Verify all required dependencies are installed
- Test that Flask can import successfully
- Confirm testing framework is available
- Validate code quality tools are working

# Environment Troubleshooting
I'm having issues with my development environment setup:
- Python version: [your version]
- Pipenv version: [your version]
- Error messages: [paste any errors]
- Operating system: [your OS]

Please help me diagnose and fix the environment setup issues.
```

## Core Development Prompts

### Feature Development
```
I need to [specific feature description] for my Flask application.

Requirements:
- [Requirement 1]
- [Requirement 2]
- [Security considerations]
- [Performance requirements]

Please analyze the requirements and suggest implementation approaches.
```

**Example**:
```
I need to add a blog posting system for my Flask application.

Requirements:
- Users can create, edit, and delete their own posts
- Posts have titles, content, and publication dates
- Support for draft and published states
- Rich text editing capability
- SEO-friendly URLs

Please analyze the requirements and suggest implementation approaches.
```

### Bug Investigation
```
I'm experiencing [specific issue description] in my Flask app.

Symptoms:
- [Symptom 1]
- [Symptom 2]
- [When it occurs]

Error messages (if any):
[Paste exact error messages]

Please help me diagnose and fix this issue.
```

**Example**:
```
I'm experiencing slow database queries in my Flask app.

Symptoms:
- Page load times over 3 seconds
- Database connection timeouts
- High CPU usage during peak hours

Error messages (if any):
"sqlalchemy.exc.TimeoutError: QueuePool limit of size 5 exceeded"

Please help me diagnose and fix this issue.
```

### Testing Requests
```
🧪 CRITICAL: Before generating ANY test, check docs/copilot/TEST_CHEATSHEET.md first!

Create comprehensive tests for [specific component/feature].

Test requirements:
- [Test type 1]: [specific scenarios]
- [Test type 2]: [specific scenarios]
- Edge cases: [list edge cases]
- Coverage target: [percentage]%

MANDATORY STEPS:
1. Check TEST_CHEATSHEET.md for actual codebase structure
2. Verify actual model fields, route paths, and form fields  
3. Use real import paths from the codebase
4. Generate tests using ONLY verified structure

Include setup fixtures and mock data as needed.

⚡ SPEED-FIRST: Use grep to filter pytest output for specific information:
- Quick status: pytest | grep -E "(PASSED|FAILED|ERROR)"
- Fast failures: pytest -x --tb=short | grep -A 5 -B 1 "FAILED\|ERROR"
- Coverage only: pytest --cov=app | grep -E "TOTAL.*[0-9]+%"
```

**Example**:
```
Create comprehensive tests for the user authentication system.

Test requirements:
- Unit tests: User model validation, password hashing, token generation
- Integration tests: Login/logout workflows, session management
- Edge cases: Invalid credentials, expired tokens, account lockout
- Coverage target: 95%

Include setup fixtures and mock data as needed.

⚡ TESTING EFFICIENCY: Use these grep patterns for fast results:
pytest | grep -q "FAILED" && echo "❌ FIX NEEDED" || echo "✅ TESTS PASS"
pytest --cov=app | grep -E "TOTAL.*[0-9]+%" | tail -1
```

## Specific Task Prompts

### Database Operations
```
# Database Schema Design
Design a database schema for [domain description] with the following entities:
- [Entity 1]: [attributes and relationships]
- [Entity 2]: [attributes and relationships]

Include proper foreign keys, indexes, and constraints.

# Migration Creation
Create a database migration to [specific change description].
Ensure the migration is reversible and handles existing data safely.

# Query Optimization
Optimize this SQLAlchemy query for better performance:
[paste query]

Consider indexing, eager loading, and query structure improvements.
```

### API Development
```
# REST API Endpoint
Create a REST API endpoint for [resource] with the following specifications:
- HTTP methods: [GET, POST, PUT, DELETE]
- Authentication: [authentication requirements]
- Validation: [input validation rules]
- Response format: [JSON structure]
- Error handling: [specific error scenarios]

# API Documentation
Generate OpenAPI/Swagger documentation for the [endpoint/API].
Include request/response examples and error codes.
```

### Security Implementation
```
# Security Audit
Review the security of [specific component/entire app] and suggest improvements.
Focus on:
- Input validation and sanitization
- Authentication and authorization
- Session security
- CSRF protection
- SQL injection prevention

# Security Feature Implementation
Implement [specific security feature] with the following requirements:
- [Security requirement 1]
- [Security requirement 2]
- [Compliance requirements if any]
```

### Performance Optimization
```
# Performance Analysis
Analyze the performance of [specific component] and suggest optimizations.
Consider:
- Database query efficiency
- Caching strategies
- Memory usage
- Response times

# Caching Implementation
Implement caching for [specific use case] using [Redis/Memcached/Flask-Caching].
Include cache invalidation strategies and error handling.
```

## Documentation Prompts

### Code Documentation
```
Add comprehensive docstrings to [file/function/class] following Google style.
Include:
- Clear description of purpose
- Parameter descriptions with types
- Return value documentation
- Usage examples
- Raises documentation for exceptions
```

### API Documentation
```
Update the API documentation in docs/API.md for the new [endpoint/feature].
Include:
- Endpoint description and purpose
- Request/response examples
- Authentication requirements
- Error responses
- Rate limiting information
```

### Setup Documentation
```
Update the development setup documentation for [new requirement/change].
Include:
- Installation steps
- Configuration requirements
- Environment variables
- Troubleshooting common issues
```

## Maintenance Prompts

### Code Review
```
Review this code for [specific aspects]:
[paste code]

Check for:
- Code quality and best practices
- Security vulnerabilities
- Performance issues
- Flask-specific patterns
- Test coverage gaps
```

### Refactoring
```
Refactor [specific code/component] to improve [specific aspect].
Maintain backward compatibility and existing functionality.
Include tests to verify the refactoring doesn't break anything.
```

### Dependency Management
```
# Dependency Updates
Review and update the project dependencies in Pipfile.
Check for:
- Security vulnerabilities
- Deprecated packages
- Version compatibility
- New features in updated packages

# New Dependency Addition
Add [package name] to the project for [specific purpose].
Include:
- Proper dependency specification in Pipfile
- Configuration if needed
- Usage examples
- Documentation updates
```

## Advanced Workflow Prompts

### Multi-Step Development
```
I need to implement [complex feature] that involves multiple components.

Step 1: Analyze the requirements and break down into smaller tasks
Step 2: Suggest the implementation order and dependencies
Step 3: Implement each component following our workflow
Step 4: Create comprehensive tests
Step 5: Update all relevant documentation

Let's start with step 1 - requirements analysis.
```

### Architecture Decisions
```
I need to make an architectural decision about [specific decision].

Options I'm considering:
1. [Option 1]: [brief description]
2. [Option 2]: [brief description]

Please analyze each option considering:
- Scalability implications
- Maintenance complexity
- Performance impact
- Security considerations
- Development time

Provide a recommendation with reasoning.
```

### Integration Tasks
```
Integrate [external service/API] with my Flask application.

Integration requirements:
- [Requirement 1]
- [Requirement 2]
- Error handling strategy
- Rate limiting considerations
- Testing approach

Please suggest the integration architecture and implementation plan.
```

## Context-Setting Prompts

### Project Context
```
Context: This is a [type of application] built with Flask that [brief description].
Current architecture uses [architectural patterns].
Key integrations include [external services].

Now I need to [specific request].
```

### Constraint Communication
```
Please implement [request] with the following constraints:
- Must maintain backward compatibility
- Cannot exceed [performance/memory] limits
- Must comply with [regulatory/security] requirements
- Deadline: [time constraint]
- Available resources: [team size/expertise]
```

### Priority Setting
```
I have multiple tasks to accomplish:
1. [Task 1] - [priority level] - [brief description]
2. [Task 2] - [priority level] - [brief description]
3. [Task 3] - [priority level] - [brief description]

Please suggest the optimal order and approach for completing these tasks.
```

## Troubleshooting Prompts

### Error Diagnosis
```
I'm getting this error: [exact error message]

Context:
- What I was trying to do: [description]
- When it occurs: [timing/conditions]
- Environment: [development/production/testing]
- Recent changes: [any recent modifications]

Please help me diagnose and fix this issue.
```

### Performance Issues
```
I'm experiencing performance issues with [specific component].

Metrics:
- Current performance: [specific measurements]
- Expected performance: [target metrics]
- Load conditions: [traffic patterns]
- Resource usage: [CPU/memory/database]

Please suggest optimization strategies.
```

### Configuration Problems
```
I'm having configuration issues with [specific component].

Current configuration:
[paste relevant configuration]

Expected behavior: [description]
Actual behavior: [description]

Please help me correct the configuration.
```

---

## Usage Guidelines

### Prompt Customization
1. **Fill in placeholders**: Replace bracketed placeholders with specific details
2. **Add context**: Include relevant background information
3. **Be specific**: Provide concrete examples and requirements
4. **Set expectations**: Clarify desired outcomes and constraints

### Effective Communication
1. **Start broad, then narrow**: Begin with context, then get specific
2. **Provide examples**: Include concrete examples when possible
3. **Ask for options**: Request multiple approaches when appropriate
4. **Confirm understanding**: Verify Copilot understood your needs

### Quality Assurance
1. **Review suggestions**: Critically evaluate Copilot's responses
2. **Test thoroughly**: Verify all suggested implementations
3. **Document learnings**: Update this file with effective new prompts
4. **Iterate and refine**: Improve prompts based on results

---

## Maintenance Instructions

### Adding New Prompts
1. Test the prompt in real scenarios
2. Document the context where it works best
3. Include examples of successful usage
4. Categorize appropriately in this document

### Updating Existing Prompts
1. Note why changes are needed
2. Test updated versions
3. Update examples and usage notes
4. Maintain backward compatibility where possible

### Quality Control
- Review prompts monthly for effectiveness
- Remove or update prompts that consistently produce poor results
- Gather feedback from team members on prompt effectiveness
- Update based on new Copilot capabilities or Flask best practices

*Last updated: June 11, 2025 - Added anti-paralysis prompts and time-boxing templates*

## Flask Extension Development Prompts

### Extension Creation
```
I need to create a Flask extension for [extension purpose].

Extension Requirements:
- Functionality: [Core functionality description]
- Configuration options: [What should be configurable]
- Integration points: [How it integrates with Flask apps]
- Dependencies: [Required packages]

Please help me:
1. Design the extension architecture
2. Create the extension class with init_app() method
3. Implement proper configuration handling
4. Add comprehensive documentation and examples
5. Set up proper testing structure

Follow the Flask extension development patterns documented in the project guidelines.
```

**Example**:
```
I need to create a Flask extension for rate limiting API endpoints.

Extension Requirements:
- Functionality: Limit requests per minute/hour per IP or user
- Configuration options: Rate limits, storage backend, exempt routes
- Integration points: Decorator for routes, automatic Flask app integration
- Dependencies: Redis for storage, Flask for core functionality

Please help me create this extension following Flask extension best practices.
```

### Extension Testing
```
I need to create comprehensive tests for my Flask extension [extension_name].

Testing Requirements:
- Unit tests for extension class and methods
- Integration tests with sample Flask applications
- Multi-app testing scenarios
- Configuration validation tests
- Teardown and cleanup verification

Please help me create a complete testing strategy that covers:
1. Extension initialization and configuration
2. Integration with different Flask app patterns
3. Error handling and edge cases
4. Performance and memory usage
5. Compatibility with different Flask versions
```

### Extension Packaging
```
I need to prepare my Flask extension [extension_name] for PyPI distribution.

Current Status:
- Extension code is complete: [Yes/No]
- Tests are passing: [Yes/No]
- Documentation is written: [Yes/No]

Please help me:
1. Create proper setup.py with all required metadata
2. Set up MANIFEST.in for package files
3. Create distribution-ready documentation
4. Validate package structure and dependencies
5. Test installation and import in clean environment

Follow Python packaging best practices for Flask extensions.
```

### Extension Debugging
```
I'm having issues with my Flask extension [extension_name].

Problem Description:
- Issue: [Specific problem]
- Expected behavior: [What should happen]
- Actual behavior: [What actually happens]
- Error messages: [Any error messages]

Extension Details:
- Extension class: [Class name]
- Integration method: [How it's added to Flask app]
- Configuration: [Current configuration]

Please help me debug this extension issue.
```

## Anti-Paralysis Prompts

### Quick Decision Prompt
```
Let's avoid analysis paralysis here. I need a working solution in the next 15 minutes.

Requirements (core only):
- [Core requirement 1]
- [Core requirement 2]  
- [Core requirement 3]

Constraints:
- Use existing patterns from this codebase
- Prefer established Flask libraries
- Start with simplest implementation

Just give me your recommended approach and let's implement it. We can iterate later.
```

### Default Choice Prompt  
```
I'm seeing multiple options here. Let's use the default approach:

For [problem type]:
- Standard Flask pattern: [pattern name]
- Established library: [library name]
- Existing codebase pattern: [reference to similar code]

Proceed with this standard approach unless there's a clear reason it won't work.
```

### Time-Box Reset Prompt
```
We've been analyzing this for [time]. Let's reset:

Core problem: [one sentence]
Simplest solution: [basic approach]
Time limit: [15 minutes max]

Stop analyzing, start implementing. We'll improve it once it works.
```

### Circuit Breaker Override Prompt
```
Analysis paralysis detected. Switching to emergency decision mode:

1. What's the simplest thing that could possibly work?
2. What patterns already exist in this codebase?
3. What's the most standard Flask approach?

Choose option [1/2/3] and implement it now. No more analysis.
```
