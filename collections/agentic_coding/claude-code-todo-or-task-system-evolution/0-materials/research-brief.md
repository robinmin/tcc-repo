# Claude Code Todo/Task System Evolution - Research Brief

**Topic**: Evolution of Claude Code's Todo/Task System
**Date**: 2026-02-02
**Confidence**: MEDIUM-HIGH
**Research Type**: Technical Documentation Analysis

---

## Executive Summary

Claude Code has undergone a significant evolution in its task management capabilities, transitioning from a basic `TodoWrite` tool to a sophisticated multi-tool task management system with `TaskList`, `TaskGet`, and `TaskUpdate`. This transition introduced dependency tracking and improved persistence but also came with several known issues that were addressed in subsequent releases.

---

## Timeline of Key Changes

| Version | Date | Change |
|---------|------|--------|
| **v2.1.16** | January 22, 2025 | Introduced new task management system with dedicated `TaskList`, `TaskGet`, and `TaskUpdate` tools (TodoWrite was already available) |
| **v2.1.19** | Late January 2025 | Added configuration option `CLAUDE_CODE_ENABLE_TASKS=false` |
| **v2.1.20** | January 2025 | Added task deletion via `TaskUpdate`, fixed multiple UI bugs |
| **v2.1.21** | January 2025 | Fixed task ID reuse bug after deletion |

---

## Current Tool Capabilities

### TodoWrite Tool
- Create and manage task lists (basic operations)
- Status tracking: pending, in_progress, completed
- Active form for current activity display
- **Note**: Original TodoWrite did not support dependency tracking (added in v2.1.16 via new tools)

### TaskList Tool
- View active tasks in current session
- Dynamically adjusts to terminal height
- Returns task list with IDs and statuses

### TaskGet Tool
- Retrieve details of a specific task by ID
- Returns full task object with metadata

### TaskUpdate Tool
- Update task status
- Delete tasks (introduced v2.1.20)
- Modify task metadata

---

## Known Issues Fixed

1. Session compaction causing full history load (v2.1.20)
2. Task ID reuse after deletion (v2.1.21)
3. Task list showing outside conversation view (v2.1.20)
4. Agents ignoring user messages during task work (v2.1.20)

---

## External Tools Integration

The rd2:tasks agent skill integrates with TodoWrite via:
- `rd2:tasks create` - Create task file
- `rd2:tasks list` - View WIP tasks
- `rd2:tasks update` - Mark task as done
- `rd2:tasks refresh` - Sync kanban board

---

## Recommendations for rd2:tasks Upgrade

1. **Migrate to dedicated tools**: Use TaskList/TaskGet/TaskUpdate instead of TodoWrite
2. **Implement dependency handling**: Support task dependencies in WBS format
3. **Add error handling**: Defensive checks for ID reuse edge cases
4. **Configuration awareness**: Detect and adapt to system version
5. **Backward compatibility**: Fallback to TodoWrite if new tools unavailable

---

## Sources
- Claude Code SDK Documentation (docs.claude.com)
- Anthropic GitHub Releases
- User CLAUDE.md configuration
