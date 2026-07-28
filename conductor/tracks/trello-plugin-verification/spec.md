# Conductor Track Specification: Trello Plugin Verification

## 1. Problem Diagnostics

- **Symptom:** Live testing of checking off a Trello-linked task inside Super Productivity (SP) does not close/archive the card on Trello. The card remains unchanged on Trello's board.
- **Root Cause:** Upstream migrated Trello from a core integration to a development plugin (`packages/plugin-dev/trello-issue-provider/`). The base plugin migrated by upstream did not implement the optional `updateIssue` method (which manages write-backs/two-way sync). Thus, checking off tasks locally in SP had no backend code to invoke PUT requests.
- **Fix Applied:** We have successfully re-engineered and implemented `updateIssue`, `extractSyncValues`, and 2-way `fieldMappings` inside the new pluggable format (`packages/plugin-dev/trello-issue-provider/src/plugin.ts`). We also exposed `twoWaySync` settings inside the plugin's configuration form in `plugin.ts`.

---

## 2. Verification Loop Design

To verify that our new plugin-based 2-way sync works flawlessly, we will establish a **local verification loop**:

1. **Build Plugin:** Compile the Trello plugin locally.
2. **Load Plugin:** In the Super Productivity desktop app settings, use **"Load Plugin from Folder"** to load `packages/plugin-dev/trello-issue-provider/`.
3. **Verify Configuration:** Open the Trello plugin settings and verify that our new `Two-Way Sync` dropdown selectors render correctly. Turn on `Two-Way Sync` for `isDone` and `title`.
4. **Create & Link Test Card:** Create a card on your Trello board and import it into SP.
5. **Trigger local complete:** Check off the task in SP.
6. **Query Trello Server:** Execute a lightweight verification command (or Python tool) on Omen to query the Trello API and confirm that the card is closed/completed on their live server.

---

## 3. Lightweight Trello CLI Verifier

Instead of installing heavy external Trello MCP servers, we will use a highly efficient, sovereign shell command utilizing your existing Trello credentials (`apiKey` and `token`) to inspect card statuses directly:

### Get Card Status

```bash
curl -s "https://api.trello.com/1/cards/{cardId}?key={apiKey}&token={token}" | jq '{id: .id, name: .name, closed: .closed, dueComplete: .dueComplete}'
```

### Force Card Update (For testing pull sync)

```bash
curl -s -X PUT "https://api.trello.com/1/cards/{cardId}?key={apiKey}&token={token}&closed=true"
```
