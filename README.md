# Public Compute Relay

This repository is an intentionally minimal GitHub Actions relay for compute-intensive jobs whose source of truth remains in a private repository.

## Security model

- No private source code, datasets, manuscripts, predictions, or scientific results are committed here.
- Workflows are manual (`workflow_dispatch`) only; pull requests and pushes cannot launch private compute.
- A least-privilege repository secret checks out the private source at a pinned branch, tag, or commit.
- Compute stdout/stderr and selected outputs are written back to a dedicated branch in the private repository.
- No Actions artifacts containing private results are uploaded from this public repository.
- The public workflow never accepts arbitrary shell commands or repository names as inputs.

## One-time secret setup

Create a fine-grained GitHub personal access token with:

- repository access: only `shengtenghou4-star/19`;
- repository permission `Contents`: read and write;
- repository permission `Metadata`: read-only;
- no organization, administration, issues, pull requests, packages, or workflow permission.

Then open this repository's **Settings → Secrets and variables → Actions → New repository secret** and add:

- name: `LAZARUS_REPO_TOKEN`
- value: the fine-grained token

Do not place the token in variables, files, commits, workflow inputs, issue comments, or Actions logs.

## Running a job

Open **Actions → Private-source compute relay → Run workflow** and choose one fixed job:

- `distribution-shift` — one seed, three split types;
- `distribution-shift-multiseed` — seeds 626–630 across entry-random, virus-held-out, and study-held-out, including the seen-antibody secondary endpoint;
- `full-reproduction` — one random-mask full reproduction;
- `random-multiseed` — five random-mask full reproductions.

The default private source ref is `agent/m3-public-compute`. A successful or failed run creates a private result branch named like:

`compute-results/<job>-<run-id>-<attempt>`

Only that private branch contains the logs and scientific outputs. The public Actions page exposes only setup status, the fixed job name, and the private result branch name—not metrics, predictions, source files, or logs.

This repository is only a runner boundary. The private repository remains the authoritative project record.
