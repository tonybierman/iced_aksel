# iced_aksel Integration Tests

This directory contains integration tests for the iced_aksel charting library.

## Structure

- `common/mod.rs` - Shared test utilities and helpers
  - Test helper macro for generating common test infrastructure
  - Snapshot testing helpers
  - Mouse/touch simulation helpers
  - Message verification helpers

- `core_axes_tests.rs` - Snapshot tests for axis rendering (7 tests)
  - **Main configurations**: minimal, engineering, custom placement
  - **Feature tests**: invisible axes, no grid, top/right positioning, custom tick renderers

## Running Tests

Run all tests:
```bash
cargo test --package iced_aksel_tests
```

Run specific test file:
```bash
cargo test --package iced_aksel_tests --test core_axes_tests
```

Run specific test:
```bash
cargo test --package iced_aksel_tests --test core_axes_tests -- test_minimal_axes_snapshot
```

## Snapshot Testing

The tests use iced's snapshot testing framework to verify visual output.

### Baseline Files

Baseline snapshots are stored in `tests/snapshots/`:
- `.sha256` files contain hash checksums for quick regression detection
- `.png` files contain reference images for visual comparison

### First Run

On the first run, baseline files are automatically generated.
Subsequent runs compare against these baselines.

### Updating Baselines

To update baselines after intentional changes:
1. Delete the relevant snapshot files in `tests/snapshots/`
2. Re-run the tests to regenerate baselines

### Platform Differences

Snapshot comparisons are skipped on macOS and Windows in CI environments
due to platform-specific rendering differences. Tests run normally on Linux
and in local development environments.

## Test Organization

Each test follows this pattern:
1. Set up axis configuration and data
2. Create a view function using the test helper
3. Run the simulator
4. Compare against baseline snapshots

All tests verify both:
- Visual correctness (PNG image comparison)
- Hash-based regression detection (SHA256 checksums)
