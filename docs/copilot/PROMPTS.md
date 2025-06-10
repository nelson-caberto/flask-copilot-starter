# Copilot Prompt Templates

## Overview
This document contains tested and effective prompt templates for common Flask development tasks with GitHub Copilot.

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
Create comprehensive tests for [specific component/feature].

Test requirements:
- [Test type 1]: [specific scenarios]
- [Test type 2]: [specific scenarios]
- Edge cases: [list edge cases]
- Coverage target: [percentage]%

Include setup fixtures and mock data as needed.
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

*Last updated: June 10, 2025 - Initial template creation*
