Mark the specified feature as complete, or the active feature if none is passed.

Usage: /feature-done <id-or-name>
Example: /feature-done 2.1
Example: /feature-done (uses active feature from .claude/active_feature)

Prerequisites — verify before proceeding:
1. All tests pass (run `pytest python/tests/ -v` to confirm)
2. No uncommitted changes to files outside the feature scope
3. User has confirmed tests pass in their real project (ask explicitly)

Steps:
1. Identify the target feature — from argument or from .claude/active_feature
2. Ask: "Have you confirmed tests pass in your real project? (yes/no)"
   Do NOT proceed until the user confirms.
3. Commit all changes with a conventional commit message:
   ```bash
   git add -A
   git commit -m "feat(epic-N): Feature X.Y — [feature name]"
   ```
4. Close the corresponding GitHub issue:
   ```bash
   gh issue close <issue-number> --comment "Feature complete. All tests passing."
   ```
   Find the issue number by matching the feature name:
   ```bash
   gh issue list --state open --json number,title
   ```
5. Clear the active feature:
   ```bash
   rm -f .claude/active_feature
   ```
6. Push to remote:
   ```bash
   git push
   ```
7. Report: "Feature X.Y — [name] is complete and closed. Ready for next feature."
8. Show the next pending feature from CLAUDE.md as a suggestion.
