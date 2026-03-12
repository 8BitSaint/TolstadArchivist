# 🕵️ Tolstad Archivist's Handbook
**Mission:** To map the world, systems, and lore of *Esoteric Ebb* with surgical precision, maintaining a definitive, high-signal completionist knowledgebase.

## 1. Operational Mandates
*Rules governing the AI's presence and actions within the vault.*

- **Source of Truth:** The `/Templates` directory is the absolute authority for file structure. All entries must eventually conform to these blueprints.
- **Session Initialization:** **ALWAYS** check for remote updates at the start of a session. Run `git fetch origin` and `git status` to ensure the local branch is synchronized. **Additionally, ALWAYS read the most recent context bridge(s) in `.gemini/` to restore session context.**
- **Topic Discipline:** **ALWAYS** ask for explicit confirmation before concluding a task or moving from one high-level topic (e.g., Git cleanup) to another (e.g., folder audits).
- **Finalization:** Before wrapping up any session, all staged and unstaged changes MUST be committed and squashed into a single commit for that session.
- **Git & Safety:**
    - **Explicit Permission:** **NEVER** execute Git commands (commit, reset, push, etc.) without explicit user permission for every action.
    - **Pushing Policy:** **NEVER** attempt to push changes to a remote repository. All pushing is to be handled manually by the user outside of the session.
- **Validation:** Always verify that links work and templates are strictly followed.
- **Proactivity:** Suggest links and create stubs for mentioned entities, but prioritize existing templates.

## 2. Archival Standards
*The craft of organizing and linking data.*

- **Linking Rules:**
    - **First Occurrence Only:** Link only the first mention of an entry in a document.
    - **Guide Exception:** In "Obtaining", "Completing", or step-by-step sections, link *every* occurrence to ensure ease of navigation without scrolling.
    - **Shortest Path:** Prefer the shortest possible link (e.g., `[[Akzel Madsson]]` instead of full file paths).
    - **Text Fidelity:** Avoid modifying link text to fit sentences unless absolutely necessary for readability.
- **Tagging Taxonomy:**
    - **High-Signal Only:** Use tags for cross-cutting attributes like `#LevelX`, `#HP`, or `#LawfulGood`. (Note: Magic schools like [[Necromancy]] use wikilinks instead of tags).
    - **No Redundant Categories:** **DO NOT** use tags that repeat the directory name (e.g., no `#Quests`, `#Spells`). The folder structure and graph "Path" groups are the primary categorization method.
    - **Inline Preferred:** Use inline tags whenever they fit naturally in the text.
    - **Frontmatter Fallback:** Use frontmatter `tags:` only for data that doesn't fit the text or is a high-level attribute.
    - **Spell Exception:** For spells in `Menus/Spellbook/`, use inline tags in the `# Info` table (e.g., `#Level1`, `#Cantrip`) to ensure they are indexed correctly while remaining readable.

## 3. Template Registry & Logic
*The blueprints and granular logic for archival entries.*

- **Interactable Character Template:**
    - *Sections:* `# Stats`, `# Locations`, `# Questlines / Events`, `# Associations`, `# Text`, `# Notes`.
    - *Logic:* Reserved for interactable characters in `Game World/`. `Text` section priority is the game's "Behold" text. If the NPC cannot be Beheld, fallback to key dialogue (e.g., [[Haelon Bondavol]]).
- **Visitable Location Template:**
    - *Sections:* `# Meta` (Affiliation, Accessibility), `# Description / Text` (Behold callouts), `# Map Connections`, `# Characters`, `# Loot`, `# Secrets`, `# Related Entries`, `# Notes`.
    - *Logic:* Reserved for visitable locations in `Game World/`. Link corresponding Journal entries in `# Related Entries`.
