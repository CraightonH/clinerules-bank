# Distributed Prompt System - Technical Documentation

## Overview
The Distributed Prompt System allows for context-aware task prompts to be placed throughout the project directory structure. This document provides technical details on how the system should process these prompts.

## File Format and Location
- Prompt files are named `prompts.md` and can exist in any directory within the project
- Each file contains a simple markdown structure with a list of prompts:
    ```markdown
    # Prompts
    - "First prompt to process"
    - "Second prompt to process"
    - "Third prompt to process"
    ```
- The order of prompts in the list determines processing priority (top to bottom)

## Processing Rules

### When to Check for Prompts
1. After completing any task
2. When explicitly instructed to check for prompts
3. At the beginning of a new session

### Context Gathering Procedure
When a `prompts.md` file is found:
1. **Local Context First**: Gather context from the current directory and its subdirectories
   - Read relevant code files, documentation, and configuration in the current directory
   - Examine subdirectories for related files
   - Build a contextual understanding based on these local files

2. **Minimal Context Expansion**: Only if the local context is insufficient:
   - Move up one directory level at a time
   - Gather additional context from each level as needed
   - Stop expanding once sufficient context is available to complete the prompt

3. **Context Prioritization**:
   - Files in the same directory as the `prompts.md` file have highest priority
   - Subdirectory files have second priority
   - Parent directory files have lower priority
   - The further from the `prompts.md` file, the lower the priority

### Prompt Processing
1. Process prompts in the order listed (top to bottom)
2. For each prompt:
   - Gather context as described above
   - Interpret the prompt based on the gathered context
   - Execute the necessary actions to complete the prompt
   - Remove the completed prompt from the file
   - If the file becomes empty (no more prompts), delete the file

3. If multiple `prompts.md` files exist:
   - Process files in directories where you're currently working first
   - Then process files in subdirectories
   - Then process files in parent directories
   - Within each level, process alphabetically by directory name

## Updating System State
After processing prompts:
1. Update `changelog.md` with any changes made while processing prompts
2. Update `.clinerules` if prompt processing affects the system or next actions

## Error Handling
If a prompt cannot be processed due to:
- Insufficient context: Note in `activeContext.md` and request more information
- Conflicts with current state: Document the conflict and suggest resolution
- Technical limitations: Explain the limitation and suggest alternatives

Never delete a prompt without either completing it or explicitly documenting why it cannot be completed.