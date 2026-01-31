# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is an empty repository, that will act has a 'home page' for the Happy Healthy Discord server. It will be a ReActive website, with a few pages:
- Home
- Rules
- Server Rules
- Server Rules
- Ban Appeals

## AI Assistant Workflow Requirements

**CRITICAL: ALWAYS PROACTIVELY USE THE TASK TOOL TO SPAWN SUBAGENTS**

To manage context effectively and avoid token budget exhaustion:

1. **Use the Task Tool for ALL exploration tasks** - Never use Grep/Glob directly when exploring the codebase
   - ✅ DO: Launch `Explore` subagent (quick/medium/very thorough) for codebase searches
   - ❌ DON'T: Run multiple Grep/Glob commands directly in the main conversation

2. **Use specialized subagents proactively**:
   - `git-ops` - For ALL git operations (status, diff, commit, push, branch management)
   - `Explore` - For understanding code structure, finding files, searching patterns
   - `general-purpose` - For multi-step complex tasks requiring research
   - `web-search` - For looking up documentation, current library versions, etc.

3. **Context preservation strategy**:
   - Subagents run with isolated context and report back results
   - This prevents the main conversation from being flooded with file contents
   - Keeps token usage low for complex tasks
   - Allows parallel execution of independent tasks

4. **When to use subagents**:
   - Before making code changes: Launch `Explore` to understand existing implementation
   - For git operations: ALWAYS use `git-ops` agent
   - When searching for patterns: Use `Explore` with appropriate thoroughness level
   - For research tasks: Use `general-purpose` or `web-search` as appropriate

**Example workflow:**
```
User: "Add a new feature X"
Assistant:
1. Launch Explore subagent to understand existing codebase structure
2. Wait for subagent results
3. Plan implementation based on findings
4. Make changes to code
5. Launch git-ops subagent to commit and push
```

This approach is MANDATORY for efficient operation and prevents context overflow on complex tasks.