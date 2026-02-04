Please read CLAUDE.md!!

---

## Machine Identifiers & Sync Ecosystem

Use these flags to indicate **WHERE work needs to be done** in task titles and descriptions.

| Flag        | Machine               | OS                             | Role                                | Status     | Current Version     |
| ----------- | --------------------- | ------------------------------ | ----------------------------------- | ---------- | ------------------- |
| `[omen]`    | 3070 home workstation | CachyOS Linux (Wayland+Nvidia) | Source of truth, builds from source | ✅ LIVE    | v17.1.0             |
| `[noi4070]` | NOI Linux workstation | Linux                          | Dev/test machine                    | 📋 TODO    | RC.12 → v17.1.0     |
| `[fw13]`    | Framework 13 laptop   | Windows 11                     | Portable/field work                 | 📋 TODO    | -                   |
| `[ios]`     | iPad/iPhone           | iOS                            | Mobile sync                         | ⏳ PENDING | v17.1.0 (App Store) |

### Usage in Task Titles

Prefix task subjects with the relevant machine flag(s):

- `[omen] Build & test v17.1.0 release`
- `[noi4070] Pull latest upstream and rebuild`
- `[fw13] Download Windows release and configure WebDAV`
- `[omen][ios] Verify iOS app store update when available`

### Current Sync Status (2026-02-04)

**Source of Truth:** `[omen]` (v17.1.0, fully synced)

- `[noi4070]`: Needs upgrade from RC.12 to v17.1.0 + rebuild
- `[fw13]`: Bonus track - download Windows release and configure
- `[ios]`: Blocked on App Store review (24-48h after 2026-02-04 release)

**Round-trip testing:** Pending until all machines are on v17.1.0

### Reference

- GitHub Release: https://github.com/johannesjo/super-productivity/releases/tag/v17.1.0
- Sync Backend: Synology NAS WebDAV (`https://taiga.arbor-insight.com:5006`)
- Taiga User Story: Project FOSS #35 "⚡ Harmonize SuperProductivity MCP"
