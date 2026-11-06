# Validation

Authoring date: November 6, 2026. Host: Windows. Target: Windows desktop.

## Local result

Target-platform source CI is recorded after publication. This host has Python, Node.js, and .NET; other native toolchains are verified through CI. No unobserved GUI/device behavior is claimed.

## Reproducible checks

The GitHub Actions workflow builds/runs the following on `windows-latest`:

```sh
dotnet build
dotnet run --no-build -- --self-test
```

## Manual acceptance

Load a CSV containing padded duplicates, empty rows, quoted commas, and multiline fields. Apply cleanup, export to a new file, and inspect formula-safe behavior with a synthetic =example cell. Also test malformed inputs and an unwritable output destination.

A workflow file is not evidence of a passing run. Observed CI run links and source commits are recorded after publication. Native GUI, sound, sleep/resume, and platform permissions require direct target-platform acceptance even when model tests pass.
