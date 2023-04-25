# docs-next

The next generation of documentation for HStreamDB.

## Table of Contents

- [Development](#development)
  - [Normal markdown files](#normal-markdown-files)
  - [\_index.md](#_indexmd)
  - [list.json](#listjson)
  - [About sidebar](#about-sidebar)
- [Release a new version](#release-a-new-version)

## Development

We use [pnpm](https://pnpm.io/) as our package manager. Run following commands to install dependencies and start the development server in your local environment.

```bash
pnpm install
pnpm run dev
```

The rest of the time after that you will most likely be editing the following files:

- `docs/**/*.md`
  - [Normal markdown files](#normal-markdown-files)
  - [`_index.md`](#_indexmd)
- [`docs/**/list.json`](#listjson)

We'll talk about what these files do later.

### Normal markdown files

Normal markdown files are just markdown files that are not `_index.md`. They are rendered as a single doc page
based on the file structure of the `docs` folder.

### \_index.md

`_index.md` is a special file that is used to generate the [sidebar](#about-sidebar).

The folder which contains `_index.md` will be rendered as a group in the sidebar. The content of `_index.md` will be rendered as the description of the group. If it is not present, the group will be rendered as the folder name.

For example, the content of `docs/guides/_index.md` is `User Guides`, so the group `guides` will be rendered as `User Guides` in the sidebar.

### list.json

`list.json` is also a special file that is used to generate the [sidebar](#about-sidebar). It includes a array of strings to specify the order of the items in a group. Every string in the array can be a file name or a folder name.

For example, the content of `docs/list.json` is:

```json
["index.md", "concepts.md", "quickstart-with-docker.md", "guides", "io", "operation", "reference", "release-notes.md"]
```

So the group `docs` (the root group) will be rendered as:

- index.md
- concepts.md
- quickstart-with-docker.md
- guides
- io
- operation
- reference
- release-notes.md

### About sidebar

The sidebar is generated base on the file structure of the `docs` folder automatically. It is generated by the following rules:

- Files in `docs/` except files in `v*` and `zh` subfolders will be generated as the en latest version sidebar.
- Files in `docs/zh` except files in `v*` subfolders will be generated as the zh latest version sidebar.
- Files in `docs/v*` will be generated as the en v\* sidebar.
- Files in `docs/zh/v*` will be generated as the zh v\* sidebar.

Even though the rules are a little complicated, you don't need to worry about it. [Once a version is released](#release-a-new-version), the sidebar will be generated automatically.

## Release a new version

To release a new version, all you need to do is create a new tag in the format of `v*.*.*`. For example, to release a new version `v1.0.0`, you can run:

```bash
git tag v1.0.0
```

And then push the tag to the remote repository:

```bash
git push origin v1.0.0
```

Then the CI will automatically open a PR to check out the new version from the latest docs.
