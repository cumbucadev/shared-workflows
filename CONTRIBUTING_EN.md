# Contributing

[Versão em Português](/CONTRIBUTING.md)

Thanks for taking the time to contribute! 🙇‍♀️🙇‍♂️ Every little bit of help counts!

Table of Contents
- [How our workflow versioning works](#how-our-workflow-versioning-works)
  * [When you add or update a workflow](#when-you-add-or-update-a-workflow)
  * [Why we version this way](#why-we-version-this-way)

## How our workflow versioning works

We version shared workflows by **including the major version in the filename**, for example:

```yml
.github/workflows/validate-pr-title-v1.yml
.github/workflows/close-stale-prs-v1.yml
```

We **only work with major versions** here:
- `-v1`, `-v2`… indicate the **major**.
- Create a **new major only for breaking changes** (changed required inputs/secrets, triggers, or
behavior).
- Non-breaking fixes stay within the same file/major — no rename needed.
- Keep the previous major for a **transition period**, then remove it after all consumers migrate.

### When you add or update a workflow

1. If the change is **backwards-compatible** → update the existing file.
2. If the change is **breaking** → copy the file, bump the suffix (`-v1` → `-v2`), and edit the new
one.
3. Update docs and any “reusable workflow” callers to point to the **new major**.
4. Keep the previous major until all repositories switch over.

### Why we version this way

1. **GitHub workflows have no built-in versioning**
Workflows are plain YAML files in the repo. There’s no native way to pin/track multiple workflow
versions; encoding the **major in the filename** makes the contract explicit for all repos.

2. **No nested folders** allowed for workflows
GitHub only recognizes files directly under `.github/workflows`. If you place a file at
`./github/workflows/python-lint/v1/lint.yml`, it won’t run. We “fake” structure by putting the
**version in the filename**.

3. **Safety during migrations across multiple repos**
Because these workflows are shared by **many repositories in the Cumbuca org**, coexistence of
majors lets us:
- Roll out upgrades gradually, repo by repo.
- Roll back instantly if needed.
- See at a glance (in the Actions UI and filename) which major was used in a given run.
