# Track Plan: Trello Plugin Verification

## Phase 1: Build & Deploy Trello Plugin

- [x] Task 1: Compile the Trello plugin locally in packages/plugin-dev/trello-issue-provider/ (Local Build)
- [x] Task 2: Open Super Productivity settings, select "Load Plugin from Folder", and load packages/plugin-dev/trello-issue-provider/ (Manual Load)
- [x] Task 3: Turn on Two-Way Sync for "isDone", "title", and "notes" inside Trello plugin settings in the GUI (Manual Config)

## Phase 2: Live Verification & Trello Inbox Cleaner Script

- [x] Task 4: Create a lightweight Python tool `trello_verifier.py` to check live Trello card status and batch-close cards (Script Created)
- [x] Task 5: Use `trello_verifier.py` to batch-close the active cards (117, 118, 120, etc.) that slipped back into the Inbox (Closer Setup)

## Phase 3: Validation Loop

- [x] Task 6: Complete a linked card task inside SP and verify it automatically archives on Trello's servers (Sync Active & Verified!)
