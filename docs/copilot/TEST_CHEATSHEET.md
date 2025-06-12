# AI Testing Cheatsheet ⚡

> **CRITICAL FOR AI INSTANCES** | Prevent "Guessing" | Use Actual Codebase Structure

## ⚡ **AI Setup**: Say `reload_context.md` for instant project context

## 🚨 **ANTI-GUESSING PROTOCOL**

### **⚠️ CRITICAL ISSUE**: AI instances often "forget" or "guess" actual code structure when generating tests
### **⚡ SOLUTION**: Always check actual codebase structure BEFORE generating any tests

---

## 🔍 **MANDATORY PRE-TEST COMMANDS**

### **Step 1: Read Actual Code Structure** (REQUIRED)
```bash
# ALWAYS run these commands BEFORE generating tests:

# Check actual model structure
find app/models -name "*.py" -exec head -20 {} \;

# Check actual route structure  
find app/routes -name "*.py" -exec head -30 {} \;

# Check existing test patterns
find tests -name "*.py" -exec head -15 {} \;

# Check actual database models
grep -n "class.*db.Model" app/models/*.py

# Check actual form classes
grep -n "class.*FlaskForm" app/forms/*.py || echo "No forms found"

# Check actual configuration
head -50 app/config.py || head -50 config.py || echo "No config.py found"
```

### **Step 2: Verify Actual Imports** (REQUIRED)
```bash
# Check what's actually imported in existing tests
grep -h "^from\|^import" tests/*.py | sort | uniq

# Check what's actually imported in models
grep -h "^from\|^import" app/models/*.py | sort | uniq

# Check actual database setup in conftest.py
cat tests/conftest.py || echo "No conftest.py found"
```

---

## 📋 **ACTUAL CODEBASE REFERENCE**

### **Real Model Classes** (Update when models change)
```python
# ACTUAL models (verified by running: grep -n "class.*db.Model" app/models/*.py)
# UPDATE THIS SECTION whenever models change

# Example - Replace with actual model structure:
class User(db.Model):
    id = db.Column(db.Integer, primary_key=True)
    email = db.Column(db.String(120), unique=True, nullable=False)
    password_hash = db.Column(db.String(128))
    # ... add actual fields from your models

# TO UPDATE: Run grep command above and replace this section
```

### **Real Route Functions** (Update when routes change)
```python
# ACTUAL routes (verified by running: grep -n "def.*:" app/routes/*.py)
# UPDATE THIS SECTION whenever routes change

# Example - Replace with actual route structure:
@auth_bp.route('/login', methods=['GET', 'POST'])
def login():
    # ... actual implementation

# TO UPDATE: Run grep command and replace this section
```

### **Real Form Classes** (Update when forms change)
```python
# ACTUAL forms (verified by running: grep -n "class.*FlaskForm" app/forms/*.py)
# UPDATE THIS SECTION whenever forms change

# Example - Replace with actual form structure:
class LoginForm(FlaskForm):
    email = StringField('Email', validators=[DataRequired(), Email()])
    password = PasswordField('Password', validators=[DataRequired()])
    # ... add actual fields from your forms

# TO UPDATE: Run grep command and replace this section
```

---

## 🧪 **SPEED-FIRST TEST GENERATION PATTERNS**

### **Pattern 1: Model Testing** (Copy-Paste Template)
```python
# STANDARD MODEL TEST PATTERN - Copy and modify for actual models
import pytest
from app.models.user import User  # UPDATE: Use actual import path
from app import db

def test_user_creation():
    """Test basic user creation"""
    user = User(
        email='test@example.com',  # UPDATE: Use actual model fields
        # Add other required fields from actual model
    )
    assert user.email == 'test@example.com'
    assert user.id is None  # Before saving

def test_user_save():
    """Test user saving to database"""
    user = User(email='test@example.com')
    db.session.add(user)
    db.session.commit()
    assert user.id is not None
    assert User.query.count() == 1
```

### **Pattern 2: Route Testing** (Copy-Paste Template)
```python
# STANDARD ROUTE TEST PATTERN - Copy and modify for actual routes
import pytest
from flask import url_for

def test_login_get(client):
    """Test login page loads"""
    response = client.get('/login')  # UPDATE: Use actual route path
    assert response.status_code == 200
    assert b'Login' in response.data  # UPDATE: Check actual page content

def test_login_post_valid(client):
    """Test valid login"""
    response = client.post('/login', data={
        'email': 'test@example.com',    # UPDATE: Use actual form fields
        'password': 'password123'       # UPDATE: Use actual form fields
    })
    assert response.status_code == 302  # Redirect after login
    # UPDATE: Add actual success checks
```

