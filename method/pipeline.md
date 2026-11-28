Superseded: this describes an early version of the pipeline.

# Lean exposition pipeline

Run from this directory with Python 3.13. A live run also needs Node, the Codex companion, a built exposition tool, and the target's Lean toolchain and cached dependencies. The runner uses the standard library and runs on macOS and Linux.

```sh
python3 run_pipeline.py --config targets/alpoge-window.toml --dry-run
python3 run_pipeline.py --config targets/alpoge-window.toml
python3 run_pipeline.py --config targets/alpoge-window.toml --from scope
python3 run_pipeline.py --config targets/alpoge-window.toml --steps scope,supply --force scope
python3 -B -m unittest -v
```

`--steps` replaces the configured list. The runner sorts selected steps into dependency order. An omitted prerequisite must already have artifacts where the runner expects them. `--from` drops selected steps earlier than the named step. Existing outputs allow a step to be skipped. `--force` can be repeated. It reruns the named selected steps and their selected dependents, including indirect dependents and all jobs for `review` or `grade`. Existing dependent jobs outside the selection are marked for rerun the next time they are selected.

A dry run prints the planned working directories, file copies, outputs, model, effort, and write settings. The planner's root statement is shown as a lookup unless the config names the file. Dry runs use the configured paths in the prompts, leave the live work directory alone, and require neither Node nor the plugin.

## Target config

Copy one of the files in [targets](targets/) and change the root and local paths. Set `work_dir` to an absolute path outside any Git repository. Other relative paths are resolved relative to the TOML file. Home-directory paths can use `~`.

```toml
target = "example"
root = "Example.finish"
module = "Example.Main"
archive_source = "/path/to/archive/Lean"
tool_dir = "/path/to/exposition-tool"
work_dir = "/path/to/pipeline-work"
answer_key_dir = "/path/to/held-out-reference"
steps = [
    "build-and-plan", "status", "why", "related", "strategy", "writer", "digest",
    "lit", "v7", "scope", "supply", "skeleton", "chase", "audit", "review", "revise", "grade",
]
scope_max_levels = 5
supply_max_levels = 5
# Optional. Set the full list to replace or extend the default panel.
# review_models = ["gpt-6.2-astra", "gpt-6.2-sol"]
# Optional. These titles or identifiers are used only if grade-keys is selected.
grade_keys = ["2", "Main reduction"]

[exclusions]
sites = ["example.org"]
authors = ["Author's write-ups of this result"]
topics = ["Write-ups and commentary on the formal proof"]

[overrides.why]
effort = "high"

[overrides."grade.sol"]
model = "gpt-6.2-sol"
effort = "high"
```

`archive_source` is the read-only Lean source tree, with paths corresponding to module names. Defaults within `tool_dir` are `targets/<target>/` for the copied Lean project and `out/<target>/pilot/` for the planner. Set `build_project` or `planner_dir` to override either location within the tool. Set `build_cache` if the build brief should direct Codex to cached dependencies in a separate folder.

Use `statement_file` to specify the root statement artifact explicitly. Otherwise the runner searches the planner's `statements/*.lean.txt` and skips `premises.lean.txt`. It looks for a declaration with the root's full name first and falls back to its short name. If multiple files match at the selected level, set `statement_file` to resolve the ambiguity. The optional `statement` field is a short description substituted into the literature briefs. The optional `research_status` file supplies dated conjecture status to `status`.

Set `codex_companion` to the full path to `codex-companion.mjs` if needed. The default uses a registered `installPath` for `codex@openai-codex` in `~/.claude/plugins/installed_plugins.json` and looks for `scripts/codex-companion.mjs` there. Per-step `model` and `effort` overrides merge with the built-in defaults. `overrides.grade` affects both graders and `overrides."grade.astra"` or `overrides."grade.sol"` takes precedence for one grader.

`review_models` takes a nonempty list of distinct model names. The default is `["gpt-6.2-astra", "gpt-6.2-sol"]`. Each model runs at high effort unless `overrides.review.effort` is set. After changing the list for an existing run, use `--force review` so the revision and grades are refreshed.

`supply_max_levels` sets the hard cap for `supply` and defaults to 5. It takes a positive integer. The supplier proofs are level 1. After each level, the worker classifies every unopened dependency the paragraph relies on as a mechanism that explains how the archive establishes the hypothesis or as a supporting fact. It stops when no mechanism dependency remains, the next level would add more than ten times the total closure lines read so far, or it reaches the cap. `levels.json` records the declarations opened, lines added, unopened dependencies, and decision at each level.

`scope_max_levels` sets the hard cap for `scope` and also defaults to 5. It takes a positive integer. Direct consumer proofs are level 1. The worker searches the archive for uses of each condition and quantity in the root's statement, including properties asserted in the conclusion. Those uses count as mechanisms. After each level, the worker classifies every unopened consumer the scope paragraph relies on as a mechanism that explains the form of the root's conclusion or a condition's downstream role, or as a supporting fact. The trace stops when no mechanism item remains, the next level would add more than ten times the lines read so far in the consumer trace, or the cap is reached. The paragraph explains and cites the downstream roles it traces. The `conditions` array in `scope.json` records each item's uses and purpose. `scope-levels.json` uses the same schema as `levels.json` and travels with `scope.json`. Rerun `scope` to generate the trace for older scope outputs before running a step that consumes them.

## Steps

