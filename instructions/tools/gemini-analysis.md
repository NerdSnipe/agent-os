---
description: Using Gemini CLI for Large Codebase Analysis
globs:
alwaysApply: false
version: 1.0
encoding: UTF-8
---

# Using Gemini CLI for Large Codebase Analysis

## Overview

When analyzing large codebases or multiple files that might exceed context limits, use the Gemini CLI with its massive context window. Use `gemini -p` to leverage Google Gemini's large context capacity.

<pre_flight_check>
  EXECUTE: @~/.agent-os/instructions/meta/pre-flight.md
</pre_flight_check>

<process_flow>

<step number="1" name="determine_analysis_scope">

### Step 1: Determine Analysis Scope

Evaluate whether Gemini CLI should be used based on codebase size and task requirements.

<use_gemini_when>
  <codebase_analysis>
    - Analyzing entire codebases or large directories
    - Comparing multiple large files
    - Need to understand project-wide patterns or architecture
    - Current context window is insufficient for the task
    - Working with files totaling more than 100KB
  </codebase_analysis>
  <verification_tasks>
    - Verifying if specific features, patterns, or security measures are implemented
    - Checking for the presence of certain coding patterns across the entire codebase
    - Checking large log files for debug change patterns
  </verification_tasks>
</use_gemini_when>

<instructions>
  ACTION: Evaluate if task requires large context analysis
  CHECK: File sizes and directory scope
  DECIDE: Use Gemini CLI for large-scale analysis
</instructions>

</step>

<step number="2" name="file_inclusion_syntax">

### Step 2: File and Directory Inclusion Syntax

Use the `@` syntax to include files and directories in your Gemini prompts. Paths should be relative to WHERE you run the gemini command.

<syntax_examples>
  <single_file>
    gemini -p "@src/main.py Explain this file's purpose and structure"
  </single_file>
  
  <multiple_files>
    gemini -p "@package.json @src/index.js Analyze the dependencies used in the code"
  </multiple_files>
  
  <entire_directory>
    gemini -p "@src/ Summarize the architecture of this codebase"
  </entire_directory>
  
  <multiple_directories>
    gemini -p "@src/ @tests/ Analyze test coverage for the source code"
  </multiple_directories>
  
  <current_directory>
    gemini -p "@./ Give me an overview of this entire project"
    # Or use --all_files flag:
    gemini --all_files -p "Analyze the project structure and dependencies"
  </current_directory>
</syntax_examples>

<instructions>
  ACTION: Construct appropriate file inclusion syntax
  NOTE: Paths are relative to command execution directory
  USE: @ syntax for explicit file/directory inclusion
</instructions>

</step>

<step number="3" name="implementation_verification">

### Step 3: Implementation Verification Examples

Use Gemini CLI to verify specific implementations and patterns across the codebase.

<verification_queries>
  <feature_check>
    gemini -p "@src/ @lib/ Has dark mode been implemented in this codebase? Show me the relevant files and functions"
  </feature_check>
  
  <authentication_check>
    gemini -p "@src/ @middleware/ Is JWT authentication implemented? List all auth-related endpoints and middleware"
  </authentication_check>
  
  <pattern_search>
    gemini -p "@src/ Are there any React hooks that handle WebSocket connections? List them with file paths"
  </pattern_search>
  
  <error_handling_check>
    gemini -p "@src/ @api/ Is proper error handling implemented for all API endpoints? Show examples of try-catch blocks"
  </error_handling_check>
  
  <rate_limiting_check>
    gemini -p "@backend/ @middleware/ Is rate limiting implemented for the API? Show the implementation details"
  </rate_limiting_check>
  
  <caching_check>
    gemini -p "@src/ @lib/ @services/ Is Redis caching implemented? List all cache-related functions and their usage"
  </caching_check>
  
  <security_check>
    gemini -p "@src/ @api/ Are SQL injection protections implemented? Show how user inputs are sanitized"
  </security_check>
  
  <test_coverage_check>
    gemini -p "@src/payment/ @tests/ Is the payment processing module fully tested? List all test cases"
  </test_coverage_check>
