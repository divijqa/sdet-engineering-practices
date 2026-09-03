# UI CI/CD Integration

UI automation in CI should provide a fast signal on pull requests and broader confidence on scheduled or release pipelines.

## Pipeline practices

Install pinned dependencies and browser binaries, validate configuration, run a focused smoke suite early, then shard larger suites when capacity allows. Publish reports, traces, screenshots, and videos as artifacts. Separate product failures from environment failures and track flaky tests explicitly.

Use the same commands locally and in CI wherever possible so failures are reproducible.
