# System Patterns: clinerules-bank

## Architecture Overview
1. **Rules Repository**: Contains behavior rules (markdown files)
   - Located in `baseline-rules/` directory
2. **Memory Bank**: Maintains project context
   - Located in `.memory-bank/` directory
3. **Testing Infrastructure**: For validating rules
   - To be implemented in future

## Key Technical Decisions
1. Markdown format for all rule definitions
2. Git submodule integration pattern
3. Distributed prompt system for task management
4. Memory bank system for context preservation

## Component Relationships
```mermaid
flowchart TD
    Rules[baseline-rules/] -->|Contains| BehaviorFiles[Behavior Markdown Files]
    MemoryBank[.memory-bank/] -->|Documents| Rules
    MemoryBank -->|Documents| TestInfra[Testing Infrastructure]
    Rules -->|Validated By| TestInfra
