<img width="1280" height="640" alt="agent-os-og" src="https://github.com/user-attachments/assets/f70671a2-66e8-4c80-8998-d4318af55d10" />

## Your system for spec-driven agentic development.

[Agent OS](https://buildermethods.com/agent-os) transforms AI coding agents from confused interns into productive developers. With structured workflows that capture your standards, your stack, and the unique details of your codebase, Agent OS gives your agents the specs they need to ship quality code on the first try—not the fifth.

Use it with:

✅ Claude Code, Cursor, or any other AI coding tool.

✅ New products or established codebases.

✅ Big features, small fixes, or anything in between.

✅ Any language or framework.

---

### Documentation & Installation

Docs, installation, useage, & best practices 👉 [It's all here](https://buildermethods.com/agent-os)

---

### 🚀 Gemini CLI Integration for Large Codebase Analysis

Agent OS now includes integration with Google's Gemini CLI for analyzing large codebases that exceed standard context limits.

#### When to Use Gemini CLI

Use Gemini CLI when:
- Analyzing entire codebases or large directories (>100KB or >50 files)
- Verifying if specific features or patterns are implemented across the entire codebase
- Checking for security measures, coding patterns, or architectural decisions
- Working with files that would overflow standard AI context windows

#### Setting Up Gemini CLI

##### 1. Install Gemini CLI

```bash
# Install via npm
npm install -g @google/generative-ai-cli

# Or install via pip
pip install google-generative-ai-cli
```

##### 2. Configure Gemini Authentication

**Option A: API Key (Recommended for personal use)**

```bash
# Set your Gemini API key as an environment variable
export GEMINI_API_KEY="your-api-key-here"

# Or add to your shell profile (.bashrc, .zshrc, etc.)
echo 'export GEMINI_API_KEY="your-api-key-here"' >> ~/.zshrc
```

Get your API key from: https://makersuite.google.com/app/apikey

**Option B: Application Default Credentials (For Google Cloud users)**

```bash
# Authenticate with Google Cloud
gcloud auth application-default login

# The Gemini CLI will automatically use these credentials
```

**Option C: Config File**

Create a `.gemini` config file in your home directory:

```json
{
  "apiKey": "your-api-key-here",
  "model": "gemini-1.5-pro-latest"
}
```

##### 3. Verify Installation

```bash
# Test the Gemini CLI
gemini -p "Hello, Gemini!"

# Test with a file
gemini -p "@README.md Summarize this file"
```

#### Usage Examples

```bash
# Analyze entire codebase architecture
gemini --all_files -p "Provide a comprehensive analysis of this codebase"

# Check for specific feature implementation
gemini -p "@src/ @lib/ Has dark mode been implemented? Show relevant files"

# Verify security measures
gemini -p "@api/ @middleware/ Is rate limiting implemented? Show details"

# Analyze test coverage
gemini -p "@src/payment/ @tests/ Is the payment module fully tested?"
```

#### Integration with Agent OS Workflows

Agent OS automatically uses Gemini CLI when:
- Running `analyze-product.md` on large codebases
- Executing tasks that require understanding of the entire codebase
- Verifying no duplicate functionality exists before implementation

See `instructions/tools/gemini-analysis.md` and `standards/large-codebase-analysis.md` for detailed usage guidelines.

---

### Created by Brian Casel @ Builder Methods

Created by Brian Casel, the creator of [Builder Methods](https://buildermethods.com), where Brian helps professional software developers and teams build with AI.

Get Brian's free resources on building with AI:
- [Builder Briefing newsletter](https://buildermethods.com)
- [YouTube](https://youtube.com/@briancasel)

