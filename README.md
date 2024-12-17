# gh fzf

An fzf wrapper around the GitHub CLI.

<!--editorconfig-checker-disable-->
<!--toc:start-->

- [gh fzf](#gh-fzf)
  - [Installation](#installation)
    - [Upgrading](#upgrading)
  - [Usage](#usage)
    - [`issue`](#issue)
    - [`pr`](#pr)
    - [`run`](#run)
    - [`workflow`](#workflow)
    - [`release`](#release)
    - [`label`](#label)
    - [`milestone`](#milestone)
    - [`repo`](#repo)
    - [`gist`](#gist)
  - [Configuration](#configuration)
  - [Related projects](#related-projects)

<!--toc:end-->

## Installation

1. Install [`gh`](https://github.com/cli/cli#installation) and
   [`fzf`](https://github.com/junegunn/fzf#installation) if you don't already
   have them. For example:

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

Alternatively, you can pin a tag when installing `gh` extensions. A convenience
command is provided for upgrading to the latest version **(recommended)**:

```sh
gh fzf upgrade
```

You can check which version of `gh-fzf` you currently have installed:

```sh
gh fzf version
```

The [changelog](./CHANGELOG.md) contains a list of features and fixes released
in each version. You can also view the release notes on the command line with:

```sh
gh fzf changelog
```

## Usage

```sh
gh fzf \<command\> [flags]
```

This extension adds a new command that wraps GitHub's `list` subcommands with
fzf to make them fuzzy findable. All of the arguments after `<command>` are
passed directly to `gh`. Because of the way shell works, you need to escape
quotes required by GitHub, e.g. [strings with whitespace](https://docs.github.com/en/search-github/getting-started-with-searching-on-github/understanding-the-search-syntax#use-quotation-marks-for-queries-with-whitespace).
There are usage examples for each command in the sections below.

A preview of the current selection is displayed when navigating through the
resulting list. Each command has keybindings to further filter the list or to
call other `gh` subcommands on the item. There are also a few global keybindings
that can be used with any `gh fzf` command:

- `ctrl-o`: Open the selected item in the browser
- `ctrl-y`: Copy the selected item's URL to the clipboard
- `ctrl-r`: Reload the list to its initial filter state and fetch changes from
  GitHub
- `alt-1` to `alt-9`: Change the number of items fetched from GitHub to 100,
  200, ..., 900
- `alt-P`: Toggle the preview window display
- `alt-H`: Toggle the header display, where the keybinding hints are located

### `issue`

- **Usage**: `gh fzf issue [flags]`
- **Aliases**: `i`, `issues`, `-i`, `--issue`, `--issues`
- **Flags**: See `gh issue list --help` for available options
- **Keybindings**:
  - `enter`: Edit the selected issue via CLI prompts
    (see `gh issue edit --help`)
  - `alt-o`: Create/checkout a branch linked to the selected issue, prompting
    for the name (see `gh issue develop --help`)
  - `alt-c`: Add a comment to the selected issue (see `gh issue comment --help`)
  - `alt-l`: Open `gh fzf label` and add the selected label(s) to the issue
  - `alt-L`: Open `gh fzf label` and remove the selected label(s) from the issue
  - `alt-X`: Close the selected issue (see `gh issue close --help`)
  - `alt-O`: Reopen the selected issue (see `gh issue reopen --help`)
  - `alt-a`: Filter the list, showing issues assigned to you
  - `alt-A`: Filter the list, showing issues authored by you
  - `alt-m`: Filter the list, showing issues where you are mentioned
  - `alt-s`: Filter the list, showing issues with any state (open or closed)
- **Examples:**
  - Filter the initial list to open and closed issues assigned to you in the
    "v1.33.7" milestone:
    ```sh
    gh fzf issue --assignee @me --milestone "v1.33.7" --state all
    ```
  - Filter the initial list to issues with the "good first issue" label, no
    assignee, and in the "backburner" milestone. Uses [GitHub's search syntax](https://docs.github.com/en/search-github/searching-on-github/searching-issues-and-pull-requests):
    ```sh
    gh fzf i -S \'no:assignee label:\"good first issue\" milestone:backburner\'
    ```

### `pr`

- **Usage**: `gh fzf pr [flags]`
- **Aliases**: `p`, `prs`, `-p`, `--pr`, `--prs`
- **Flags**: See `gh pr list --help` for available options
- **Keybindings**:
  - `enter`: Edit the selected PR via CLI prompts (see `gh pr edit --help`)
  - `alt-o`: Checkout the HEAD branch of the selected PR
    (see `gh pr checkout --help`)
  - `alt-c`: Add a comment to the selected PR (see `gh pr comment --help`)
  - `alt-d`: Show the diff for the selected PR (see `gh pr diff --help`)
  - `alt-r`: Start/continue/finish a review for the selected PR
    (see `gh pr review --help`)
  - `alt-y`: Copy the branch name of the selected PR
  - `alt-l`: Open `gh fzf label` and add the selected label(s) to the PR
  - `alt-L`: Open `gh fzf label` and remove the selected label(s) from the PR
  - `alt-R`: Mark the selected draft PR as "ready for review"
    (see `gh pr ready --help`)
  - `alt-M`: Merge the selected PR (see `gh pr merge --help`)
  - `alt-X`: Close the selected PR (see `gh pr close --help`)
  - `alt-O`: Reopen the selected PR (see `gh pr reopen --help`)
  - `alt-C`: Open `gh fzf run` filtered for the selected PR (see [run](#run))
  - `alt-a`: Filter the list, showing PRs assigned to you
  - `alt-A`: Filter the list, showing PRs authored by you
  - `alt-b`: Filter the list, showing PRs from the current branch
  - `alt-s`: Filter the list, showing PRs in any state (open, closed, or merged)
- **Examples:**
  - Filter the initial list to your merged pull requests with the
    "breaking change" label:
    ```sh
    gh fzf pr --state merged --author @me --label \"breaking change\"
    ```
  - Filter the initial list to your pull requests merged since the beginning
    of 2023 that have "breaking change" in the body. Uses
    [GitHub's search syntax](https://docs.github.com/en/search-github/searching-on-github/searching-issues-and-pull-requests):
    ```sh
    gh fzf p -S \'merged:">=2023-01-01" \"breaking change\" in:body author:@me\'
    ```

### `run`

- **Usage**: `gh fzf run [flags]`
- **Aliases**: `r`, `runs`, `-r`, `--run`, `--runs`
- **Flags**: See `gh run list --help` for available options
- **Keybindings**:
  - `enter`: Watch for status changes or view logs, depending on whether the
    selected run is in progress or completed.
    (see `gh run watch --help` and `gh run view --help`)
  - `alt-l`: Display logs for the selected run (**deprecated**, use `enter` instead)
  - `alt-d`: Download artifacts from the selected run
    (see `gh run download --help`)
  - `alt-r`: Rerun the selected run (see `gh run rerun --help`)
  - `alt-R`: Rerun only failed jobs of the selected run (see `gh run rerun --help`)
  - `alt-x`: Cancel the selected run (see `gh run cancel --help`)
  - `alt-p`: Open `gh fzf pr` filtered for the selected run's branch as HEAD
    (see [`pr`](#pr))
  - `alt-n`: Create a desktop notification with the conclusion (failed, passed,
    etc.) when the selected run ends. The supported notification tools (tried in
    order) are `dunstify`, `notify-send`, and `osascript`. The notification has
    [actions](https://dunst-project.org/documentation#ACTIONS) for "view logs"
    and "open in browser" when using `dunstify`. There is an additional
    "download artifacts" or "rerun failed jobs" action depending on whether the
    run passed or failed, respectively.
    > **NOTE:** The run watching process is executed in the background, so
    > closing `gh-fzf` won't prevent the desktop notification from displaying.
    > Use `killall gh` to end all `gh` processes, including the run watcher.
  - `alt-w`: Filter the list, showing runs for the selected item from
    `gh fzf workflow` (see [`workflow`](#workflow))
  - `alt-b`: Filter the list, showing runs from the current branch
  - `alt-u`: Filter the list, showing runs triggered by you
  - `alt-f`: Filter the list, showing failed runs
  - `alt-i`: Filter the list, showing in_progress runs
- **Examples:**
  - Filter the initial list to runs for the "tests" workflow:
    ```sh
    gh fzf run --workflow tests
    ```
  - Filter the initial list to failed runs on the main branch:
    ```sh
    gh fzf r -b main -s failure
    ```

### `workflow`

- **Usage**: `gh fzf workflow [flags]`
- **Aliases**: `workflows`, `--workflow`, `--workflows`
- **Flags**: See `gh workflow list --help` for available options
- **Keybindings**:
  - `enter`: Open `gh fzf run` filtered for the selected workflow
    (see [`run`](#run))
  - `alt-d`: Dispatch the selected workflow (see `gh workflow run --help`)
  - `alt-X`: Disable the selected workflow (see `gh workflow disable --help`)
  - `alt-E`: Enable the selected workflow (see `gh workflow enable --help`)
  - `alt-a`: Filter the list, showing all workflows (including disabled ones)
- **Examples**:
  - Filter the initial list to show all workflows:
    ```sh
    gh fzf workflow --all
    ```

### `release`

- **Usage**: `gh fzf release [flags]`
- **Aliases**: `releases`, `--release`, `--releases`
- **Flags**: See `gh release list --help` for available options
- **Keybindings**:
  - `enter`: Download the assets from the selected release
    (see `gh release download --help`)
  - `alt-X`: Delete the selected release (see `gh release delete --help`)
  - `alt-s`: Filter the list, showing stable releases (exclude prereleases)
  - `alt-p`: Filter the list, showing published releases (exclude drafts)
  - `alt-a`: Filter the list, showing releases in ascending order by date
    (defaults to descending)
- **Examples**:
  - Filter the initial list to exclude drafts and prereleases:
    ```sh
    gh fzf release --exclude-drafts --exclude-prereleases
    ```

### `label`

- **Usage**: `gh fzf label [flags]`
- **Aliases**: `labels`, `--label`, `--labels`
- **Flags**: See `gh label list --help` for available options
- **Keybindings**:
  - `enter`: Print the name of the selected label(s) to stdout
  - `alt-n`: Edit the name of the most recently selected label (see `gh label edit --help`)
  - `alt-d`: Edit the description of the most recently selected label
    (see `gh label edit --help`)
  - `alt-c`: Edit the color of the mostly recently selected label (see `gh label edit --help`)
  - `alt-X`: Delete the most recently selected label (see `gh label delete --help`)
  - `alt-N`: Filter the list, sorting labels by name (defaults to creation date)
  - `alt-D`: Filter the list, showing labels in descending order
    (defaults to ascending)
- **Examples**:
  - Filter the initial list to sort by label name in descending order
    ```sh
    gh fzf label --sort name --order desc
    ```

### `milestone`

- **Usage**: `gh fzf milestone`
- **Aliases**: `milestones`, `--milestone`, `--milestones`
- **Flags**: N/A
- **Keybindings**:
  - `enter`: Print the name of the selected milestone to stdout
  - `alt-t`: Edit the title of the selected milestone
  - `alt-d`: Edit the description of the selected milestone
  - `alt-X`: Close the selected milestone
  - `alt-O`: Reopen the selected milestone
  - `alt-s`: Filter the list, showing both open and closed milestones
    (defaults to open)
  - `alt-c`: Filter the list, sorting milestones by completeness
    (defaults to due date)
  - `alt-D`: Filter the list, showing milestones in descending order
    (defaults to ascending)

### `repo`

- **Usage**: `gh fzf repo [flags]`
- **Aliases**: `repos`, `--repo`, `--repos`
- **Flags**: See `gh repo list --help` for available options
- **Keybindings**:
  - `alt-i`: Run `gh fzf issue` on the selected repo (see [`issue`](#issue))
  - `alt-p`: Run `gh fzf pr` on the selected repo (see [`pr`](#pr))
  - `alt-r`: Run `gh fzf run` on the selected repo (see [`run`](#run))
  - `enter`: Edit the selected repo's settings (see `gh repo edit --help`)
  - `alt-C`: Clone the selected repo (see `gh repo clone --help`)
  - `alt-F`: Fork the selected repo (see `gh repo fork --help`)
  - `alt-c`: Filter the list, showing private repos (i.e. closed source)
  - `alt-o`: Filter the list, showing public repos (i.e. open source)
  - `alt-f`: Filter the list, showing forked repos
  - `alt-s`: Filter the list, showing source (non-forked) repos
- **Examples**:
  - Filter the initial list to your non-archived, private repos with the "cli"
    topic:
    ```sh
    gh fzf repo --no-archived --visibility private --topic cli
    ```
  - Filter the initial list to archived repos created by the "google"
    organization where the primary language was "typescript":
    ```sh
    gh fzf repo google --archived --language typescript
    ```

### `gist`

- **Usage**: `gh fzf gist [flags]`
- **Aliases**: `gists`, `--gist`, `--gists`
- **Flags**: See `gh gist list --help` for available options
- **Keybindings**:
  - `enter`: Edit the selected gist (see `gh gist edit --help`)
  - `alt-c`: Clone the selected gist to the current directory
    (see `gh gist clone --help`)
  - `alt-X`: Delete the selected gist (see `gh gist delete --help`)
  - `alt-s`: Filter the list, showing only secret gists
  - `alt-p`: Filter the list, showing only public gists
- **Examples**:
  - Filter the initial list to only show public gists (excluding secret ones):
    ```sh
    gh fzf gist --public
    ```

## Configuration

Environment variables are used to configure `gh-fzf`.

| Variable                         | Description                                                                                                                                                                                                                                                                                                    | Default                                                                                                      |
| -------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------ |
| `GH_FZF_DEFAULT_LIMIT`           | The initial number of items to request from GitHub. The number of items can be changed at runtime with the `alt-1` to `alt-9` commands, see the [Usage](#usage) section for more info.                                                                                                                         | 75                                                                                                           |
| `GH_FZF_TRUNCATE_FIELDS`         | Set the variable to any value to make `gh` truncate text to ensure all fields fit on the screen. When set, truncated text is **not** fuzzy findable. When unset, fields may be cut off, but all text is still fuzzy findable.                                                                                  | unset                                                                                                        |
| `GH_FZF_HIDE_HINTS`              | Set the variable to any value to hide the header (where the keybinding hints are) on startup. The header can still be toggled with the `alt-H` keybinding.                                                                                                                                                     | unset                                                                                                        |
| `GH_FZF_BRANCH_PREFIX`           | A string to prepend to the branch name entered for the `pr` command's `alt-o` keybinding. Spaces are replaced with hyphens. See the [commit](https://github.com/benelan/gh-fzf/commit/f6f78e2dce617f17c6048f28f568fbdc57895119) message for examples.                                                          | unset                                                                                                        |
| `GH_FZF_BRANCH_ADD_ISSUE_NUMBER` | When set, the issue number is added after the prefix (if specified) for the `pr` command's `alt-o` keybinding. The variable's value is added after the number, unless it is a space. See the [commit](https://github.com/benelan/gh-fzf/commit/f6f78e2dce617f17c6048f28f568fbdc57895119) message for examples. | unset                                                                                                        |
| `GH_FZF_NOTIFY_ICON`             | A path to an icon for the desktop notification displayed by the `run` command's `alt-n` keybinding. Only supported by `dunstify` and `notify-send` for now.                                                                                                                                                    | unset                                                                                                        |
| `GH_FZF_COPY_CMD`                | The command used by your operating system to copy an item's URL to the clipboard. Expects the URL from stdin. This only needs to be set if the default doesn't work on your machine.                                                                                                                           | [see code](https://github.com/benelan/gh-fzf/blob/830e6562f9494a5489d5c4c38c99ed409908cf32/gh-fzf#L124-L134) |

You can also set the [`FZF_DEFAULT_OPTS`](https://github.com/junegunn/fzf/blob/master/README.md#environment-variables)
environment variable to add/change `fzf` options used by `gh-fzf` commands.

For example, create aliases in the `gh` config file that add new keybindings to
the [`issue`](#issue), [`pr`](#pr), [`run`](#run), and [`milestone`](#milestone)
commands:

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
  - the `<number>` for the [`issue`](#issue) and [`pr`](#pr) commands
  - the `<tag>` for the [`release`](#release) command
  - the `<id>` for the [`gist`](#gist) command
  - the `<name>` for the [`label`](#label) command
- Use `{-1}` in place of:
  - the `<run-id>` for the [`run`](#run) command
  - the `<workflow-id>` for the [`workflow`](#workflow) command
  - the `<number>` for the [`milestone`](#milestone) command

For a list of the fzf options shared by all `gh-fzf` commands, see the
[source code](https://github.com/benelan/gh-fzf/blob/f8d5b23e283e234557cbed615993e618fd45ccf3/gh-fzf#L109-L129).

> [!WARNING]
> If any of the shared keybindings set by `gh-fzf` don't work, you may be
> overriding them in your shell's start up scripts (e.g. `~/.bashrc`) by setting
> the `$FZF_DEFAULT_OPTS` environment variable.

## Related projects

There is another `fzf` wrapper around `gh` that also provides some `git`
functionality. However, it doesn't provide as many `gh` commands, keybindings,
or configuration options.

- [`gh-f`](https://github.com/gennaro-tedesco/gh-f)

The main focus of `gh-fzf` is providing keybindings to run `gh` subcommands on
the selected item, so `git` functionality is left to other tools. The
following `fzf` wrappers around `git` are good options to bridge that gap.

- [`forgit`](https://github.com/wfxr/forgit)
- [`git-fuzzy`](https://github.com/bigH/git-fuzzy)
