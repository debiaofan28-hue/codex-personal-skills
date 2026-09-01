---
name: obsidian-markmap-project-management
description: Maintain project task maps inside an Obsidian Vault with the Mindmap NextGen plugin. Use only when explicitly invoked for project tracking, task status, version history, or feature evolution; do not create standalone Markmap HTML.
---

# Obsidian Markmap Project Management

Obsidian is the only viewing surface for this skill. Markdown is the source of truth; the Mindmap NextGen plugin renders it inside Obsidian.

## Core contract

- Treat `TASKS.md` as the sole editable task source unless the user names another Markdown file.
- Do not generate `task-map.html`, standalone Markmap files, screenshots, or duplicate dashboards.
- Keep existing project instructions and user-authored files intact. Do not add project-specific rules to `AGENTS.md`.
- Do not overwrite a hand-built Canvas or note. Patch the Markdown source instead.
- Keep the workflow local. Do not publish, sync, or upload project files unless the user explicitly requests it.

## Obsidian setup boundary

- Check whether the project folder is already inside an Obsidian Vault.
- If it is not, tell the user to open the project folder as a Vault (or move/copy the Markdown into an existing Vault). Do not silently create `.obsidian`, install plugins, or change Vault trust/security settings.
- Check that the Vault has the Mindmap NextGen/Markmap view plugin enabled before relying on its rendering.
- After changing `TASKS.md`, ask the user to refresh or reopen the Mindmap tab if the view is stale.

## Update workflow

1. Inspect the applicable project instructions and only the relevant `TASKS.md` headings.
2. Patch the smallest branches affected by the request. Keep nodes short and actionable.
3. Use the standard structure when it fits the project:
   - `项目目标`
   - `当前范围`
   - `已完成`
   - `当前工作`
   - `版本迭代`
   - `功能演进索引`
   - `下一步`
   - `风险与限制`
   - `项目入口`
4. Keep major versions beside one another (`V1`, `V2`, `V3`); never nest a later version under an earlier one.
5. Keep `功能演进索引` compact: one branch per feature and one short line per meaningful version. Do not add a special “current version” marker.
6. For episodic video projects, separate the management view into `制作流水线` and `期数进度`; keep detailed subtitles, translations, TTS text, and render logs in their episode files.
7. Preserve status accurately:
   - `[x]` completed
   - `[ ]` pending or paused
   - Use plain labels such as `进行中`, `阻塞`, and `风险` when needed; do not add Emoji status markers unless requested.
8. Verify that `TASKS.md` still parses as Markdown, its `markmap` frontmatter remains valid, and links point to real project files where practical.
9. Report the changed branches and the Obsidian note to refresh. Do not report an HTML output because none is produced.

## Markmap frontmatter

For a new task note, use this compact configuration unless the user requests another style:

```yaml
---
markmap:
  coloring: branch
  color:
    - "#1f77b4"
    - "#ff7f0e"
    - "#2ca02c"
    - "#d62728"
    - "#9467bd"
    - "#8c564b"
    - "#e377c2"
    - "#7f7f7f"
    - "#bcbd22"
    - "#17becf"
  colorFreezeLevel: 2
  initialExpandLevel: 4
  maxWidth: 0
---
```

Use `coloring: branch` with `colorFreezeLevel: 2` to match normal Markmap: each top-level branch keeps its own color and deeper descendants inherit that branch color. Depth-based coloring ignores the freeze-level behavior.
Use `maxWidth: 0` to keep node text on one line; a positive value forces automatic wrapping at that width.

For an existing note, change only the requested `markmap` properties. Use inline `nodeColor`, `bgColor`, or `color` comments only for deliberate branch emphasis; do not decorate every node.

## Token and edit discipline

- Read targeted headings instead of repeatedly loading the entire project.
- Update once after a batch of related changes, then let Obsidian render the note.
- Keep the map an index, not a transcript or archive.
- Do not paste generated rendering data into the conversation.
- Preserve old versions and actual completion marks; do not invent progress states.

## Resource

- Use [assets/TASKS.template.md](assets/TASKS.template.md) when a new Obsidian task note needs a compact starting structure.
