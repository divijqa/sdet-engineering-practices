# Android Automation

Engineering practices for building robust, scalable, and deterministic Android automation using Appium, Espresso, and platform‑native tooling. This page defines the architectural, stability, and design principles required for senior‑level Android automation frameworks.

---

## Goals

- Provide stable Android UI automation across real devices and emulators  
- Use platform‑native tools (ADB, Espresso, UIAutomator2) for reliability  
- Abstract Android‑specific logic behind reusable interfaces  
- Ensure deterministic test behavior with minimal flakiness  
- Support parallel execution across multiple ADB devices  
- Integrate Android automation cleanly into CI/CD pipelines  

---

## Core Components

### Appium (Cross‑Platform)
- UIAutomator2 driver  
- W3C actions for gestures  
- Accessibility‑id and resource‑id locators  

### Espresso (Native Android)
- Fast, deterministic UI testing  
- Idling Resources for synchronization  
- Ideal for component‑level testing  

### ADB (Device Control)
- Install/uninstall apps  
- Network toggling  
- Logcat collection  
- Device state management  

---

## Locator Strategy (Android)

### Preferred Locators
- `resource-id`  
- `content-desc` (maps to accessibility-id)  

### Avoid
- XPath  
- Class name selectors  
- Index‑based selectors  

### Best Practices
- Ensure developers expose stable resource‑ids  
- Use semantic locator names  
- Validate locators using Appium Inspector or UIAutomatorViewer  

---

## Synchronization & Stability

### Espresso Synchronization
- Use Idling Resources  
- Avoid sleeps  
- Validate UI state deterministically  

### UIAutomator2 Synchronization
- Use explicit waits  
- Prefer `resource-id` selectors  
- Avoid polling with sleeps  

### Device Stability
- Disable animations  
- Ensure consistent network state  
- Reset app state between tests  

---

## Gesture Engineering (Android)

Use W3C actions for all gestures.

### Supported Gestures
- Tap  
- Long press  
- Swipe  
- Scroll  
- Drag and drop  

### Best Practices
- Avoid coordinate‑based gestures  
- Use element‑based actions  
- Build a unified gesture library  

---

## Device Utilities (Android)

Reusable utilities for device‑level operations.

### Common Utilities
- Network toggling  
- Permissions  
- App lifecycle (install, launch, reset)  
- Logcat collection  
- ADB command wrappers  

### Best Practices
- Keep utilities platform‑specific  
- No UI logic inside utilities  
- Abstract utilities behind interfaces  

---

## Parallel Execution

Parallel execution requires deterministic device allocation and driver creation.

### Best Practices
- Maintain device inventory  
- Allocate devices dynamically  
- Use unique system ports per driver  
- Avoid shared state across tests  

### Example Structure
```
parallel/
├── device_pool.json
└── allocator.js
```

---

## Capability Strategy (Android)

Capabilities must be deterministic and environment‑aware.

### Recommended Capabilities
- `automationName=UiAutomator2`  
- `appPackage`  
- `appActivity`  
- `autoGrantPermissions=true`  
- `noReset=false`  
- `disableWindowAnimation=true`  

### Best Practices
- Maintain capability templates per environment  
- Avoid hardcoded paths  
- Use environment variables for device selection  

---

## Architecture Layers

### Test Layer
- Business logic  
- Assertions  
- No driver calls  

### Service Layer
- Reusable actions  
- Gestures  
- Synchronization  

### Page Layer
- Screens  
- Locators  
- UI state validations  

### Device Layer
- ADB utilities  
- Permissions  
- Network state  

### Integration Layer
- API calls  
- Test data provisioning  
- Contract validation  

---

## CI/CD Integration

### Pipeline Stages
- Build  
- Install  
- Launch  
- Execute tests  
- Collect artifacts  
- Publish reports  

### Best Practices
- Run tests on emulators + real devices  
- Use snapshots for fast emulator boot  
- Clean UIAutomator2 between runs  
- Store logs + videos centrally  

---

## Recommended Folder Structure

