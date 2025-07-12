# Agent Instructions

To modify this repository's Scratch project:
1. Unzip `Project.sb3` into a temporary directory using `unzip`. The contents include `project.json` and media files.
2. Use a tool such as `jq` or `python -m json.tool` to pretty-print `project.json` so the JSON is spread across multiple lines (not a single line).
3. Make any code fixes or additions to `project.json` as required by the task.
4. Rezip the modified files back into `Project.sb3` preserving the original filenames.
5. Summarize each change in the `changes` file with a short explanation of what was changed and why.
