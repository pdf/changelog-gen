# changelog-gen

A small Utility to generates Changelog files based on simple conventions in commit summary.

## Installation

`npm install -g changelog-gen`

## Usage

In a git project directory that contains a `package.json` file:

`changelog` - Will generates a markedown changelog from the latest available tag or from the first commit if no tags are available.

In a git project  directory that doesn't contain a `package.json` file:

`changelog --repo {REPO_URL}` - Will generates a markedown changelog from the latest available tag or from the first commit if no tags are available. All the generated links to issues and commits will be constructed using the passed-in `{REPO_URL}`.

### Specifying The Commits Range

You can specify the commit range using the `--start` and `--end` options such as:

- `changelog --start TAIL` - Will start with the root commit in the current commit ancestors.
- `changelog --start {TAG}` - Will start with the first commit after the given `{TAG}`.
- `changelog --start {SHA}` - Will start at the first commit after the last tag before the specified commit. Meaning that if the commit specified with the given `{SHA}` is positionned 3 commits after the `v0.0.1` tag, the range will spans `(v0.0.1 + 1commit)..HEAD`.
- `changelog --start v0.0.1 --end v0.0.2` - Will spans only the commits between these two tags.

## Configuration

The utility works by parsing the commits summaries and test them against the regular expressions defined in the configuration file.

The default configuration being:

```coffee
sections: [
  {
    name: 'Bug Fixes'
    match: '^:bug:'
  }
  {
    name: 'Performances'
    match: '^:racehorse:'
  }
]
```

The configuration file can be either a JSON or a CSON file located in the same directory as your `package.json` file and named `changelog.json` or `changelog.cson`.

You can specify another path to the configuration file using the `--config` option.

`changelog --config my_config.cson`
