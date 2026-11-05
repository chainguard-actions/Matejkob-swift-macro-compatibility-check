<!-- markdownlint-disable -->

# Hardening Report: Matejkob--swift-macro-compatibility-check/v1.0.0

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **Matejkob--swift-macro-compatibility-check/v1.0.0** was hardened automatically. 4 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### script-injection (severity: high)

Sub-rule (a): GitHub Actions expressions are placed directly inside the run: script of the 'Run Swift Macro Compatibility Check Script' step. The lines are: `if [ "${{ inputs.run-tests }}" = "true" ]; then`, `if [ "${{ inputs.major-versions-only }}" = "true" ]; then`, `if [ "${{ inputs.verbose }}" = "true" ]; then` and `bash ${{ github.action_path }}/swift-macro-compatibility-check.sh $ARGS`. Fix: pass each value in through env: variables (INPUT_RUN_TESTS, and so on) and use "$GITHUB_ACTION_PATH" quoted.

Locations:

- `action.yml:28`
- `action.yml:31`
- `action.yml:34`
- `action.yml:39`

### static-inline-injection (severity: high)

shell injection: expression "${{ inputs.run-tests }}" appears directly in run: block of step "Run Swift Macro Compatibility Check Script"; move to env: map

Locations:

- `action.yml:29`

### static-inline-injection (severity: high)

shell injection: expression "${{ inputs.major-versions-only }}" appears directly in run: block of step "Run Swift Macro Compatibility Check Script"; move to env: map

Locations:

- `action.yml:32`

### static-inline-injection (severity: high)

shell injection: expression "${{ inputs.verbose }}" appears directly in run: block of step "Run Swift Macro Compatibility Check Script"; move to env: map

Locations:

- `action.yml:35`

## Iteration Notes

### Iteration 1

**Fixes applied:** script-injection, static-inline-injection

**Notes:**

Moved inputs.run-tests, major-versions-only, verbose into env vars; replaced github.action_path with quoted $GITHUB_ACTION_PATH; built args with a bash array (bash 3.2-safe empty expansion).

