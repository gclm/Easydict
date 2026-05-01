---
name: update-pod-dependencies
description: Workflow command scaffold for update-pod-dependencies in Easydict.
allowed_tools: ["Bash", "Read", "Write", "Grep", "Glob"]
---

# /update-pod-dependencies

Use this workflow when working on **update-pod-dependencies** in `Easydict`.

## Goal

Updates CocoaPods dependencies and project settings to resolve warnings or add/remove pods.

## Common Files

- `Podfile`
- `Podfile.lock`
- `Pods/Manifest.lock`
- `Pods/Pods.xcodeproj/project.pbxproj`

## Suggested Sequence

1. Understand the current state and failure mode before editing.
2. Make the smallest coherent change that satisfies the workflow goal.
3. Run the most relevant verification for touched files.
4. Summarize what changed and what still needs review.

## Typical Commit Signals

- Edit Podfile as needed
- Run `pod install` or `pod update` to update Podfile.lock, Pods/Manifest.lock, and Pods/Pods.xcodeproj/project.pbxproj
- Commit all changed Pod-related files

## Notes

- Treat this as a scaffold, not a hard-coded script.
- Update the command if the workflow evolves materially.