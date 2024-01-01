# Changelog

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
