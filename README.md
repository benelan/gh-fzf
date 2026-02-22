# gh-fzf

An fzf wrapper around the GitHub CLI.

<!--editorconfig-checker-disable-->

<details>
  <summary>Table of Contents</summary>

<!--toc:start-->

- [gh-fzf](#gh-fzf)
  - [Installation](#installation)
    - [Upgrading](#upgrading)
  - [Usage](#usage)
    - [Command: `issue`](#command-issue)
      - [Aliases](#aliases)
      - [Flags](#flags)
      - [Keybindings](#keybindings)
      - [Examples](#examples)
    - [Command: `pr`](#command-pr)
      - [Aliases](#aliases-1)
      - [Flags](#flags-1)
      - [Keybindings](#keybindings-1)
      - [Examples](#examples-1)
    - [Command: `run`](#command-run)
      - [Aliases](#aliases-2)
      - [Flags](#flags-2)
      - [Keybindings](#keybindings-2)
      - [Examples](#examples-2)
    - [Command: `workflow`](#command-workflow)
      - [Aliases](#aliases-3)
      - [Flags](#flags-3)
      - [Keybindings](#keybindings-3)
      - [Examples](#examples-3)
    - [Command: `release`](#command-release)
      - [Aliases](#aliases-4)
      - [Flags](#flags-4)
      - [Keybindings](#keybindings-4)
      - [Examples](#examples-4)
    - [Command: `label`](#command-label)
      - [Aliases](#aliases-5)
      - [Flags](#flags-5)
      - [Keybindings](#keybindings-5)
      - [Examples](#examples-5)
    - [Command: `milestone`](#command-milestone)
      - [Aliases](#aliases-6)
      - [Keybindings](#keybindings-6)
    - [Command: `repo`](#command-repo)
      - [Aliases](#aliases-7)
      - [Flags](#flags-6)
      - [Keybindings](#keybindings-7)
      - [Examples](#examples-6)
    - [Command: `gist`](#command-gist)
      - [Aliases](#aliases-8)
      - [Flags](#flags-7)
      - [Keybindings](#keybindings-8)
      - [Examples](#examples-7)
    - [Command: `search`](#command-search)
      - [Aliases](#aliases-9)
      - [Subcommands](#subcommands)
      - [Flags](#flags-8)
      - [Keybindings](#keybindings-9)
      - [Examples](#examples-8)
  - [Configuration](#configuration)
  - [Related projects](#related-projects)

<!--toc:end-->

</details>

## Installation

1. Install [`gh`](https://github.com/cli/cli#installation) and [`fzf`](https://github.com/junegunn/fzf#installation) if you don't already have them. For example:
   - **Homebrew**

     ```sh
     brew install gh fzf
     ```

   - **DNF**

     ```sh
     sudo dnf install gh fzf
     ```

   - ... see the links above for other package managers

2. Authenticate with the GitHub CLI:

   ```sh
   gh auth login
   ```

3. Install this extension:

   ```sh
   gh extension install benelan/gh-fzf
   ```

4. **[???](#usage)**

5. **PROFIT**

### Upgrading

To upgrade `gh-fzf` to the latest commit on `main`:

```sh
gh extension upgrade gh-fzf
```

Alternatively, you can pin a tag when installing `gh` extensions. A convenience command is provided for upgrading to the latest version **(recommended)**:

```sh
gh fzf upgrade
```

You can check which version of `gh-fzf` you currently have installed:

```sh
gh fzf version
```

The [changelog](./CHANGELOG.md) contains a list of features and fixes released in each version. You can also view the release notes via `gh-fzf` itself:

```sh
gh fzf changelog
```

## Usage

```sh
gh fzf <command> [flags]
```

This extension adds a new command that wraps GitHub's `list` subcommands with fzf to make them fuzzy findable. All of the arguments after `<command>` are passed directly to `gh`. Because of the way shell works, you need to escape quotes required by GitHub, e.g. [strings with whitespace](https://docs.github.com/en/search-github/getting-started-with-searching-on-github/understanding-the-search-syntax#use-quotation-marks-for-queries-with-whitespace). There are usage examples for each command in the sections below.

A preview of the current selection is displayed when navigating through the resulting list. Each command has keybindings that execute `gh` subcommands on the item or filter the list further. The command-specific keybindings are listed in the following sections.

There are also global keybindings that work on all `gh-fzf` commands:

| Key               | Description                                                               | Configuration Environment Variable |
| ----------------- | ------------------------------------------------------------------------- | ---------------------------------- |
| `ctrl-o`          | Open the selected item in the browser                                     | `GH_FZF_OPEN_KEY`                  |
| `ctrl-y`          | Copy the selected item's URL to the clipboard                             | `GH_FZF_COPY_KEY`                  |
| `ctrl-r`          | Reload the list to its initial filter state and fetch changes from GitHub | `GH_FZF_RELOAD_KEY`                |
| `alt-?`           | View the current command's readme section from the terminal               | `GH_FZF_HELP_KEY`                  |
| `alt-P`           | Toggle the preview window layout from default, bottom, and hidden         | `GH_FZF_TOGGLE_PREVIEW_KEY`        |
| `alt-H`           | Toggle displaying the header, where the keybinding hints are located      | `GH_FZF_TOGGLE_HINTS_KEY`          |
| `alt-1` - `alt-9` | Change the number of items fetched from GitHub to 100, 200, ..., 900      | N/A                                |

### Command: `issue`

`gh fzf issue [flags]`

#### Aliases

`i`, `issues`, `-i`, `--issue`, `--issues`

#### Flags

See `gh issue list --help` for available options

#### Keybindings

| Key     | Description                                                                                                   | Configuration Environment Variable  |
| ------- | ------------------------------------------------------------------------------------------------------------- | ----------------------------------- |
| `enter` | Edit the selected issue via CLI prompts (see `gh issue edit --help`)                                          | `GH_FZF_ISSUE_EDIT_KEY`             |
| `alt-c` | Add a comment to the selected issue (see `gh issue comment --help`)                                           | `GH_FZF_ISSUE_COMMENT_KEY`          |
| `alt-o` | Create/checkout a branch linked to the selected issue, prompting for the name (see `gh issue develop --help`) | `GH_FZF_ISSUE_CHECKOUT_KEY`         |
| `alt-X` | Close the selected issue (see `gh issue close --help`)                                                        | `GH_FZF_ISSUE_CLOSE_KEY`            |
| `alt-O` | Reopen the selected issue (see `gh issue reopen --help`)                                                      | `GH_FZF_ISSUE_REOPEN_KEY`           |
| `alt-l` | Open `gh fzf label` and add the selected label(s) to the issue                                                | `GH_FZF_ISSUE_ADD_LABEL_KEY`        |
| `alt-L` | Open `gh fzf label` and remove the selected label(s) from the issue                                           | `GH_FZF_ISSUE_REMOVE_LABEL_KEY`     |
| `alt-a` | Filter the list, showing issues assigned to you                                                               | `GH_FZF_ISSUE_ASSIGNED_FILTER_KEY`  |
| `alt-A` | Filter the list, showing issues authored by you                                                               | `GH_FZF_ISSUE_AUTHOR_FILTER_KEY`    |
| `alt-m` | Filter the list, showing issues where you are mentioned                                                       | `GH_FZF_ISSUE_MENTIONED_FILTER_KEY` |
| `alt-M` | Open `gh fzf milestone` and filter issues by the selected milestone                                           | `GH_FZF_ISSUE_MILESTONE_FILTER_KEY` |
| `alt-s` | Filter the list, showing issues with any state (open or closed)                                               | `GH_FZF_ISSUE_STATE_FILTER_KEY`     |

#### Examples

- Filter the initial list to open and closed issues assigned to you in the "v1.33.7" milestone:

  ```sh
  gh fzf issue --assignee @me --milestone "v1.33.7" --state all
  ```

- Filter the initial list to issues with the "good first issue" label, no assignee, and in the "backburner" milestone. Uses [GitHub's search syntax](https://docs.github.com/en/search-github/searching-on-github/searching-issues-and-pull-requests):

  ```sh
  gh fzf i -S \'no:assignee label:\"good first issue\" milestone:backburner\'
  ```

### Command: `pr`

`gh fzf pr [flags]`

#### Aliases

`p`, `prs`, `-p`, `--pr`, `--prs`

#### Flags

See `gh pr list --help` for available options

#### Keybindings

| Key     | Description                                                                    | Configuration Environment Variable |
| ------- | ------------------------------------------------------------------------------ | ---------------------------------- |
| `enter` | Edit the selected PR via CLI prompts (see `gh pr edit --help`)                 | `GH_FZF_PR_EDIT_KEY`               |
| `alt-o` | Checkout the HEAD branch of the selected PR (see `gh pr checkout --help`)      | `GH_FZF_PR_CHECKOUT_KEY`           |
| `alt-c` | Add a comment to the selected PR (see `gh pr comment --help`)                  | `GH_FZF_PR_COMMENT_KEY`            |
| `alt-d` | Show the diff for the selected PR (see `gh pr diff --help`)                    | `GH_FZF_PR_DIFF_KEY`               |
| `alt-r` | Start/continue/finish a review for the selected PR (see `gh pr review --help`) | `GH_FZF_PR_REVIEW_KEY`             |
| `alt-y` | Copy the branch name of the selected PR                                        | `GH_FZF_PR_COPY_BRANCH_KEY`        |
| `alt-R` | Mark the selected draft PR as "ready for review" (see `gh pr ready --help`)    | `GH_FZF_PR_READY_KEY`              |
| `alt-M` | Merge the selected PR (see `gh pr merge --help`)                               | `GH_FZF_PR_MERGE_KEY`              |
| `alt-X` | Close the selected PR (see `gh pr close --help`)                               | `GH_FZF_PR_CLOSE_KEY`              |
| `alt-O` | Reopen the selected PR (see `gh pr reopen --help`)                             | `GH_FZF_PR_REOPEN_KEY`             |
| `alt-C` | Open `gh fzf run` filtered for the selected PR (see [run](#command-run))       | `GH_FZF_PR_CHECKS_KEY`             |
| `alt-l` | Open `gh fzf label` and add the selected label(s) to the PR                    | `GH_FZF_PR_ADD_LABEL_KEY`          |
| `alt-L` | Open `gh fzf label` and remove the selected label(s) from the PR               | `GH_FZF_PR_REMOVE_LABEL_KEY`       |
| `alt-a` | Filter the list, showing PRs assigned to you                                   | `GH_FZF_PR_ASSIGNED_FILTER_KEY`    |
| `alt-A` | Filter the list, showing PRs authored by you                                   | `GH_FZF_PR_AUTHOR_FILTER_KEY`      |
| `alt-b` | Filter the list, showing PRs from the current branch                           | `GH_FZF_PR_BRANCH_FILTER_KEY`      |
| `alt-s` | Filter the list, showing PRs in any state (open, closed, or merged)            | `GH_FZF_PR_STATE_FILTER_KEY`       |

#### Examples

- Filter the initial list to your merged pull requests with the "breaking change" label:

  ```sh
  gh fzf pr --state merged --author @me --label \"breaking change\"
  ```

- Filter the initial list to your pull requests merged since the beginning of 2023 that have "breaking change" in the body. Uses [GitHub's search syntax](https://docs.github.com/en/search-github/searching-on-github/searching-issues-and-pull-requests):

  ```sh
  gh fzf p -S \'merged:">=2023-01-01" \"breaking change\" in:body author:@me\'
  ```

### Command: `run`

`gh fzf run [flags]`

#### Aliases

`r`, `runs`, `-r`, `--run`, `--runs`

#### Flags

See `gh run list --help` for available options

#### Keybindings

| Key     | Description                                                                                                                                                   | Configuration Environment Variable  |
| ------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------- |
| `enter` | Watch for status changes or view logs, depending on whether the selected run is in progress or completed (see `gh run watch --help` and `gh run view --help`) | `GH_FZF_RUN_VIEW_KEY`               |
| `alt-l` | Display logs for the selected run (**deprecated**, use `enter` instead)                                                                                       | N/A                                 |
| `alt-r` | Rerun the selected run (see `gh run rerun --help`)                                                                                                            | `GH_FZF_RUN_RERUN_KEY`              |
| `alt-R` | Rerun only failed jobs of the selected run (see `gh run rerun --help`)                                                                                        | `GH_FZF_RUN_RERUN_FAILED_KEY`       |
| `alt-x` | Cancel the selected run (see `gh run cancel --help`)                                                                                                          | `GH_FZF_RUN_CANCEL_KEY`             |
| `alt-d` | Download artifacts from the selected run (see `gh run download --help`)                                                                                       | `GH_FZF_RUN_DOWNLOAD_KEY`           |
| `alt-p` | Open `gh fzf pr` filtered for the selected run's branch as HEAD (see [`pr`](#command-pr))                                                                     | `GH_FZF_RUN_PR_KEY`                 |
| `alt-n` | Create a desktop notification with the conclusion (failed, success, etc.) when the selected run ends[^1]                                                      | `GH_FZF_RUN_NOTIFY_KEY`             |
| `alt-u` | Filter the list, showing runs triggered by you                                                                                                                | `GH_FZF_RUN_USER_FILTER_KEY`        |
| `alt-f` | Filter the list, showing failed runs                                                                                                                          | `GH_FZF_RUN_FAILED_FILTER_KEY`      |
| `alt-i` | Filter the list, showing in_progress runs                                                                                                                     | `GH_FZF_RUN_IN_PROGRESS_FILTER_KEY` |
| `alt-b` | Filter the list, showing runs from the current branch                                                                                                         | `GH_FZF_RUN_BRANCH_FILTER_KEY`      |
| `alt-w` | Filter the list, showing runs for the selected item from `gh fzf workflow` (see [`workflow`](#command-workflow))                                              | `GH_FZF_RUN_WORKFLOW_FILTER_KEY`    |

#### Examples

- Filter the initial list to runs for the "tests" workflow:

  ```sh
  gh fzf run --workflow tests
  ```

- Filter the initial list to failed runs on the main branch:

  ```sh
  gh fzf r -b main -s failure
  ```

[^1]:
    The supported notification tools (in order of precedence) are `dunstify`, `notify-send`, and `osascript`. The notification has [actions](https://dunst-project.org/documentation#ACTIONS) for "view logs" and "open in browser" when using `dunstify`. There is an additional "download artifacts" or "rerun failed jobs" action depending on whether the run passed or failed, respectively.

    > **NOTE:** The run watcher process is executed in the background, so closing `gh-fzf` won't prevent the desktop notification from displaying. Use `pkill -f "gh run watch --exit-status"` to terminate the run watcher.

### Command: `workflow`

`gh fzf workflow [flags]`

#### Aliases

`workflows`, `--workflow`, `--workflows`

#### Flags

See `gh workflow list --help` for available options

#### Keybindings

| Key     | Description                                                                      | Configuration Environment Variable    |
| ------- | -------------------------------------------------------------------------------- | ------------------------------------- |
| `enter` | Open `gh fzf run` filtered for the selected workflow (see [`run`](#command-run)) | `GH_FZF_WORKFLOW_VIEW_RUNS_KEY`       |
| `alt-d` | Dispatch the selected workflow (see `gh workflow run --help`)                    | `GH_FZF_WORKFLOW_DISPATCH_KEY`        |
| `alt-X` | Disable the selected workflow (see `gh workflow disable --help`)                 | `GH_FZF_WORKFLOW_DISABLE_KEY`         |
| `alt-E` | Enable the selected workflow (see `gh workflow enable --help`)                   | `GH_FZF_WORKFLOW_ENABLE_KEY`          |
| `alt-a` | Filter the list, showing all workflows (including disabled ones)                 | `GH_FZF_WORKFLOW_SHOW_ALL_FILTER_KEY` |

#### Examples

- Filter the initial list to show all workflows:

  ```sh
  gh fzf workflow --all
  ```

### Command: `release`

`gh fzf release [flags]`

#### Aliases

`releases`, `--release`, `--releases`

#### Flags

See `gh release list --help` for available options

#### Keybindings

| Key     | Description                                                                           | Configuration Environment Variable    |
| ------- | ------------------------------------------------------------------------------------- | ------------------------------------- |
| `enter` | Download the assets from the selected release (see `gh release download --help`)      | `GH_FZF_RELEASE_DOWNLOAD_KEY`         |
| `alt-X` | Delete the selected release (see `gh release delete --help`)                          | `GH_FZF_RELEASE_DELETE_KEY`           |
| `alt-s` | Filter the list, showing stable releases (exclude prereleases)                        | `GH_FZF_RELEASE_STABLE_FILTER_KEY`    |
| `alt-p` | Filter the list, showing published releases (exclude drafts)                          | `GH_FZF_RELEASE_PUBLISHED_FILTER_KEY` |
| `alt-a` | Filter the list, showing releases in ascending order by date (defaults to descending) | `GH_FZF_RELEASE_ASCENDING_SORT_KEY`   |

#### Examples

- Filter the initial list to exclude drafts and prereleases:

  ```sh
  gh fzf release --exclude-drafts --exclude-prereleases
  ```

### Command: `label`

`gh fzf label [flags]`

#### Aliases

`labels`, `--label`, `--labels`

#### Flags

See `gh label list --help` for available options

#### Keybindings

| Key     | Description                                                                           | Configuration Environment Variable  |
| ------- | ------------------------------------------------------------------------------------- | ----------------------------------- |
| `enter` | Print the name of the selected label(s) to stdout                                     | `GH_FZF_LABEL_PRINT_KEY`            |
| `alt-n` | Edit the name of the most recently selected label (see `gh label edit --help`)        | `GH_FZF_LABEL_EDIT_NAME_KEY`        |
| `alt-d` | Edit the description of the most recently selected label (see `gh label edit --help`) | `GH_FZF_LABEL_EDIT_DESCRIPTION_KEY` |
| `alt-c` | Edit the color of the mostly recently selected label (see `gh label edit --help`)     | `GH_FZF_LABEL_EDIT_COLOR_KEY`       |
| `alt-X` | Delete the most recently selected label (see `gh label delete --help`)                | `GH_FZF_LABEL_DELETE_KEY`           |
| `alt-N` | Filter the list, sorting labels by name (defaults to creation date)                   | `GH_FZF_LABEL_NAME_SORT_KEY`        |
| `alt-D` | Filter the list, showing labels in descending order (defaults to ascending)           | `GH_FZF_LABEL_DESCENDING_ORDER_KEY` |

#### Examples

- Filter the initial list to sort by label name in descending order

  ```sh
  gh fzf label --sort name --order desc
  ```

### Command: `milestone`

`gh fzf milestone`

#### Aliases

`milestones`, `--milestone`, `--milestones`

#### Keybindings

| Key     | Description                                                                     | Configuration Environment Variable       |
| ------- | ------------------------------------------------------------------------------- | ---------------------------------------- |
| `enter` | Print the name of the selected milestone to stdout                              | `GH_FZF_MILESTONE_PRINT_KEY`             |
| `alt-i` | Open `gh fzf issue` filtered for the selected milestone                         | `GH_FZF_MILESTONE_VIEW_ISSUES_KEY`       |
| `alt-X` | Close the selected milestone                                                    | `GH_FZF_MILESTONE_CLOSE_KEY`             |
| `alt-O` | Reopen the selected milestone                                                   | `GH_FZF_MILESTONE_REOPEN_KEY`            |
| `alt-t` | Edit the title of the selected milestone                                        | `GH_FZF_MILESTONE_EDIT_TITLE_KEY`        |
| `alt-d` | Edit the description of the selected milestone                                  | `GH_FZF_MILESTONE_EDIT_DESCRIPTION_KEY`  |
| `alt-s` | Filter the list, showing both open and closed milestones (defaults to open)     | `GH_FZF_MILESTONE_STATE_FILTER_KEY`      |
| `alt-c` | Filter the list, sorting milestones by completeness (defaults to due date)      | `GH_FZF_MILESTONE_COMPLETENESS_SORT_KEY` |
| `alt-D` | Filter the list, showing milestones in descending order (defaults to ascending) | `GH_FZF_MILESTONE_DESCENDING_ORDER_KEY`  |

### Command: `repo`

`gh fzf repo [flags]`

#### Aliases

`repos`, `--repo`, `--repos`

#### Flags

See `gh repo list --help` for available options

#### Keybindings

| Key     | Description                                                             | Configuration Environment Variable |
| ------- | ----------------------------------------------------------------------- | ---------------------------------- |
| `enter` | Edit the selected repo's settings (see `gh repo edit --help`)           | `GH_FZF_REPO_EDIT_KEY`             |
| `alt-i` | Run `gh fzf issue` on the selected repo (see [`issue`](#command-issue)) | `GH_FZF_REPO_VIEW_ISSUES_KEY`      |
| `alt-p` | Run `gh fzf pr` on the selected repo (see [`pr`](#command-pr))          | `GH_FZF_REPO_VIEW_PRS_KEY`         |
| `alt-r` | Run `gh fzf run` on the selected repo (see [`run`](#command-run))       | `GH_FZF_REPO_VIEW_RUNS_KEY`        |
| `alt-C` | Clone the selected repo (see `gh repo clone --help`)                    | `GH_FZF_REPO_CLONE_KEY`            |
| `alt-F` | Fork the selected repo (see `gh repo fork --help`)                      | `GH_FZF_REPO_FORK_KEY`             |
| `alt-c` | Filter the list, showing private repos (i.e. closed source)             | `GH_FZF_REPO_PRIVATE_FILTER_KEY`   |
| `alt-o` | Filter the list, showing public repos (i.e. open source)                | `GH_FZF_REPO_PUBLIC_FILTER_KEY`    |
| `alt-s` | Filter the list, showing source (non-forked) repos                      | `GH_FZF_REPO_SOURCE_FILTER_KEY`    |
| `alt-f` | Filter the list, showing forked repos                                   | `GH_FZF_REPO_FORK_FILTER_KEY`      |

#### Examples

- Filter the initial list to your non-archived, private repos with the "cli" topic:

  ```sh
  gh fzf repo --no-archived --visibility private --topic cli
  ```

- Filter the initial list to archived repos created by the "google" organization where the primary language was "typescript":

  ```sh
  gh fzf repo google --archived --language typescript
  ```

### Command: `gist`

`gh fzf gist [flags]`

#### Aliases

`gists`, `--gist`, `--gists`

#### Flags

See `gh gist list --help` for available options

#### Keybindings

| Key     | Description                                                                   | Configuration Environment Variable |
| ------- | ----------------------------------------------------------------------------- | ---------------------------------- |
| `enter` | Edit the selected gist (see `gh gist edit --help`)                            | `GH_FZF_GIST_EDIT_KEY`             |
| `alt-c` | Clone the selected gist to the current directory (see `gh gist clone --help`) | `GH_FZF_GIST_CLONE_KEY`            |
| `alt-X` | Delete the selected gist (see `gh gist delete --help`)                        | `GH_FZF_GIST_DELETE_KEY`           |
| `alt-p` | Filter the list, showing only public gists                                    | `GH_FZF_GIST_PUBLIC_FILTER_KEY`    |
| `alt-s` | Filter the list, showing only secret gists                                    | `GH_FZF_GIST_SECRET_FILTER_KEY`    |

#### Examples

- Filter the initial list to only show public gists (excluding secret ones):

  ```sh
  gh fzf gist --public
  ```

### Command: `search`

`gh fzf search <subcommand> [flags]`

> [!WARNING]
> The `search` command is **experimental**, which means it is subject to breaking changes without a major version bump. Please report any bugs you find!

The `search` command works differently than the others. There are two different search modes:

1. **gh:** This is the initial mode and nothing is displayed until you type a query. The mode uses GitHub's search syntax, which you can read about in their documentation:
   - [`issues` & `prs`](https://docs.github.com/en/search-github/searching-on-github/searching-issues-and-pull-requests)
   - [`repos`](https://docs.github.com/en/search-github/searching-on-github/searching-for-repositories)
   - [`commits`](https://docs.github.com/en/search-github/searching-on-github/searching-commits)
   - [`code`](https://docs.github.com/en/search-github/searching-on-github/searching-code)

2. **fzf:** This is the mode used by the rest of the commands, which uses `fzf` search syntax.

The mode is displayed in the bottom left corner. Start by searching with GitHub syntax. For example, you may type `author:@me` when using the `issues` or `prs` subcommands. When you switch modes from `gh` to `fzf`, the list remains the same and the GitHub query is saved to state and cleared from the search bar. You can then use `fzf` syntax to filter the list further. When you switch modes from `fzf` to `gh`, the GitHub query is restored and the list is reloaded.

#### Aliases

`s`, `-s`, `--search`

#### Subcommands

`issues`, `prs`, `repos`, `commits`, `code`

#### Flags

See `gh search <subcommand> --help` for available options

#### Keybindings

| Key     | Description                                | Configuration Environment Variable |
| ------- | ------------------------------------------ | ---------------------------------- |
| `alt-/` | Toggle between `gh` and `fzf` search modes | `GH_FZF_SEARCH_TOGGLE_MODE_KEY`    |

#### Examples

- Search for open issues that you're involved with, sorted by most recent update:

  ```sh
  gh fzf search issues state:open involves:@me sort:updated
  ```

- Search for public repos that use the "lua" language and have the "neovim-plugin" topic, sorted by the number of stars:

  ```sh
  gh fzf search repos --visibility=public --language=lua --topic=neovim-plugin --sort=stars
  ```

- Search for commits you made in 2024 that contain the phrase "breaking change" in the message:

  ```sh
  gh fzf search commits --author=$(gh api user --jq '.login') --author-date=2024-01-01..2024-12-31 \"breaking change\"
  ```

- Search for code in repos you own that matches "fetch":

  ```sh
  gh fzf search code --owner=$(gh api user --jq '.login') fetch
  ```

## Configuration

Environment variables are used to configure `gh-fzf`.

| Variable                         | Description                                                                                                                                                                                                                           | Default    |
| -------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------- |
| `GH_FZF_DEFAULT_LIMIT`           | The initial number of items to request from GitHub. The number of items can be changed at runtime with the `alt-1` to `alt-9` commands, see the [Usage](#usage) section for more info.                                                | 75         |
| `GH_FZF_TRUNCATE_FIELDS`         | Set the variable to any value to make `gh` truncate text to ensure all fields fit on the screen. When set, truncated text is **not** fuzzy findable. When unset, fields may be cut off, but all text is still fuzzy findable.         | unset      |
| `GH_FZF_HIDE_HINTS`              | Set the variable to any value to hide the header (where the keybinding hints are) on startup. The header can still be toggled with the `alt-H` keybinding.                                                                            | unset      |
| `GH_FZF_BRANCH_PREFIX`           | A string to prepend to the branch name entered for the `pr` command's `alt-o` keybinding. Spaces are replaced with hyphens. See the feature's [commit message] for examples.                                                          | unset      |
| `GH_FZF_BRANCH_ADD_ISSUE_NUMBER` | When set, the issue number is added after the prefix (if specified) for the `pr` command's `alt-o` keybinding. The variable's value is added after the number, unless it is a space. See the feature's [commit message] for examples. | unset      |
| `GH_FZF_NOTIFY_ICON`             | A path to an icon for the desktop notification displayed by the `run` command's `alt-n` keybinding. Only supported by `dunstify` and `notify-send` for now.                                                                           | unset      |
| `GH_FZF_COPY_CMD`                | The command used by your operating system to copy an item's URL to the clipboard. Expects the URL from stdin. This only needs to be set if the default doesn't work on your machine.                                                  | [see code] |

[commit message]: https://github.com/benelan/gh-fzf/commit/f6f78e2dce617f17c6048f28f568fbdc57895119
[see code]: https://github.com/benelan/gh-fzf/blob/65bfdb81a30fc55878e04758e5cbcec68a242a18/gh-fzf#L113-L125

You can also set the [`FZF_DEFAULT_OPTS`](https://github.com/junegunn/fzf/blob/master/README.md#environment-variables) environment variable to add/change `fzf` options used by `gh-fzf` commands.

For example, create aliases in the `gh` config file that add new keybindings to the [`issue`](#command-issue), [`pr`](#command-pr), [`run`](#command-run), and [`milestone`](#command-milestone) commands:

```yml
# ~/.config/gh/config.yml
aliases:
  i: |
    !FZF_DEFAULT_OPTS="$FZF_DEFAULT_OPTS
      --bind='alt-+:execute(gh issue edit --add-assignee @me {1})'
      --bind='alt--:execute(gh issue edit --remove-assignee @me {1})'
      --bind='alt-@:execute(
        selected=\"\$(gh fzf milestone)\"
        [ -n \"\$selected\" ] && gh issue edit --milestone \"\$selected\" {1}
      )'
    " gh fzf issue $*

  p: |
    !FZF_DEFAULT_OPTS="$FZF_DEFAULT_OPTS
      --bind='alt-+:execute(gh pr review --approve --body \":+1:\" {1})'
      --bind='alt--:execute(gh pr review --request-changes {1})'
      --bind='alt-m:execute(gh pr merge --delete-branch --squash {1})'
      " gh fzf pr $*

  r: |
    !FZF_DEFAULT_OPTS="$FZF_DEFAULT_OPTS
      --bind='alt-e:execute(gh run view --log-failed {-1})'
      --bind='alt-q:reload(eval \"\$FZF_DEFAULT_COMMAND --status queued\")'
    " gh fzf run $*

  m: |
    !FZF_DEFAULT_OPTS="$FZF_DEFAULT_OPTS
      --bind='alt-bspace:execute(
        gh api --silent --method DELETE /repos/{owner}/{repo}/milestones/{-1}
      )+reload(eval \"\$FZF_DEFAULT_COMMAND\")'
    " gh fzf milestone
```

When adding or modifying fzf keybindings:

- Use `{1}` in place of:
  - the `<number>` for the [`issue`](#command-issue) and [`pr`](#command-pr) commands
  - the `<tag>` for the [`release`](#command-release) command
  - the `<id>` for the [`gist`](#command-gist) command
  - the `<name>` for the [`label`](#command-label) command
- Use `{-1}` in place of:
  - the `<run-id>` for the [`run`](#command-run) command
  - the `<workflow-id>` for the [`workflow`](#command-workflow) command
  - the `<number>` for the [`milestone`](#command-milestone) command

Check out the `gh-fzf` author's [`~/.config/gh/config.yml`](https://github.com/benelan/dotfiles/blob/master/.config/gh/config.yml) for more inspiration.

See the [code](https://github.com/benelan/gh-fzf/blob/65bfdb81a30fc55878e04758e5cbcec68a242a18/gh-fzf#L157-L179) for the list of fzf options shared by all `gh-fzf` commands.

> [!WARNING]
> If any of the shared keybindings set by `gh-fzf` don't work, you may be overriding them in your shell's start up scripts (e.g. `~/.bashrc`) by setting the `$FZF_DEFAULT_OPTS` environment variable.

## Related projects

There is another `fzf` wrapper around `gh` that also provides some `git` functionality. However, it doesn't provide as many `gh` commands, keybindings, or configuration options.

- [`gh-f`](https://github.com/gennaro-tedesco/gh-f)

The main focus of `gh-fzf` is providing keybindings to run `gh` subcommands on the selected item, so `git` functionality is left to other tools. The following `fzf` wrappers around `git` are good options to bridge that gap.

- [`forgit`](https://github.com/wfxr/forgit)
- [`git-fuzzy`](https://github.com/bigH/git-fuzzy)
