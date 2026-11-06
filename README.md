# Csv Cleanup Studio

Profile and clean local CSV files with quoted-field parsing, trimming, blank-row removal, deduplication, and explicit export.

[![Build and verify](https://github.com/netcodermike/csv-cleanup-studio/actions/workflows/verify.yml/badge.svg)](https://github.com/netcodermike/csv-cleanup-studio/actions/workflows/verify.yml)

**Language:** C# · **Platform:** Windows desktop · **App type:** Windows CSV profiling and transformation app

First-release learning implementation, with explicit scope below. This is one independently runnable app, not a placeholder in a combined repository.

## Features

- Quoted/multiline CSV parsing
- Column/blank-cell profile
- One-click cleanup
- Optional spreadsheet-safe export

## Requirements

.NET 10 SDK/Windows Desktop runtime. WPF runs only on Windows. No NuGet packages.

## Quick start

```sh
git clone https://github.com/netcodermike/csv-cleanup-studio.git
cd csv-cleanup-studio
dotnet run
```

Commands run from the repository root. Lines marked for a particular operating system apply only there. Language tools are prerequisites, not installed by the app. Close desktop windows normally; terminal/server apps stop with Ctrl+C unless their usage notes say otherwise.

## Example workflow

Load a CSV containing padded duplicates, empty rows, quoted commas, and multiline fields. Apply cleanup, export to a new file, and inspect formula-safe behavior with a synthetic =example cell.

## Architecture, configuration, and data

Program.cs uses TextFieldParser for comma-separated quoted records, preserves raw whitespace on load, and displays synthetic Column 1..N headers in a WPF DataGrid. Cleanup trims cells, removes all-empty rows, and deduplicates exact trimmed row arrays using JSON keys. Export escapes CSV quotes/newlines; spreadsheet-safe mode prefixes formula-like cells with an apostrophe. Limits are 2 MiB, 20,000 rows, and 100 columns. Tests cover quoted commas/newlines, round trips, and cleanup.

## Verification

Build with the quick-start command where needed, then run:

```sh
dotnet run -- --self-test
```

Manual acceptance: Load a CSV containing padded duplicates, empty rows, quoted commas, and multiline fields. Apply cleanup, export to a new file, and inspect formula-safe behavior with a synthetic =example cell. Also test malformed inputs and an unwritable output destination.

See [validation record](docs/VALIDATION.md) for observed checks and their limits. CI results verify only what the workflow runs; they do not establish native GUI correctness or production readiness.

## Limitations and next steps

Comma/UTF-8-oriented import only, no delimiter detection, type inference, cell editing, undo, encoding selector, header semantics, formulas, or large-file streaming. The first CSV row remains data. Ragged rows display padded empty cells but exports preserve their original field counts. Safe mode intentionally alters formula-like strings. Cleanup is destructive in memory; reload to undo.

## Troubleshooting

Use the exact platform/toolchain above. Preserve originals and use synthetic fixtures first. Errors are displayed in the UI or stderr. A headless machine can run the model tests but cannot verify native GUI/audio behavior. Output paths are chosen explicitly; keep backups of important data.

## Source map

- `App.csproj`
- `Program.cs`

## Development and license

Read [contributing](CONTRIBUTING.md) before changing the app, and [security/privacy](SECURITY.md) before supplying private data. Use synthetic fixtures for tests. No telemetry, paid API key, or account is required by the app itself. Dependencies, when present, are stated in Requirements.

[MIT license](LICENSE), copyright 2026 netcodermike.
