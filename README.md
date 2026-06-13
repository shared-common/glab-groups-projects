# glab-groups-projects

Thin GitHub Actions wrapper for explicit single-project GitLab mirrors.

## Scope

- Loads `gh-actions-cfg/glab-groups-projects`
- Calls the reusable workflow in `glab-groups-shared@mcr/main`
- Uses the BWS target PAT secret `GL_PAT_GROUP_PROJ_SVC`
- Mirrors only the explicitly configured source repositories into their
  configured target groups without deriving target path segments from the
  source URL
- Syncs the source default branch to the managed target branch named by
  `GIT_BRANCH_GLAB_FORKS`
- Reconciles only the explicitly configured target branch protections after
  push; the runtime does not bootstrap extra target-only `mcr/*` branches
- Runs deterministic mirror batch shards with five jobs max in parallel
- Schedules at minute 35 of hours 0, 6, 12, and 18 UTC
- Publishes discovery, plan, report, CSV, JSON, and Parquet artifacts for each run

## Validation

```sh
python3 -m unittest discover -s tests
```
