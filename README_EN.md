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

# shared-workflows

[Versão em Português](/README.md)

Central repository with **reusable GitHub Actions workflows** for the organization's repositories.

## What's in here?

This repository stores standardized workflows that can be reused in other repositories within the organization using the [`workflow_call`](https://docs.github.com/en/actions/using-workflows/reusing-workflows) feature.

Here you'll find:

- Standardized CI/CD workflows
- Automation flows for testing, building, and deployment
- Shared conventions across projects

## How to use in other repositories

To reuse a workflow from this repository, add something like the example below to the desired repository:

```yaml
jobs:
  example:
    uses: cumbucadev/shared-workflows/.github/workflows/<workflow-name.yml>@main
```

Replacing <workflow-name.yml> with the file you want to use.

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

[![contributors](https://contrib.rocks/image?repo=cumbucadev/generic-template)](https://github.com/cumbucadev/generic-template/graphs/contributors)

_Made with [contrib.rocks](https://contrib.rocks)._

[github-discussions-doc]: https://docs.github.com/discussions
[github-discussions]: https://github.com/cumbucadev/shared-workflows/discussions
[github-issues-doc]: https://docs.github.com/issues/tracking-your-work-with-issues/creating-an-issue
[github-issues]: https://github.com/cumbucadev/shared-workflows/issues
