# Public Compute Relay

This repository is an intentionally minimal GitHub Actions relay for compute-intensive jobs whose source of truth remains in a private repository.

## Security model

- No private source code, datasets, manuscripts, predictions, or scientific results are committed here.
- Workflows are manual (`workflow_dispatch`) only; pull requests and pushes cannot launch private compute.
- A least-privilege repository secret checks out the private source at a pinned commit.
- Compute stdout/stderr and selected outputs are written back to a dedicated branch in the private repository.
- No Actions artifacts containing private results are uploaded from this public repository.
- The public workflow never accepts arbitrary shell commands or repository names as inputs.

This repository is only a runner boundary. The private repository remains the authoritative project record.
