# gh fzf

An fzf wrapper around the GitHub CLI.

<!--toc:start-->

- [gh fzf](#gh-fzf)
  - [Installation](#installation)
  - [Usage](#usage)
    - [`issue`](#issue)
    - [`pr`](#pr)
    - [`run`](#run)
    - [`workflow`](#workflow)
    - [`release`](#release)
    - [`label`](#label)
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

## Usage

```sh
gh fzf <command> [flags]
```

This extension adds a new command that wraps GitHub's `list` subcommands with
fzf to make them fuzzy findable. All of the arguments after `<command>` are
passed directly to `gh`. Because of the way shell works, you need to escape
quotes required by GitHub, e.g. [strings with whitespace](https://docs.github.com/en/search-github/getting-started-with-searching-on-github/understanding-the-search-syntax#use-quotation-marks-for-queries-with-whitespace).
There are example usages for each command in the sections below.

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
- `alt-P`: Toggle the preview window
- `alt-H`: Toggle the header display, where the keybinding hints are located

### `issue`

- **Usage**: `gh fzf issue [flags]`
- **Aliases**: `i`, `issues`, `-i`, `--issue`, `--issues`
- **Flags**: See `gh issue list --help` for available options
- **Keybindings**:
  - `enter`: Edit the selected issue in the CLI via prompts
    (see `gh issue edit --help`)
  - `alt-o`: Checkout the linked branch of the selected issue, creating one if
    necessary (see `gh issue develop --help`)
  - `alt-c`: Add a comment to the selected issue
    (see `gh issue comment --help`)
  - `alt-l`: Open `gh fzf label` and add the label to the selected issue
    (see `gh issue edit --help`)
  - `alt-L`: Open `gh fzf label` and remove the label from the selected issue
    (see `gh issue edit --help`)
  - `alt-X`: Close the selected issue
    (see `gh issue close --help`)
  - `alt-O`: Reopen the selected issue
    (see `gh issue reopen --help`)
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
  - `enter`: Edit the selected pull request in the CLI via prompts
    (see `gh pr edit --help`)
  - `alt-o`: Checkout the branch of the selected pull request
    (see `gh pr checkout --help`)
  - `alt-c`: Add a comment to the selected pull request
    (see `gh issue comment --help`)
  - `alt-d`: Show the diff for the selected pull request
    (see `gh pr diff --help`)
  - `alt-r`: Start/continue/finish a review for the selected pull request
    (see `gh pr review --help`)
  - `alt-l`: Open `gh fzf label` and add the label to the selected pull request
    (see `gh issue edit --help`)
  - `alt-L`: Open `gh fzf label` and remove the label from the selected pull
    request (see `gh issue edit --help`)
  - `alt-R`: Mark the selected draft pull request as "ready for review"
    (see `gh pr ready --help`)
  - `alt-M`: Merge the selected pull request
    (see `gh pr merge --help`)
  - `alt-X`: Close the selected pull request
    (see `gh pr close --help`)
  - `alt-O`: Reopen the selected pull request
    (see `gh pr reopen --help`)
  - `alt-C`: Open `gh fzf run` filtered for the selected pull request
    (see [run](#run))
  - `alt-a`: Filter the list, showing pull requests assigned to you
  - `alt-A`: Filter the list, showing pull requests authored by you
  - `alt-b`: Filter the list, showing pull requests from the current branch
  - `alt-s`: Filter the list, showing pull requests with any state
    (open, closed, or merged)
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
  - `enter`: Watch the status updates for the selected run
    (see `gh run watch --help`)
  - `alt-l`: Display the logs for the selected run
    (see `gh run view --help`)
  - `alt-d`: Download artifacts from the selected run
    (see `gh run download --help`)
  - `alt-r`: Rerun the selected run
    (see `gh run rerun --help`)
  - `alt-x`: Cancel the selected run
    (see `gh run cancel --help`)
  - `alt-p`: Open `gh fzf pr` filtered for the selected run's branch as head
    (see [`pr`](#pr))
  - `alt-b`: Filter the list, showing runs from the current branch
  - `alt-u`: Filter the list, showing runs triggered by you
  - `alt-f`: Filter the list, showing failed runs
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
  - `alt-d`: Create a `workflow_dispatch` event for the selected workflow
    (see `gh workflow run --help`)
  - `alt-X`: Disable the selected workflow
    (see `gh workflow disable --help`)
  - `alt-E`: Enable the selected workflow
    (see `gh workflow enable --help`)
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
  - `enter`: Download the assets for the selected release
    (see `gh release download --help`)
  - `alt-X`: Delete the selected release
    (see `gh release delete --help`)
  - `alt-s`: Filter the list, showing stable releases
    (i.e. excluding pre-releases)
  - `alt-p`: Filter the list, showing published releases
    (i.e. excluding drafts)
  - `alt-a`: Filter the list, showing releases in ascending order by release date
    (defaults to descending)
- **Examples**:
  - Filter the initial list to exclude drafts and pre-releases:
    ```sh
    gh fzf release --exclude-drafts --exclude-pre-releases
    ```

### `label`

- **Usage**: `gh fzf label [flags]`
- **Aliases**: `labels`, `--label`, `--labels`
- **Flags**: See `gh label list --help` for available options
- **Keybindings**:
  - `enter`: Print the name of the selected label
  - `alt-n`: Edit the name of the selected label
    (see `gh label edit --help`)
  - `alt-d`: Edit the description of the selected label
    (see `gh label edit --help`)
  - `alt-c`: Edit the color of the selected label
    (see `gh label edit --help`)
  - `alt-X`: Delete the selected label
    (see `gh label delete --help`)
  - `alt-N`: Filter the list, sorting labels by name
    (defaults to creation date)
  - `alt-D`: Filter the list, showing labels in descending order
    (defaults to ascending)
- **Examples**:
  - Filter the initial list to sort by label name in descending order
    ```sh
    gh fzf label --sort name --order desc
    ```

### `repo`

- **Usage**: `gh fzf repo [flags]`
- **Aliases**: `repos`, `--repo`, `--repos`
- **Flags**: See `gh repo list --help` for available options
- **Keybindings**:
  - `alt-i`: Run `gh fzf issue` on the selected repo
    (see [`issue`](#issue))
  - `alt-p`: Run `gh fzf pr` on the selected repo
    (see [`pr`](#pr))
  - `alt-r`: Run `gh fzf run` on the selected repo
    (see [`run`](#run))
  - `enter`: Edit the selected repo's settings
    (see `gh repo edit --help`)
  - `alt-C`: Clone the selected repo
    (see `gh repo clone --help`)
  - `alt-F`: Fork the selected repo
    (see `gh repo fork --help`)
  - `alt-c`: Filter the list, showing private repos
  - `alt-o`: Filter the list, showing public repos
  - `alt-f`: Filter the list, showing forked repos
  - `alt-s`: Filter the list, showing source (non-forked) repos
- **Examples**:
  - Filter the initial list to non-archived, private repos created by you with
    the "cli" topic:
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
  - `enter`: Edit the selected gist
    (see `gh gist edit --help`)
  - `alt-c`: Clone the selected gist to the current directory
    (see `gh gist clone --help`)
  - `alt-X`: Delete the selected gist
    (see `gh gist delete --help`)
  - `alt-s`: Filter the list, showing only secret gists
  - `alt-p`: Filter the list, showing only public gists
- **Examples**:
  - Filter the initial list to only show public gists (excluding secret ones):
    ```sh
    gh fzf gist --public
    ```

## Configuration

Environment variables are used to configure different options in `gh-fzf`.

| Variable                 | Description                                                                                                                                                                                                                   | Default                                                                                                      |
| ------------------------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------ |
| `GH_FZF_DEFAULT_LIMIT`   | The initial number of items to request from GitHub. The number of items can be changed at runtime with the `alt-1` to `alt-9` commands, see the [Usage](#usage) section for more info.                                        | 69                                                                                                           |
| `GH_FZF_TRUNCATE_FIELDS` | Set the variable to any value to make `gh` truncate text to ensure all fields fit on the screen. When set, truncated text is **not** fuzzy findable. When unset, fields may be cut off, but all text is still fuzzy findable. | unset                                                                                                        |
| `GH_FZF_HIDE_HINTS`      | Set the variable to any value to hide the header (where the keybinding hints are) on startup. The header can still be toggled with the `alt-H` keybinding.                                                                    | unset                                                                                                        |
| `GH_FZF_COPY_CMD`        | The command used by your operating system to copy an item's URL to the clipboard. Expects the URL from stdin. This only needs to be set if the default doesn't work on your machine.                                          | [see code](https://github.com/benelan/gh-fzf/blob/830e6562f9494a5489d5c4c38c99ed409908cf32/gh-fzf#L124-L134) |

You can set the [`FZF_DEFAULT_OPTS`](https://github.com/junegunn/fzf/blob/master/README.md#environment-variables)
environment variable to add/change `fzf` options used by `gh-fzf` commands.

For example, create aliases in the `gh` config file that add new keybindings to
the issue and pr commands:

```yml
# ~/.config/gh/config.yml
aliases:
  i: |
    !FZF_DEFAULT_OPTS="$FZF_DEFAULT_OPTS
      --bind='alt-+:execute(gh issue edit --add-assignee @me {1})'
      --bind='alt--:execute(gh issue edit --remove-assignee @me {1})'
    " gh fzf issue $*
  p: |
    !FZF_DEFAULT_OPTS="$FZF_DEFAULT_OPTS
      --bind='alt-+:execute(gh pr review --approve --body \":+1:\" {1})'
      --bind='alt--:execute(gh pr review --request-changes {1})'
      --bind='alt-m:execute(gh pr merge --delete-branch --squash {1})'
      " gh fzf pr $*
```

When adding or modifying fzf keybindings:

- Use `{1}` in place of:
  - the `<number>` for the `issue` and `pr` commands
  - the `<tag>` for the `release` command
  - the `<id>` for the `gist` command
  - the `<name>` for the `label` command
- Use `{-1}` in place of:
  - the `<run-id>` for the `run` command
  - the `<workflow-id>` for the `workflow` command

For a list of the fzf options shared by all `gh-fzf` commands, see the
[source code](https://github.com/benelan/gh-fzf/blob/c455e3034f49da1ae81c26779de2419fda87e4a8/gh-fzf#L145-L165).

**NOTE:** If any of the keybindings set by `gh-fzf` don't work, you may be
overriding them in your shell's start up scripts (e.g. `~/.bashrc`) by setting
the `$FZF_DEFAULT_OPTS` environment variable.

## Related projects

- [`gh-f`](https://github.com/gennaro-tedesco/gh-f): another `fzf` wrapper
  around `gh` that also provides some `git` functionality.

**NOTE:** `gh-fzf` leaves `git` functionality to other tools, and instead
focuses on providing keybindings to run `gh` subcommands on the selected item.
The following `fzf` wrappers around `git` are both good options to bridge that
gap:

- [`forgit`](https://github.com/wfxr/forgit)
- [`git-fuzzy`](https://github.com/bigH/git-fuzzy)
