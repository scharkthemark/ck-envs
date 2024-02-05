# contributing

Thanks for taking an interest in improving this project! Here are some guidelines to help you get started:

-   [commits](#commits): provides guidance for working with commits
-   [miscellanea](#miscellanea): provides guidance for other miscellaneous scenarios
-   [pull requests](#pull-requests): outlines the process for submitting pull requests

_Note: Parts of these guidelines were based upon guides from [GitHub](https://docs.github.com), [Node](https://github.com/nodejs/node/blob/main/CONTRIBUTING.md), and [Angular](https://github.com/angular/angular/blob/main/CONTRIBUTING.md)_

## commits

This section provides guidance for working with commits.

### message format

In general, the commit message format follows [Angular's](https://github.com/angular/angular/blob/main/CONTRIBUTING.md) implementation of the [Conventional Commits](https://www.conventionalcommits.org/) specification. At a high level, this means that each commit message should be structured as follows:

```
<type>(<optional scope>): <summary>

<optional body>

<optional footer(s)>
```

The `<header>` provides a summary of the change, where `<type>` documents the commit type and `<scope>` provides contextual information about which part of the project the commit affects. The table below defines the list of valid commit types. The `<body>` explains why the change is necessary, and the `<footer>` documents breaking changes, deprecations, and references to issues, tickets, and other PRs associated with the commit.

| type     | description                                              |
| -------- | -------------------------------------------------------- |
| build    | changes the build system, auxiliary tools, or libraries  |
| ci       | changes the ci configuration or ci-specific tooling      |
| docs     | changes the documentation                                |
| feat     | creates a new feature                                    |
| fix      | fixes a previously discovered failure or bug             |
| perf     | improves the performance                                 |
| refactor | changes the code without affecting its external behavior |
| revert   | reverts a previous commit                                |
| test     | adds to, corrects, or improves the test suite            |

In addition to following that general structure, there are a few other rules to keep in mind:

-   specify breaking changes by placing a `!` after the type or scope
-   headers should use the imperative, present tense (e.g., "add" not "adds")
-   headers should neither start with a capitalized letter nor end with a period
-   each line in the message should be 72 characters or fewer

Refer to the [Conventional Commits](https://www.conventionalcommits.org/) documentation for examples of valid commit messages.

### reverts

If a commit reverts a previous commit, the header should begin with `revert:`, followed by the header of the reverted commit. Additionally, the body should contain information about the hash of the reverted commit, as well as a clear description of the reason for reverting the commit.

```shell
git revert <hash>
```

If there is a tag associated with the reverted commit, delete the tag as well.

```shell
git tag --delete <tagname>
git push origin --delete <tagname>
```

## miscellanea

This section provides guidance for other miscellaneous scenarios.

### publishing releases

Once you have made some significant changes and feel that the code is at a stable point, you can publish a new release.

```shell
git checkout main
git tag <tagname>
git push --tags
```

## pull requests

This section outlines the process for submitting pull requests. It assumes that you have:

-   [installed](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git) and [configured](https://git-scm.com/book/en/v2/Getting-Started-First-Time-Git-Setup) Git
-   [configured](https://docs.github.com/en/authentication/connecting-to-github-with-ssh) a connection to GitHub using SSH
-   searched for an open or closed pull request that relates to your submission (to avoid duplicating existing efforts)
-   created or identified an issue that describes the changes you plan to make (to ensure they align with the overall goals of the project)

#### Step 01

Fork the repository and clone your fork locally. This allows you to freely experiment with changes without affecting the original project.

```shell
# create a local copy of your fork
git clone git@github.com:<username>/ck-envs.git
cd ck-envs

# add a reference to the upstream repository; fetch the latest changes
git remote add upstream git@github.com:scharkthemark/ck-envs.git
git fetch upstream
```

#### Step 02

Set up the local development environment.

#### Step 03

Create a new local branch to perform your work. Branches provide a space to safely develop features, fix bugs, and experiment with new ideas without impacting the `main` branch of the repository.

```shell
git checkout -b my-branch --track upstream/main
```

#### Step 04

Make your changes! Be sure to include new tests if the changes involve new features or bug fixes.

#### Step 05

Run any formatters and linters. This helps ensure that your changes adhere to the proper styling conventions.

#### Step 06

Commit your changes using a descriptive commit message that follows the [commit message format](#message-format). Adherence to these conventions is necessary so that release notes can be automatically generated from these messages. If you are reverting a commit, see the guidance [here](#reverts).

```shell
git add --all
git commit
```

#### Step 07

Synchronize your work with the `main` branch of the upstream repository.

```shell
git fetch upstream main
git rebase upstream/main
```

#### Step 08

Run the full test suite. This helps ensure that your changes do not introduce any new bugs.

#### Step 09

Push your local branch to your fork.

```shell
git push origin my-branch
```

#### Step 10

Send a pull request to the `main` branch of the upstream repository. Only do this once you are sure that your changes are ready (e.g., formatted, tests passed, etc.).

#### Step 11

You will probably get feedback or requests for changes to your pull request. This is a big part of the submission process, so do not be discouraged! Some contributors may sign off on the pull request right away, while others may have more detailed comments or feedback. This is a necessary part of the process in order to evaluate whether the changes are correct and necessary.

To modify an existing pull request, make the changes to your local branch, add a new commit with those changes, and push the commit to your fork. The pull request will automatically reflect those changes.

```shell
git add --all
git commit
git push origin my-branch
```

It is also frequently necessary to synchronize your pull request with other changes that have landed in the `main` branch by using `git rebase`:

```shell
git fetch upstream main
git rebase upstream/main
git push --force-with-lease origin my-branch
```

_Note: The `git push --force-with-lease` command is one of the few ways to delete history in git. It also complicates the review process, as it does not allow reviewers to get a quick glance at what changed. Before you use it, make sure you understand the risks. If in doubt, you can always ask for guidance in the pull request._

#### Step 12

After a reviewer merges your pull request, delete your branch and pull the changes from the upstream repository:

```shell
git checkout main
git branch my-branch --delete --force
git pull upstream main
```
