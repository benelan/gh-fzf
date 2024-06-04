# Changelog

## [0.12.0](https://github.com/benelan/gh-fzf/compare/v0.11.0...v0.12.0) (2024-06-03)


### Features

* **milestone, issue:** Add `milestone` command and an `alt-M` keybinding for the `issue` command, which filters by the selected milestone ([#23](https://github.com/benelan/gh-fzf/issues/23)) ([86cb9da](https://github.com/benelan/gh-fzf/commit/86cb9dad3e3edd2ad57f3742d12cbeac1af66d12)), closes [#21](https://github.com/benelan/gh-fzf/issues/21)
* **issue, pr:** Support fzf multi-selection when adding or removing labels via `alt-l` or `alt-L` keybindings, respectively ([cac5f20](https://github.com/benelan/gh-fzf/commit/cac5f209d27b5958eaa8d0e7b042522953a24ec7))
* **label:** Include the selected label's name in the prompt for editing the name via `alt-n`, description via `alt-d`, and color via `alt-c` ([d45ea06](https://github.com/benelan/gh-fzf/commit/d45ea067405e0973b88fae84bb27cdcfeab6c3df))
* **label:** Reload list after the edit keybindings (`alt-n`, `alt-d`, `alt-c`) to ensure info is up to date ([b76453a](https://github.com/benelan/gh-fzf/commit/b76453a1bec2ceeb3875b5ed4a239146df07e3d6))
* **run:** Prompt to rerun (if failed) after viewing logs via the `dunstify` notification action ([ff14747](https://github.com/benelan/gh-fzf/commit/ff1474732b3bab78bf2d5fddf5bf86773ce04184))


### Bug Fixes

* **issue, pr:** Exit with code 0 after checking out a branch via the `alt-o` keybindings ([2dbea75](https://github.com/benelan/gh-fzf/commit/2dbea75be3260cbcd89555901f978cefa927ba43))
* **label:** Fix regression where `enter` keybinding printed the whole row of the selected item(s), rather than only the name ([44bd0af](https://github.com/benelan/gh-fzf/commit/44bd0afbb347e3d41e7254f298e3952d16202590))
* **run:** Fix the message/format of notifications when the watcher's process is killed before completion ([b419d35](https://github.com/benelan/gh-fzf/commit/b419d352e78fdc3ad1beaad452932c7d5d2ac40a))


## [0.11.0](https://github.com/benelan/gh-fzf/compare/v0.10.0...v0.11.0) (2024-05-31)


### Features

* **changelog:** Add `changelog` command as a shortcut for `gh fzf release --repo "benelan/gh-fzf"` ([f8d5b23](https://github.com/benelan/gh-fzf/commit/f8d5b23e283e234557cbed615993e618fd45ccf3))
* **run:** Add `alt-i` keybinding to filter by `in_progress` ([89580c0](https://github.com/benelan/gh-fzf/commit/89580c0ec4c37f3ec632d2b7409164028e29aa6d))
* **run:** Add `alt-n` keybinding to to display a desktop notification on completion ([b4185b7](https://github.com/benelan/gh-fzf/commit/b4185b71727c69c70b49fcf668d5cc83854f9bbf))
* **run:** Improve fallback log viewer for the `dunstify` action ([31d4199](https://github.com/benelan/gh-fzf/commit/31d419911033d8c2063a9bee1a8be2341c8c86cc))
* **run:** Add [actions](https://dunst-project.org/documentation#ACTIONS) to notifications created by `dunstify` ([a5c3c50](https://github.com/benelan/gh-fzf/commit/a5c3c5032fea1f5d4b9a7c706862b8c3fdcf6148))
* **run:** Add util for displaying a desktop notification when the selected run completes. Requires `dunstify`, `notify-send`, or `osascript` ([009598c](https://github.com/benelan/gh-fzf/commit/009598c4271dba7a2d4ef2b1c866606bfa02368a))


### Bug Fixes

* **run:** Resolve issues opening logs from the `dunstify` notification's action ([922fb4b](https://github.com/benelan/gh-fzf/commit/922fb4b5a591eeb5506cc28e7eac3ae882cc6ca7))
* **run:** Fix quoting errors in the `osascript` notification ([8a86ee7](https://github.com/benelan/gh-fzf/commit/8a86ee7861cbe45b63bb3f2f17f4553feb5c71a1), [36c5676](https://github.com/benelan/gh-fzf/commit/36c5676c2cd11ccce1429b7dd65b5bff73616070))
* **util:** Correctly pass --repo and -R flags to gh ([46adb7e](https://github.com/benelan/gh-fzf/commit/46adb7e7f030d768457c10e2f83e23756cae931e))


### Performance Improvements

* **issue, pr:** Abort before sending request if a label wasn't selected via `alt-l` or `alt-L` keybindings ([86b4457](https://github.com/benelan/gh-fzf/commit/86b445769884c829d56b7f193aa970e32f2eae52))

## [0.10.0](https://github.com/benelan/gh-fzf/compare/v0.9.0...v0.10.0) (2024-05-18)


### Features

* Improve the default fzf user interface for users that haven't set `FZF_DEFAULT_OPTS` ([d891a07](https://github.com/benelan/gh-fzf/commit/d891a07056838e97b9e8155e3eb4adf65445a924))
* **issue:** Add config options for naming the linked branch created via `alt-o` keybinding. See commit message for details/examples ([f6f78e2](https://github.com/benelan/gh-fzf/commit/f6f78e2dce617f17c6048f28f568fbdc57895119))
* **issue:** Checkout the existing linked branch if it exists with the `alt-o` keybinding ([ecfd426](https://github.com/benelan/gh-fzf/commit/ecfd4269419131a9861da21f7cfffb64c48f7d79))
* **issue:** Prompt for branch name in `alt-o` keybinding ([1aca50f](https://github.com/benelan/gh-fzf/commit/1aca50fbf8a159dc36504891bf13877642d0ec99))


### Bug Fixes

* Resolve ANSI escape code issues when user hasn't set `FZF_DEFAULT_OPTS` ([5ae01a4](https://github.com/benelan/gh-fzf/commit/5ae01a44dd546473fb29f15f5438ff3255040446))
* **issue:** Fix syntax error setting linked branch name ([9c484d8](https://github.com/benelan/gh-fzf/commit/9c484d894c25578e4aeb97628d7eb40351f5fa58))

## [0.9.0](https://github.com/benelan/gh-fzf/compare/v0.8.0...v0.9.0) (2024-05-02)


### Features

* **preview, header:** Improve readability on small width terminals ([ca8bbf5](https://github.com/benelan/gh-fzf/commit/ca8bbf596fd66dd5687e17c38b977f832175db79))
* Refresh the preview after keybinding actions execute ([f3b5fad](https://github.com/benelan/gh-fzf/commit/f3b5fad561ff5d99199c40f582bd5c4dd6025dee))


### Bug Fixes

* **label:** Handle spaces in label names ([b7697a0](https://github.com/benelan/gh-fzf/commit/b7697a0212231419ab5630ca32dc288db207e351))

## [0.8.0](https://github.com/benelan/gh-fzf/compare/v0.7.0...v0.8.0) (2024-04-09)


### Features

* Add `label` command ([#15](https://github.com/benelan/gh-fzf/issues/15)) ([abec1bd](https://github.com/benelan/gh-fzf/commit/abec1bde9f12310d6a7c8cd7af38aba16caa70b4))
* Add `workflow` command ([#13](https://github.com/benelan/gh-fzf/issues/13)) ([09e402b](https://github.com/benelan/gh-fzf/commit/09e402bf40525b86be51b2d08bab02722f37c440))
* **issue, pr:** Increase the default limit when selecting label via `alt-l` and `alt-L` keybindings ([1b81c6f](https://github.com/benelan/gh-fzf/commit/1b81c6f3e9b1018d8b67203a46740366b45ccc39))
* **issue, pr:** Add `alt-l` and `alt-L` keybindings to add and remove a label, respectively ([fea7b42](https://github.com/benelan/gh-fzf/commit/fea7b4238dddf9c4e374782f5071beaa62a87cc3))


### Bug Fixes

* Fix blocked process when opening an item in browser via `ctrl-o` keybinding ([0284389](https://github.com/benelan/gh-fzf/commit/0284389b07d039ead201803be47acbbfd0ddb8ad))
* Ensure all commands respect `--repo` flag ([526452b](https://github.com/benelan/gh-fzf/commit/526452b58488ddd63331377906b831b6eb5a3bf1))

## [0.7.0](https://github.com/benelan/gh-fzf/compare/v0.6.0...v0.7.0) (2024-03-06)


### Features

* Add `gist` command ([#12](https://github.com/benelan/gh-fzf/issues/12)) ([13ac32c](https://github.com/benelan/gh-fzf/commit/13ac32c90865a7c4484824d080583948af35ab97))
* Add `release` command ([#10](https://github.com/benelan/gh-fzf/issues/10)) ([8b9fa6f](https://github.com/benelan/gh-fzf/commit/8b9fa6fa125412a2673e6ba482d3180888e70250))

## [0.6.0](https://github.com/benelan/gh-fzf/compare/v0.5.0...v0.6.0) (2024-02-12)


### Features

* Add `repo` command ([#9](https://github.com/benelan/gh-fzf/issues/9)) ([4ce7fbd](https://github.com/benelan/gh-fzf/commit/4ce7fbdf8cba5d524b3acb91e0e92329b71ac402))
* **run:** Add `alt-d` keybinding to download artifacts ([#6](https://github.com/benelan/gh-fzf/issues/6)) ([8bc2f1a](https://github.com/benelan/gh-fzf/commit/8bc2f1a90c1e2860d6fa0dc35b32c0fdb2b4ffd2))


### Bug Fixes

* Pass `--repo` flag to gh commands executed via the preview and keybindings ([#8](https://github.com/benelan/gh-fzf/issues/8)) ([d97c8cb](https://github.com/benelan/gh-fzf/commit/d97c8cbcdac5d2559e80c6a313238b5103e87937))

## [0.5.0](https://github.com/benelan/gh-fzf/compare/v0.4.0...v0.5.0) (2024-02-05)


### Features

* Add `GH_FZF_TRUNCATE_FIELDS` config option ([aa9984b](https://github.com/benelan/gh-fzf/commit/aa9984b221bc7e4a822ea1ada59307c5ec9194df))


### Bug Fixes

* Allow most fzf options to be overridden ([c455e30](https://github.com/benelan/gh-fzf/commit/c455e3034f49da1ae81c26779de2419fda87e4a8))
* Wrap lines at correct column in preview window ([9177fd6](https://github.com/benelan/gh-fzf/commit/9177fd66fd3aad60dcea66cc40e30320fb261f3e))

## [0.4.0](https://github.com/benelan/gh-fzf/compare/v0.3.0...v0.4.0) (2023-12-30)


### Features

* **run:** Add additional status colors to further differentiate conclusions ([932579f](https://github.com/benelan/gh-fzf/commit/932579fe734b4793beb470fe440cba6b0299a993))
* **run:** Add `alt-p` keybinding to open `gh fzf pr` filtered for the selected run's branch ([f836706](https://github.com/benelan/gh-fzf/commit/f8367060da9608cb40170fb0964214a554e6eef8))


### Reverts

* docs(readme): fix yml code block indenting ([39d262a](https://github.com/benelan/gh-fzf/commit/39d262a57a5b321f2144cbd2dee55853a2464534))

## [0.3.0](https://github.com/benelan/gh-fzf/compare/v0.2.0...v0.3.0) (2023-12-28)


### Features

* **issue, pr, run:** Add newline between keybinding hints and column headers ([4ee118a](https://github.com/benelan/gh-fzf/commit/4ee118a8f91d886cbacc89b669bb6e52d1471dc4))
* Manually truncate results columns to improve search matches and readability ([0f08e40](https://github.com/benelan/gh-fzf/commit/0f08e40a1f9db4c35addac5bddbfb79177c40227))
* **pr:** Change the `alt-C` keybinding to run `gh fzf run` filtered for the selected branch instead of `gh pr checks` ([7ffca65](https://github.com/benelan/gh-fzf/commit/7ffca650924a58d3fc64747977f1dc8c7173a867))


### Bug Fixes

* **pr:** Fix typo in the previous commit to use `gh fzf run` for viewing checks ([7f4e869](https://github.com/benelan/gh-fzf/commit/7f4e86975f021ae7ef023e8192fe1f9e2a2ee02c))
* **run:** Display status when the run hasn't concluded ([830e656](https://github.com/benelan/gh-fzf/commit/830e6562f9494a5489d5c4c38c99ed409908cf32))

## [0.2.0](https://github.com/benelan/gh-fzf/compare/v0.1.0...v0.2.0) (2023-12-22)


### Features

* **issue, pr, run:** Format lists to provide more fuzzy finding fields ([af83fdd](https://github.com/benelan/gh-fzf/commit/af83fdd2e797f88a8a6f2eb0fbde2020dac9468b))
* **issue, pr:** Display all comments in the preview window ([b15f973](https://github.com/benelan/gh-fzf/commit/b15f9737e5f8ac47d6a4100b8bdf2ca088cc213c))


### Bug Fixes

* **issue:** Fix typo in `--comments` flag ([6c29bc4](https://github.com/benelan/gh-fzf/commit/6c29bc4598b0feffebe8809aeff23cb1df96e2c0))

## 0.1.0 (2023-11-28)


### Features

* Add `run`, `issue`, and `pr` commands ([9e254a0](https://github.com/benelan/gh-fzf/commit/9e254a05e3f230c1ab0a9474a6a186d1a13f92ba))
* Add `GH_FZF_DEFAULT_LIMIT` config option for setting the default list items limit ([71e9722](https://github.com/benelan/gh-fzf/commit/71e97227a62f3255d693c7cfc2366ea068a59a8e))
* Add `GH_FZF_HIDE_HINTS` config option to hide the header by default ([ed6b3d2](https://github.com/benelan/gh-fzf/commit/ed6b3d2265b7561bcdac97a60be26c9471939ac5))
* Add `ctrl-y` keybinding for copying the item's url to the clipboard ([44bf38c](https://github.com/benelan/gh-fzf/commit/44bf38ca487c535c5f13568c9ada415d25c4588e))
* Add `version` and `help` commands ([c20abc8](https://github.com/benelan/gh-fzf/commit/c20abc8933c9dccbbdb9685ce76ae817c68319d1))
* Display command picker when one is not provided ([ea326e1](https://github.com/benelan/gh-fzf/commit/ea326e1ba242d3affb513dd2320f0469ea5654b7))
* **issue, pr:** Add `alt-s` and `alt-b` keybindings to filter by "state=all" and the current branch, respectively ([0c2c377](https://github.com/benelan/gh-fzf/commit/0c2c3773432bf2f5093ff78badd1ee1dccffd769))
