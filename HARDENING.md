<!-- markdownlint-disable -->

# Hardening Report: Matejkob--swift-macro-compatibility-check/v1.0.1

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **Matejkob--swift-macro-compatibility-check/v1.0.1** was hardened automatically. 4 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### script-injection (severity: high)

Rule (a) failed: the composite step 'Run Swift Macro Compatibility Check Script' puts GitHub Actions expressions straight into its run: script. The offending lines are: `if [ "${{ inputs.run-tests }}" = "true" ]; then` (line 29), `if [ "${{ inputs.major-versions-only }}" = "true" ]; then` (line 32), `if [ "${{ inputs.verbose }}" = "true" ]; then` (line 35), and `bash ${{ github.action_path }}/swift-macro-compatibility-check.sh $ARGS` (line 40). The action_path expansion is also unquoted. Fix: pass these values in through env: variables (e.g. RUN_TESTS, MAJOR_ONLY, VERBOSE, and the built-in GITHUB_ACTION_PATH) and quote them in the script, e.g. `bash "$GITHUB_ACTION_PATH/swift-macro-compatibility-check.sh"`.

Locations:

- `action.yml:29`
- `action.yml:32`
- `action.yml:35`
- `action.yml:40`

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

Moved inputs.run-tests, inputs.major-versions-only, inputs.verbose into env (RUN_TESTS, MAJOR_ONLY, VERBOSE); replaced ${{ github.action_path }} with quoted "$GITHUB_ACTION_PATH"; built flag list with a bash array (safe-expanded for empty case on bash 3.2) preserving argument behavior.

