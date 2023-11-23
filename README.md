# gh fzf

An fzf wrapper around the GitHub CLI.

## Installation

1. Install [GitHub CLI](https://github.com/cli/cli#installation) (`>= v2.0.0`) and [fzf](https://github.com/junegunn/fzf#installation) if you don't already have them. For example:
   - Homebrew: `brew install gh fzf`
   - DNF: `sudo dnf install gh fzf`
   - ... see the links above for other package managers
2. Authenticate with the GitHub CLI: `gh auth login`
3. Install the extension: `gh extension install benelan/gh-fzf`

## Usage

```sh
gh fzf COMMAND [flags]
```

The extension adds a new command that wraps GitHub's "list" subcommands with fzf to make them searchable. It also adds keybindings to perform actions on the selected item.

There are a few global keybindings that can be used with any command:

- `ctrl-o`: Open the selected item in the browser
- `ctrl-y`: Copy the selected item's URL to the clipboard
- `ctrl-r`: Reload the list
- `alt-1` to `alt-9`: Change the number of items fetched from GitHub to 100, 200, ..., 900

### issue

- Usage: `gh fzf issue [flags]`
- Aliases: `i`, `issues`, `-i`, `--issue`, `--issues`
- Flags: See `gh issue list --help` for available options
- Keybindings:
  - `enter`: Edit the selected issue on the CLI (see `gh issue edit --help`)
  - `alt-o`: Checkout the branch linked to the selected issue (see `gh issue develop --help`)
  - `alt-c`: Add a comment to the selected issue (see `gh issue comment --help`)
  - `alt-X`: Close an open issue (see `gh issue close --help`)
  - `alt-O`: Reopen a closed issue (see `gh issue reopen --help`)
  - `alt-a`: Only show issues assigned to you
  - `alt-A`: Only show issues that you authored
  - `alt-m`: Only show issues that you are mentioned in

### pr

- Usage: `gh fzf pr [flags]`
- Aliases: `p`, `prs`, `-p`, `--pr`, `--prs`
- Flags: See `gh pr list --help` for available options
- Keybindings:
  - `enter`: Edit the selected pull request on the CLI (see `gh pr edit --help`)
  - `alt-o`: Checkout the pull request's branch (see `gh pr checkout --help`)
  - `alt-c`: Add a comment to the selected issue (see `gh issue comment --help`)
  - `alt-C`: Show the pull request's status checks (see `gh pr checks --help`)
  - `alt-d`: Show the pull request's diff (see `gh pr diff --help`)
  - `alt-r`: Start a pull request review (see `gh pr review --help`)
  - `alt-R`: Mark a draft pull request as "ready" (see `gh pr ready --help`)
  - `alt-M`: Merge the pull request (see `gh pr merge --help`)
  - `alt-X`: Close an open pull request (see `gh pr close --help`)
  - `alt-O`: Reopen a closed pull request (see `gh pr reopen --help`)
  - `alt-a`: Only show pull requests assigned to you
  - `alt-A`: Only show pull requests that you authored

### run

- Usage: `gh fzf run [flags]`
- Aliases: `r`, `runs`, `-r`, `--run`, `--runs`
- Flags: See `gh run list --help` for available options
- Keybindings:
  - `enter`: Watch the selected run's status (see `gh run watch --help`)
  - `alt-l`: Show the selected run's logs (see `gh run view --help`)
  - `alt-r`: Rerun the selected run (see `gh run rerun --help`)
  - `alt-x`: Cancel the selected run (see `gh run cancel --help`)
  - `alt-b`: Only show runs from the current branch
  - `alt-u`: Only show runs triggered by the current user
  - `alt-f`: Only show failed runs
