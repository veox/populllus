# PopuLLLus

**NOTE** from @veox:

This is a fork of [Populus](https://github.com/ethereum/populus) with some
rough commits to enable developing in LLL. It is the same as my
[`lll-to-merge`](https://github.com/veox/populus/tree/lll-to-merge) branch.

It will install as `populus`, not `populllus`! For this reason, it is
recommended installing inside a `virtualenv`.

Also, it will _still_ require specifying the `LLLBackend` manually in the
project config.

I never got to making its use sane; for example, it will proceed without
raising an exception even if `lllc` failed to compile a contract, and won't
even print what the compiler complained about.

I never got to proper integration into upstream Populus, since the latter
fell behind in maintenance, and is now in re-design/re-implementation phase
anyway.

I did, however, use this fork in a number of projects:

* https://gitlab.com/veox/lll-contracts
* https://gitlab.com/veox/lll-creation-patterns
* https://gitlab.com/veox/oobiqoo

Breaking this fork out as a standalone project allows me to make a PyPI
package, specify it as a dependency in those other codebases, and allow
for straightforward reproduction by others. In the end, this is the goal:
make the software easy to approach and hack on, is so you may wish.

Runnable CI is a bonus. :)

-----

The rest of README remains as-is since forked.

**Many other project-level documentation is outdated, too.**

-----
-----


## Documentation

[Documentation on ReadTheDocs](http://populus.readthedocs.org/en/latest/)


## Installation

```sh
pip install populus
```

## Development

```sh
pip install -e . -r requirements-dev.txt
```


### Running the tests

You can run the tests with:

```sh
py.test tests
```

Or you can install `tox` to run the full test suite.


### Releasing

Pandoc is required for transforming the markdown README to the proper format to
render correctly on pypi.

For Debian-like systems:

```
apt install pandoc
```

Or on OSX:

```sh
brew install pandoc
```

To release a new version:

```sh
bumpversion $$VERSION_PART_TO_BUMP$$
git push && git push --tags
make release
```


#### How to bumpversion

The version format for this repo is `{major}.{minor}.{patch}` for stable, and
`{major}.{minor}.{patch}-{stage}.{devnum}` for unstable (`stage` can be alpha or beta).

To issue the next version in line, use bumpversion and specify which part to bump,
like `bumpversion minor` or `bumpversion devnum`.

If you are in a beta version, `bumpversion stage` will switch to a stable.

To issue an unstable version when the current version is stable, specify the
new version explicitly, like `bumpversion --new-version 4.0.0-alpha.1 devnum`
