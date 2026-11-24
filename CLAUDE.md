# CLAUDE.md

## Project
SubTrack is a Turkey-focused subscription and bill tracker for iPhone. It converts USD/EUR
subscriptions to TRY with reference exchange rates and reminds the user before renewals
and free-trial ends.

## Tech rules
- UIKit with programmatic UI. Don't add storyboards or SwiftUI unless Ömer asks.
- Architecture is MVVM-C: view controllers never push or present screens; coordinators do.
- Money is `Decimal`, never `Double`.
- Minimum iOS 17.0, iPhone only, portrait only. Never raise the deployment target;
  use `#available` for newer APIs.
- No third-party dependencies without asking.

## Commands
Single scheme `SubTrack` (targets: `SubTrack`, `SubTrackTests`, `SubTrackUITests`).

```bash
# Build
xcodebuild -project SubTrack.xcodeproj -scheme SubTrack -destination 'platform=iOS Simulator,name=iPhone 16,OS=18.5' build

# All tests
xcodebuild -project SubTrack.xcodeproj -scheme SubTrack -destination 'platform=iOS Simulator,name=iPhone 16,OS=18.5' -parallel-testing-enabled NO test

# Single test (Target/Suite/function() — Swift Testing needs the parentheses)
xcodebuild -project SubTrack.xcodeproj -scheme SubTrack -destination 'platform=iOS Simulator,name=iPhone 16,OS=18.5' -parallel-testing-enabled NO test -only-testing:'SubTrackTests/<Suite>/<test>()'
```

Unit tests use Swift Testing (`import Testing`, `@Test`, `#expect`); UI tests use XCTest.
The project uses file-system synchronized groups: new `.swift` files under `SubTrack/`
join the target automatically — don't edit `project.pbxproj` for that.

## Working rules
- Ömer writes the first instance of each new kind of code (first ViewModel, first
  coordinator, first service…); Claude writes later repeats of it from Ömer's spec.
  This overrides "you write the code" in the global CLAUDE.md.
- Always Ömer's, Claude only reviews and gives hints (not code): business logic
  (money, date math, exchange rates) and the Claude layer (CLAUDE.md, hooks, skills, agents).
- Never commit to `main`; every change goes on a branch and a PR.
  Conventional Commits; commit only with Ömer's approval; Ömer pushes.