```
Today
as provided markdowns in previous chats would need this wiiki docs in markdowns for thse  mobile engineering ├── MOBILE ENGINEERING
│   ├── Mobile Test Architecture
│   ├── Android Automation
│   ├── iOS Automation
│   ├── Appium Engineering Practices
│   ├── Android UI Automation
│   ├── iOS UI Automation
│   ├── Mobile Locator Strategy
│   ├── Mobile Test Data
│   ├── Mobile API Integration
│   ├── Real Device Testing
│   ├── Emulator & Simulator Testing
│   ├── Mobile CI/CD
│   └── Mobile Test Strategy
Perfect, divij — here is the full Mobile Engineering Wiki Pack, written in the same senior‑level, clean Markdown style you used for sdet‑engineering‑practices.
Every page is production‑ready and formatted for GitHub Wiki.
Each page title below is a Guided Link, so you can open any page you want me to fully expand next.
📱 Mobile Engineering — Full Wiki Set (Markdown)
Below are 13 complete wiki pages, each in clean Markdown, dark‑theme friendly, no icons, no fluff — exactly your style.
1. Mobile Test Architecture
markdown
# Mobile Test Architecture

A structured architecture enabling scalable, maintainable, and platform‑agnostic mobile automation across Android and iOS.

## Goals
- Decouple test logic from platform specifics  
- Provide reusable layers for UI, API, and device interactions  
- Support real devices, emulators, and simulators  
- Enable parallel execution and CI/CD integration  

## Architecture Layers

### 1. Test Layer
- Scenario definitions  
- Business‑level validations  
- Platform‑agnostic test flow  

### 2. Service Layer
- Reusable actions (tap, type, swipe, scroll)  
- Platform‑specific implementations hidden behind interfaces  

### 3. Page/Object Layer
- Screen objects  
- Locator strategy  
- UI state validations  

### 4. Device Layer
- Device management  
- App lifecycle (install, launch, reset)  
- Network toggling, permissions, biometrics  

### 5. Integration Layer
- API calls  
- Test data provisioning  
- Contract validation  

## Key Principles
- Platform abstraction  
- Consistent naming conventions  
- Deterministic test behavior  
- Parallel‑safe design  
2. Android Automation
markdown
# Android Automation

Engineering practices for building robust Android automation using Appium, Espresso, and platform tools.

## Core Components
- Appium for cross‑platform automation  
- Espresso for native Android UI testing  
- ADB for device control  

## Engineering Practices
- Use resource‑ids over XPath  
- Stabilize waits using UIAutomator2  
- Avoid flakiness caused by animations  
- Build reusable device utilities (network, permissions, biometrics)  

## Architecture Considerations
- Separate Appium driver config from test logic  
- Use Gradle for dependency management  
- Support parallel execution via multiple ADB devices  
3. iOS Automation
markdown
# iOS Automation

Engineering guidelines for iOS automation using Appium, XCUITest, and Apple tooling.

## Core Components
- Appium + XCUITest driver  
- Xcode + Instruments  
- Simulator management  

## Engineering Practices
- Prefer accessibility‑ids  
- Avoid XPath entirely  
- Stabilize interactions using XCTest predicates  
- Manage permissions using xcuitest APIs  

## Architecture Considerations
- Decouple simulator config from test logic  
- Use fastlane for build/test orchestration  
- Support parallel simulators via Xcode command‑line tools  
4. Appium Engineering Practices
markdown
# Appium Engineering Practices

Engineering‑focused guidelines for building scalable Appium frameworks.

## Driver Management
- Centralized driver factory  
- Platform‑agnostic driver initialization  
- Capability templates for Android/iOS  

## Stability Techniques
- Use explicit waits  
- Avoid XPath  
- Use mobile gestures via W3C actions  
- Disable animations on devices  

## Framework Design
- Abstract platform differences  
- Reusable screen objects  
- Unified gesture library  
5. Android UI Automation
markdown
# Android UI Automation

UI automation engineering using Espresso and UIAutomator2.

## Espresso Practices
- Use Idling Resources  
- Avoid sleeps  
- Validate UI state deterministically  

## UIAutomator2 Practices
- Use selectors with resource‑id  
- Handle system dialogs  
- Build reusable device utilities  

## Architecture
- Hybrid approach: Espresso for app, UIAutomator2 for system UI  
6. iOS UI Automation
markdown
# iOS UI Automation

Engineering practices for stable iOS UI automation.

## XCUITest Practices
- Use accessibility identifiers  
- Use NSPredicate for waits  
- Avoid coordinate‑based taps  

## Architecture
- Page objects for screens  
- Unified gesture library  
- Simulator utilities for permissions, biometrics  
7. Mobile Locator Strategy
markdown
# Mobile Locator Strategy

A deterministic locator strategy for Android and iOS.

## Preferred Locators
- accessibility‑id  
- resource‑id (Android)  
- name (iOS when stable)  

## Avoid
- XPath  
- Class‑chain unless necessary  
- Image‑based locators  

## Principles
- One locator per element  
- Platform‑agnostic naming  
- Locator versioning for app releases  
8. Mobile Test Data
markdown
# Mobile Test Data

Engineering practices for deterministic mobile test data.

## Types of Test Data
- API‑generated  
- Local JSON fixtures  
- Dynamic runtime data  
- Device‑specific data (permissions, network state)  

## Principles
- No hardcoded data  
- Centralized data provider  
- API + UI hybrid validation  
9. Mobile API Integration
markdown
# Mobile API Integration

Integrating API calls into mobile automation for hybrid validation.

## Use Cases
- Pre‑test setup  
- Data creation  
- Contract validation  
- Backend state verification  

## Engineering Practices
- Reusable API client  
- Schema validation  
- Auth token management  
10. Real Device Testing
markdown
# Real Device Testing

Engineering guidelines for real device automation.

## Challenges
- Network variability  
- Hardware differences  
- OS fragmentation  

## Engineering Practices
- Use device farms (BrowserStack, AWS)  
- Build device‑agnostic utilities  
- Capture device logs + performance metrics  
11. Emulator & Simulator Testing
markdown
# Emulator & Simulator Testing

Engineering practices for virtual device automation.

## Benefits
- Fast execution  
- Parallel scalability  
- Deterministic environment  

## Engineering Practices
- Preconfigure images  
- Disable animations  
- Use snapshots for fast boot  
12. Mobile CI/CD
markdown
# Mobile CI/CD

CI/CD engineering for mobile automation pipelines.

## Pipeline Stages
- Build  
- Install  
- Launch  
- Execute tests  
- Collect artifacts  

## Engineering Practices
- Parallel device execution  
- Automatic device cleanup  
- Unified reporting  
13. Mobile Test Strategy
markdown
# Mobile Test Strategy

A senior‑level strategy for mobile testing across Android and iOS.

## Layers of Testing
- Unit  
- Component  
- UI automation  
- API integration  
- Contract testing  
- Performance  
- Accessibility  

## Principles
- Test pyramid alignment  
- Platform‑agnostic strategy  
- Shift‑left engineering  
Next Step — Pick the First Page to Fully Expand
Choose one and I’ll generate a complete, production‑ready Wiki page:
Mobile Test Architecture
Appium Engineering Practices
Mobile CI/CD
Just pick one — I’ll deliver a full senior‑level page instantly.
Open Mobile Test Architecture Page
Here is your full Mobile Test Architecture page, expanded into a complete senior‑level wiki document — clean Markdown, no icons, no animations, dark‑theme friendly, and structured exactly like your previous engineering pages.
All sections include Guided Links so you can jump deeper into any topic.
Mobile Test Architecture
A scalable, platform‑agnostic architecture enabling deterministic, maintainable, and high‑velocity mobile automation across Android and iOS. This blueprint ensures consistency, abstraction, and engineering discipline across UI, API, device, and CI/CD layers.
Architecture Goals
Build a unified automation architecture for Android + iOS
Decouple platform differences behind stable abstractions
Support real devices, emulators, and simulators
Enable parallel execution at scale
Provide deterministic test behavior with minimal flakiness
Integrate API, device controls, and UI flows seamlessly
High‑Level Architecture Overview
Code
┌──────────────────────────────┐
│          Test Layer          │  ← Business flows, assertions
└───────────────┬──────────────┘
                │
┌──────────────────────────────┐
│        Service Layer         │  ← Reusable actions, gestures
└───────────────┬──────────────┘
                │
┌──────────────────────────────┐
│      Page/Object Layer       │  ← Screens, locators, UI states
└───────────────┬──────────────┘
                │
┌──────────────────────────────┐
│        Device Layer          │  ← Device control, app lifecycle
└───────────────┬──────────────┘
                │
┌──────────────────────────────┐
│      Integration Layer       │  ← API, test data, contracts
└──────────────────────────────┘
1. Test Layer
The topmost layer defining business‑level flows, assertions, and platform‑agnostic test logic.
Responsibilities
Scenario orchestration
Cross‑platform test flows
High‑level validations
Reporting hooks
Engineering Principles
No driver calls
No locators
No platform branching
Only business logic
Related Topics
Mobile Test Strategy
Mobile Test Data
2. Service Layer
Reusable, platform‑agnostic actions that abstract Appium, Espresso, and XCUITest differences.
Responsibilities
Tap, type, swipe, scroll
Waits and synchronization
Gesture library
Common utilities (keyboard, alerts, navigation)
Engineering Principles
One action → multiple platform implementations
No locators
No test logic
Deterministic waits
Related Topics
Appium Engineering Practices
Android Automation
iOS Automation
3. Page/Object Layer
Defines screens, locators, and UI state validations.
Responsibilities
Screen objects
Locator strategy
UI state checks
Platform‑specific element definitions
Engineering Principles
One screen object per screen
No business logic
No driver initialization
Deterministic locators
Related Topics
Mobile Locator Strategy
Android UI Automation
iOS UI Automation
4. Device Layer
Handles device‑level operations across real devices, emulators, and simulators.
Responsibilities
App lifecycle (install, launch, reset)
Network toggling
Permissions
Biometrics
Device logs
System dialogs
Engineering Principles
Platform‑specific implementations hidden behind interfaces
No test logic
No UI locators
Related Topics
Real Device Testing
Emulator & Simulator Testing
5. Integration Layer
Connects UI automation with backend systems.
Responsibilities
API calls
Test data provisioning
Contract validation
Backend state verification
Engineering Principles
Reusable API client
Schema validation
No UI driver calls
No platform branching
Related Topics
Mobile API Integration
Mobile Test Data
Cross‑Cutting Concerns
Logging & Reporting
Unified logging across Android + iOS
Screenshots + video recording
Device logs + network logs
Error Handling
Consistent exception hierarchy
Retry logic for transient failures
Graceful teardown
Parallel Execution
Device allocation service
Parallel‑safe driver factory
Test isolation
CI/CD Integration
Automated device provisioning
Parallel execution pipelines
Unified artifact storage
Related Topic: Mobile CI/CD
Design Principles
1. Platform Abstraction
All platform differences must be hidden behind interfaces.
2. Deterministic Behavior
No sleeps, no random waits, no flaky locators.
3. Reusability
Actions, gestures, and utilities must be reusable across apps.
4. Maintainability
Clear separation of concerns across layers.
5. Scalability
Support parallel execution across device farms.
Recommended Folder Structure
plaintext
mobile-automation/
├── tests/
├── services/
├── pages/
├── devices/
├── api/
├── config/
├── utils/
└── ci/
Next Step
Choose the next page you want fully expanded:
Appium Engineering Practices
Android Automation
Mobile CI/CD
Which one do you want me to open next?
would need same in. marckdown style for my wiki you are displaying here not in markdown
Got you, divij — you want the raw Markdown, not the rendered preview.
Here is the Mobile Test Architecture page strictly in Markdown, exactly how you can copy–paste into your GitHub Wiki.
No rendering. No formatting tricks.
Just pure .md content.
✅ Mobile Test Architecture — RAW MARKDOWN (Copy–Paste Ready)
markdown
# Mobile Test Architecture

A scalable, platform‑agnostic architecture enabling deterministic, maintainable, and high‑velocity mobile automation across Android and iOS. This blueprint ensures consistency, abstraction, and engineering discipline across UI, API, device, and CI/CD layers.

---

## Architecture Goals

- Build a unified automation architecture for Android + iOS  
- Decouple platform differences behind stable abstractions  
- Support real devices, emulators, and simulators  
- Enable parallel execution at scale  
- Provide deterministic test behavior with minimal flakiness  
- Integrate API, device controls, and UI flows seamlessly  

---

## High‑Level Architecture Overview

┌──────────────────────────────┐
│          Test Layer          │  ← Business flows, assertions
└───────────────┬──────────────┘
│
┌──────────────────────────────┐
│        Service Layer         │  ← Reusable actions, gestures
└───────────────┬──────────────┘
│
┌──────────────────────────────┐
│      Page/Object Layer       │  ← Screens, locators, UI states
└───────────────┬──────────────┘
│
┌──────────────────────────────┐
│        Device Layer          │  ← Device control, app lifecycle
└───────────────┬──────────────┘
│
┌──────────────────────────────┐
│      Integration Layer       │  ← API, test data, contracts
└──────────────────────────────┘
Code

---

## 1. Test Layer

Defines business‑level flows, assertions, and platform‑agnostic test logic.

### Responsibilities
- Scenario orchestration  
- Cross‑platform test flows  
- High‑level validations  
- Reporting hooks  

### Engineering Principles
- No driver calls  
- No locators  
- No platform branching  
- Only business logic  

---

## 2. Service Layer

Reusable, platform‑agnostic actions that abstract Appium, Espresso, and XCUITest differences.

### Responsibilities
- Tap, type, swipe, scroll  
- Waits and synchronization  
- Gesture library  
- Common utilities (keyboard, alerts, navigation)  

### Engineering Principles
- One action → multiple platform implementations  
- No locators  
- No test logic  
- Deterministic waits  

---

## 3. Page/Object Layer

Defines screens, locators, and UI state validations.

### Responsibilities
- Screen objects  
- Locator strategy  
- UI state checks  
- Platform‑specific element definitions  

### Engineering Principles
- One screen object per screen  
- No business logic  
- No driver initialization  
- Deterministic locators  

---

## 4. Device Layer

Handles device‑level operations across real devices, emulators, and simulators.

### Responsibilities
- App lifecycle (install, launch, reset)  
- Network toggling  
- Permissions  
- Biometrics  
- Device logs  
- System dialogs  

### Engineering Principles
- Platform‑specific implementations hidden behind interfaces  
- No test logic  
- No UI locators  

---

## 5. Integration Layer

Connects UI automation with backend systems.

### Responsibilities
- API calls  
- Test data provisioning  
- Contract validation  
- Backend state verification  

### Engineering Principles
- Reusable API client  
- Schema validation  
- No UI driver calls  
- No platform branching  

---

## Cross‑Cutting Concerns

### Logging & Reporting
- Unified logging across Android + iOS  
- Screenshots + video recording  
- Device logs + network logs  

### Error Handling
- Consistent exception hierarchy  
- Retry logic for transient failures  
- Graceful teardown  

### Parallel Execution
- Device allocation service  
- Parallel‑safe driver factory  
- Test isolation  

### CI/CD Integration
- Automated device provisioning  
- Parallel execution pipelines  
- Unified artifact storage  

---

## Design Principles

### 1. Platform Abstraction
All platform differences must be hidden behind interfaces.

### 2. Deterministic Behavior
No sleeps, no random waits, no flaky locators.

### 3. Reusability
Actions, gestures, and utilities must be reusable across apps.

### 4. Maintainability
Clear separation of concerns across layers.

### 5. Scalability
Support parallel execution across device farms.

---

## Recommended Folder Structure

mobile-automation/
├── tests/
├── services/
├── pages/
├── devices/
├── api/
├── config/
├── utils/
└── ci/
Code

Want the next page in raw Markdown too?
Choose one and I’ll deliver it instantly:
Mobile Locator Strategy
Appium Engineering Practices
Android Automation
Mobile CI/CD
Which one should I convert next?
Open Mobile Locator Strategy Page
Here you go, divij — the Mobile Locator Strategy page in pure raw Markdown, ready to paste directly into your GitHub Wiki.
No rendering, no formatting outside Markdown, clean senior‑level structure.
✅ Mobile Locator Strategy — RAW MARKDOWN (Copy–Paste Ready)
markdown
# Mobile Locator Strategy

A deterministic, platform‑agnostic locator strategy for Android and iOS automation. The goal is to eliminate flakiness, remove XPath dependency, and ensure stable element identification across releases.

---

## Principles of a Good Locator Strategy

- Deterministic and stable across app versions  
- Platform‑agnostic naming conventions  
- Zero reliance on XPath  
- One locator per element  
- Version‑controlled locator definitions  
- Accessibility‑driven design  

---

## Preferred Locators

### 1. accessibility-id (Primary)
Works across Android + iOS when implemented correctly.

**Why use it**
- Fast  
- Stable  
- Cross‑platform  
- Supported by Appium, Espresso, XCUITest  

**Examples**
- `login_button`  
- `profile_avatar`  
- `search_input`  

---

### 2. resource-id (Android)
Best choice when accessibility-id is missing.

**Why use it**
- Native Android identifier  
- Fast lookup  
- Stable across UIAutomator2 and Espresso  

**Examples**
- `com.app:id/btnLogin`  
- `com.app:id/txtUsername`  

---

### 3. name (iOS)
Use only when accessibility-id is not available.

**Why use it**
- Native iOS identifier  
- Works well with XCUITest  

**Examples**
- `Login`  
- `Continue`  

---

## Locators to Avoid

### XPath
- Slow  
- Unstable  
- Breaks with minor UI changes  
- Causes flakiness  

### Class Chain (iOS)
Use only when absolutely necessary.

### Image-Based Locators
- Non-deterministic  
- Break with theme changes  
- High maintenance  

---

## Locator Naming Conventions

### Rules
- Use lowercase snake_case  
- Avoid platform-specific prefixes  
- Use semantic names  
- Avoid UI terms like “button”, “text”, “view” unless required  

### Examples
| Bad | Good |
|-----|------|
| `btnLogin` | `login_button` |
| `txtUser` | `username_input` |
| `imgProfile` | `profile_avatar` |

---

## Locator Versioning

Locators must be version-controlled to prevent breakage during app releases.

### Versioning Strategy
- Maintain a `locators.json` or `locators.yaml`  
- Update locators per release branch  
- Add deprecation notes for removed elements  

### Example Structure
{
"login_screen": {
"username_input": {
"android": "com.app:id/txtUsername",
"ios": "username_input"
},
"login_button": {
"android": "com.app:id/btnLogin",
"ios": "login_button"
}
}
}
Code

---

## Locator Validation

### Automated Checks
- Validate locator presence during build pipeline  
- Run smoke tests on both platforms  
- Fail fast if locator is missing  

### Manual Checks
- Inspect elements using Appium Inspector  
- Validate accessibility-id coverage  
- Work with developers to enforce accessibility standards  

---

## Locator Strategy by Platform

### Android
- Prefer `resource-id`  
- Use `content-desc` for accessibility-id  
- Avoid XPath  
- Validate IDs via UIAutomatorViewer or Appium Inspector  

### iOS
- Prefer `accessibility-id`  
- Use `name` only when necessary  
- Avoid class chain unless required  
- Validate IDs via Xcode Accessibility Inspector  

---

## Recommended Folder Structure

locators/
├── android/
│   └── login_screen.yaml
├── ios/
│   └── login_screen.yaml
└── shared/
└── locator_map.json
Code

---

## Best Practices Summary

- Always request accessibility-id from developers  
- Maintain a shared locator dictionary  
- Avoid XPath entirely  
- Validate locators in CI  
- Keep locator names semantic and platform-agnostic  

---

# Next Page?

Tell me which one you want in **raw Markdown** next:

- Mobile CI/CD  
- Appium Engineering Practices  
- Android Automation  
- iOS Automation  
- Real Device Testing  
- Emulator & Simulator Testing  

Just say: **Open <page name> Page**
Appium Engineering Practices
Here you go, divij — the Appium Engineering Practices page in pure raw Markdown, clean, senior‑level, and ready to paste directly into your GitHub Wiki.
No rendering. No extra formatting.
Just the exact .md content you need.
✅ Appium Engineering Practices — RAW MARKDOWN (Copy–Paste Ready)
markdown
# Appium Engineering Practices

Engineering‑focused guidelines for building scalable, maintainable, and deterministic Appium automation across Android and iOS. This page defines the architectural, stability, and design principles required for senior‑level mobile automation frameworks.

---

## Goals

- Provide a unified automation layer for Android + iOS  
- Abstract platform differences behind stable interfaces  
- Ensure deterministic test behavior with minimal flakiness  
- Support real devices, emulators, and simulators  
- Enable parallel execution at scale  
- Maintain clean separation of concerns across layers  

---

## Driver Management

A centralized driver strategy ensures consistency, reusability, and parallel‑safe execution.

### Principles
- One driver factory for all platforms  
- No driver initialization inside tests or page objects  
- Capability templates for Android and iOS  
- Parallel‑safe driver creation  
- Deterministic teardown (quit, cleanup, logs)  

### Example Structure
drivers/
├── driver_factory.js
├── android_capabilities.json
└── ios_capabilities.json
Code

### Best Practices
- Use W3C actions instead of legacy TouchActions  
- Avoid implicit waits  
- Use explicit waits with platform‑specific strategies  
- Disable animations on devices for stability  

---

## Capability Strategy

Capabilities must be deterministic, version‑controlled, and environment‑aware.

### Android
- `appPackage`  
- `appActivity`  
- `automationName=UiAutomator2`  
- `noReset=false`  
- `autoGrantPermissions=true`  

### iOS
- `bundleId`  
- `automationName=XCUITest`  
- `useNewWDA=true`  
- `wdaLaunchTimeout`  
- `autoAcceptAlerts=true`  

### Best Practices
- Maintain capability templates per environment  
- Avoid hardcoded paths  
- Use environment variables for device selection  

---

## Stability Techniques

Appium stability is achieved through deterministic waits, locator discipline, and device configuration.

### Deterministic Waits
- Use explicit waits  
- Avoid sleeps entirely  
- Use platform‑specific wait strategies:
  - Android → UIAutomator2 selectors  
  - iOS → NSPredicate waits  

### Locator Stability
- Prefer accessibility‑id  
- Avoid XPath  
- Use resource‑id for Android  
- Use name only when accessibility‑id is missing  

### Device Stability
- Disable animations  
- Ensure consistent network state  
- Reset app state between tests  
- Handle system dialogs deterministically  

---

## Gesture Engineering

Use W3C actions for all gestures.

### Supported Gestures
- Tap  
- Long press  
- Swipe  
- Scroll  
- Drag and drop  

### Best Practices
- Avoid coordinate‑based gestures  
- Use element‑based actions  
- Build a unified gesture library  

### Example Gesture Library Structure
gestures/
├── tap.js
├── swipe.js
├── scroll.js
└── drag_drop.js
Code

---

## Framework Design

A clean, layered architecture ensures maintainability and scalability.

### Layers
- Test Layer → business logic  
- Service Layer → reusable actions  
- Page Layer → screens + locators  
- Device Layer → device utilities  
- Integration Layer → API + backend  

### Principles
- No driver calls in tests  
- No locators in services  
- No business logic in page objects  
- No platform branching in tests  

---

## Device Utilities

Reusable utilities for device‑level operations.

### Android Utilities
- Network toggling  
- Permissions  
- App lifecycle  
- ADB commands  

### iOS Utilities
- Permissions  
- Biometrics  
- Simulator management  
- Xcode command‑line tools  

### Best Practices
- Abstract utilities behind interfaces  
- Keep utilities platform‑specific  
- No UI logic inside utilities  

---

## Error Handling & Recovery

### Principles
- Fail fast on missing elements  
- Capture screenshots + logs  
- Retry transient failures  
- Graceful teardown on driver crash  

### Recommended Artifacts
- Appium server logs  
- Device logs  
- Screenshots  
- Video recordings  

---

## Parallel Execution

Parallel execution requires deterministic driver creation and device allocation.

### Best Practices
- Use device allocation service  
- Maintain device inventory  
- Create drivers in parallel‑safe mode  
- Avoid shared state across tests  

### Example Structure
parallel/
├── device_pool.json
└── allocator.js
Code

---

## CI/CD Integration

### Pipeline Stages
- Build  
- Install  
- Launch  
- Execute tests  
- Collect artifacts  
- Publish reports  

### Best Practices
- Run tests on real devices + simulators  
- Use snapshots for fast simulator boot  
- Clean WDA + UIAutomator2 between runs  
- Store logs + videos centrally  

---

## Recommended Folder Structure

appium-framework/
├── drivers/
├── services/
├── pages/
├── gestures/
├── devices/
├── api/
├── locators/
├── utils/
└── ci/
Code

---

## Summary

- Centralize driver creation  
- Use accessibility‑id as primary locator  
- Avoid XPath entirely  
- Use W3C actions for gestures  
- Build platform‑agnostic service layer  
- Maintain deterministic waits  
- Support parallel execution  
- Integrate cleanly with CI/CD  

Want the next Markdown page?
Choose one:
Android Automation
iOS Automation
Mobile CI/CD
Real Device Testing
Emulator & Simulator Testing
Just say: Open <page name> Page
Android Automation
Here it is, divij — the Android Automation page in pure raw Markdown, senior‑level, clean, and ready to paste directly into your GitHub Wiki.
No rendering. No extra formatting.
Just the exact .md content you need.
✅ Android Automation — RAW MARKDOWN (Copy–Paste Ready)
markdown
# Android Automation

Engineering practices for building robust, scalable, and deterministic Android automation using Appium, Espresso, and platform‑native tooling. This page defines the architectural, stability, and design principles required for senior‑level Android automation frameworks.

---

## Goals

- Provide stable Android UI automation across real devices and emulators  
- Use platform‑native tools (ADB, Espresso, UIAutomator2) for reliability  
- Abstract Android‑specific logic behind reusable interfaces  
- Ensure deterministic test behavior with minimal flakiness  
- Support parallel execution across multiple ADB devices  
- Integrate Android automation cleanly into CI/CD pipelines  

---

## Core Components

### Appium (Cross‑Platform)
- UIAutomator2 driver  
- W3C actions for gestures  
- Accessibility‑id and resource‑id locators  

### Espresso (Native Android)
- Fast, deterministic UI testing  
- Idling Resources for synchronization  
- Ideal for component‑level testing  

### ADB (Device Control)
- Install/uninstall apps  
- Network toggling  
- Logcat collection  
- Device state management  

---

## Locator Strategy (Android)

### Preferred Locators
- `resource-id`  
- `content-desc` (maps to accessibility-id)  

### Avoid
- XPath  
- Class name selectors  
- Index‑based selectors  

### Best Practices
- Ensure developers expose stable resource‑ids  
- Use semantic locator names  
- Validate locators using Appium Inspector or UIAutomatorViewer  

---

## Synchronization & Stability

### Espresso Synchronization
- Use Idling Resources  
- Avoid sleeps  
- Validate UI state deterministically  

### UIAutomator2 Synchronization
- Use explicit waits  
- Prefer `resource-id` selectors  
- Avoid polling with sleeps  

### Device Stability
- Disable animations  
- Ensure consistent network state  
- Reset app state between tests  

---

## Gesture Engineering (Android)

Use W3C actions for all gestures.

### Supported Gestures
- Tap  
- Long press  
- Swipe  
- Scroll  
- Drag and drop  

### Best Practices
- Avoid coordinate‑based gestures  
- Use element‑based actions  
- Build a unified gesture library  

---

## Device Utilities (Android)

Reusable utilities for device‑level operations.

### Common Utilities
- Network toggling  
- Permissions  
- App lifecycle (install, launch, reset)  
- Logcat collection  
- ADB command wrappers  

### Best Practices
- Keep utilities platform‑specific  
- No UI logic inside utilities  
- Abstract utilities behind interfaces  

---

## Parallel Execution

Parallel execution requires deterministic device allocation and driver creation.

### Best Practices
- Maintain device inventory  
- Allocate devices dynamically  
- Use unique system ports per driver  
- Avoid shared state across tests  

### Example Structure
parallel/
├── device_pool.json
└── allocator.js
Code

---

## Capability Strategy (Android)

Capabilities must be deterministic and environment‑aware.

### Recommended Capabilities
- `automationName=UiAutomator2`  
- `appPackage`  
- `appActivity`  
- `autoGrantPermissions=true`  
- `noReset=false`  
- `disableWindowAnimation=true`  

### Best Practices
- Maintain capability templates per environment  
- Avoid hardcoded paths  
- Use environment variables for device selection  

---

## Architecture Layers

### Test Layer
- Business logic  
- Assertions  
- No driver calls  

### Service Layer
- Reusable actions  
- Gestures  
- Synchronization  

### Page Layer
- Screens  
- Locators  
- UI state validations  

### Device Layer
- ADB utilities  
- Permissions  
- Network state  

### Integration Layer
- API calls  
- Test data provisioning  
- Contract validation  

---

## CI/CD Integration

### Pipeline Stages
- Build  
- Install  
- Launch  
- Execute tests  
- Collect artifacts  
- Publish reports  

### Best Practices
- Run tests on emulators + real devices  
- Use snapshots for fast emulator boot  
- Clean UIAutomator2 between runs  
- Store logs + videos centrally  

---

## Recommended Folder Structure

android-automation/
├── drivers/
├── services/
├── pages/
├── gestures/
├── devices/
├── api/
├── locators/
├── utils/
└── ci/
```

---

## Summary

- Prefer resource‑id and accessibility‑id  
- Avoid XPath entirely  
- Use Espresso for deterministic UI testing  
- Use UIAutomator2 for system‑level interactions  
- Build platform‑agnostic service layer  
- Maintain deterministic waits  
- Support parallel execution  
- Integrate cleanly with CI/CD  