</verification_queries>

<instructions>
  ACTION: Use specific queries for targeted verification
  INCLUDE: Relevant directories in @ syntax
  REQUEST: Concrete evidence and file paths
</instructions>

</step>

<step number="4" name="integration_with_agent_os">

### Step 4: Integration with Agent OS Workflows

Incorporate Gemini CLI analysis into standard Agent OS processes.

<integration_points>
  <during_analyze_product>
    When executing analyze-product.md:
    - Use Gemini to scan entire codebase for feature detection
    - Verify implementation completeness
    - Identify architectural patterns
  </during_analyze_product>
  
  <during_execute_task>
    When executing execute-task.md:
    - Use Gemini to understand existing implementations before modifications
    - Check for similar patterns in the codebase
    - Verify no duplicate functionality exists
  </during_execute_task>
  
  <during_create_spec>
    When executing create-spec.md:
    - Use Gemini to analyze existing code for integration points
    - Verify technical constraints across the codebase
    - Check for conflicting implementations
  </during_create_spec>
</integration_points>

<workflow_example>
  # Before implementing new feature
  gemini -p "@src/ @lib/ Is there existing functionality for [FEATURE]? List any related implementations"
  
  # After implementation
  gemini -p "@src/ @tests/ Verify the new [FEATURE] integrates properly with existing code. Check for conflicts or duplications"
</workflow_example>

<instructions>
  ACTION: Integrate Gemini analysis at key decision points
  VERIFY: Implementation doesn't duplicate existing code
  CHECK: Integration with existing architecture
</instructions>

</step>

<step number="5" name="best_practices">

### Step 5: Gemini CLI Best Practices

Follow these guidelines for effective Gemini CLI usage.

<usage_guidelines>
  <context_management>
    - Include only relevant directories/files for the query
    - Use specific paths rather than entire codebase when possible
    - Structure queries to get actionable responses
  </context_management>
  
  <query_optimization>
    - Be specific about what you're looking for
    - Request concrete evidence (file paths, function names)
    - Ask for examples when verifying implementations
  </query_optimization>
  
  <performance_considerations>
    - Use --all_files sparingly (only for full project analysis)
    - Target specific directories for focused analysis
    - Break large analyses into smaller, targeted queries
  </performance_considerations>
</usage_guidelines>

<important_notes>
  - Paths in @ syntax are relative to your current working directory when invoking gemini
  - The CLI will include file contents directly in the context
  - No need for --yolo flag for read-only analysis
  - Gemini's context window can handle entire codebases that would overflow Claude's context
  - When checking implementations, be specific about what you're looking for to get accurate results
</important_notes>

<instructions>
  ACTION: Follow best practices for optimal results
  OPTIMIZE: Query structure for actionable responses
  MANAGE: Context efficiently with targeted inclusions
</instructions>

</step>

</process_flow>

## Error Handling

<error_scenarios>
  <scenario name="context_overflow">
    <condition>Even Gemini's context is exceeded</condition>
    <action>Break analysis into smaller directory chunks</action>
  </scenario>
  <scenario name="unclear_results">
    <condition>Gemini provides vague or incomplete analysis</condition>
    <action>Refine query with more specific requirements</action>
  </scenario>
  <scenario name="path_errors">
    <condition>Files not found with @ syntax</condition>
    <action>Verify current directory and adjust paths</action>
  </scenario>
</error_scenarios>

## Execution Summary

<final_checklist>
  <verify>
    - [ ] Appropriate use case for Gemini CLI identified
    - [ ] Correct @ syntax used for file inclusion
    - [ ] Specific verification queries constructed
    - [ ] Results integrated into Agent OS workflow
    - [ ] Best practices followed for optimal analysis
  </verify>
</final_checklist>