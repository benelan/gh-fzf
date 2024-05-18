# Changelog

## [0.10.0](https://github.com/benelan/gh-fzf/compare/v0.9.0...v0.10.0) (2024-05-18)


### Features

* Improve default user interface ([d891a07](https://github.com/benelan/gh-fzf/commit/d891a07056838e97b9e8155e3eb4adf65445a924))
* **issue:** Add options for naming linked branch ([f6f78e2](https://github.com/benelan/gh-fzf/commit/f6f78e2dce617f17c6048f28f568fbdc57895119))
* **issue:** Checkout existing linked branch if exists ([ecfd426](https://github.com/benelan/gh-fzf/commit/ecfd4269419131a9861da21f7cfffb64c48f7d79))
* **issue:** Prompt for branch name in develop keybind ([1aca50f](https://github.com/benelan/gh-fzf/commit/1aca50fbf8a159dc36504891bf13877642d0ec99))


### Bug Fixes

* Config issues when user hasn't set FZF_DEFAULT_OPTS ([5ae01a4](https://github.com/benelan/gh-fzf/commit/5ae01a44dd546473fb29f15f5438ff3255040446))
* **issue:** Syntax error setting linked branch name ([9c484d8](https://github.com/benelan/gh-fzf/commit/9c484d894c25578e4aeb97628d7eb40351f5fa58))

## [0.9.0](https://github.com/benelan/gh-fzf/compare/v0.8.0...v0.9.0) (2024-05-02)


### Features

* **preview, header:** Readable on small width terminals ([ca8bbf5](https://github.com/benelan/gh-fzf/commit/ca8bbf596fd66dd5687e17c38b977f832175db79))
* Refresh preview after keybind actions execute ([f3b5fad](https://github.com/benelan/gh-fzf/commit/f3b5fad561ff5d99199c40f582bd5c4dd6025dee))


### Bug Fixes

* **label:** Handle spaces in label names ([b7697a0](https://github.com/benelan/gh-fzf/commit/b7697a0212231419ab5630ca32dc288db207e351))

## [0.8.0](https://github.com/benelan/gh-fzf/compare/v0.7.0...v0.8.0) (2024-04-09)


### Features

* Add label command ([#15](https://github.com/benelan/gh-fzf/issues/15)) ([abec1bd](https://github.com/benelan/gh-fzf/commit/abec1bde9f12310d6a7c8cd7af38aba16caa70b4))
* Add workflow command ([#13](https://github.com/benelan/gh-fzf/issues/13)) ([09e402b](https://github.com/benelan/gh-fzf/commit/09e402bf40525b86be51b2d08bab02722f37c440))
* **issue, pr:** Increase labels limit in keybinds ([1b81c6f](https://github.com/benelan/gh-fzf/commit/1b81c6f3e9b1018d8b67203a46740366b45ccc39))
* **issue, pr:** Keybindings to add/remove label ([fea7b42](https://github.com/benelan/gh-fzf/commit/fea7b4238dddf9c4e374782f5071beaa62a87cc3))


### Bug Fixes

* Blocked process when opening item in browser ([0284389](https://github.com/benelan/gh-fzf/commit/0284389b07d039ead201803be47acbbfd0ddb8ad))
* Ensure all commands respect --repo flag ([526452b](https://github.com/benelan/gh-fzf/commit/526452b58488ddd63331377906b831b6eb5a3bf1))

## [0.7.0](https://github.com/benelan/gh-fzf/compare/v0.6.0...v0.7.0) (2024-03-06)


### Features

* Add gist command ([#12](https://github.com/benelan/gh-fzf/issues/12)) ([13ac32c](https://github.com/benelan/gh-fzf/commit/13ac32c90865a7c4484824d080583948af35ab97))
* Add release command ([#10](https://github.com/benelan/gh-fzf/issues/10)) ([8b9fa6f](https://github.com/benelan/gh-fzf/commit/8b9fa6fa125412a2673e6ba482d3180888e70250))

## [0.6.0](https://github.com/benelan/gh-fzf/compare/v0.5.0...v0.6.0) (2024-02-12)


### Features

* Add repo command ([#9](https://github.com/benelan/gh-fzf/issues/9)) ([4ce7fbd](https://github.com/benelan/gh-fzf/commit/4ce7fbdf8cba5d524b3acb91e0e92329b71ac402))
* **run:** Add keymap to download artifacts ([#6](https://github.com/benelan/gh-fzf/issues/6)) ([8bc2f1a](https://github.com/benelan/gh-fzf/commit/8bc2f1a90c1e2860d6fa0dc35b32c0fdb2b4ffd2))


### Bug Fixes

* Pass repo flag to preview and keybinding commands ([#8](https://github.com/benelan/gh-fzf/issues/8)) ([d97c8cb](https://github.com/benelan/gh-fzf/commit/d97c8cbcdac5d2559e80c6a313238b5103e87937))

## [0.5.0](https://github.com/benelan/gh-fzf/compare/v0.4.0...v0.5.0) (2024-02-05)


### Features

* Add GH_FZF_TRUNCATE_FIELDS config option ([aa9984b](https://github.com/benelan/gh-fzf/commit/aa9984b221bc7e4a822ea1ada59307c5ec9194df))


### Bug Fixes

* Allow most fzf options to be overridden ([c455e30](https://github.com/benelan/gh-fzf/commit/c455e3034f49da1ae81c26779de2419fda87e4a8))
* Wrap lines at correct column in preview window ([9177fd6](https://github.com/benelan/gh-fzf/commit/9177fd66fd3aad60dcea66cc40e30320fb261f3e))

## [0.4.0](https://github.com/benelan/gh-fzf/compare/v0.3.0...v0.4.0) (2023-12-30)


### Features

* **run:** Add additional status colors to further differentiate conclusions ([932579f](https://github.com/benelan/gh-fzf/commit/932579fe734b4793beb470fe440cba6b0299a993))
* **run:** Add keybinding to show the pr for the run's branch ([f836706](https://github.com/benelan/gh-fzf/commit/f8367060da9608cb40170fb0964214a554e6eef8))


### Reverts

* Docs(readme): fix yml code block indenting ([39d262a](https://github.com/benelan/gh-fzf/commit/39d262a57a5b321f2144cbd2dee55853a2464534))

## [0.3.0](https://github.com/benelan/gh-fzf/compare/v0.2.0...v0.3.0) (2023-12-28)


### Features

* **issue, pr, run:** Add newline between keybind hints and column headers ([4ee118a](https://github.com/benelan/gh-fzf/commit/4ee118a8f91d886cbacc89b669bb6e52d1471dc4))
* Manually truncate results columns to improve search matches and readability ([0f08e40](https://github.com/benelan/gh-fzf/commit/0f08e40a1f9db4c35addac5bddbfb79177c40227))
* **pr:** Replace the 'gh pr checks' keybinding with 'gh fzf run' ([7ffca65](https://github.com/benelan/gh-fzf/commit/7ffca650924a58d3fc64747977f1dc8c7173a867))


### Bug Fixes

* **pr:** Typo in the previous commit to use 'gh fzf run' for viewing checks ([7f4e869](https://github.com/benelan/gh-fzf/commit/7f4e86975f021ae7ef023e8192fe1f9e2a2ee02c))
* **run:** Display status when the run hasn't concluded ([830e656](https://github.com/benelan/gh-fzf/commit/830e6562f9494a5489d5c4c38c99ed409908cf32))

## [0.2.0](https://github.com/benelan/gh-fzf/compare/v0.1.0...v0.2.0) (2023-12-22)


### Features

* **issue, pr, run:** Format lists to provide more fuzzy finding fields ([af83fdd](https://github.com/benelan/gh-fzf/commit/af83fdd2e797f88a8a6f2eb0fbde2020dac9468b))
* **issue, pr:** Display all comments in the preview window ([b15f973](https://github.com/benelan/gh-fzf/commit/b15f9737e5f8ac47d6a4100b8bdf2ca088cc213c))


### Bug Fixes

* **issue:** Typo in comments flag ([6c29bc4](https://github.com/benelan/gh-fzf/commit/6c29bc4598b0feffebe8809aeff23cb1df96e2c0))

## 0.1.0 (2023-11-28)


### Features

* Add 'run', 'issue', and 'pr' commands ([9e254a0](https://github.com/benelan/gh-fzf/commit/9e254a05e3f230c1ab0a9474a6a186d1a13f92ba))
* Add config option for setting the default limit ([71e9722](https://github.com/benelan/gh-fzf/commit/71e97227a62f3255d693c7cfc2366ea068a59a8e))
* Add config option to hide the header by default ([ed6b3d2](https://github.com/benelan/gh-fzf/commit/ed6b3d2265b7561bcdac97a60be26c9471939ac5))
* Add keybinding for copying the url to clipboard ([44bf38c](https://github.com/benelan/gh-fzf/commit/44bf38ca487c535c5f13568c9ada415d25c4588e))
* Add version and help commands ([c20abc8](https://github.com/benelan/gh-fzf/commit/c20abc8933c9dccbbdb9685ce76ae817c68319d1))
* Display command picker when one is not provided ([ea326e1](https://github.com/benelan/gh-fzf/commit/ea326e1ba242d3affb513dd2320f0469ea5654b7))
* **issue, pr:** Add filter keybindings for state=all and current branch ([0c2c377](https://github.com/benelan/gh-fzf/commit/0c2c3773432bf2f5093ff78badd1ee1dccffd769))
