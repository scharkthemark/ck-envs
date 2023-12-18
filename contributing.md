# contributing

Thanks for taking an interest in improving this project! Here are some guidelines to help you get started:

-   [commit messages](#commit-messages): outlines the desired structure and style of commit messages
-   [miscellanea](#miscellanea): provides guidelines for other miscellaneous scenarios
-   [pull requests](#pull-requests): outlines the process for submitting pull requests

_Note: Parts of these guidelines were based upon guides from [GitHub](https://docs.github.com), [Node](https://github.com/nodejs/node/blob/main/CONTRIBUTING.md), and [Angular](https://github.com/angular/angular/blob/main/CONTRIBUTING.md)_

## commit messages

This section outlines the desired structure and style of commit messages. In general, these guidelines follow [Angular's](https://github.com/angular/angular/blob/main/CONTRIBUTING.md) implementation of the [Conventional Commits](https://www.conventionalcommits.org/) specification. At a high level, this means that each commit message should be structured as follows:

```
<type>(<optional scope>): <description>
<optional body>
<optional footer(s)>
```

In addition to following that general structure, there are a few other rules to keep in mind:

-   headers should use the imperative, present tense (e.g. 'add' not 'adds')
-   headers should not end with a period
-   each line in the message should be 72 characters or fewer

Finally, a table of valid commit types is provided as follows:

| type     | description                                              | example                        |
| -------- | -------------------------------------------------------- | ------------------------------ |
| build    | changes the build system, auxiliary tools, or libraries  | update dependencies            |
| ci       | changes the ci configuration or ci-specific tooling      | add new platform to pipeline   |
| docs     | changes the documentation                                | fix typo in readme             |
| feat     | creates a new feature                                    | add toggle for dark mode       |
| fix      | fixes a previously discovered failure or bug             | compare using strict equality  |
| perf     | improves the performance                                 | increase the number of threads |
| refactor | changes the code without affecting its external behavior | create abstraction layer       |
| style    | changes the style or format of the code                  | remove whitespace              |
| test     | adds to, corrects, or improves the test suite            | add test to capture edge case  |

## miscellanea

This section provides guidelines for other miscellaneous scenarios.

### publishing releases

Once you've made some significant changes and feel that the code is at a stable point, you can publish a new release.

```shell
git checkout main
git tag <tagname>
git push --tags
```

### reverting commits

If the commit reverts a previous commit, it should begin with `revert:`, followed by the header of the reverted commit. Additionally, the body should contain information about the hash of the commit being reverted, as well as a clear description of the reason for reverting the commit.

```shell
git revert <hash>
```

If the commit you are rolling back is tagged, you will need to delete the tag as well.

```shell
git tag --delete <tagname>
git push origin --delete <tagname>
```

## pull requests

This section outlines the process for submitting pull requests. It assumes that you have:

-   [installed](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git) and [configured](https://docs.github.com/en/github/getting-started-with-github/set-up-git) Git
-   searched for an open or closed pull request that relates to your submission (to avoid duplicating existing efforts)
-   created or identified an issue that describes the changes you plan to make (to ensure they align with the overall goals of the project)

#### Step 01

Fork the main repository and clone your fork locally. This allows you to freely experiment with changes without affecting the original project.

```shell
# create a local copy of your fork
git clone https://github.com/<username>/ck-envs.git
cd ck-envs

# add a reference to the upstream repository, fetch latest changes
git remote add upstream https://github.com/scharkthemark/ck-envs.git
git fetch upstream
```

#### Step 02

Set up the local development environment.

#### Step 03

Create a new local branch to perform your work. Branches allow you to develop features, fix bugs, and safely experiment with new ideas in a contained area, without affecting the other efforts in the repository.

```shell
git checkout -b my-branch --track upstream/main
```

#### Step 04

Make your changes! If you are modifying code, please be sure to run any formatting and linting checks to ensure that your changes adhere to the styling conventions. Additionally, any bug fixes and features should come with new tests.

#### Step 05

Commit your changes using a descriptive commit message that follows the [commit message conventions](#commit-messages). Adherence to these conventions is necessary so that release notes can be automatically generated from these messages. If you are reverting a commit, see the guidelines [here](#reverting-commits).

```shell
git add --all
git commit
```

#### Step 06

Synchronize your work with the main branch of the upstream repository.

```shell
git fetch upstream main
git rebase upstream/main
```

#### Step 07

Run the full test suite. This helps ensure your changes don't introduce any new bugs.

#### Step 08

Push your local branch to your fork.

```shell
git push origin my-branch
```

#### Step 09

Send a pull request to the main branch of the upstream repository. Only do this once you are sure your changes are ready to go (e.g. formatted, tests passed, etc.).

#### Step 10

You will probably get feedback or requests for changes to your pull request. This is a big part of the submission process so don't be discouraged! Some contributors may sign off on the pull request right away, others may have more detailed comments or feedback. This is a necessary part of the process in order to evaluate whether the changes are correct and necessary.

To make changes to an existing pull request, make the changes to your local branch, add a new commit with those changes, and push those to your fork. The pull request will automatically reflect those changes.

```shell
git add --all
git commit
git push origin my-branch
```

It is also frequently necessary to synchronize your pull request with other changes that have landed in `main` by using `git rebase`:

```shell
git fetch upstream main
git rebase upstream/main
git push --force-with-lease origin my-branch
```

#### Step 11

After your pull request is merged, you can safely delete your branch and pull the changes from the upstream repository:

```shell
git checkout main
git branch my-branch --delete --force
git pull upstream main
```