- **Journal Entry Template:**
    - *Sections:* `# [Skill Name or General]`, `## Meta`, `## Text`, `# Related Entries`, `# Notes`.
    - *Logic:* Used for all `Menus/Journal/` subdirectories. The top-level header MUST be the skill name (e.g., `# Intelligence`) or `# General` if unknown.
    - *Meta:* Includes `**Difficulty Check:**`, `**Source:**` (e.g., "Book", "NPC Name"), and `**Categories:**`.
    - *Multi-Entry Logic:** If multiple skill versions exist (e.g., Intelligence vs. Wisdom):
        1. Each gets a top-level `# [Skill Name]` header.
        2. Each has its own `## Meta` and `## Text`.
        3. Separate different skill versions with a horizontal rule (`---`).
        4. **Always** include a horizontal rule (`---`) before the `# Related Entries` and `# Notes` sections at the bottom of the file.
- **Inventory Item Template:**
    - *Sections:* `# Meta`, `# Description / Text`, `# Mechanics / Effects`, `# Obtaining`, `# Related Entries`.
    - *Naming:* Use **Title Case** for filenames (e.g., `Pickaxe of Secrets.md`).
    - *Meta:* Tracks the primary `**Source:**` of the item.
    - *Mechanics / Effects:* Distinguishes between flat `**Stats:**` and `**Special:**` abilities or utility.
    - *Related Entries:* Explicitly links to related `Quests`, `Characters`, and `Locations`.
    - *Legacy:* OCR artifacts (like ALL CAPS) should be removed or converted to Title Case during audits.
- **Spell Template:**
    - *Sections:* `# Info` (Tables), `# Text / Effect`, `# Mechanics`, `# Obtaining`, `# Related Entries`.
    - *Logic:* Strictly for functional entries in `Menus/Spellbook/`. Entries in `Menus/Journal/Spells/` use the **Journal Entry Template**. Use the `# Info` tables for technical stats (Level, School, Range, etc.).
    - *Leveling:* Use inline tags in the `Level` column: `#Level1`, `#Level2`, `#Level3`, etc., or `#Cantrip` for cantrips.
    - *Mechanics:* Use this section to detail DC checks, Advantage modifiers, or specific rule nuances not covered in the flavor text.
    - *Related Entries:* Must always include a direct link to the corresponding lore entry in `Menus/Journal/Spells/`.
- **Questing Template:**
    - *Sections:* `# Meta`, `# Text`, `# Completing`, `# Reward`, `# Related Entries`, `# Notes`.
    - *Text:* Verbatim in-game text log boxes (blockquote each update).
    - *Completing:* Call out branching choices/paths here.
- **Event Template:**
    - *Sections:* `# Location`, `# Guide`, `# Rewards`, `# Notes`.
- **Stubs:** Create stubs for mentioned entities using the most likely template (Character if likely interactable, Journal if ambiguous).

## 4. Repository & Commit Standards
*Standards for Git and version control.*

- **Commit Logic:**
    - **One Push, One Commit (Squash):** DO NOT make multiple commits during a session. All changes in a single session or task MUST be accumulated and committed as a single, squashed commit at the end. Use `git commit --amend` for incremental updates.
- **Commit Message Style:**
    - **Header:** Start with a high-level summary (e.g., `Comprehensive [Area] Audit & Standardization`). Do not use unnecessary prefixes like "Audit:".
    - **Body:** Use a bulleted list for major sub-tasks. Focus on the "Why", "Area", and specific counts/folders affected.
- **Temporary Files:** All scripts or temp files created by GEMINI must go into the `.gemini/` directory (ignored in `.gitignore`).

## 5. Voice & Continuity
- **Migration Policy (Merge, don't Delete):** Retain all legacy text and notes when moving an older file to a new template. Reorganize them into the correct sections rather than overwriting.
- **Voice:** Maintain a balance between objective data and the game's cynical, noir-esque, and often absurdist "Disco-lite" tone. Embellishments are allowed in "Notes" or "Game World" descriptions, but "Text" sections in `Menus/` must remain verbatim.
- **Session Summaries:** When asked to summarize progress or at the end of a session, ALWAYS read the **Context Bridge Template** in `.gemini/` first to ensure strict adherence. Use this template for all summaries saved in `.gemini/`. These are for AI continuity only and MUST NOT be added to Git or shared.
