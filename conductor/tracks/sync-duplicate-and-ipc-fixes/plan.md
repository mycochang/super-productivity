# Track Plan: Sync Duplicate & IPC Fixes

## Phase 1: Fix IPC getTasks Filter Bug (SP-MCP)

- [x] Task 1: Implement `project_id` and `projectId` filtering inside `get_tasks` in `/home/mchang/repos/SP-MCP/mcp_server.py` (Completed - 2f61d05)
- [x] Task 2: Run a local Python-based test script to verify that `get_tasks` strictly filters and returns only CEO project tasks when the filter is applied (Verified - 2f61d05)

## Phase 2: Audit & Verify Trello Plugin Card Matching

- [x] Task 3: Audit `mapSearchResult` and `mapIssue` inside `packages/plugin-dev/trello-issue-provider/src/plugin.ts` to ensure they use stable, unique identifiers (`card.shortLink` or `card.id`) as their matching `id` property (Audited)
- [x] Task 4: Compile and build the Trello plugin to ensure it remains 100% syntactically correct and fully operational (Compiled - dist/plugin.js)

## Phase 3: Final Integration Verification

- [x] Task 5: Verify the complete live synchronization loop is robust, keeps duplicates out, and is safe from cascade deletions (Sync Confirmed & Protected!)
