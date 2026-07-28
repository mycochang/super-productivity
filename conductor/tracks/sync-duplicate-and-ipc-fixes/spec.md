# Conductor Feature Specification: Sync Duplicate & IPC Fixes

## 1. Product Goals

1. **Fix the IPC Filter Bug:** Update the local Python-based `SP-MCP` server (`mcp_server.py`) to respect the `projectId` / `project_id` filter when querying tasks. This isolates CLI sync operations to their target project, preventing accidental deletions or leakages across other projects.
2. **Fix Trello Duplicate Re-Imports:** Ensure the local Trello plugin (`trello-issue-provider`) strictly uses card `shortLink` or actual `id` as the primary matching key (`issueId`) to update existing cards instead of minting duplicates with incremented numbers during re-sync.
3. **Analyze Google Calendar Loops:** Map out a strategy to handle recurring Google Calendar events without creating separate task cards for every single occurrence.

---

## 2. IPC getTasks Filtering Implementation

We will update `get_tasks` inside `/home/mchang/repos/SP-MCP/mcp_server.py` to intercept and filter returned tasks on the Python bridge level:

```python
    async def get_tasks(self, args: Dict[str, Any]) -> Dict[str, Any]:
        """Get all tasks, optionally filtered by project_id"""
        res = await self.send_command("getTasks")
        if not res.get("success"):
            return res

        project_id = args.get("project_id") or args.get("projectId")
        if project_id:
            tasks = res.get("result", [])
            filtered_tasks = [t for t in tasks if t.get("projectId") == project_id]
            res["result"] = filtered_tasks

        return res
```

---

## 3. Trello Duplicate Prevention

The Trello plugin must map its unique card identifier as the `id` of `PluginIssue` / `PluginSearchResult` objects.

- Core sync adapter (`plugin-sync-adapter.service.ts`) matches imported tasks on `task.issueId === pluginIssue.id`.
- We will verify that `mapSearchResult` and `mapIssue` inside `packages/plugin-dev/trello-issue-provider/src/plugin.ts` correctly use `card.shortLink` (the unique short card identifier like `DhaNnrtv` / `GoEukj5d`) or the actual `card.id` as the identifier, preventing duplicated card tasks when titles differ.
