# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Working Principles

Behavioral guidelines to reduce common mistakes. They bias toward caution over speed; for trivial tasks, use judgment.

### Think before coding

Don't assume. Don't hide confusion. Surface tradeoffs.

Before implementing:

- State your assumptions explicitly. If uncertain, ask.
- If multiple interpretations exist, present them — don't pick silently.
- If a simpler approach exists, say so. Push back when warranted.
- If something is unclear, stop. Name what's confusing. Ask.

### Simplicity first

Minimum code that solves the problem. Nothing speculative.

- No features beyond what was asked.
- No abstractions for single-use code.
- No "flexibility" or "configurability" that wasn't requested.
- No error handling for impossible scenarios.
- If you write 200 lines and it could be 50, rewrite it.

Ask yourself: "Would a senior engineer say this is overcomplicated?" If yes, simplify.

### Surgical changes

Touch only what you must. Clean up only your own mess.

When editing existing code:

- Don't "improve" adjacent code, comments, or formatting.
- Don't refactor things that aren't broken.
- Match existing style, even if you'd do it differently.
- If you notice unrelated dead code, mention it — don't delete it.

When your changes create orphans:

- Remove imports/variables/functions that _your_ changes made unused.
- Don't remove pre-existing dead code unless asked.

The test: every changed line should trace directly to the user's request.

### Goal-driven execution

Define success criteria. Loop until verified.

Transform tasks into verifiable goals:

- "Add validation" → "Write tests for invalid inputs, then make them pass"
- "Fix the bug" → "Write a test that reproduces it, then make it pass"
- "Refactor X" → "Ensure tests pass before and after"

For multi-step tasks, state a brief plan:

```text
1. [Step] → verify: [check]
2. [Step] → verify: [check]
3. [Step] → verify: [check]
```

Strong success criteria let you loop independently. Weak criteria ("make it work") require constant clarification.

These guidelines are working if: fewer unnecessary changes in diffs, fewer rewrites due to overcomplication, and
clarifying questions come before implementation rather than after mistakes.

## Logging

```python
from loguru import logger as log
```

- **Levels:** `log.trace()`, `log.debug()`, `log.info()`, `log.warning()`, `log.error()`, `log.exception()`. Choose by
  hotness/verbosity — `trace` for per-token / hot-path detail, `debug` for routine method entry/exit, `info` for notable
  lifecycle events, `warning` / `error` / `exception` for problems.
- **Interpolate with f-strings, not loguru's `{}` positional args.** Consistent with the Code Style rule, use
  `f"…{value}"`; only add the `f` prefix when the string actually interpolates (`"START: …"` with no params stays a
  plain string).
- **`START:` / `DONE:` bracketing.** Wrap a method (or other notable operation) with a `START:` line at entry and a
  `DONE:` line at exit, both naming `ClassName: method_name` (append `: param={value}` context where useful):

  ```python
  log.debug("START: IntentBertClassifier: predict")
  ...
  log.debug(f"DONE: IntentBertClassifier: predict. Elapsed time: {perf_counter() - start_time:.5f}")
  ```

- **Timing uses `perf_counter()`, rendered `:.5f`.** Measure elapsed time with `time.perf_counter()` captured as a start
  value and subtracted at the `DONE:` line; always format the elapsed value with the `:.5f` spec:

  ```python
  from time import perf_counter

  start_time: float = perf_counter()
  ...
  log.info(f"DONE: SESSION SERVICER: DetectIntent. Elapsed time: {perf_counter() - start_time:.5f}")
  ```

  Never measure a duration with `time.time()` — reserve `time.time()` for wall-clock timestamps (epoch seconds persisted
  to a DB / proto, unique-id or filename stamps). `perf_counter()` has an undefined epoch and must not be stored or
  compared across processes.

## Docstrings

Google-style, triple double-quotes:

```python
"""
Short imperative summary line.

Args:
    param_name (type):
        Description of the parameter.

Returns:
    type:
        Description of the return value.

Raises:
    ExceptionType:
        When this exception is raised.
"""
```

## Git Commits

