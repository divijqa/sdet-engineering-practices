# Playwright Engineering Practices

Playwright provides browser automation with strong isolation, auto-waiting, tracing, and multi-browser projects.

## Practices

- Use web-first assertions and locator APIs instead of arbitrary sleeps.
- Prefer role, label, text, and test-id locators that describe user intent.
- Isolate tests with fixtures and controlled test data.
- Capture traces on retry and retain screenshots or video when failure diagnosis benefits.
- Run projects deliberately across supported browsers and device profiles.

Keep tests deterministic by controlling network dependencies, time-sensitive data, and authentication state.