### **Pattern 3: Form Testing** (Copy-Paste Template)
```python
# STANDARD FORM TEST PATTERN - Copy and modify for actual forms
import pytest
from app.forms.auth import LoginForm  # UPDATE: Use actual import path

def test_login_form_valid():
    """Test valid form data"""
    form = LoginForm(data={
        'email': 'test@example.com',    # UPDATE: Use actual form fields
        'password': 'password123'       # UPDATE: Use actual form fields
    })
    assert form.validate()

def test_login_form_invalid_email():
    """Test invalid email"""
    form = LoginForm(data={
        'email': 'invalid-email',       # UPDATE: Use actual validation rules
        'password': 'password123'
    })
    assert not form.validate()
    assert 'Invalid email address' in form.email.errors  # UPDATE: Check actual error messages
```

---

## 🔧 **MAINTENANCE COMMANDS**

### **Update Cheatsheet After Code Changes**
```bash
# Run these commands to update the cheatsheet after ANY code changes:

echo "=== UPDATING TEST CHEATSHEET ==="

echo "## Current Models:"
grep -n "class.*db.Model" app/models/*.py

echo "## Current Routes:"
grep -n "def.*:" app/routes/*.py | head -20

echo "## Current Forms:"
grep -n "class.*FlaskForm" app/forms/*.py || echo "No forms found"

echo "## Current Imports in Tests:"
grep -h "^from\|^import" tests/*.py | sort | uniq | head -20

echo "## Database Tables:"
sqlite3 instance/app.db ".tables" || echo "No database found"

echo "## Update docs/copilot/TEST_CHEATSHEET.md with this information"
```

---

## 🚫 **ANTI-GUESSING RULES**

### **❌ NEVER Do These:**
- Generate tests without checking actual model fields
- Assume import paths without verifying them
- Guess form field names or validation rules
- Create tests for non-existent routes or methods
- Use hardcoded values without checking actual data types
- Assume database schema without verification

### **✅ ALWAYS Do These:**
- Run the pre-test commands BEFORE generating ANY test
- Check actual imports in existing test files
- Verify actual model field names and types
- Confirm actual route paths and HTTP methods
- Use actual form field names from the codebase
- Copy patterns from existing working tests

---

## 📊 **SPEED-FIRST TEST VERIFICATION**

### **Quick Verification Commands** (< 30 seconds)
```bash
# Verify tests work IMMEDIATELY after generation:

# Run only the new test file
pytest tests/test_new_feature.py -v

# Quick pass/fail check
pytest tests/test_new_feature.py | grep -q "FAILED" && echo "❌ FIX NEEDED" || echo "✅ TESTS PASS"

# Check what failed (if any)
pytest tests/test_new_feature.py -x --tb=short | grep -A 5 -B 1 "FAILED\|ERROR"
```

### **Common Test Failures and Fixes** 
```bash
# Import errors - check actual import paths:
grep -n "ImportError\|ModuleNotFoundError" pytest output
# Fix: Verify import paths with: find app -name "*.py" | grep model_name

# Attribute errors - check actual model fields:
grep -n "AttributeError" pytest output  
# Fix: Verify fields with: grep -A 20 "class ModelName" app/models/file.py

# Database errors - check actual schema:
grep -n "OperationalError\|IntegrityError" pytest output
# Fix: Check schema with: sqlite3 instance/app.db ".schema table_name"
```

---

## 💡 **SPEED-FIRST PROMPT TEMPLATES**

### **For Model Tests**
```
I need tests for [ModelName]. 

BEFORE generating tests, please:
1. Run: grep -A 20 "class [ModelName]" app/models/[file].py
2. Show me the actual model fields and their types
3. Then generate tests using ONLY the actual fields you found

Generate basic tests for creation, validation, and database operations.
Use the patterns from docs/copilot/TEST_CHEATSHEET.md.
```

### **For Route Tests**
```
I need tests for [route_path].

BEFORE generating tests, please:
1. Run: grep -A 15 "def.*[route_name]" app/routes/[file].py  
2. Show me the actual route implementation
3. Check what HTTP methods it supports
4. Then generate tests using ONLY the actual route structure

Generate tests for GET/POST requests and expected responses.
Use patterns from docs/copilot/TEST_CHEATSHEET.md.
```

### **For Form Tests**
```
I need tests for [FormName].

BEFORE generating tests, please:
1. Run: grep -A 20 "class [FormName]" app/forms/[file].py
2. Show me the actual form fields and validators
3. Then generate tests using ONLY the actual form structure

Generate tests for valid/invalid form data and validation.
Use patterns from docs/copilot/TEST_CHEATSHEET.md.
```

---

## 🔄 **MAINTENANCE PROTOCOL**

### **Daily Updates** (When code changes)
1. Run maintenance commands to check current structure
2. Update the "ACTUAL CODEBASE REFERENCE" section
3. Verify test patterns still work with: `pytest tests/ -q`
4. Update any broken patterns immediately

### **Weekly Reviews**
1. Check if test patterns are still optimal
2. Add new common patterns discovered
3. Remove outdated examples
4. Update speed-first commands if needed

---

*Last updated: June 12, 2025*  
*CRITICAL: Always check actual codebase structure before generating tests*  
*This file prevents AI "guessing" and ensures accurate test generation*