- **Never include Claude as author or co-author** in commit messages, PR descriptions, or any other text. Do not add
  `Co-Authored-By: Claude…` trailers, "Generated with Claude Code" footers, or any similar attribution.
- The user's own git author identity (already configured in git) is the only identity that should appear on commits.
- This rule overrides the default Claude Code commit-template guidance.
- **Never prepend the JIRA ticket ID** (e.g. `[OND211-2386]`) to the commit subject yourself. The `giticket` pre-commit
  hook reads the ticket from the branch name (`(feature|bugfix|support|hotfix)/<TICKET>-…`) and prepends `[<ticket>]`
  (with a trailing space) automatically. Writing the prefix manually produces a duplicate like
  `[OND211-2386] [OND211-2386] feat: …`. Write the subject as plain Conventional Commits (`feat: …`, `fix(scope): …`,
  `docs(types): …`) and let the hook add the prefix on commit.

## General Principles

- Follow existing patterns before introducing new abstractions.
- Keep changes minimal and consistent with surrounding code.
- Validate inputs early with descriptive, context-rich error messages.
- Use context managers for files, sockets, and thread pools.
- Prefer region comments for grouping methods in files that already use them.
- End edited Markdown and YAML files with a trailing newline.

## Client-release orchestration (`release_all_clients`)

- It **fails loudly** on a genuine client-release error: the piped sub-make runs under `bash -c 'set -o pipefail; make -C … | tee …'` (a plain sh pipe returns tee's 0 and masks failures), and a **marker file** distinguishes an "already released" SKIP from a real FAILURE (make flattens recipe exit codes to 2, so the code alone can't tell them apart). Do not regress either.
- Every token-bearing recipe line is `@`-prefixed so make never echoes a secret — `docker run -e <TOKEN>`, `echo $(TOKEN) | gh auth`, `twine … -p${PYPI_PASSWORD}`, and the credential sub-make `make release $(info)` (which expands the token at runtime and is easy to miss).

## Pre-commit upgraded (language-agnostic hook set)

Pre-commit here uses only the language-agnostic hooks — **markdownlint-cli2, pre-commit-hooks hygiene, giticket, conventional-pre-commit** — no ruff/mypy/uv (there is no Python). Generated docs (`docs/`) and any generated code are excluded via the top-level `exclude:`.

- **markdownlint MD053 is disabled** (its auto-fix deletes `[comment]: <>` reference-definition markers).
- **markdownlint RELEASE.md reformatting is content-safe**: it only strips trailing whitespace and adds blank lines around headings — the `## Release … <VERSION>` headings and `*****` separators that `ondewo_release` greps for remain intact. (Confirmed: the 6.5.0 release notes sliced correctly after the reformat.)

## GitHub Actions — `Generate API Documentation` is a required gate

`.github/workflows/generate-doc-and-deploy.yaml` is the repository's **only** workflow and it is a blocking check,
not advisory: it runs on every push to `master`, on every pull request whose **base** is `master`, and on
`workflow_dispatch`. One job, `generate-doc-and-deploy`, with three declared steps — none of them a `run:` script,
all three `uses:` — plus the implicit image build GitHub inserts for the docker action:

1. `actions/checkout@v5` with `submodules: true`.
2. `ondewo/ondewo-protoc-gen-doc-action@master` — a **docker** action. GitHub first builds its `Dockerfile`
   (`FROM pseudomuto/protoc-gen-doc`) as its own step, then runs `entrypoint.sh` with the action's default inputs
   `formats=html,md` and `filename=index`. The entrypoint copies `resources/html/style.css` into `docs/` and runs
   `protoc -I. -Igoogleapis --doc_opt=/resources/templates/<fmt>.tmpl,index.<fmt> --doc_out=docs` over
   `$(find ondewo -name '*.proto' | sort)`, once per format.
3. `JamesIves/github-pages-deploy-action@v4`, which commits the regenerated `docs/` back to `master`'s `docs/`
   folder. It is skipped under `act` (`if: ${{ !env.ACT }}`) and **cannot be reproduced locally** — it needs the
   runner's `GITHUB_TOKEN` and push rights. Do not try; the other two steps are the whole gate.

