# Copilot instructions for foobar2000-skins-collection

Purpose
- Help an AI coding agent understand the repository quickly and take safe, high-value actions (add/update skin archives, update metadata, and make small docs edits).

Quick repo summary
- This repo is a curated collection of foobar2000 skins. The primary content lives in the `fb2k skins/` directory as archive files (`.rar`, `.zip`, `.7z`).
- There is no build system, tests, or executable code. The README (`README.md`) contains installation notes and a manual list of included skins.

Key locations and patterns
- `fb2k skins/` — primary directory containing skin archives. Example filenames: `DarkOnev4_by_tedgo.rar`, `darkone_v2_1_by_tedgo.7z`, `minty-foobar-main.zip`.
- `README.md` — high-level description and the manual list of skins; when adding/removing a skin, update this file's list if appropriate.
- Archive filename pattern commonly used: `<name>_by_<author>[_vX.Y][_extra].<ext>` or variants with spaces and dashes. Many files embed author and version in the filename.

What the agent can and should do (concrete)
- Add a new skin: place the archive into `fb2k skins/`, verify the filename follows the repository's visible convention (include `by_<author>` when known), and update `README.md` to add a one-line entry to the "Skins Collection" list.
  - Example change: add `fb2k skins/FoobarNew_by_alice_v1.0.zip` and append `* FoobarNew` to the README list.
- Validate metadata by inspecting the archive (do not extract into repo): look for `*.fcl` files, `components/` folder, or fonts (`*.ttf`, `*.otf`) inside the archive and note them in the commit message or README update.
- Small docs fixes: correct typos in `README.md`, improve installation steps, or add a per-skin README when a skin requires special installation steps (create `fb2k skins/<skin-name>/README.md` only if you choose to store an unpacked helper folder — default repo currently stores archives flat).

What the agent must NOT do
- Do not add extracted binaries or unpacked skin folders wholesale into the repo. The repository stores archives; adding large extracted directories would change repository intent and increase size.
- Avoid changing archive contents or editing binary files. Changes to archives should be made upstream and re-uploaded as a new archive file.

Developer workflows (how humans verify)
- No build/test cycle. To test a skin locally: extract the archive and copy the skin folder into the foobar2000 install path (per README):
  - Skins: `C:\Program Files (x86)\foobar2000` (or the foobar installation folder)
  - Components: `%APPDATA%\foobar2000\user-components` or portable profile `path/to/foobar/profile/user-components`
- Recommended local tooling for inspection: 7-Zip (or `unzip`) to preview archive contents without committing extracted files.

Repo-specific conventions and gotchas
- Filenames use mixed separators (`_`, `-`, spaces). When scripting or searching, use case-insensitive patterns: `by_` or `by ` and extensions `\.rar|\.zip|\.7z`.
- Many archives include the author name and version in the filename; preserve that when adding files.
- The README list is manually curated and may not reflect the directory perfectly. If you add/remove items, update both the archive and README to keep them consistent.
- Licensing: README contains a disclaimer that the repository does not own skins. When adding a skin, include the original credit in the commit message and optionally add a short attribution line in the README.

Examples (concrete edits)
- Add archive + README line:
  - Files changed: `fb2k skins/FoobarNew_by_alice_v1.0.zip`, `README.md` (append `* FoobarNew`).
  - Commit message example: `Add skin: FoobarNew by alice (source: <url if available>)`.
- Inspect archive and add note:
  - If archive includes `components/` or `.fcl`, mention it in the README or a short per-skin note: `fb2k skins/FoobarNew_by_alice_v1.0.zip — includes components and FCL; install instructions: ...`.

Search tips for agents
- To find skins or authors, search for `by_`, `by `, or archive extensions. Example regex: `by[_ ]|\.rar$|\.zip$|\.7z$`.
- To find README references, search `Skins Collection` or the skin name.

Completion criteria for edits
- New skin archive added under `fb2k skins/` (binary present in repo) OR README updated to reflect accurate list.
- Commit message includes original author credit and optional source URL when available.

If anything is missing or you want a stricter convention (naming, commit messages, per-skin metadata files), tell me which rules you'd like enforced and I can update this guidance and create a small CONTRIBUTING.md or PR template to automate it.
