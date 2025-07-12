# Agent Instructions

To modify this repository's Scratch project:
1. Unzip `Project.sb3` into a temporary directory using `unzip`. The contents include `project.json` and media files.
2. Use a tool such as `jq` or `python -m json.tool` to pretty-print `project.json` so the JSON spans multiple lines.
3. For quick lookups of variables, lists and custom blocks, consult `PROJECT_OBJECTS.md` and use the example `jq` commands in the "Searching project.json" section. This avoids scanning the entire file.
4. When editing `project.json`, focus solely on the sprite named `renderer`. Keep complex block structures intact and ignore code from other sprites.
5. Make any code fixes or additions to `project.json` as required by the task.
6. Rezip the modified files back into `Project.sb3` preserving the original filenames.
7. Summarize each change in the `changes` file with a short explanation of what was changed and why.