**Reproduce steps 1–2 locally with the repository's own target.** It clones the same action at the same ref and
builds the same image, so it is the CI command rather than an approximation — do not hand-roll a `protoc` invocation
against a locally installed compiler, which would use a different protoc version and different templates:

```bash
make build_docs          # clone ondewo-protoc-gen-doc-action@master, docker build, docker run "html,md" "index"
make clean_docs_builder  # ALWAYS finish with this; see the untracked-clone note below
```

What is sharp about it, all of it observed while running the above:

- **The gate is "protoc succeeds", NOT "`docs/` is up to date".** `entrypoint.sh` only writes files; nothing
  compares the generated output against what is committed. A proto edit whose `docs/` was never regenerated passes
  the workflow, and step 3 then regenerates and commits it on `master`. So a green run is **not** evidence that the
  committed `docs/` matches the protos — regenerate and diff if you need to know that.
- **What does turn the step red is an unresolvable import.** `-Igoogleapis` names a directory this repo does not
  contain, so every run prints `googleapis: warning: directory does not exist.` once per format. That is harmless
  only because `ondewo/sip/sip.proto` imports nothing beyond `google/protobuf/empty.proto` and
  `google/protobuf/timestamp.proto`, which protoc resolves from its own bundled include. Verified by adding a
  scratch proto that imports `google/api/annotations.proto`: the same container exits **1** with
  `google/api/annotations.proto: File not found.`. If a proto ever needs googleapis, the workflow has to vendor or
  check it out — the existing warning is not a spare tyre.
- **The action is pinned to `@master`, a moving ref**, and it publishes no tag to pin to instead. A green run is
  evidence about the action as it was that day, not a standing guarantee. `make build_docs` clones `--depth 1`
  master as well, which is exactly what makes it a faithful reproduction.
- **`make build_docs` leaves `.tmp-protoc-gen-doc-action/` behind and that path is NOT in `.gitignore`** — one
  careless `git add .` vendors a whole clone of the action into this repo. `make clean_docs_builder` removes it
  together with the local image.
- **`submodules: true` is a no-op** — there is no `.gitmodules`. Do not add a proto dependency expecting checkout to
  fetch it for you.
- **There is no uv / ruff / mypy / pytest / coverage step to reproduce.** This repository tracks zero `.py` files;
  the `flake8` and `mypy` Makefile targets download their configs from `ondewo-sip-client-python` and would lint
  nothing here, and no workflow calls them. Hunting for a `--cov-fail-under` or a `[tool.coverage.run] source` list
  in this repo is a dead end — the protos and the generated docs are the whole surface.
- The single deliberate divergence in `make build_docs` is `--user $(id -u):$(id -g)`, so the regenerated files
  belong to you rather than to root. Container, arguments and generated bytes are otherwise identical to CI.

**Read the real verdict instead of guessing** (there is no `gh` CLI on these machines):

```bash
SHA=$(git rev-parse HEAD)
curl -s "https://api.github.com/repos/ondewo/ondewo-sip-api/actions/runs?head_sha=$SHA" \
  | python3 -c 'import json,sys
for r in json.load(sys.stdin)["workflow_runs"]:
    print(r["path"], r["status"], r["conclusion"])'
```

A commit on a feature branch with no open PR into `master` has **no run at all** — an empty `workflow_runs` list
means "never triggered", which is not the same as a failure.

## Jenkins — never trigger a multibranch scan or branch indexing

**NEVER trigger a Jenkins multibranch scan or branch indexing.** Do not call a multibranch/folder job's
`build`, `scan`, or reindex endpoints, click "Scan Repository Now" / "Build Now" on a folder, run
`p4 scan`, or use any API/CLI that reindexes branches or scans the repository. A scan/reindex runs across
**every** branch, consumes CI resources, and can kick off unintended builds and deploys.

If a branch is not building — it was not discovered, or its job is marked `buildable: false` / orphaned —
**report it and stop**. Let the user or a Jenkins admin adjust branch-discovery/config or rename the branch
to the convention. Never force a build by scanning or reindexing.
