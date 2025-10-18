<div align="center">
  <picture>
    <source
      media="(prefers-color-scheme: dark)"
      srcset="https://github.com/cumbucadev/design/raw/main/images/logo-dark-transparent.png"
    >
    <img
      alt="Logo do Cumbuca Dev"
      src="https://github.com/cumbucadev/design/raw/main/images/logo-light-transparent.png"
      width="20%"
    >
  </picture>
</div>

# Shared Workflows

[Versão em Português](/README.md)

Central repository with **reusable GitHub Actions workflows** for the organization's repositories.

- [Shared Workflows](#shared-workflows)
  - [What's in here?](#whats-in-here)
  - [How to use in other repositories](#how-to-use-in-other-repositories)
  - [Catalog](#catalog)
    - [autoassign-issue](#autoassign-issue)
    - [close-stale-issues](#close-stale-issues)
    - [validate-pr-title](#validate-pr-title)
  - [💬 New Features and Reporting Bugs](#-new-features-and-reporting-bugs)
  - [💡 Questions? Ideas?](#-questions-ideas)
  - [💻 Contributing to the Project's Code](#-contributing-to-the-projects-code)
  - [❤️ Contributors](#-contributors)

## What's in here?

This repository stores standardized workflows that can be reused in other repositories within the organization using the [`workflow_call`](https://docs.github.com/en/actions/using-workflows/reusing-workflows) feature.

Here you'll find:

- Standardized CI/CD workflows
- Automation flows for testing, building, and deployment
- Shared conventions across projects

## How to use in other repositories

You can reuse workflows from this repository in other projects by adding a snippet like the one
below to your `.github/workflows/<name>.yml` file:

```yml
permissions: <permissions>

jobs:
  example:
    uses: cumbucadev/shared-workflows/.github/workflows/<workflow-name.yml>@main
```

Replace `<permissions>` with the required permissions and `<workflow-name>` with the desired
workflow file.

Real example of use:

```yml
permissions:
  pull-requests: write

jobs:
  example:
    uses: cumbucadev/shared-workflows/.github/workflows/validate-pr-title-v1.yml@main
```

## Catalog

Below are the shared workflows currently used across the Cumbuca org. We version **by major in the
filename** (e.g., `-v1`, `-v2`). See the changelogs for breaking changes and migration notes.

### autoassign-issue

#### Description

This workflow automatically assigns an issue to a user when they comment a **specific keyword** on the issue.
The comment works as a trigger of “I want to take this issue,” making the self-assignment process simple, fast, and transparent.
Additionally, the workflow posts a bilingual (English + Portuguese) comment confirming that the issue has been assigned to the user.

#### Triggers

- `issue_comment` (created)

#### Keywords (triggers)

- `"bora"`, `"bora!"`, `"dibs"`, `"dibs!"`
  _(case-insensitive — any combination of uppercase/lowercase letters is accepted)_

#### Behavior Summary

- When someone comments one of the trigger keywords on an open issue:
  - The issue is automatically assigned to that user
  - A bilingual comment is posted confirming the assignment and including a link to the contributing guide
- Helps streamline the contribution process, avoiding manual assignee management and improving visibility of who is working on each issue

#### Changelog

- **v1** — Initial release
  - Implements autoassign for comments containing specific trigger keywords
  - Supported keywords: `"bora"`, `"bora!"`, `"dibs"`, `"dibs!"`
  - Posts a bilingual confirmation comment (PT-BR + EN)

### close-stale-issues

#### Description

This workflow automatically identifies inactive issues and pull requests and marks them as “stale” after a period 
without activity. If there is no interaction after being marked, they are automatically closed. All messages are 
bilingual (Portuguese + English) to facilitate communication with contributors.

#### Triggers

- `schedule` (cron: `00 4 * * *`)
- `workflow_dispatch` (manual run)

#### Messages

- Message for issue marked as stale:
  - Explains that the issue had 45 days without activity and will be closed in 15 days if there is no interaction
  - Bilingual (PT-BR + EN)

- Message for PR marked as stale:
  - Explains that the PR had 30 days without activity and will be closed in 15 days if there is no interaction
  - Bilingual (PT-BR + EN)

- Message when closing issue:
  - Summarizes the timeline: marked as inactive after 45 days, closed after an additional 15 days
  - Provides next steps (reopen, update context, create a new issue if necessary)
  - Bilingual (PT-BR + EN)

- Message when closing PR:
  - Summarizes the timeline: marked as inactive after 30 days, closed after an additional 15 days
  - Provides next steps (reopen, address reviews, rebase/merge with main)
  - Bilingual (PT-BR + EN)

#### Behavior summary

- Every day at 04:00 (UTC in cron `00 4 * * *`), the workflow evaluates issues and PRs:
  - Issues: marked as stale after 45 days without activity; closed after an additional 15 days (bilingual messages)
  - PRs: marked as stale after 30 days without activity; closed after an additional 15 days (bilingual messages)
- Can be run manually via `workflow_dispatch`
- Posts clear comments with instructions on what to do to keep it open (remove the stale label or comment)

#### Changelog

- **v1** — Initial release
  - Implements automatic inactivity marking (stale) for issues (45 days) and PRs (30 days)
  - Automatically closes after an additional 15 days without response
  - Includes bilingual messages for marking and closing issues/PRs
  - Daily scheduling via cron and manual run support

### validate-pr-title

#### Description

Ensures that pull request titles follow the
[Conventional Commits](https://www.conventionalcommits.org/en/v1.0.0/) specification.
If the title doesn’t match the expected format, the workflow posts a bilingual (Portuguese +
English) comment explaining the problem, giving examples of valid prefixes, and linking to the
official docs for guidance. Once the title is fixed, the comment is automatically removed.

#### Triggers

- `workflow_call`
- `pull_request` (opened, edited, reopened)

#### Behavior summary

- Validates PR titles against the allowed list of Conventional Commit types:
  - `build`, `chore`, `ci`, `docs`, `feat`, `fix`, `perf`, `refactor`, `revert`, `style`, `test`
- If invalid:
  - Fails the check
  - Posts a sticky comment with context, examples, and links in both PT-BR and EN
- If valid:
  - Removes any previous error comment
- Helps maintain a clean, standardized project history, improving automation (e.g., changelogs,
  releases)

#### Changelog

- **v1** — Initial release.
  - Enforces allowed Conventional Commit types (`chore`, `ci`, `docs`, `feat`, `fix`, `refactor`,
    `style`, `test`)
  - Adds bilingual guidance for contributors when the title is invalid
  - Automatically cleans up guidance comments once the title is fixed

## 💬 New Features and Reporting Bugs

If you would like to suggest new features or report bugs, just create a new [issue][github-issues] and we will respond there!

(To learn more about GitHub issues, check out the [official GitHub documentation][github-issues-doc]).

## 💡 Questions? Ideas?

Do you have questions about how to use the library? New ideas for the project? Want to share something with us? Feel free to create a topic in our [Discussions][github-discussions], and we’ll interact with you there!

(To learn more about GitHub discussions, check out the [official GitHub documentation][github-discussions-doc]).

## 💻 Contributing to the Project's Code

Your contribution is always very welcome! To help you get started, we’ve prepared the following files:

- [CONTRIBUTING.md](/CONTRIBUTING.md): Here you’ll find all the necessary instructions to contribute to the project.
- [CONTRIBUTING_EN.md](/CONTRIBUTING_EN.md): English version of the contribution guidelines.
- [CODE_OF_CONDUCT.md](/CODE_OF_CONDUCT.md): Our code of conduct, which defines expectations for respectful and inclusive interactions within the community.
- [CODE_OF_CONDUCT_EN.md](/CODE_OF_CONDUCT_EN.md): English version of the code of conduct.
- [CORE_TEAM.md](/CORE_TEAM.md): Lists and presents information about the members of the project’s core team, including their roles and contact details.
- [CORE_TEAM_EN.md](CORE_TEAM_EN.md): English version of the list and information about the project’s core team.
- [LICENSE.md](/LICENSE.md): Details about the project’s license. It defines what you can and cannot do with the code. In general, the license allows you to use, modify, and distribute the code as long as you follow the defined terms. However, it’s important to check for specific restrictions, such as credit attribution to the original author or prohibition of commercial use.

Make sure to read these files carefully before contributing. If you have any difficulties or questions, feel free to ask us using [GitHub Discussions][github-discussions]. Every bit of help counts!

## ❤️ Contributors

[![contributors](https://contrib.rocks/image?repo=cumbucadev/shared-workflows)](https://github.com/cumbucadev/shared-workflows/graphs/contributors)

_Made with [contrib.rocks](https://contrib.rocks)._

[github-discussions-doc]: https://docs.github.com/discussions
[github-discussions]: https://github.com/cumbucadev/shared-workflows/discussions
[github-issues-doc]: https://docs.github.com/issues/tracking-your-work-with-issues/creating-an-issue
[github-issues]: https://github.com/cumbucadev/shared-workflows/issues
