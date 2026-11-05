<!-- markdownlint-disable -->

# Hardening Report: Matejkob--swift-macro-compatibility-check/v0.1.0

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **Matejkob--swift-macro-compatibility-check/v0.1.0** was hardened automatically. 4 finding(s) were identified and resolved across 2 iteration(s).

## Findings Fixed

### script-injection (severity: high)

Sub-rule (a): the composite step 'Check Swift package compatibility' puts input expressions straight into the run: script. The offending lines are: `if [ "${{ inputs.major-versions-only }}" = "true" ]; then` (line 46), `if [ "${{ inputs.verbose }}" = "true" ]; then` (line 54) and `if [ "${{ inputs.run-tests }}" = "true" ]; then` (line 69). The caller controls these values, and they are substituted into the script text before bash parses it, so a crafted value can inject shell commands. Fix: map each input to an env: variable (e.g. MAJOR_ONLY: ${{ inputs.major-versions-only }}) and refer to it in the script as "$MAJOR_ONLY", in double quotes.

Locations:

- `action.yml:46`
- `action.yml:54`
- `action.yml:69`

### static-inline-injection (severity: high)

shell injection: expression "${{ inputs.major-versions-only }}" appears directly in run: block of step "Check Swift package compatibility"; move to env: map

Locations:

- `action.yml:46`

### static-inline-injection (severity: high)

shell injection: expression "${{ inputs.verbose }}" appears directly in run: block of step "Check Swift package compatibility"; move to env: map

Locations:

- `action.yml:54`

### static-inline-injection (severity: high)

shell injection: expression "${{ inputs.run-tests }}" appears directly in run: block of step "Check Swift package compatibility"; move to env: map

Locations:

- `action.yml:69`

## Iteration Notes

### Iteration 1

**Fixes applied:** script-injection, static-inline-injection

**Notes:**

Mapped inputs.major-versions-only, inputs.verbose, inputs.run-tests to env vars MAJOR_ONLY, VERBOSE, RUN_TESTS in the composite step and referenced them double-quoted in the bash script. Behavior unchanged.

### Iteration 2

**Fixes applied:** script-injection, static-inline-injection

**Notes:**

Replaced ${{ inputs.major-versions-only }} and ${{ inputs.verbose }} in run: with existing env vars $MAJOR_ONLY and $VERBOSE; repaired the corrupted VERSIONS assignment and restored the else branch.

