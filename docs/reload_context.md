# AI Context Reload Guide ⚡

> **SHORTCUT**: Just mention `reload_context.md` and AI automatically executes full context loading

## 🚀 **IMMEDIATE AUTO-EXECUTION** 

When user mentions this file, AI should immediately:

### **Step 1: Read Project Files** (Auto-Execute)
```
Reading .vscode/copilot-instructions.md and all docs/ files now...
```

### **Step 2: Confirm Understanding** (Auto-State)
```
I have read the project guidelines and commit to following all instructions, workflows, and safety protocols outlined in the files.
```

### **Step 3: Demonstrate Knowledge** (Auto-Summarize)
**Mandatory 8-Step Workflow:**
1. Requirements (< 5 min) - Clear definition, no analysis paralysis
2. Implementation (< 15 min) - Minimal viable version using Flask standards  
3. Testing (< 5 min) - Basic tests, grep-filtered results
4. Validation (< 3 min) - Quick functionality check
5. Security (< 2 min) - Basic validation using project patterns
6. Documentation (< 5 min) - Update relevant docs immediately
7. Knowledge Base (< 3 min) - Save patterns/lessons to copilot docs
8. Git Commit (< 2 min) - Descriptive commit message

**Anti-Paralysis Protocols:**
- Analysis > 5 minutes → EMERGENCY: Choose simplest option immediately
- Same suggestion 2+ times → STOP, choose different approach  
- No code > 10 minutes → CRITICAL: Implement something now
- Solution getting complex → EMERGENCY: Return to minimal approach

**Speed-First Principles:**
- < 30 minutes per feature maximum
- Flask conventions take priority
- Use existing codebase patterns
- Minimal viable implementations first
- Working code beats perfect code

### **Step 4: Ready State** (Auto-Confirm)
```
✅ Context loaded. Ready for immediate development.
✅ Following 8-step workflow with anti-paralysis protocols.
✅ All documentation will be updated per requirements.

What would you like to implement?
```

---

## 📋 **FULL CONTEXT LOADING REFERENCE**

### **When Manual Loading Needed**
If automatic execution doesn't work, use this prompt:

```
Before we start working together, please read the following files to understand this project's development guidelines:

1. Read `.vscode/copilot-instructions.md` - This contains the complete development guidelines, safety protocols, and mandatory 8-step workflow for this Flask project.

2. Read all files in the `docs/` directory to understand the project structure, documentation standards, and what needs to be documented when making changes.

After reading these files, please confirm you understand and commit to following:
- The mandatory 8-step development workflow (never skip any steps)
- The safety protocols and circuit breakers 
- The Flask coding standards and patterns to follow
- All testing and documentation requirements

Please explicitly state: "I have read the project guidelines and commit to following all instructions, workflows, and safety protocols outlined in the files."
```

### **Context Verification Checklist**
- [ ] AI has read `.vscode/copilot-instructions.md`
- [ ] AI understands the 8-step mandatory workflow
- [ ] AI commits to anti-paralysis protocols
- [ ] AI knows speed-first principles (< 30 minutes per feature)
- [ ] AI understands the safety circuit breakers
- [ ] AI knows to update `docs/CHANGELOG.md` for all changes
- [ ] AI commits to following existing documentation structure
- [ ] AI knows Flask conventions take priority
- [ ] AI commits to minimal viable implementations first
- [ ] AI is aware of template resources (SDD/SDS) for complex projects

---

## 🔧 **ESSENTIAL PROJECT PATTERNS**

### **File Structure**
```
app/
├── models/         # SQLAlchemy models
├── routes/         # Flask blueprints
├── templates/      # Jinja2 templates
...
docs/
├── copilot/       # Copilot collaboration knowledge base
├── templates/     # Project document templates (SDD, SDS)
```

### **Documentation Templates**
For complex projects, use the established templates:
- `docs/templates/SDD_TEMPLATE.md` - Software Design Document for technical architecture
- `docs/templates/SDS_TEMPLATE.md` - Software Development Specification for requirements
├── static/         # CSS, JS, images
└── __init__.py     # App factory

tests/              # Pytest test files
docs/               # All documentation
├── copilot/        # AI collaboration knowledge base
└── CHANGELOG.md    # Required updates for all changes
```

### **Preferred Libraries**
- **Authentication**: Flask-Login
- **Forms**: Flask-WTF + WTForms
- **Database**: SQLAlchemy with Flask-SQLAlchemy
- **Testing**: pytest + pytest-cov
- **Environment**: python-dotenv
- **Security**: Flask-Talisman for headers

### **Speed-First Commands**
```bash
# Quick test status
pytest | grep -q "FAILED" && echo "❌ FIX NEEDED" || echo "✅ READY TO SHIP"

# Fast failure details  
pytest -x --tb=short | grep -A 5 -B 1 "FAILED\|ERROR"

# Coverage percentage only
pytest --cov=app | grep -E "TOTAL.*[0-9]+%"

# Run and commit (after validation)
git add . && git commit -m "feat: [description]"
```

---

## 📚 **DOCUMENTATION REQUIREMENTS**

### **Always Update These Files**
1. **`docs/CHANGELOG.md`** - Every change gets documented
2. **`docs/copilot/INTERACTIONS.md`** - Successful patterns
3. **`docs/copilot/LESSONS.md`** - Insights and learnings
4. **`docs/copilot/PROMPTS.md`** - Effective prompts used
5. **`docs/copilot/TEST_CHEATSHEET.md`** - 🧪 Actual codebase structure (prevents AI guessing)

---

## 🎯 **QUICK DECISION HIERARCHY**

### **When Multiple Options Exist**
1. **Use existing pattern** from codebase → Copy and adapt
2. **Use Flask standard** → Follow Flask conventions
3. **Use simplest approach** → Minimal working version

### **For Analysis Paralysis**
1. **Set 5-minute timer** for any analysis
2. **Choose first viable option** and proceed
3. **Implement immediately** without further research

---

## ⚠️ **CRITICAL SUCCESS FACTORS**

### **DO - Speed First Principles**
- ✅ Choose standard Flask patterns immediately
- ✅ Use existing codebase examples
- ✅ Implement minimal working versions
- ✅ Set time limits for all phases
- ✅ Follow the 8-step workflow religiously

### **DON'T - Analysis Paralysis Triggers**
- ❌ "What's the best approach?" → Use Flask standards
- ❌ "Let me analyze options..." → Choose first viable option
- ❌ Spend > 5 minutes on analysis → Emergency: pick and proceed
- ❌ Skip workflow steps → All 8 steps are mandatory
- ❌ Skip documentation → Always update CHANGELOG.md

---

*Last updated: June 12, 2025*  
*Usage: Just say "reload_context.md" for instant AI context loading*