| Step | Work and main outputs |
| --- | --- |
| `build-and-plan` | Copy the import closure, build the module, run Pass A, and package proof slices, statements, units, the plan, and spine. The companion runs with `--cwd` set to the tool directory, and the build writes its artifacts there. |
| `status` | Classify premises and spine results in `status.md` and `status.json`. |
| `why` | Extract reasons for the proof's form from source slices into `why5-a.md` and `why5-a.json`. |
| `related` | Compare the theorem with literature using the configured exclusions. Writes `related-work.md` and `related-work.json`. |
| `strategy` | Explain the proof's design decisions and where obvious alternatives break, in `strategy.md` and `strategy.json`. |
| `writer` | Draft the expert exposition, check the trace of required reasons, and write `assembled.md`. The runner checks both the folder root and `drafts/`. |
| `digest` | Rank the key ideas and write `digest.md` and `digest.json`. |
| `lit` | Search for precedents per idea and per strategy decision. The runner supplies the writer's matching literature lines with original line numbers. Writes `lit.md` and `lit.json`. |
| `v7` | Add a thesis, update the literature claims, and write `assembled-v7.md` and `digest-v7.md/json`. |
| `scope` | Follow Lean consumers using the stopping rule, record variants and open obligations, and insert a scope paragraph. Writes `scope.md`, `scope.json`, and `scope-levels.json`. |
| `supply` | Trace the declarations that supply the root hypothesis using the stopping rule, then insert a paragraph describing the source of the hypothesis. Requires the scope report and writes `supply.md`, `supply.json`, and `levels.json`. |
| `skeleton` | Identify the classical structure of the proof and add one or two sourced sentences to the thesis. |
| `chase` | Follow citations back and forward one hop, record attribution changes, and update only the affected literature lines. |
| `audit` | Check quantifiers, necessity, sufficiency, signs, and vanishing against the Lean and the mathematics. Saves the read-only review as `report.md`. |
| `review` | Independently review the newest exposition against `units4.json`, `scope.json`, `supply.json`, and the audit. Each read-only job produces `r0.json` and `r0.md` under its model name in `<target>-review/`. |
| `revise` | Check the audit and the configured reviewers' `r0.json` reports against the Lean before editing. Sol at high effort runs with `--write` and produces the next numbered assembly and `revise-log.md`, with each finding's disposition and each edit's old and new text. |
| `grade` | Two read-only graders compare the exposition and digest with `key-insights.md` and `sources.md`. Astra and Sol default to high effort and get separate copies, logs, and reports in the `astra/` and `sol/` subdirectories. |
| `grade-keys` | Optional read-only review of the configured key titles or identifiers and the supply paragraph against the traced Lean. Uses `key-insights.md`, `scope.json`, `scope-levels.json`, `supply.json`, and `levels.json`. Saves the review as `report.md`. |

Status, why, and related run concurrently. The two full graders also run concurrently. Each job uses a directory of the form `<work_dir>/<target>-<step>/` for staged artifacts, `TASK.md`, and `codex.log`. Later revisions and reviews pick the highest numbered assembly from preceding steps, with the writer's unversioned assembly as a fallback. A revision stages its previous assembly under `previous/` and produces the next numbered version, preserving the historical version floor if steps are omitted. The live log at `<work_dir>/<target>-pipeline-log.md` records UTC start and end times, exit status, and observed outputs, including skips. A failed job stops subsequent batches. Its marker forces a retry even if it left every output behind. Retrying or forcing a job replaces its declared outputs and run log.

## Review method

The default panel uses two model families, Astra and Sol. Reviewers run concurrently with separate copies of the same inputs. Each reports false claims, overstatements, missing ideas, and unsupported attribution, then identifies three to six central ideas and marks whether the exposition conveys each one. The revision checks those findings and the audit against the Lean or a computation and preserves untouched lines. A subsequent `grade` uses the revised assembly. Reference answers are staged only for grading. Before release, have a human or Claude check the findings outside this script.

## Limits and historical inputs

- The supplied driver invokes Codex for the build. This version does the same, using the build-and-plan brief in place of the historical window build's one-word no-op. The tool, compiled artifacts, caches, and key files are external prerequisites. No live Lean or Codex run was performed for these snapshots.
- The historical driver leaves planner paths and some input folders implicit. The samples derive the planner directory from the configured tool and target and use `alp-status/research-status.md` for the reused status input. The Landau TOML records the inferred module and grading-key location in comments. Verify them and replace the `TODO` values before a live run. Dry runs allow `TODO` values.
- The sample configs use a shared `pipeline-work` directory and prefix stage folders with the target name. To resume from historical artifacts, place the relevant outputs at the stage paths shown in the dry-run plan. The historical record-folder README and the separate task that constructed the key remain outside this pipeline. The supplied chase brief came from a different theorem, so chase is available without being part of either default run.
- A nonzero companion exit fails the job. For `audit`, `grade`, and `grade-keys`, the runner writes the text after the final `[codex]` progress line to `report.md` and requires non-whitespace content. For `review`, it parses the final JSON response and saves the structured findings and Markdown report as separate files. It also validates expected files and planner directories. The workers perform the mathematical, trace, and line-preservation checks.
- The companion times out after 90 minutes. A Codex child process can keep running after the timeout. Check for a surviving child and stop it before retrying the job.
- The runner stages reference files only for grading. Keep the references outside the tool, archive, and blind input trees. The read-only flags and literature exclusions are passed to Codex. Exclusion compliance depends on the worker and the companion's sandbox.
- Existing files drive resumption. Changes to config or inputs do not automatically invalidate prior outputs. Use `--force` for affected jobs. Only one live run for the same target and work directory can proceed at a time. Use separate build project and planner paths if running distinct targets concurrently.
