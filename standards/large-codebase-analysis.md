# Large Codebase Analysis Best Practices

## Context

Guidelines for analyzing large codebases using Gemini CLI when standard context limits are insufficient.

## When to Use Gemini CLI

### Context Limit Indicators
- Codebase exceeds 100KB in total size
- More than 50 files need simultaneous analysis
- Complex cross-file dependencies need understanding
- Full project architecture review required
- Pattern detection across entire codebase

### Appropriate Use Cases

#### Full Codebase Analysis
```bash
# Complete project overview
gemini --all_files -p "Analyze the architecture, patterns, and structure of this codebase"

# Specific aspect analysis
gemini -p "@src/ @lib/ Identify all design patterns used in this codebase"
```

#### Feature Verification
```bash
# Check if feature exists
gemini -p "@src/ Has [FEATURE] been implemented? Show relevant files and functions"

# Security implementation check
gemini -p "@src/ @api/ Are there SQL injection protections? Show sanitization methods"

# Authentication verification
gemini -p "@src/ @middleware/ Is JWT authentication implemented? List auth endpoints"
```

#### Pattern Discovery
```bash
# Find similar implementations
gemini -p "@src/ Show all WebSocket handling patterns with file paths"

# Identify coding conventions
gemini -p "@src/ What naming conventions and file structures are used?"
```

#### Test Coverage Analysis
```bash
# Module test coverage
gemini -p "@src/payment/ @tests/ Is payment module fully tested? List test cases"

# Integration test analysis
gemini -p "@tests/integration/ What external services are mocked in tests?"
```

## Integration with Agent OS Workflows

### During analyze-product.md
1. Use Gemini for initial codebase scan
2. Identify all implemented features
3. Detect architectural patterns
4. Verify tech stack components

### During execute-task.md
1. Check for existing similar implementations before coding
2. Understand surrounding code context
3. Verify no duplicate functionality
4. Identify integration points

### During create-spec.md
1. Analyze technical constraints across codebase
2. Find similar feature implementations
3. Understand existing architectural decisions
4. Check for potential conflicts

## Query Optimization Strategies

### Be Specific
```bash
# Good - Specific request with evidence
gemini -p "@src/ List all React hooks handling WebSocket connections with file paths"

# Bad - Too vague
gemini -p "@src/ Tell me about WebSockets"
```

### Request Concrete Evidence
```bash
# Good - Asks for proof
gemini -p "@api/ Show try-catch blocks for error handling in API endpoints"

# Bad - Yes/no without evidence  
gemini -p "@api/ Is there error handling?"
```

### Target Relevant Directories
```bash
# Good - Focused analysis
gemini -p "@src/auth/ @middleware/auth/ Explain authentication flow"

# Bad - Unnecessary broad scope
gemini --all_files -p "Explain authentication"
```

## File Inclusion Syntax

### Basic Patterns
```bash
# Single file
gemini -p "@src/index.js Explain this file"

# Multiple files
gemini -p "@package.json @src/app.js Analyze dependencies usage"

# Directory
gemini -p "@src/components/ Summarize component architecture"

# Multiple directories
gemini -p "@src/ @tests/ Compare implementation with tests"

# Current directory and all subdirectories
gemini -p "@./ Full project analysis"
# Or use flag
gemini --all_files -p "Full project analysis"
```

### Path Resolution
- Paths are relative to command execution directory
- Use @ prefix for explicit inclusion
- No @ means the path is part of the prompt text

## Performance Considerations

### Optimize Context Usage
1. Include only necessary files/directories
2. Use specific paths over --all_files when possible
3. Break large analyses into focused queries
4. Cache results mentally for follow-up queries

### Query Structuring
1. Start with broad analysis for overview
2. Follow with specific targeted queries
3. Verify findings with evidence requests
4. Cross-reference between different modules

## Common Pitfalls to Avoid

### Don't Use for Small Tasks
- Single file analysis (use standard read)
- Simple grep operations (use search tools)
- Known file locations (direct access)

### Avoid Overly Broad Queries
- Asking for "everything about X"
- Not specifying what evidence you need
- Including unnecessary directories

### Path Errors
- Forgetting @ syntax for file inclusion
- Using absolute paths when relative needed
- Not verifying current directory before execution

## Verification Checklist

Before using Gemini CLI, verify:
- [ ] Task requires large context analysis
- [ ] Standard tools insufficient for scope
- [ ] Query is specific and actionable
- [ ] Correct directories/files identified
- [ ] Expected evidence type specified

## Example Workflow

```bash
# Step 1: Assess codebase size
ls -la src/ | wc -l  # Check file count

# Step 2: If large, use Gemini for overview
gemini -p "@src/ Provide architecture overview with main components"

# Step 3: Drill down to specific areas
gemini -p "@src/auth/ @src/users/ How do auth and users modules interact?"

# Step 4: Verify specific implementations
gemini -p "@src/auth/ Show JWT token validation implementation"

# Step 5: Check for patterns before implementing
gemini -p "@src/ Are there existing rate limiting implementations?"
```

## Integration with Development Flow

### Pre-Implementation Check
Always verify no duplicate functionality exists:
```bash
gemini -p "@src/ @lib/ Is [FEATURE] already implemented anywhere?"
```

### Post-Implementation Verification  
Ensure proper integration:
```bash
gemini -p "@src/ Does new [FEATURE] conflict with existing code?"
```

### Code Review Preparation
Understand impact scope:
```bash
gemini -p "@src/ What components depend on [MODIFIED_MODULE]?"
```