```markdown
# Easydict Development Patterns

> Auto-generated skill from repository analysis

## Overview
This skill introduces the core development patterns, coding conventions, and workflows used in the Easydict Swift codebase. Easydict is a Swift-based project (no external framework detected) that emphasizes clear code organization, conventional commit messages, and structured workflows for dependency management, asset handling, feature development, refactoring, and event monitoring. This guide will help you quickly align with the team's practices, from file naming to workflow automation.

## Coding Conventions

### File Naming
- **PascalCase** is used for all file names.
  - Example: `EZEventMonitor.h`, `EZMiniWindowController.m`

### Import Style
- **Relative imports** are preferred.
  - Example (Objective-C/Swift):
    ```swift
    import "../Controller/EZMiniWindowController"
    ```

### Export Style
- **Named exports** are used.
  - Example (Objective-C):
    ```objc
    @interface EZEventMonitor : NSObject
    // ...
    @end
    ```

### Commit Messages
- **Conventional commit prefixes**: `perf`, `chore`, `fix`, `feat`, `refactor`, `style`
- **Average length**: ~42 characters
  - Example: `feat: add support for new translation API`

---

## Workflows

### Update Pod Dependencies
**Trigger:** When you need to update or fix CocoaPods dependencies.  
**Command:** `/update-pods`

1. Edit the `Podfile` as needed.
2. Run `pod install` or `pod update` to update:
    - `Podfile.lock`
    - `Pods/Manifest.lock`
    - `Pods/Pods.xcodeproj/project.pbxproj`
3. Commit all changed Pod-related files.

**Example:**
```sh
# After editing Podfile
pod install
git add Podfile Podfile.lock Pods/Manifest.lock Pods/Pods.xcodeproj/project.pbxproj
git commit -m "chore: update pod dependencies"
```

---

### Add or Update App Icons/Assets
**Trigger:** When adding new icons or updating existing app icon/image assets.  
**Command:** `/update-assets`

1. Add or update images in `OpenBob/Assets.xcassets/[icon-set]`.
2. Update the `Contents.json` in the relevant imageset.
3. Update `OpenBob.xcodeproj/project.pbxproj` to register new assets.

**Example:**
```sh
# Add new icon to Assets.xcassets
# Update Contents.json as needed
git add OpenBob/Assets.xcassets/*/Contents.json OpenBob/Assets.xcassets/*/*.png OpenBob.xcodeproj/project.pbxproj
git commit -m "feat: update app icons"
```

---

### Feature Development: Controller and View
**Trigger:** When implementing a new feature or UI component.  
**Command:** `/new-feature`

1. Create or update controller files in `OpenBob/Feature/TranslateWindow/Easydict/Controller/`.
2. Create or update view files in `OpenBob/Feature/TranslateWindow/Easydict/View/`.
3. Optionally update `OpenBob.xcodeproj/project.pbxproj` to register new files.

**Example:**
```objc
// OpenBob/Feature/TranslateWindow/Easydict/Controller/EZNewFeatureController.h
@interface EZNewFeatureController : NSObject
@end
```
```sh
git add OpenBob/Feature/TranslateWindow/Easydict/Controller/EZNewFeatureController.h OpenBob/Feature/TranslateWindow/Easydict/View/EZNewFeatureView.m OpenBob.xcodeproj/project.pbxproj
git commit -m "feat: add new translation feature"
```

---

### Refactor or Rename Classes
**Trigger:** When renaming or reorganizing classes and their files.  
**Command:** `/refactor-class`

1. Rename or move class files (`.h`/`.m`) in relevant directories.
2. Update references in other source files.
3. Update `OpenBob.xcodeproj/project.pbxproj` to reflect changes.

**Example:**
```sh
mv EZOldController.h EZNewController.h
# Update all references in codebase
git add OpenBob/Feature/TranslateWindow/Easydict/Controller/EZNewController.h OpenBob.xcodeproj/project.pbxproj
git commit -m "refactor: rename EZOldController to EZNewController"
```

---

### Improve Event Monitor or Selection
**Trigger:** When tweaking or fixing text selection or event monitoring logic.  
**Command:** `/improve-event-monitor`

1. Edit `OpenBob/Feature/EventMonitor/EZEventMonitor.h` and/or `.m`.
2. Edit related controller files (e.g., `EZMiniWindowController.m`).
3. Test and commit changes.

**Example:**
```objc
// OpenBob/Feature/EventMonitor/EZEventMonitor.m
- (void)monitorSelection {
    // Improved selection logic here
}
```
```sh
git add OpenBob/Feature/EventMonitor/EZEventMonitor.m OpenBob/Feature/TranslateWindow/Easydict/Controller/EZMiniWindowController.m
git commit -m "fix: improve event monitoring logic"
```

---

## Testing Patterns

- **Test file naming:** Files follow the pattern `*.test.*` (e.g., `EZEventMonitor.test.swift`).
- **Testing framework:** Not explicitly detected; follow Swift or Objective-C testing best practices.
- **Typical test example:**
    ```swift
    import XCTest
    class EZEventMonitorTests: XCTestCase {
        func testSelection() {
            // Test logic here
        }
    }
    ```

---

## Commands

| Command              | Purpose                                                   |
|----------------------|-----------------------------------------------------------|
| /update-pods         | Update CocoaPods dependencies and related project files    |
| /update-assets       | Add or update app icons or image assets                   |
| /new-feature         | Start a new feature or UI component (controller/view)     |
| /refactor-class      | Refactor or rename classes and update references          |
| /improve-event-monitor | Improve event monitoring or selection logic             |
```
